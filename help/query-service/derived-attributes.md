---
title: 파생 속성
description: 파생된 특성을 사용하면 일반 케이던스에 대한 속성을 계산하고 선택적으로 이러한 파생된 특성을 실시간 고객 프로필에 프로필 속성으로 게시할 수 있습니다. 이 문서에서는 Query Service를 사용하여 프로필 데이터에 사용할 파생된 속성을 만드는 방법에 대한 개요를 제공합니다.
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# 파생 특성

파생된 특성을 사용하면 일반 케이던스에 대한 속성을 계산하고 선택적으로 이러한 파생된 특성을 실시간 고객 프로필에 프로필 속성으로 게시할 수 있습니다.

프로필 데이터를 분석하는 다양한 사용 사례에 필요한 데코일 데이터로 생성된 속성과 같은 파생 특성이 있습니다. 십진수 데이터를 사용하여 백분위수 또는 주어진 속성의 등급을 기준으로 세그먼트에서 대상을 만들 수 있습니다. 예를 들어 다음과 같은 활용 사례가 있을 수 있습니다.

* 채널별 시청률을 기준으로 가장 낮은 10% 가입자 식별 이를 통해 마케터는 특정 대상을 타겟팅하고 새 가입자 패키지를 판매할 수 있습니다.
* 전체 마일을 기준으로 전단 10%에 있는 고객을 식별하고 &quot;플라이어&quot; 상태를 갖습니다. 이 대상은 새 신용 카드 오퍼의 판매를 선택적으로 타깃팅하는 데 사용될 수 있다.

## 시작하기

이 개요에서는 다음을 작업해야 합니다 [플랫폼 API 호출](../landing/api-guide.md) 및 Adobe Experience Platform의 다음 구성 요소:

* [실시간 고객 프로필 개요](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [스키마 작성 기본 사항](../xdm/schema/composition.md): XDM(Experience Data Model) 스키마 및 스키마 작성을 위한 빌딩 블록, 원칙 및 우수 사례를 소개합니다.
* [실시간 고객 프로필에 대한 스키마를 활성화하는 방법](../profile/tutorials/add-profile-data.md): 이 자습서에서는 실시간 고객 프로필에 데이터를 추가하는 데 필요한 단계를 간략하게 설명합니다.

## 파생 특성에 대한 SQL 지원

특정 차원(카테고리) 및 해당 지표(매출, 포인트, 방문자 기간 등)를 기반으로 10차 파일의 등급을 정의하려면, 그룹 조정을 위해 스키마를 설계해야 합니다. 이 스키마는 더 큰 프로필 스키마의 일부로 사용할 수 있습니다.

### 프로필 스키마에 대한 ID 네임스페이스 만들기 {#identity-namespace}

ID 네임스페이스는 [ ID 서비스](../identity-service/home.md)의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 프로필 조각에서 레코드 데이터를 일치시키고 병합하는 경우 ID 값과 네임스페이스가 모두 일치해야 합니다.

ID와 관련하여 생성된 데이터 세트는 데이터 그룹으로 그룹화할 수 있으며 데이터 수명 주기를 유지하는 데 도움이 됩니다. 사용자 지정 네임스페이스는 [ID 서비스 API](../identity-service/api/create-custom-namespace.md) 또는 UI를 통해 자세한 내용은 [사용자 지정 네임스페이스 설명서 관리](../identity-service/namespaces.md#manage-namespaces) ui를 통해 이 작업을 수행하는 방법에 대한 지침을 참조하십시오.

기본 ID 설명자는 스키마 UI의 필드에 할당하거나 스키마 레지스트리 API를 사용하여 생성할 수 있습니다. 방법에 대한 지침은 설명서를 참조하십시오 [Adobe Experience Platform UI에서 ID 필드 정의](../xdm/ui/fields/identity.md#define-an-identity-field)또는 [스키마 레지스트리 API](../xdm/api/descriptors.md#create).

또한 Query Service를 사용하면 SQL을 통해 직접 Ad Hoc 스키마 데이터 세트 필드에 대한 ID 또는 기본 ID를 설정할 수 있습니다. 다음 문서를 참조하십시오. [ad hoc 스키마 ID에서 보조 ID 및 기본 ID 설정](./data-governance/ad-hoc-schema-identities.md) 추가 정보.

## 파생 특성 만들기

이 문서에서 제공하는 예제 쿼리는 큰 데이터 세트를 분류하고 데이터를 가장 높은 값에서 가장 낮은 값(또는 그 반대의 경우)으로 분류하고 기간을 기준으로 필터링하는 데 중점을 둡니다.

### 디킬레스 {#deciles}

디파일은 등급 데이터 세트를 10개의 동일한 부분으로 분할하는 방법입니다. 데이터를 십분위수로 분할하면 데이터 세트의 각 행에 십중계 등급이 지정됩니다. 이렇게 하면 데이터를 내림차순이나 오름차순으로 정렬할 수 있습니다.

십진수 등급은 데이터를 가장 낮은 것부터 가장 높은 순으로 정렬하고 연속되는 각 숫자가 10%포인트의 증가에 해당하는 1-10의 배율로 수행됩니다.

십진수 버킷은 등급 그룹 수를 나타내며 데이터 집합에 있는 차원(카테고리)에 등급을 지정하는 데 사용됩니다. 버킷은 각 파티션에 대한 양의 정수 값으로 평가되는 숫자 또는 식일 수 있습니다. 버킷에는 null 값이 없어야 합니다.

사분위수는 분포를 4로 나누어 백분위수를 100으로 나누는 데 사용됩니다.

### 디파일 버킷에 대한 스키마 만들기 {#create-schema}

십진수 버킷용으로 생성된 스키마에는 세 가지 필수 부분이 있습니다. 데이터 유형, 데이터 유형의 필드 그룹(소스 데이터 세트당) 및 기본 ID 필드입니다.

>[!NOTE]
>
>스키마를 만들려면 먼저 ID 네임스페이스를 만들어야 합니다. 자세한 내용은 [id 네임스페이스](#identity-namespace) 섹션을 참조하십시오.

Adobe은 XDM 개별 프로필 및 XDM ExperienceEvent를 포함한 몇 가지 표준(&quot;코어&quot;) XDM 클래스를 제공합니다. 이러한 핵심 클래스 외에도 고유한 사용자 지정 클래스를 만들어 조직에 대한 더 구체적인 사용 사례를 설명할 수도 있습니다. 방법에 대한 안내서를 참조하십시오. [UI에서 스키마 만들기 및 편집](../xdm/ui/resources/schemas.md#create) 또는 [스키마 레지스트리 API의 스키마 끝점](../xdm/api/schemas.md#create) 자세한 내용

실시간 고객 프로필에서 사용하기 위해 Experience Platform에 수집되는 데이터는 프로필에 대해 활성화된 XDM(Experience Data Model) 스키마를 준수해야 합니다. 프로필에 대해 스키마를 활성화하려면 XDM 개별 프로필 또는 XDM ExperienceEvent 클래스를 구현해야 합니다.

다음을 수행할 수 있습니다 [스키마 레지스트리 API를 사용하여 실시간 고객 프로필에 사용할 스키마를 활성화](../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 사용자 인터페이스](../xdm/tutorials/create-schema-ui.md).  프로필용 스키마를 활성화하는 방법에 대한 자세한 지침은 해당 설명서에서 확인할 수 있습니다.

### 데이터 유형 만들기 {#create-data-type}

데이터 유형은 클래스 또는 스키마 필드 그룹에서 참조 유형 필드로 사용되며 스키마의 모든 위치에 포함할 수 있는 다중 필드 구조를 일관되게 사용할 수 있습니다. 데이터 형식을 만드는 것은 모든 데칠리 관련 필드 그룹에 다시 사용할 수 있으므로 샌드박스당 한 번의 단계입니다.

방법에 대한 지침은 설명서를 참조하십시오 [사용자 지정 데이터 유형 정의](../xdm/api/data-types.md) 사용 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### 십자 필드 그룹을 만듭니다 {#create-field-group}

필드 그룹을 만드는 것은 샌드박스당 1회 단계입니다. 또한 모든 디파일 관련 스키마에 다시 사용할 수 있습니다.

방법에 대한 지침은 설명서를 참조하십시오 [UI를 통해 필드 그룹 만들기](../xdm/ui/resources/field-groups.md#create)

## Query Service를 사용하여 Decimal 파일을 만듭니다.

Query Service는 카테고리적 분류법을 포함하는 데이터 세트를 만드는 이상적인 방법을 제공합니다. 그런 다음 특성 등급을 기반으로 대상을 만들기 위해 세그멘테이션 서비스와 함께 사용할 수 있습니다.

다음 예제에 표시된 개념은 카테고리(차원)가 정의되어 있고 지표를 사용할 수 있는 한 다른 데코일 버킷 데이터 세트를 만들기 위해 적용할 수 있습니다. 이러한 예는 항공사 충성도 체계에 대한 데이터를 기반으로 합니다. 항공사의 충성도 데이터는 각 이벤트가 비즈니스 거래의 레코드인 경험 이벤트 클래스를 사용합니다 **마일리지**, 기여 또는 기여 및 멤버십 **충성도 상태** &quot;Flyer&quot;, &quot;Frequency&quot;, &quot;Silver&quot; 또는 &quot;Gold&quot; 중 하나. 기본 ID 필드는 다음과 같습니다. `membershipNumber`.

### 쿼리 템플릿 만들기 {#create-a-query-template}

템플릿은 UI의 쿼리 편집기를 사용하거나 [쿼리 서비스 API](./api/query-templates.md#create-a-query-template).

아래에 표시되는 쿼리 템플릿의 섹션은 자세히 검사됩니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### 전환 확인 기간

데이터 유형 1, 3, 6, 9, 12 및 라이프타임 룩백에 대한 버킷이 포함되어 있습니다. 이 쿼리는 1, 3 및 6개월의 전환 기간을 사용하므로 각 전환 기간에 대한 임시 테이블을 생성하기 위해 각 섹션에 몇 가지 &quot;반복&quot; 쿼리를 포함합니다.

>[!NOTE]
>
>소스 데이터에 전환 확인 기간을 결정하는 데 사용할 수 있는 열이 없는 경우 모든 데이터 클래스 등급은 `decileMonthAll`.

#### 집계

일반적인 테이블 표현식(CTE)을 사용하여 데코일 버킷을 만들기 전에 마일리지를 함께 집계하십시오. 이렇게 하면 특정 전환 확인 기간에 대한 총 마일이 제공됩니다. CTE는 일시적으로 존재하며 더 큰 쿼리의 범위 내에서만 사용할 수 있습니다.

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

### 쿼리 템플릿 실행

쿼리는 [ui를 통해 실행됨](./ui/user-guide.md#executing-queries) 또는 [쿼리 서비스 API](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

십분위수를 사용하므로 순위 번호와 백분위수 간의 상관 관계는 쿼리 결과에서 보장됩니다. 각 등급은 10%와 같으므로 상위 30%를 기반으로 대상을 식별하려면 1, 2 및 3등급을 타깃팅해야 합니다.

## 다음 단계

세그멘테이션 서비스에서는 이러한 decile 버킷을 기반으로 대상을 생성할 수 있도록 해주는 사용자 인터페이스 및 RESTful API를 제공합니다. 자세한 내용은 [세그먼테이션 서비스 개요](../segmentation/home.md) 세그먼트 만들기, 평가 및 액세스 방법에 대한 자세한 내용을 참조하십시오.

세그먼트 빌더(세그먼테이션 서비스의 UI 구현)에서 세그먼트를 만들고 사용하는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](../segmentation/ui/overview.md).

API를 사용하여 세그먼트 정의 작성에 대한 자세한 내용은 [api를 사용하여 대상 세그먼트 만들기](../segmentation/tutorials/create-a-segment.md).
