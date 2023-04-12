---
keywords: Experience Platform;홈;인기 항목;필터;필터;데이터 필터링;데이터 필터링;날짜 범위
solution: Experience Platform
title: 쿼리 매개 변수를 사용하여 카탈로그 데이터 필터링
description: 카탈로그 서비스 API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. 카탈로그에 대한 우수 사례의 일부는 API의 로드를 줄이고 전체 성능을 개선하기 위해 모든 API 호출에서 필터를 사용하는 것입니다.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 1%

---

# 필터 [!DNL Catalog] 쿼리 매개 변수를 사용한 데이터

다음 [!DNL Catalog Service] API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. 에 대한 우수 사례 [!DNL Catalog] 는 API의 로드를 줄이고 전체 성능을 개선하기 위해 모든 API 호출에서 필터를 사용하는 것입니다.

이 문서에서는 필터링에 대한 가장 일반적인 방법을 간략하게 설명합니다 [!DNL Catalog] API의 개체. 문서를 읽는 동안 이 문서를 참조하는 것이 좋습니다 [카탈로그 개발자 안내서](getting-started.md) 와 상호 작용하는 방법에 대해 자세히 알아보기 [!DNL Catalog] API. 자세한 내용은 [!DNL Catalog Service]를 참조하고 [[!DNL Catalog] 개요](../home.md).

## 반환된 개체 제한

다음 `limit` 쿼리 매개 변수는 응답에서 반환되는 개체 수를 제한합니다. [!DNL Catalog] 구성된 제한에 따라 응답이 자동으로 측정됩니다.

* 다음과 같은 경우 `limit` 매개 변수를 지정하지 않았습니다. 응답 페이로드당 최대 개체 수는 20개입니다.
* 데이터 집합 쿼리의 경우 `observableSchema` 는 `properties` 쿼리 매개 변수인 반환되는 최대 데이터 세트 수는 20개입니다.
* 다른 모든 카탈로그 쿼리에 대한 전역 제한은 100개의 개체입니다.
* 유효하지 않습니다 `limit` 매개 변수(포함) `limit=0`)이면 적절한 범위를 간략하게 하는 400 수준 오류 응답이 발생합니다.
* 쿼리 매개 변수로 전달되는 제한 또는 오프셋은 헤더로 전달되는 제한 또는 오프셋보다 우선합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 반환할 개체 수를 나타내는 정수(1부터 100까지)입니다. |

**요청**

다음 요청은 응답을 세 개의 개체로 제한하는 동안 데이터 세트 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 데이터 세트 목록이 반환되고, 이는 로 표시된 숫자로 제한됩니다 `limit` 쿼리 매개 변수.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 표시된 속성 제한

를 사용하여 반환되는 개체 수를 필터링할 때에도 `limit` 매개 변수를 사용하면 반환된 객체 자체가 실제로 필요한 정보보다 많은 정보를 포함할 수 있습니다. 시스템의 로드를 더 줄이려면 필요한 속성만 포함하도록 응답을 필터링하는 것이 좋습니다.

다음 `properties` 매개 변수는 지정된 속성 집합만 반환하도록 응답 개체를 필터링합니다. 매개 변수는 하나 이상의 속성을 반환하도록 설정할 수 있습니다.

