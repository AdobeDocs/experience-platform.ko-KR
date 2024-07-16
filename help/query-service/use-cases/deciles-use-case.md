---
title: 십분위수 기반 파생 데이터 세트 사용 사례
description: 이 안내서에서는 프로필 데이터에 사용할 십분위수 기반 파생 데이터 세트를 만들기 위해 쿼리 서비스를 사용하는 데 필요한 단계를 보여줍니다.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 2ffb8724b2aca54019820335fb21038ec7e69a7f
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---

# 십분위수 기반 파생 데이터 세트 사용 사례

파생된 데이터 세트는 다른 다운스트림 플랫폼 서비스와 함께 사용하거나 실시간 고객 프로필 데이터에 게시할 수 있는 데이터 레이크의 데이터를 분석하는 복잡한 사용 사례를 용이하게 합니다.

이 예제 사용 사례에서는 실시간 고객 프로필 데이터에 사용할 십분위수 기반 파생 데이터 세트를 만드는 방법을 보여 줍니다. 이 안내서에서는 항공사 충성도 시나리오를 예로 들어, 카테고리적 십분위수를 사용하여 등급 속성을 기반으로 대상을 세그먼트화하고 만드는 데이터 세트를 만드는 방법을 알려줍니다.

다음과 같은 주요 개념이 나와 있습니다.

* 십분위수 버킷팅에 대한 스키마 생성.
* 카테고리별 십분위수 만들기.
* 복잡한 파생 데이터 세트를 만듭니다.
* 전환 확인 기간 동안의 십분위수 계산.
* 집계, 등급 지정 및 고유 ID 추가를 보여 주는 예제 쿼리를 통해 이러한 십분위수 버킷을 기반으로 대상을 생성할 수 있습니다.

## 시작하기

