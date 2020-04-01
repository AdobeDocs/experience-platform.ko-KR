---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 매개 변수를 사용하여 카탈로그 데이터 필터링
topic: developer guide
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 쿼리 매개 변수를 사용하여 카탈로그 데이터 필터링

카탈로그 서비스 API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. 카탈로그에 대한 우수 사례 중 하나는 API에 대한 로드를 줄이고 전반적인 성능을 개선하기 위해 모든 API 호출에 필터를 사용하는 것입니다.

이 문서에서는 API에서 카탈로그 개체를 필터링하는 가장 일반적인 방법에 대해 간략하게 설명합니다. 카탈로그 API와 상호 작용하는 방법에 대한 자세한 내용은 [카탈로그 개발자 안내서를](getting-started.md) 읽는 동안 이 문서를 참조하는 것이 좋습니다. 카탈로그 서비스에 대한 자세한 내용은 카탈로그 [개요를](../home.md)참조하십시오.

## 반환된 개체 제한

쿼리 매개 `limit` 변수는 응답으로 반환되는 개체 수를 제한합니다. 카탈로그 응답은 구성된 제한에 따라 자동으로 측정됩니다.

* 매개 변수를 지정하지 않으면 응답 페이로드당 최대 개체 수는 20개입니다. `limit`
* 데이터 집합 쿼리의 경우 `observableSchema` 쿼리 매개 변수를 사용하여 `properties` 요청하는 경우 반환되는 데이터 집합의 최대 수는 20개입니다.
* 다른 모든 카탈로그 쿼리에 대한 전체 제한은 100개의 개체입니다.
* 잘못된 `limit` 매개 변수(포함 `limit=0`)로 인해 적절한 범위의 윤곽이 지정된 400수준 오류 응답이 발생합니다.
* 쿼리 매개 변수로 전달되는 제한이나 오프셋은 헤더로 전달되는 제한이나 오프셋보다 우선합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 반환할 개체의 수를 1부터 100까지 나타내는 정수입니다. |

**요청**

다음 요청은 3개의 개체로 응답을 제한하는 동안 데이터 집합 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `limit` 쿼리 매개 변수로 지정된 수로 제한된 데이터 집합 목록을 반환합니다.

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

매개 변수를 사용하여 반환되는 개체 수를 필터링할 때도 반환된 개체 자체에 실제 필요한 정보보다 많은 정보가 포함될 수 있습니다. `limit` 시스템의 부하를 더 줄이기 위해 필요한 속성만 포함하도록 응답을 필터링하는 것이 좋습니다.

매개 `properties` 변수는 응답 개체를 필터링하여 지정된 속성 집합만 반환합니다. 매개 변수를 하나 또는 여러 속성을 반환하도록 설정할 수 있습니다.

이 `properties` 매개 변수는 최상위 수준의 객체 속성만 허용하므로 다음 샘플 객체의 경우 필터, 필터 및 필터 `name`를 적용할 수 `description`있지만 NOT은 적용할 수 `subItem``sampleKey`있습니다.

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
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 응답 본문에 포함할 속성의 이름입니다. |
| `{OBJECT_ID}` | 검색할 특정 카탈로그 개체의 고유 식별자입니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색합니다. 매개 변수 아래에 제공된 속성 이름의 쉼표로 구분된 목록은 응답으로 반환되는 속성을 나타냅니다. `properties` 반환되는 데이터 집합 수를 제한하는 매개 `limit` 매개 변수도 포함됩니다. 요청에 `limit` 매개 변수가 없으면 응답에 최대 20개의 개체가 포함됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 속성만 표시된 카탈로그 개체 목록을 반환합니다.

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

위의 응답에 따라 다음을 유추할 수 있습니다.

* 요청된 속성이 없는 객체에는 포함된 요청된 속성만 표시됩니다.(`Dataset1`)
* 개체에 요청된 속성이 없으면 빈 개체로 표시됩니다.(`Dataset2`)
* 데이터 세트에 속성이 포함되어 있지만 값이 없는 경우 요청된 속성을 빈 개체로 반환할 수 있습니다.(`Dataset3`)
* 그렇지 않으면 데이터 세트에 요청된 모든 속성의 전체 값이 표시됩니다.(`Dataset4`)