다음 `properties` 매개 변수는 최상위 객체 속성만 허용합니다. 즉, 다음 샘플 객체의 경우 필터를 적용할 수 있습니다 `name`, `description`, 및 `subItem`, ( 는 아님) `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API 형식**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 응답 본문에 포함할 속성의 이름입니다. |
| `{OBJECT_ID}` | 특정 대상의 고유 식별자입니다 [!DNL Catalog] 개체를 검색하는 중입니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색합니다. 아래에 제공되는 속성 이름의 쉼표로 구분된 목록입니다 `properties` 매개 변수는 응답에서 반환할 속성을 나타냅니다. A `limit` 매개 변수도 포함되어 반환되는 데이터 세트 수를 제한합니다. 요청에 `limit` 매개 변수에는 최대 20개의 개체가 포함됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 목록을 반환합니다. [!DNL Catalog] 요청된 속성만 표시된 객체입니다.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

위의 응답에 따라 다음을 추론할 수 있습니다.

* 개체에 요청된 속성이 없으면 개체에 포함된 요청된 속성만 표시됩니다. (`Dataset1`)
* 개체에 요청된 속성이 포함되지 않으면 빈 개체로 표시됩니다. (`Dataset2`)
* 데이터 집합에 속성이 포함되어 있지만 값이 없는 경우 요청한 속성을 빈 개체로 반환할 수 있습니다. (`Dataset3`)
* 그렇지 않으면 데이터 집합에 요청된 모든 속성의 전체 값이 표시됩니다. (`Dataset4`)

>[!NOTE]
>
>에서 `schemaRef` 각 데이터 세트에 대한 속성, 버전 번호는 스키마의 최신 부 버전을 나타냅니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오.

## 응답 목록의 오프셋 시작 인덱스

다음 `start` 쿼리 매개 변수는 영(0) 기반 번호 지정을 사용하여 응답 목록을 지정된 숫자로 오프셋합니다. 예, `start=2` 세 번째 나열된 개체에서 시작할 응답을 오프셋합니다.

만약 `start` 매개 변수가 `limit` 매개 변수에는 반환되는 최대 개체 수가 20개입니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 응답을 오프셋할 개체 수를 나타내는 정수입니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색하여 다섯 번째 개체(`start=4`)를 클릭하고 응답을 두 개의 반환된 데이터 세트(`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

이 응답에는 두 개의 최상위 항목(`limit=2`). 각 데이터 세트 및 세부 정보에 대해 하나씩,(세부 사항은 예에서 요약됨). 응답이 4로 바뀝니다(`start=4`). 즉, 표시된 데이터 세트는 연대순으로 5번 및 6번.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 태그로 필터링

일부 카탈로그 개체는 `tags` 속성을 사용합니다. 태그는 개체에 정보를 연결한 다음 나중에 해당 개체를 검색하는 데 사용할 수 있습니다. 사용할 태그와 태그를 적용하는 방법 중 선택은 조직 프로세스에 따라 다릅니다.

태그를 사용할 때는 다음과 같은 몇 가지 제한 사항이 있습니다.