이 안내서를 사용하려면 [쿼리 서비스에서 쿼리 실행](../best-practices/writing-queries.md) 및 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [실시간 고객 프로필 개요](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [스키마 작성의 기본 사항](../../xdm/schema/composition.md): XDM(Experience Data Model) 스키마와 스키마 작성을 위한 기본 요소, 원칙 및 모범 사례에 대해 소개합니다.
* [실시간 고객 프로필에 대해 스키마를 활성화하는 방법](../../profile/tutorials/add-profile-data.md): 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.
* [사용자 지정 데이터 형식을 정의하는 방법](../../xdm/api/data-types.md): 데이터 형식은 클래스 또는 스키마 필드 그룹의 참조 형식 필드로 사용되며 스키마의 모든 위치에 포함할 수 있는 다중 필드 구조를 일관되게 사용할 수 있습니다.

## 목표

이 문서에 제공된 예제 에서는 십분위수를 사용하여 항공사 충성도 스키마의 등급 데이터에 대한 파생된 데이터 세트를 만듭니다. 파생 데이터 세트를 사용하면 선택한 카테고리의 상위 &#39;n&#39;%를 기반으로 대상을 식별하여 데이터의 유틸리티를 극대화할 수 있습니다.

## 십분위수 기반 파생 데이터 세트 구축

특정 차원 및 해당 지표를 기반으로 십분위수 순위를 정의하려면 십분위수 버킷팅을 허용하도록 스키마를 디자인해야 합니다.

이 안내서는 항공사 충성도 데이터 세트를 사용하여 쿼리 서비스를 사용하여 다양한 전환 확인 기간 동안 날아온 마일을 기반으로 십분위수를 작성하는 방법을 보여줍니다.

## 쿼리 서비스를 사용하여 십분위수 만들기

Query Service를 사용하면 카테고리적 십분위수가 포함된 데이터 세트를 생성할 수 있습니다. 그런 다음 이 데이터 세트를 세그먼트화하여 속성 등급에 따라 대상자를 생성할 수 있습니다. 범주가 정의되어 있고 지표를 사용할 수 있는 한 다음 예에 표시된 개념을 사용하여 다른 십분위수 버킷 데이터 세트를 만들 수 있습니다.

예제 항공사 충성도 데이터는 [XDM ExperienceEvents 클래스](../../xdm/classes/experienceevent.md)를 사용합니다. 각 이벤트는 크레딧 또는 디베이트 마일리지에 대한 비즈니스 거래 기록이며 &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; 또는 &quot;Gold&quot;의 회원 충성도 상태입니다. 기본 ID 필드는 `membershipNumber`입니다.

### 샘플 데이터 세트

이 예제의 초기 항공사 충성도 데이터 세트는 &quot;항공사 충성도 데이터&quot;이며, 다음 스키마를 포함합니다. 스키마의 기본 ID는 `_profilefoundationreportingstg.membershipNumber`입니다.

![항공사 충성도 데이터 스키마의 다이어그램입니다.](../images/use-cases/airline-loyalty-data.png)

**샘플 데이터**

다음 표에는 이 예제에 사용된 `_profilefoundationreportingstg` 개체에 포함된 샘플 데이터가 표시됩니다. 복잡한 파생 데이터 세트를 만들기 위해 십분위수 버킷을 사용하는 컨텍스트를 제공합니다.

>[!NOTE]
>
>간단히 하기 위해 테넌트 ID `_profilefoundationreportingstg`은(는) 열 제목과 문서 전체에서 후속 언급에서 네임스페이스의 시작 부분에서 생략되었습니다.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | 새 구성원 | 5000 | 전단지 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | 에프라 | 7500 | 실버 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | 에프라 | 7500 | 실버 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JF | 5000 | 실버 |
| A123487284 | rritson1zn@sciencedaily.com | 2022년 1월 7일 | STATUS_MILES | 새 신용 카드 | 10000 | 전단지 |

{style="table-layout:auto"}

## 십분위수 데이터 세트 생성

위에 표시된 항공사 충성도 데이터에서 `.mileage` 값은 모든 개별 항공편에 대해 회원이 비행한 마일 수를 포함합니다. 이 데이터는 라이프타임 전환 및 다양한 전환 확인 기간을 통해 날아온 마일 수에 대한 십분위수를 만드는 데 사용됩니다. 이를 위해 각 전환 기간에 대한 맵 데이터 형식의 십분위수와 `membershipNumber`에 할당된 각 전환 기간에 대한 적절한 십분위수를 포함하는 데이터 집합이 만들어집니다.

쿼리 서비스를 사용하여 십분위수 데이터 세트를 만들려면 &quot;항공사 충성도 십분위수 스키마&quot;를 만듭니다.

![항공사 충성도 십분위수 스키마 다이어그램입니다.](../images/use-cases/airline-loyalty-decile-schema.png)

### 실시간 고객 프로필에 대한 스키마 활성화

실시간 고객 프로필에서 사용하기 위해 Experience Platform에 수집되는 데이터는 프로필에 대해 활성화된 [XDM(경험 데이터 모델) 스키마](../../xdm/ui/resources/schemas.md)를 준수해야 합니다. 프로필에 대해 스키마를 활성화하려면 XDM 개인 프로필 또는 XDM ExperienceEvent 클래스를 구현해야 합니다.

[스키마 레지스트리 API를 사용하여 실시간 고객 프로필에 사용할 스키마를 사용하도록 설정](../../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 사용자 인터페이스](../../xdm/tutorials/create-schema-ui.md)를 사용합니다.  프로필에 대해 스키마를 활성화하는 방법에 대한 자세한 지침은 해당 설명서에서 확인할 수 있습니다.

그런 다음 모든 십분위수 관련 필드 그룹에 재사용할 데이터 유형을 만듭니다. 십분위수 필드 그룹 만들기는 샌드박스당 한 번의 단계입니다. 모든 십분위수 관련 스키마에 다시 사용할 수도 있습니다.

### ID 네임스페이스를 만들고 기본 식별자로 표시 {#identity-namespace}

십분위수와 함께 사용하기 위해 만들어진 모든 스키마에는 기본 ID가 할당되어야 합니다. [Adobe Experience Platform 스키마 UI에서 ID 필드를 정의](../../xdm/ui/fields/identity.md#define-an-identity-field)하거나 [스키마 레지스트리 API](../../xdm/api/descriptors.md#create)를 통해 정의할 수 있습니다.

또한 쿼리 서비스를 사용하면 SQL을 통해 직접 임시 스키마 데이터 세트 필드에 대한 ID 또는 기본 ID를 설정할 수 있습니다. 자세한 내용은 [임시 스키마 ID에서 보조 ID 및 기본 ID 설정](../data-governance/ad-hoc-schema-identities.md)에 대한 설명서를 참조하십시오.

### 전환 확인 기간 동안 십분위수를 계산하기 위한 쿼리를 만듭니다 {#create-a-query}

다음 예제에서는 전환 확인 기간 동안 십분위수를 계산하기 위한 SQL 쿼리를 보여 줍니다.

UI에서 쿼리 편집기를 사용하거나 [쿼리 서비스 API](../api/query-templates.md#create-a-query-template)를 통해 템플릿을 만들 수 있습니다.

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

예제 쿼리의 섹션은 아래에 자세히 조사됩니다.

#### 전환 기간

십분위수 데이터 유형에는 1, 3, 6, 9, 12 및 라이프타임 전환 확인을 위한 버킷이 포함됩니다. 쿼리는 1, 3 및 6개월의 전환 확인 기간을 사용하므로 각 전환 확인 기간에 대한 임시 테이블을 만들기 위해 각 섹션에는 몇 가지 &quot;반복된&quot; 쿼리가 포함됩니다.

>[!NOTE]
>
>소스 데이터에 전환 확인 기간을 결정하는 데 사용할 수 있는 열이 없는 경우 `decileMonthAll` 아래에서 모든 십분위수 클래스 순위가 수행됩니다.

#### 집계

십분위수 버킷을 만들기 전에 마일리지를 함께 집계하려면 일반 테이블 표현식(CTE)을 사용합니다. 이는 특정 전환 확인 기간에 대한 총 마일리지를 제공합니다. CTE는 일시적으로 존재하며 더 큰 쿼리의 범위 내에서만 사용할 수 있습니다.

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

다른 전환 확인 기간에 대한 데이터를 생성하기 위해 템플릿(`summed_miles_3` 및 `summed_miles_6`)에서 날짜 계산이 변경되어 블록이 두 번 반복됩니다.

쿼리에 대한 ID, 차원 및 지표 열(`membershipNumber`, `loyaltyStatus` 및 `totalMiles`)을 참고하십시오.

#### 순위

십분위수를 사용하여 범주형 버킷팅을 수행할 수 있습니다. 순위 번호를 만들기 위해 `loyaltyStatus` 필드로 그룹화된 WINDOW 내에서 `10`의 매개 변수와 함께 `NTILE` 함수를 사용합니다. 그 결과 1에서 10까지 순위가 매겨집니다. `WINDOW`의 `ORDER BY` 절을 `DESC`(으)로 설정하여 `1`의 순위 값이 차원 내의 **greatest** 지표에 지정되도록 합니다.

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

전환 확인 기간이 여러 개인 경우 `MAP_FROM_ARRAYS` 및 `COLLECT_LIST` 함수를 사용하여 십분위수 버킷 맵을 미리 만들어야 합니다. 예제 코드 조각에서 `MAP_FROM_ARRAYS`은(는) 키 쌍(`loyaltyStatus`)과 값(`decileBucket`) 배열로 맵을 만듭니다. `COLLECT_LIST`이(가) 지정된 열에 있는 모든 값이 있는 배열을 반환합니다.

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
>십분위수 등급이 라이프타임 기간 동안만 필요한 경우에는 맵 집계가 필요하지 않습니다.

#### 고유 ID

모든 멤버십의 고유 목록을 만들려면 고유 ID 목록(`membershipNumber`)이 필요합니다.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>십분위수 순위가 생애 기간 동안만 필요한 경우 이 단계를 생략하고 마지막 단계에서 `membershipNumber`에 의한 집계를 수행할 수 있습니다.

#### 모든 임시 데이터 결합

마지막 단계는 모든 임시 자료를 필드 그룹의 십분위수 구조와 동일한 형태로 함께 결합하는 것이다.

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

라이프타임 데이터만 사용할 수 있는 경우 쿼리는 다음과 같이 표시됩니다.

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

십분위수의 사용으로 인해 쿼리 결과에서 순위 번호와 백분위수 간의 상관 관계가 보장됩니다. 각 등급은 10%와 같으므로 상위 30%를 기준으로 대상을 식별하려면 등급 1, 2 및 3만 타겟팅하면 됩니다.

### 쿼리 템플릿 실행

쿼리를 실행하여 십분위수 데이터 세트를 채웁니다. 쿼리를 템플릿으로 저장하고 케이던스로 실행되도록 예약할 수도 있습니다. 템플릿으로 저장하면 쿼리를 업데이트하여 `table_exists` 명령을 참조하는 create 및 insert 패턴을 사용할 수도 있습니다. `table_exists`명령을 사용하는 방법에 대한 자세한 내용은 [SQL 구문 안내서](../sql/syntax.md#table-exists)를 참조하십시오.

## 다음 단계

위에 제공된 예제 사용 사례에서는 실시간 고객 프로필에서 십분위수 기반 파생 데이터 세트를 사용할 수 있도록 하는 단계를 강조표시합니다. 이렇게 하면 사용자 인터페이스 또는 RESTful API를 통해 세분화 서비스가 이러한 십분위수 버킷을 기반으로 대상을 생성할 수 있습니다. 세그먼트를 만들고, 평가하고, 액세스하는 방법에 대한 자세한 내용은 [세그먼테이션 서비스 개요](../../segmentation/home.md)를 참조하세요.