## 응답 목록의 오프셋 시작 인덱스

쿼리 매개 변수는 0부터 시작하는 번호 매기기를 사용하여 응답 목록을 지정된 번호로 오프셋합니다. `start` 예를 들어 세 번째 나열된 객체에서 시작할 응답을 `start=2` 오프셋합니다.

매개 `start` `limit` 변수가 매개 변수와 일치하지 않으면 반환되는 최대 개체 수는 20개입니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 응답을 오프셋할 개체 수를 나타내는 정수입니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색하여 다섯 번째 개체(`start=4`)로 오프셋하고 두 개의 반환된 데이터 집합(`limit=2`)으로 응답을 제한합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 두 개의 최상위 항목(`limit=2`)이 들어 있는 JSON 개체가 포함되어 있으며, 각 데이터 세트에 대해 하나씩, 세부 사항(예제의 세부 사항은 요약됨)이 포함되어 있습니다. 응답은 4로 이동되며(`start=4`) 표시된 데이터 세트는 시간순으로 5번 및 6번입니다.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 태그로 필터링

일부 카탈로그 개체는 `tags` 속성 사용을 지원합니다. 태그는 개체에 정보를 첨부한 다음 나중에 해당 개체를 검색하는 데 사용할 수 있습니다. 사용할 태그의 선택 및 적용 방법은 조직 프로세스에 따라 다릅니다.

태그 사용 시 고려해야 할 몇 가지 제한 사항이 있습니다.

* 현재 태그를 지원하는 Catalog 개체는 데이터 집합, 배치 및 연결뿐입니다.
* 태그 이름은 IMS 조직에 고유합니다.
* Adobe 프로세스는 특정 동작에 태그를 활용할 수 있습니다. 이러한 태그의 이름에는 &quot;adobe&quot;가 표준 접두사로 추가됩니다. 따라서 태그 이름을 선언할 때는 이 규칙을 사용하지 않아야 합니다.
* 다음 태그 이름은 경험 플랫폼 전체에서 사용하도록 예약되어 있으므로 조직의 태그 이름으로 선언할 수 없습니다.
   * `unifiedProfile`:이 태그 이름은 실시간 고객 프로필에서 인제스트할 데이터 [세트에 대해 예약되어 있습니다](../../profile/home.md).
   * `unifiedIdentity`:이 태그 이름은 Identity Service에서 인제스트할 데이터 세트에 [대해 예약됩니다](../../identity-service/home.md).

다음은 `tags` 속성을 포함하는 데이터 집합의 예입니다. 해당 속성 내의 태그는 키-값 쌍의 형태를 취하며 각 태그 값은 단일 문자열이 포함된 배열로 표시됩니다.

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
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

매개 변수의 값은 `tags` 형식을 사용하여 키-값 쌍의 형식을 사용합니다 `{TAG_NAME}:{TAG_VALUE}`. 여러 개의 키-값 쌍을 쉼표로 구분된 목록 형식으로 제공할 수 있습니다. 여러 태그가 제공되면 AND 관계가 가정됩니다.

이 매개 변수는 태그 값에 대해 와일드카드 문자(`*`)를 지원합니다. 예를 들어, 검색 문자열은 태그 값이 &quot;test&quot;로 시작하는 모든 객체를 `test*` 반환합니다. 와일드카드로만 구성된 검색 문자열을 사용하여 값에 상관없이 특정 태그가 포함되어 있는지 여부를 기준으로 객체를 필터링할 수 있습니다.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 필터링할 태그의 이름입니다. |
| `{TAG_VALUE}` | 필터링할 태그의 값입니다. 와일드카드 문자(`*`)를 지원합니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색하여 특정 값이 있는 태그와 현재 있는 두 번째 태그를 기준으로 필터링합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 값이 &quot;123456&quot; `sampleTag` 이고 값이 있는 데이터 집합 목록을 반환합니다 `secondTag` . 또한 제한을 지정하지 않으면 응답에 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

