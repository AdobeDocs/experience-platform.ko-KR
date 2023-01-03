---
title: 데칠레 기반 파생 속성 사용 사례
description: 이 안내서에서는 Query Service를 사용하여 프로필 데이터에 사용할 데코일 기반 파생 속성을 만드는 데 필요한 단계를 보여줍니다.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# 데파일 기반 파생 속성 사용 사례

파생된 특성을 사용하면 다른 다운스트림 플랫폼 서비스와 함께 사용하거나 실시간 고객 프로필 데이터에 게시할 수 있는 데이터 레이크에서 데이터를 분석하는 복잡한 사용 사례를 용이하게 할 수 있습니다.

이 사용 사례에서는 실시간 고객 프로필 데이터에 사용할 데칠레 기반 파생 속성을 만드는 방법을 보여줍니다. 항공사 충성도 시나리오를 예로 사용하면 이 안내서에서는 카테고리적 특성을 기반으로 대상을 세그먼트화하고 만드는 카테고리를 사용하는 데이터 세트를 만드는 방법을 알려줍니다.

다음 주요 개념을 설명합니다.

* Decimal Bucketing용 스키마 만들기
* 카테고리적 decimal 생성.
* 복합 파생 특성 만들기.
* 전환 확인 기간 동안의 분류 계산.
* 이러한 데코일 버킷을 기반으로 대상을 생성할 수 있도록 집계, 순위 지정 및 고유 ID를 추가하는 방법을 보여주는 예제 쿼리.

## 시작하기

이 안내서에서는 다음 사항을 이해하고 있어야 합니다 [쿼리 서비스에서 쿼리 실행](../best-practices/writing-queries.md) 및 Adobe Experience Platform의 다음 구성 요소:

* [실시간 고객 프로필 개요](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [스키마 작성 기본 사항](../../xdm/schema/composition.md): XDM(Experience Data Model) 스키마 및 스키마 작성을 위한 빌딩 블록, 원칙 및 우수 사례를 소개합니다.
* [실시간 고객 프로필에 대한 스키마를 활성화하는 방법](../../profile/tutorials/add-profile-data.md): 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.
* [사용자 지정 데이터 유형을 정의하는 방법](../../xdm/api/data-types.md): 데이터 유형은 클래스 또는 스키마 필드 그룹에서 참조 유형 필드로 사용되며 스키마의 모든 위치에 포함할 수 있는 다중 필드 구조를 일관되게 사용할 수 있습니다.

## 목표

이 문서에서 제공하는 예제는 데모를 사용하여 항공사 충성도 스키마에서 등급 데이터에 대한 파생 속성을 만듭니다. 파생된 특성을 사용하면 선택한 카테고리에 대한 상위 &#39;n&#39;%를 기반으로 대상을 식별하여 데이터의 유틸리티를 최대화할 수 있습니다.

## 빌드 데파일 기반 파생 특성

특정 차원 및 해당 지표를 기반으로 십진수 등급을 정의하려면, 스키마를 설계하여 분류 그룹화를 허용해야 합니다.

이 안내서에서는 항공사 충성도 데이터 세트를 사용하여 다양한 전환 확인 기간을 거친 마일에 따라 Query Service를 사용하여 프로필을 빌드하는 방법을 보여줍니다.

## Query Service를 사용하여 Decimal 파일을 만듭니다.

Query Service를 사용하여 카테고리적 분류가 포함된 데이터 세트를 만들 수 있으며, 이를 세그먼트화하여 속성 순위를 기준으로 대상을 만들 수 있습니다. 다음 예제에 표시된 개념은 카테고리가 정의되고 지표를 사용할 수 있는 한 다른 decimal 버킷 데이터 세트를 만들기 위해 적용할 수 있습니다.

예제 항공사 충성도 데이터는 [XDM ExperienceEvents 클래스](../../xdm/classes/experienceevent.md). 각 이벤트는 &quot;Flyer&quot;, &quot;Frequency&quot;, &quot;Silver&quot; 또는 &quot;Gold&quot; 중 하나에 대한 마일리지 및 차변에 대한 비즈니스 거래 기록입니다. 기본 ID 필드는 다음과 같습니다. `membershipNumber`.

### 샘플 데이터 세트

이 예제의 초기 항공사 충성도 데이터 세트는 &quot;항공사 충성도 데이터&quot;이며 다음 스키마를 가집니다. 스키마의 기본 ID는 다음과 같습니다 `_profilefoundationreportingstg.membershipNumber`.

![항공사 충성도 데이터 스키마 다이어그램입니다.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**샘플 데이터**

다음 표에는 `_profilefoundationreportingstg` 이 예제에 사용되는 객체입니다. 이 확장은 복잡한 파생 속성을 만들기 위해 디파일 버킷을 사용하는 컨텍스트를 제공합니다.

>[!NOTE]
>
>간결성을 위해 테넌트 ID `_profilefoundationreportingstg` 열 제목과 문서 전체의 후속 언급 등에서 네임스페이스 시작에서 이 생략되었습니다.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | 새 멤버 | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | 은 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | 은 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | 은 |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | 새 신용 카드 | 10000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 생성

위에 표시된 항공사 충성도 데이터에서 `.mileage` 값에는 탑승한 모든 개별 비행에 대해 구성원이 비행한 마일 수가 포함됩니다. 이 데이터는 라이프타임 전환 확인 기간과 다양한 전환 기간에 대해 비행기를 따라 비행한 마일 수에 대한 채우기를 만드는 데 사용됩니다. 이를 위해 각 전환 확인 기간에 대한 맵 데이터 유형의 데이터와 지정된 각 전환 기간에 대한 적절한 설명을 포함하는 데이터 세트가 만들어집니다 `membershipNumber`.

Query Service를 사용하여 데코일 데이터 세트를 만들려면 &quot;항공사 충성도 데코일 스키마&quot;를 만드십시오.

![&quot;Airline 로열티 데코일 스키마&quot;의 다이어그램입니다.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### 실시간 고객 프로필에 대한 스키마 활성화

실시간 고객 프로필에서 사용하기 위해 Experience Platform에 수집되는 데이터는 [프로필에 대해 활성화된 XDM(Experience Data Model) 스키마](../../xdm/ui/resources/schemas.md). 프로필에 대해 스키마를 활성화하려면 XDM 개별 프로필 또는 XDM ExperienceEvent 클래스를 구현해야 합니다.

[스키마 레지스트리 API를 사용하여 실시간 고객 프로필에 사용할 스키마를 사용하도록 설정합니다](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 사용자 인터페이스](../../xdm/tutorials/create-schema-ui.md).  프로필용 스키마를 활성화하는 방법에 대한 자세한 지침은 해당 설명서에서 확인할 수 있습니다.

그런 다음 모든 파일 관련 필드 그룹에 다시 사용할 데이터 유형을 만듭니다. decile 필드 그룹을 만드는 것은 샌드박스당 1회 단계입니다. 또한 모든 디파일 관련 스키마에 다시 사용할 수 있습니다.

### ID 네임스페이스를 만들어 기본 식별자로 표시 {#identity-namespace}

10차 파일에 사용하기 위해 만들어진 모든 스키마에는 기본 ID가 할당되어 있어야 합니다. 다음을 수행할 수 있습니다 [Adobe Experience Platform 스키마 UI에서 id 필드 정의](../../xdm/ui/fields/identity.md#define-an-identity-field)또는 [스키마 레지스트리 API](../../xdm/api/descriptors.md#create).

또한 Query Service를 사용하면 SQL을 통해 직접 Ad Hoc 스키마 데이터 세트 필드에 대한 ID 또는 기본 ID를 설정할 수 있습니다. 다음 문서를 참조하십시오. [ad hoc 스키마 ID에서 보조 ID 및 기본 ID 설정](../data-governance/ad-hoc-schema-identities.md) 추가 정보.

### 전환 확인 기간 동안의 분류를 계산하기 위한 쿼리를 만듭니다 {#create-a-query}

다음 예제에서는 전환 확인 기간 동안의 설명을 계산하기 위한 SQL 쿼리를 보여 줍니다.

템플릿은 UI의 쿼리 편집기를 사용하거나 [쿼리 서비스 API](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### 쿼리 검토

예제 쿼리의 섹션은 아래에 자세히 검사됩니다.

#### 전환 확인 기간

데이터 유형 1, 3, 6, 9, 12 및 라이프타임 전환 확인을 위한 버킷이 포함되어 있습니다. 쿼리는 1, 3 및 6개월의 전환 확인 기간을 사용하므로 각 전환 기간에 대한 임시 테이블을 만들기 위해 각 섹션에 몇 가지 &quot;반복&quot; 쿼리를 포함합니다.

>[!NOTE]
>
>소스 데이터에 전환 확인 기간을 결정하는 데 사용할 수 있는 열이 없는 경우 모든 데이터 분류 등급이 `decileMonthAll`.

#### 집계

일반적인 테이블 표현식(CTE)을 사용하여 데코일 버킷을 만들기 전에 마일리지를 함께 집계하십시오. 이렇게 하면 특정 전환 확인 기간에 대한 총 마일리지 수가 제공됩니다. CTE는 일시적으로 존재하며 더 큰 쿼리의 범위 내에서만 사용할 수 있습니다.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

블록은 템플릿에서 두 번 반복됩니다(`summed_miles_3` 및 `summed_miles_6`) 다른 전환 확인 기간에 대한 데이터를 생성하기 위해 날짜 계산에 변경 사항이 있는 경우

쿼리의 ID, 차원 및 지표 열(`membershipNumber`, `loyaltyStatus` 및 `totalMiles` 각각 사용할 수 있습니다.

#### 등급

분류 그룹을 사용하여 카테고리를 수행할 수 있습니다. 등급 번호를 만들려면 `NTILE` 함수는 `10` WINDOW 내에서 `loyaltyStatus` 필드. 이 경우 1부터 10까지의 순위가 표시됩니다. 설정 `ORDER BY` 의 조항 `WINDOW` to `DESC` 의 등급 값을 `1` 이 **가장** 차원 내의 지표입니다.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### 맵 집계

여러 전환 확인 기간을 사용하는 경우 을 사용하여 미리 세부 사항 버킷 맵을 만들어야 합니다 `MAP_FROM_ARRAYS` 및 `COLLECT_LIST` 함수 위에 있어야 합니다. 예제 코드 조각에서 `MAP_FROM_ARRAYS` 한 쌍의 키(`loyaltyStatus`) 및 값( )`decileBucket`) 배열이 포함되어 있습니다. `COLLECT_LIST` 지정된 열에 모든 값이 있는 배열을 반환합니다.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>라이프타임 기간에만 데코일 등급을 사용해야 하는 경우에는 맵 집계가 필요하지 않습니다.

#### 고유 ID

고유 ID 목록(`membershipNumber`)은 모든 멤버십에 대한 고유한 목록을 만드는 데 필요합니다.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>라이프타임 기간 동안에만 데코일 등급이 필요한 경우 이 단계를 생략하고 다음을 수행하여 합계를 수행할 수 있습니다 `membershipNumber` 최종 단계에서 수행할 수 있습니다.

#### 모든 임시 데이터 결합

마지막 단계는 모든 임시 데이터를 필드 그룹에 있는 파일의 구조와 동일한 형태로 결합하는 것입니다.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

라이프타임 데이터만 사용할 수 있는 경우 쿼리가 다음과 같이 나타납니다.

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

십분위수를 사용하므로 순위 번호와 백분위수 간의 상관 관계는 쿼리 결과에서 보장됩니다. 각 등급은 10%와 같으므로 상위 30%를 기반으로 대상을 식별하려면 1, 2 및 3등급을 타깃팅해야 합니다.

### 쿼리 템플릿 실행

쿼리를 실행하여 데이터 세트를 채웁니다. 쿼리를 템플릿으로 저장하여 케이던스에서 실행하도록 예약할 수도 있습니다. 템플릿으로 저장되면 쿼리를 업데이트하여 `table_exists` 명령. 사용 방법에 대한 자세한 정보 `table_exists`명령은 [SQL 구문 안내서](../sql/syntax.md#table-exists).

## 다음 단계

위에 제공된 예제 사용 사례에서는 실시간 고객 프로필에서 데코일 속성을 사용할 수 있도록 하는 단계를 중점적으로 설명합니다. 이렇게 하면 사용자 인터페이스나 RESTful API를 통해 세그멘테이션 서비스가 이러한 decimal 버킷을 기반으로 대상을 생성할 수 있습니다. 자세한 내용은 [세그먼테이션 서비스 개요](../../segmentation/home.md) 세그먼트 만들기, 평가 및 액세스 방법에 대한 자세한 내용을 참조하십시오.