* 현재 태그를 지원하는 유일한 카탈로그 개체는 데이터 세트, 배치 및 연결입니다.
* 태그 이름은 조직에 고유합니다.
* Adobe 프로세스는 특정 동작에 대한 태그를 활용할 수 있습니다. 이러한 태그의 이름에는 &quot;adobe&quot; 접두사가 표준 태그로 붙습니다. 따라서 태그 이름을 선언할 때에는 이 규칙을 사용하지 않아야 합니다.
* 다음 태그 이름은 여러 곳에서 사용할 수 있도록 예약되어 있습니다 [!DNL Experience Platform], 따라서 를 조직의 태그 이름으로 선언할 수 없습니다.
   * `unifiedProfile`: 이 태그 이름은 데이터 세트용으로 예약되어 있습니다. [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: 이 태그 이름은 데이터 세트용으로 예약되어 있습니다. [[!DNL Identity Service]](../../identity-service/home.md).

다음은 를 포함하는 데이터 집합의 예입니다 `tags` 속성을 사용합니다. 해당 속성 내의 태그는 키-값 쌍의 형태를 취하며 각 태그 값은 단일 문자열을 포함하는 배열로 표시됩니다.

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API 형식**

에 대한 값 `tags` 매개 변수는 형식을 사용하여 키-값 쌍의 형식을 취합니다 `{TAG_NAME}:{TAG_VALUE}`. 여러 키-값 쌍은 쉼표로 구분된 목록 형태로 제공할 수 있습니다. 여러 태그를 제공하면 AND 관계를 가정합니다.

매개 변수는 와일드카드 문자(`*`) 내의 아무 곳에나 삽입할 수 있습니다. 예를 들어 `test*` 태그 값이 &quot;test&quot;로 시작되는 모든 개체를 반환합니다. 와일드카드만으로 구성된 검색 문자열을 사용하여 값에 관계없이 특정 태그가 포함되어 있는지 여부에 따라 객체를 필터링할 수 있습니다.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 필터링할 태그의 이름입니다. |
| `{TAG_VALUE}` | 필터링할 태그의 값입니다. 와일드카드 문자(`*`). |

**요청**

다음 요청은 데이터 세트 목록을 검색하여 특정 값 AND 두 번째 태그가 있는 하나의 태그로 필터링합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 를 포함하는 데이터 세트 목록을 반환합니다 `sampleTag` 값 &quot;123456&quot;, AND 사용 `secondTag` 값 포함. 제한을 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## 날짜 범위별로 필터링

의 일부 엔드포인트 [!DNL Catalog] API에는 대부분의 경우 날짜 범위 쿼리를 허용하는 쿼리 매개 변수가 있습니다.

**API 형식**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch 시간의 날짜/시간 정수입니다. |

**요청**

다음 요청은 2019년 4월 한 달 동안 생성된 배치 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 [!DNL Catalog] 지정한 날짜 범위에 속하는 개체입니다. 제한을 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 속성별 정렬

다음 `orderBy` 쿼리 매개 변수를 사용하면 지정된 속성 값을 기준으로 응답 데이터를 정렬(순서)할 수 있습니다. 이 매개 변수에는 &quot;direction&quot;(`asc` 오름차순 또는 `desc` 내림차순의 경우) 뒤에 콜론(`:`)를 클릭한 다음 결과를 기준으로 정렬하는 속성을 사용합니다. 방향을 지정하지 않으면 기본 방향은 오름차순입니다.

쉼표로 구분된 목록으로 여러 정렬 속성을 제공할 수 있습니다. 첫 번째 정렬 속성에서 해당 속성에 대해 동일한 값을 포함하는 여러 개체를 생성하면 두 번째 정렬 속성이 해당 일치하는 개체를 추가로 정렬하는 데 사용됩니다.

예를 들어 다음 쿼리를 고려해 보십시오. `orderBy=name,desc:created`. 결과는 첫 번째 정렬 속성을 기준으로 오름차순으로 정렬됩니다. `name`. 여러 레코드가 동일한 경우 `name` 등록 정보에서 일치하는 레코드는 두 번째 정렬 등록 정보별로 정렬됩니다. `created`. 반환된 레코드가 동일한 레코드를 공유하지 않는 경우 `name`, `created` 속성은 정렬에 영향을 주지 않습니다.


**API 형식**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 결과를 정렬하는 속성의 이름입니다. |

**요청**

다음 요청은 데이터 세트별로 정렬된 목록을 검색합니다 `name` 속성을 사용합니다. 데이터 세트가 동일한 경우 `name`로 설정되면 해당 데이터 세트는 순서대로 정렬됩니다 `updated` 속성을 내림차순으로 표시합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 [!DNL Catalog] 정렬된 개체 `orderBy` 매개 변수. 제한을 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 속성별 필터링

[!DNL Catalog] 에서는 다음 섹션에 자세히 설명되어 있는 속성에 따라 필터링하는 두 가지 방법을 제공합니다.

* [단순 필터 사용](#using-simple-filters): 특정 속성이 특정 값과 일치하는지 여부에 따라 필터링합니다.
* [속성 매개 변수 사용](#using-the-property-parameter): 조건부 표현식을 사용하여 속성이 있는지 여부 또는 속성 값이 지정된 다른 값 또는 정규 표현식과 일치하는지, 근사값이나 비교되는지 여부를 필터링합니다.

### 단순 필터 사용 {#using-simple-filters}

단순 필터를 사용하면 특정 속성 값에 따라 응답을 필터링할 수 있습니다. 간단한 필터는 `{PROPERTY_NAME}={VALUE}`.

예: 쿼리 `name=exampleName` 다음 `name` 속성에 &quot;exampleName&quot; 값이 포함되어 있습니다. 반대로 쿼리는 `name=!exampleName` 다음 `name` property **not** &quot;exampleName&quot;.

또한 단순 필터는 단일 속성에 대해 여러 값을 쿼리하는 기능을 지원합니다. 여러 값을 제공하면 속성이 일치하는 개체를 반환합니다 **임의** 제공된 목록에 있는 값 중에서 선택합니다. 다중 값 쿼리를 접두사로 변환할 수 있습니다 `!` 목록에 문자를 추가하여 속성 값이 인 객체만 반환합니다. **not** 제공된 목록(예: `name=!exampleName,anotherName`).

**API 형식**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 값을 필터링할 속성의 이름입니다. |
| `{VALUE}` | 포함할(또는 쿼리에 따라 제외) 결과를 결정하는 속성 값입니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색하는 경우 `name` 속성에는 &quot;exampleName&quot; 또는 &quot;anotherName&quot; 값이 있습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 `name` 는 &quot;exampleName&quot; 또는 &quot;anotherName&quot;입니다. 제한을 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### 사용 `property` 매개 변수 {#using-the-property-parameter}

다음 `property` 쿼리 매개 변수는 간단한 필터보다 속성 기반 필터링에 더 많은 유연성을 제공합니다. 속성에 특정 값이 있는지 여부를 기준으로 필터링할 뿐만 아니라 `property` 매개 변수 는 다른 비교 연산자(예: &quot;보다 큼&quot;)(`>`) 및 &quot;보다 작음&quot;(`<`) 및 속성 값별로 필터링할 정규 표현식입니다. 또한 값에 관계없이 속성이 존재하는지 여부에 따라 필터링할 수 있습니다.

다음 `property` 매개 변수는 최상위 객체 속성만 허용합니다. 즉, 다음 샘플 객체의 경우 `name`, `description`, 및 `subItem`, ( 는 아님) `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API 형식**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 쿼리할 속성과 그 값을 평가할 방법을 나타내는 조건부 식입니다. 예는 아래에 나와 있습니다. |

의 값 `property` 매개 변수는 여러 종류의 조건부 표현식을 지원합니다. 다음 표에서는 지원되는 표현식에 대한 기본 구문을 설명합니다.

| 기호 | 설명 | 예 |
| --- | --- | --- |
| (None) | 연산자가 없는 속성 이름을 지정하면 값에 관계없이 속성이 있는 객체만 반환합니다. | `property=name` |
| ! | &quot; 접두어`!`&quot; 값을 `property` 매개 변수는 속성이 수행하는 객체만 반환합니다. **not** 존재 | `property=!name` |
| ~ | 물결표(`~`) 기호를 포함합니다. | `property=name~^example` |
| == | 속성 값이 double-equals 기호(`==`). | `property=name==exampleName` |
| != | 속성 값이 수행하는 객체만 반환합니다. **not** not-equals 기호 뒤에 제공된 일치 문자열(`!=`). | `property=name!=exampleName` |
| &lt; | 속성 값이 지정된 양보다 작음(하지만 이보다 같지 않음)한 객체만 반환합니다. | `property=version<1.0.0` |
| &lt;= | 속성 값이 지정된 양보다 작거나 같은 객체만 반환합니다. | `property=version<=1.0.0` |
| > | 등록 정보 값이 지정된 양보다 크거나 같은 객체만 반환합니다. | `property=version>1.0.0` |
| >= | 속성 값이 지정된 양보다 크거나 같은 객체만 반환합니다. | `property=version>=1.0.0` |

>[!NOTE]
>
>다음 `name` 속성은 와일드카드 사용을 지원합니다 `*`를 전체 검색 문자열 또는 그 일부로 포함하거나, 와일드카드는 검색 문자열과 일치하므로 `te*st` 은 값 &quot;test&quot;와 일치합니다. 별표는 두 배로 이스케이프됩니다(`**`). 검색 문자열의 이중 별표는 단일 별표를 리터럴 문자열로 나타냅니다.

**요청**

다음 요청은 버전 번호가 1.0.3보다 큰 데이터 세트를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 버전 번호가 1.0.3보다 큰 데이터 세트 목록이 포함되어 있습니다. 제한을 지정하지 않으면 응답에는 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 여러 필터 결합

앰퍼샌드 사용(`&`), 여러 필터를 하나의 요청에 결합할 수 있습니다. 요청에 추가 조건을 추가하면 AND 관계를 가정합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