카탈로그 API의 일부 끝점에는 대부분의 경우 날짜 범위 쿼리를 허용하는 쿼리 매개 변수가 있습니다.

**API 형식**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch 시간의 datetime 정수입니다. |

**요청**

다음 요청은 2019년 4월 동안 만들어진 일괄 처리 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 지정된 날짜 범위 내에 있는 카탈로그 개체 목록이 포함됩니다. 또한 제한을 지정하지 않으면 응답에 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

쿼리 매개 변수를 사용하면 지정된 속성 값을 기준으로 응답 데이터를 정렬(순서 지정)할 수 있습니다. `orderBy` 이 매개 변수에는 &quot;direction&quot;`asc` (오름차순 또는 `desc` 내림차순)이 뒤에 콜론(`:`)이 오는 다음 결과를 정렬하는 속성이 필요합니다. 방향을 지정하지 않으면 기본 방향은 오름차순입니다.

여러 정렬 속성을 쉼표로 구분된 목록으로 제공할 수 있습니다. 첫 번째 정렬 속성이 해당 속성에 대해 동일한 값이 들어 있는 여러 개의 객체를 만드는 경우 두 번째 정렬 속성이 해당 일치하는 객체를 더 정렬하는 데 사용됩니다.

예를 들어 다음 쿼리를 고려해 보십시오. `orderBy=name,desc:created`Adobe 결과는 첫 번째 정렬 속성을 기준으로 오름차순으로 정렬됩니다 `name`. 여러 레코드가 동일한 `name` 속성을 공유하는 경우 일치하는 레코드가 두 번째 정렬 속성으로 정렬됩니다 `created`. 반환된 레코드가 동일한 `name`레코드를 공유하지 않으면 `created` 속성이 정렬에 영향을 주지 않습니다.


**API 형식**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 결과를 정렬할 속성의 이름입니다. |

**요청**

다음 요청은 해당 `name` 속성별로 정렬된 데이터 집합 목록을 검색합니다. 데이터 집합이 동일한 `name`데이터를 공유하면 해당 데이터 집합은 `updated` 속성 순서대로 내림차순으로 정렬됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 `orderBy` 매개 변수에 따라 정렬된 카탈로그 개체 목록이 포함됩니다. 또한 제한을 지정하지 않으면 응답에 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

카탈로그는 다음 섹션에 자세히 설명된 속성별로 필터링하는 두 가지 방법을 제공합니다.

* [간단한 필터](#using-simple-filters)사용:특정 속성이 특정 값과 일치하는지 여부를 기준으로 필터링합니다.
* [속성 매개 변수](#using-the-property-parameter)사용:조건부 표현식을 사용하여 속성이 있는지 여부 또는 속성의 값이 다른 지정된 값 또는 정규 표현식과 일치하는지, 근접하거나, 근사치를 적용하는지 또는 비교하는지 여부를 필터링할 수 있습니다.

### 간단한 필터 사용 {#using-simple-filters}

단순 필터를 사용하면 특정 속성 값을 기반으로 응답을 필터링할 수 있습니다. 단순 필터는 형식을 `{PROPERTY_NAME}={VALUE}`취합니다.

예를 들어 쿼리는 `name=exampleName` 속성에 &quot;exampleName&quot;의 값이 포함된 객체만 `name` 반환합니다. 반면 쿼리는 속성이 &quot;exampleName&quot;이 `name=!exampleName` 아닌 `name` **** 객체만 반환합니다.

또한 단순 필터는 단일 속성에 대해 여러 값을 쿼리하는 기능을 지원합니다. 여러 값이 제공되면 응답에서는 속성이 제공된 목록의 값과 일치하는 **** 객체를 반환합니다. 목록에 `!` 문자를 접두사로 추가하여 다중 값 쿼리를 변환할 수 있으며 속성 값이 제공된 목록에 **없는** 객체만 반환합니다(예: `name=!exampleName,anotherName`).

**API 형식**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 값을 필터링할 속성의 이름입니다. |
| `{VALUE}` | 포함할(또는 쿼리에 따라 제외)의 결과를 결정하는 속성 값입니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색하며, 필터링되어 속성 값이 &quot;exampleName&quot; 또는 &quot;anotherName&quot;인 데이터 `name` 집합만 포함합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 &quot;exampleName&quot; 또는 &quot;anotherName&quot; `name` 인 데이터 집합을 제외한 데이터 집합 목록이 포함됩니다. 또한 제한을 지정하지 않으면 응답에 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

### 매개 변수 `property` 사용 {#using-the-property-parameter}

쿼리 매개 변수는 `property` 단순 필터보다 속성 기반 필터링에 더 많은 유연성을 제공합니다. 속성에 특정 값이 있는지 여부를 기반으로 필터링하는 것 외에도 `property` 매개 변수는 다른 비교 연산자(예: &quot;보다 큼&quot;(`>`) 및 &quot;보다 작음&quot;(`<`)와 같은 정규 표현식을 사용하여 속성 값별로 필터링할 수 있습니다. 또한 해당 값에 상관없이 속성이 존재하는지 여부를 기준으로 필터링할 수 있습니다.

이 `property` 매개 변수는 최상위 수준의 객체 속성만 허용하므로 다음 샘플 객체의 경우 속성을 기준으로 `name``description`필터링할 수 `subItem`있지만 NOT은 사용할 수 `sampleKey`있습니다.

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
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 쿼리할 속성과 값을 평가하는 방법을 나타내는 조건부 표현식. 예는 아래에 나와 있습니다. |

매개 변수의 값은 여러 종류의 조건부 표현식을 지원합니다. `property` 다음 표에서는 지원되는 표현식에 대한 기본 구문에 대해 설명합니다.

| 기호 | 설명 | 예 |
| --- | --- | --- |
| (없음) | 연산자가 없는 속성 이름을 지정하면 값에 관계없이 속성이 있는 객체만 반환됩니다. | `property=name` |
| ! | 매개 변수 값에 &quot;`!`&quot;를 접두사로 사용하면 속성이 `property` 없는 **** 객체만 반환됩니다. | `property=!name` |
| ~ | 속성 값(문자열)이 물결표(`~`) 기호 다음에 제공된 정규 표현식과 일치하는 객체만 반환합니다. | `property=name~^example` |
| == | 이중 같음 기호(`==`) 다음에 제공된 문자열과 속성 값이 정확히 일치하는 객체만 반환합니다. | `property=name==exampleName` |
| != | 같지 않음 기호( **) 다음에 제공된 문자열과 속성 값이 일치하지** 않는`!=`객체만 반환합니다. | `property=name!=exampleName` |
| &lt; | 속성 값이 지정된 양보다 작거나 같지 않은 개체만 반환합니다. | `property=version<1.0.0` |
| &lt;= | 속성 값이 지정된 양보다 작거나 같은 객체만 반환합니다. | `property=version<=1.0.0` |
| > | 속성 값이 지정된 양보다 크거나 같지 않은 개체만 반환합니다. | `property=version>1.0.0` |
| >= | 속성 값이 지정된 양보다 크거나 같은 객체만 반환합니다. | `property=version>=1.0.0` |

>[!NOTE] 이 `name` `*`속성은 전체 검색 문자열 또는 와일드카드의 일부로 와일드카드 사용을 지원합니다. 와일드카드는 검색 문자열이 값 &quot;test&quot;와 `te*st` 일치하도록 빈 문자와 일치합니다. 별표는 두 배로 옮겨서 escape됩니다(`**`). 검색 문자열의 이중 별표는 단일 별표를 리터럴 문자열로 나타냅니다.

**요청**

다음 요청은 버전 번호가 1.0.3보다 큰 데이터 세트를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 버전 번호가 1.0.3보다 큰 데이터 집합 목록이 포함됩니다.또한 제한을 지정하지 않으면 응답에 최대 20개의 개체가 포함됩니다.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

앰퍼샌드(`&`)를 사용하면 하나의 요청에 여러 필터를 결합할 수 있습니다. 요청에 추가 조건이 추가되면 AND 관계가 가정합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
