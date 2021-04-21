---
keywords: Experience Platform;홈;인기 항목;필터;필터;필터 데이터;필터 데이터;날짜 범위
solution: Experience Platform
title: 쿼리 매개 변수를 사용하여 카탈로그 데이터 필터링
topic-legacy: developer guide
description: 카탈로그 서비스 API를 사용하면 요청 쿼리 매개 변수의 사용을 통해 응답 데이터를 필터링할 수 있습니다. 카탈로그에 대한 우수 사례 중 하나는 API에 대한 로드를 줄이고 전반적인 성능을 개선하는 데 도움이 되기 때문에 모든 API 호출에서 필터를 사용하는 것입니다.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 1%

---

# 쿼리 매개 변수를 사용하여 [!DNL Catalog] 데이터 필터링

[!DNL Catalog Service] API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. [!DNL Catalog]에 대한 우수 사례 중 하나는 API에 대한 로드를 줄이고 전반적인 성능을 개선하는 데 도움이 되기 때문에 모든 API 호출에 필터를 사용하는 것입니다.

이 문서에서는 API에서 [!DNL Catalog] 개체를 필터링하는 가장 일반적인 방법에 대해 간략히 설명합니다. [!DNL Catalog] API와 상호 작용하는 방법에 대한 자세한 내용은 [카탈로그 개발자 안내서](getting-started.md)를 읽는 동안 이 문서를 참조하는 것이 좋습니다. [!DNL Catalog Service]에 대한 자세한 내용은 [[!DNL Catalog] 개요](../home.md)를 참조하십시오.

## 반환된 개체 제한

`limit` 쿼리 매개 변수는 응답으로 반환되는 개체 수를 제한합니다. [!DNL Catalog] 구성된 제한에 따라 응답이 자동으로 측정됩니다.

* `limit` 매개 변수가 지정되지 않은 경우 응답 페이로드당 최대 개체 수는 20개입니다.
* 데이터 집합 쿼리의 경우 `properties` 쿼리 매개 변수를 사용하여 `observableSchema`이 요청되면 반환되는 데이터 집합의 최대 수는 20개입니다.
* 다른 모든 카탈로그 쿼리에 대한 전체 한도는 100개의 개체입니다.
* `limit` 매개 변수(`limit=0` 포함)가 잘못되면 적절한 범위를 외곽선으로 하는 400수준 오류 응답이 발생합니다.
* 쿼리 매개 변수로 전달되는 제한이나 오프셋은 헤더로 전달되는 제한보다 우선합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 반환할 개체의 수를 1부터 100까지 나타내는 정수입니다. |

**요청**

다음 요청은 3개의 객체로 응답을 제한하는 동안 데이터 세트 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `limit` 쿼리 매개 변수로 지정된 번호로 제한된 데이터 집합 목록을 반환합니다.

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

`limit` 매개 변수를 사용하여 반환되는 개체 수를 필터링할 때도 반환된 객체 자체에 실제 필요한 정보보다 많은 정보가 포함될 수 있습니다. 시스템의 부하를 추가로 줄이기 위해 필요한 속성만 포함하도록 응답을 필터링하는 것이 좋습니다.

`properties` 매개 변수는 지정된 속성 집합만 반환하도록 응답 개체를 필터링합니다. 매개 변수를 하나 이상의 속성을 반환하도록 설정할 수 있습니다.

`properties` 매개 변수는 최상위 객체 속성만 허용합니다. 즉, 다음 샘플 객체의 경우 `name`, `description` 및 `subItem`에 필터를 적용할 수 있지만 `sampleKey`에 대해서는 필터를 적용할 수 없습니다.

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
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 응답 본문에 포함할 속성의 이름입니다. |
| `{OBJECT_ID}` | 검색할 특정 [!DNL Catalog] 개체의 고유 식별자입니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색합니다. `properties` 매개 변수 아래에 제공된 속성 이름의 쉼표로 구분된 목록은 응답에서 반환할 속성을 나타냅니다. 반환되는 데이터 세트 수를 제한하는 `limit` 매개 변수도 포함됩니다. 요청에 `limit` 매개 변수가 포함되지 않은 경우 응답에는 최대 20개의 개체가 포함됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 요청된 속성만 표시된 [!DNL Catalog] 개체 목록이 반환됩니다.

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
* 개체에 요청된 속성이 포함되어 있지 않으면 빈 개체로 표시됩니다.(`Dataset2`)
* 데이터 세트에 속성이 포함되어 있지만 값이 없는 경우 요청된 속성을 빈 개체로 반환할 수 있습니다.(`Dataset3`)
* 그렇지 않으면 데이터 세트에 요청된 모든 속성의 전체 값이 표시됩니다.(`Dataset4`)

>[!NOTE]
>
>각 데이터 세트에 대한 `schemaRef` 속성에서 버전 번호는 스키마의 최신 부 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.

## 응답 목록의 오프셋 시작 인덱스

`start` 쿼리 매개 변수는 0부터 매기기를 사용하여 응답 목록을 지정된 번호로 오프셋합니다. 예를 들어 `start=2`은(는) 세 번째 나열된 객체에서 시작할 응답을 오프셋합니다.

`start` 매개 변수가 `limit` 매개 변수와 짝이 맞지 않으면 반환되는 최대 개체 수는 20개입니다.

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

응답에는 각 데이터 세트 및 세부 정보(예제에 세부 정보가 들어 있음)에 대한 두 개의 최상위 수준 항목(`limit=2`)이 포함된 JSON 개체가 포함됩니다. 응답이 4로 이동합니다(`start=4`). 즉, 표시된 데이터 집합은 5번, 6번 시간순으로 이동합니다.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 태그로 필터링

일부 카탈로그 개체는 `tags` 특성 사용을 지원합니다. 태그는 개체에 정보를 첨부한 다음 나중에 해당 개체를 검색하는 데 사용할 수 있습니다. 사용할 태그의 선택 및 적용 방법은 조직 프로세스에 따라 다릅니다.

태그 사용 시 고려해야 할 몇 가지 제한 사항이 있습니다.

* 현재 태그를 지원하는 Catalog 객체는 데이터 세트, 배치 및 연결뿐입니다.
* 태그 이름은 IMS 조직에 고유합니다.
* Adobe 프로세스는 특정 비헤이비어에 태그를 활용할 수 있습니다. 이러한 태그의 이름 앞에 &quot;adobe&quot;가 기본으로 붙습니다. 따라서 태그 이름을 선언할 때는 이 규칙을 사용하지 않아야 합니다.
* 다음 태그 이름은 [!DNL Experience Platform]에서 사용하도록 예약되어 있으므로 조직의 태그 이름으로 선언할 수 없습니다.
   * `unifiedProfile`:이 태그 이름은 데이터 세트에서 인제스트할 수 있도록 예약되어  [[!DNL Real-time Customer Profile]](../../profile/home.md)있습니다.
   * `unifiedIdentity`:이 태그 이름은 데이터 세트에서 인제스트할 수 있도록 예약되어  [[!DNL Identity Service]](../../identity-service/home.md)있습니다.

다음은 `tags` 속성을 포함하는 데이터 집합의 예입니다. 해당 속성 내의 태그는 키-값 쌍의 형태를 취하며 각 태그 값은 단일 문자열을 포함하는 배열로 나타납니다.

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

`tags` 매개 변수의 값은 `{TAG_NAME}:{TAG_VALUE}` 형식을 사용하여 키-값 쌍의 형식을 사용합니다. 쉼표로 구분된 목록 형식으로 여러 개의 키-값 쌍을 제공할 수 있습니다. 여러 태그가 제공되면 AND 관계가 가정됩니다.

이 매개 변수는 태그 값에 대한 와일드카드 문자(`*`)를 지원합니다. 예를 들어 `test*`의 검색 문자열은 태그 값이 &quot;test&quot;로 시작하는 모든 객체를 반환합니다. 와일드카드만으로 구성된 검색 문자열을 사용하여 값에 상관없이 특정 태그가 포함되는지 여부를 기준으로 객체를 필터링할 수 있습니다.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 필터링할 태그의 이름입니다. |
| `{TAG_VALUE}` | 필터링할 태그의 값입니다. 와일드카드 문자(`*`)를 지원합니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색하여 특정 값 AND 두 번째 태그가 있는 하나의 태그로 필터링합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 값이 &quot;123456&quot;이고 값이 &quot;a1/&quot;인 `sampleTag`이 포함된 데이터 집합 목록을 반환합니다. `secondTag` 한계도 지정하지 않으면 응답에 최대 20개의 객체가 포함됩니다.

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

[!DNL Catalog] API의 일부 끝점에는 대부분의 날짜 경우 범위 쿼리를 허용하는 쿼리 매개 변수가 있습니다.

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

성공적인 응답에는 지정된 날짜 범위 내에 속하는 [!DNL Catalog] 개체 목록이 포함됩니다. 한계도 지정하지 않으면 응답에 최대 20개의 객체가 포함됩니다.

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

`orderBy` 쿼리 매개 변수를 사용하면 지정된 속성 값을 기반으로 응답 데이터를 정렬(순서 지정)할 수 있습니다. 이 매개 변수에는 &quot;direction&quot;(`asc`, 내림차순의 경우 `desc`), 콜론(`:`), 결과를 정렬하는 속성이 필요합니다. 방향을 지정하지 않으면 기본 방향은 오름차순입니다.

여러 정렬 속성을 쉼표로 구분된 목록으로 제공할 수 있습니다. 첫 번째 정렬 속성이 해당 속성에 대해 동일한 값을 포함하는 여러 개의 객체를 만드는 경우 두 번째 정렬 속성을 사용하여 일치하는 객체를 추가로 정렬합니다.

예를 들어 다음 쿼리를 생각해 보십시오.`orderBy=name,desc:created`. 결과는 첫 번째 정렬 속성인 `name`을 기준으로 오름차순으로 정렬됩니다. 여러 레코드가 동일한 `name` 속성을 공유하는 경우 일치하는 레코드는 두 번째 정렬 속성인 `created`로 정렬됩니다. 반환된 레코드가 동일한 `name`을(를) 공유하지 않으면 `created` 속성은 정렬에 영향을 주지 않습니다.


**API 형식**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 결과를 정렬하는 속성의 이름입니다. |

**요청**

다음 요청은 `name` 속성을 기준으로 정렬된 데이터 집합 목록을 검색합니다. 데이터 세트가 동일한 `name`을 공유하는 경우 해당 데이터 집합은 다시 `updated` 속성 순서로 내림차순으로 정렬됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 `orderBy` 매개 변수에 따라 정렬되는 [!DNL Catalog] 개체 목록이 포함되어 있습니다. 한계도 지정하지 않으면 응답에 최대 20개의 객체가 포함됩니다.

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

[!DNL Catalog] 다음 섹션에 자세히 설명된 속성별로 필터링하는 두 가지 방법을 제공합니다.

* [간단한 필터](#using-simple-filters) 사용:특정 속성이 특정 값과 일치하는지 여부를 기준으로 필터링합니다.
* [속성 매개 변수](#using-the-property-parameter) 사용:조건부 표현식을 사용하여 속성이 있는지 여부 또는 속성의 값이 다른 지정된 값 또는 정규 표현식과 일치하는지, 근사치를 적용할지 또는 비교할 것인지를 기준으로 필터링할 수 있습니다.

### 단순 필터 사용 {#using-simple-filters}

단순 필터를 사용하면 특정 속성 값에 따라 응답을 필터링할 수 있습니다. 단순 필터는 `{PROPERTY_NAME}={VALUE}` 형식을 취합니다.

예를 들어 `name=exampleName` 쿼리는 `name` 속성에 &quot;exampleName&quot; 값이 포함된 객체만 반환합니다. 반대로 `name=!exampleName` 쿼리는 `name` 속성이 **&quot;exampleName&quot;이 아닌**&#x200B;인 객체만 반환합니다.

또한 단순 필터는 단일 속성에 대해 여러 값을 쿼리하는 기능을 지원합니다. 여러 값이 제공되면 응답은 제공된 목록의 값 중 **임의의**&#x200B;과(와) 일치하는 속성을 가진 객체를 반환합니다. `!` 문자를 목록에 접두어로 사용하여 다중 값 쿼리를 변환할 수 있으며, 속성 값이 **가 아닌 개체만 제공된 목록에 반환합니다(예: `name=!exampleName,anotherName`).**

**API 형식**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 값을 필터링할 속성의 이름입니다. |
| `{VALUE}` | 포함할(또는 쿼리에 따라 제외) 결과를 결정하는 속성 값입니다. |

**요청**

다음 요청은 데이터 집합 목록을 검색합니다. 이는 `name` 속성에 &quot;exampleName&quot; 또는 &quot;anotherName&quot;의 값이 있는 데이터 집합만 포함하도록 필터링됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 데이터 집합 목록이 들어 있습니다. 단, `name`이 &quot;exampleName&quot; 또는 &quot;anotherName&quot;인 데이터 집합은 제외됩니다. 한계도 지정하지 않으면 응답에 최대 20개의 객체가 포함됩니다.

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

### `property` 매개 변수 {#using-the-property-parameter} 사용

`property` 쿼리 매개 변수는 단순 필터보다 속성 기반 필터링에 더 많은 유연성을 제공합니다. 속성에 특정 값이 있는지 여부를 기반으로 필터링하는 것 외에도 `property` 매개 변수는 다른 비교 연산자(예: &quot;보다 큼&quot;(`>`) 및 &quot;보다 작음&quot;(`<`))와 일반 표현식을 사용하여 속성 값을 기준으로 필터링할 수 있습니다. 또한 해당 값에 상관없이 속성이 있는지 여부에 따라 필터링할 수 있습니다.

`property` 매개 변수는 최상위 수준의 객체 속성만 허용합니다. 즉, 다음 샘플 객체의 경우 `name`, `description` 및 `subItem`에 대한 속성별로 필터링할 수 있지만 `sampleKey`에 대해서는 NOT을 사용할 수 있습니다.

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
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 쿼리할 속성과 해당 값이 평가되는 방법을 나타내는 조건부 표현식. 예제는 아래에 제공됩니다. |

`property` 매개 변수의 값은 여러 종류의 조건부 표현식을 지원합니다. 다음 표에서는 지원되는 표현식에 대한 기본 구문에 대해 설명합니다.

| 심볼 | 설명 | 예 |
| --- | --- | --- |
| (None) | 연산자가 없는 속성 이름을 지정하면 값에 관계없이 속성이 있는 객체만 반환합니다. | `property=name` |
| ! | `property` 매개 변수의 값으로 &quot;`!`&quot;을 접두어로 사용하면 속성이 **이(가) 아닌**&#x200B;인 객체만 반환됩니다. | `property=!name` |
| ~ | 물결표(`~`) 기호 뒤에 제공된 정규 표현식과 속성 값(문자열)이 일치하는 객체만 반환합니다. | `property=name~^example` |
| == | 이중 같음 기호(`==`) 뒤에 제공된 문자열과 속성 값이 정확히 일치하는 객체만 반환합니다. | `property=name==exampleName` |
| != | 같지 않음 기호(`!=`) 뒤에 제공된 문자열 일치(**)가 아닌 속성 값을 가진 객체만 반환합니다.** | `property=name!=exampleName` |
| &lt;> | 속성 값이 지정된 금액보다 작거나 같지 않은 개체만 반환합니다. | `property=version<1.0.0` |
| &lt;> | 속성 값이 지정된 금액보다 작거나 같은 객체만 반환합니다. | `property=version<=1.0.0` |
| > | 속성 값이 지정된 금액보다 크거나 같지 않은 개체만 반환합니다. | `property=version>1.0.0` |
| >= | 속성 값이 지정된 금액보다 크거나 같은 객체만 반환합니다. | `property=version>=1.0.0` |

>[!NOTE]
>
>`name` 속성은 전체 검색 문자열 또는 그 일부로 와일드카드 `*`의 사용을 지원합니다. 와일드카드가 빈 문자와 일치하는데, 이러한 검색 문자열 `te*st`은 값 &quot;test&quot;와 일치합니다. 별표는 두 배로(`**`)하여 이스케이프됩니다. 검색 문자열의 이중 별표는 단일 별표를 리터럴 문자열로 나타냅니다.

**요청**

다음 요청은 버전 번호가 1.0.3 이상인 데이터 세트를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 버전 번호가 1.0.3보다 큰 데이터 집합 목록이 들어 있습니다. 제한이 지정되지 않으면 응답에는 최대 20개의 개체가 포함됩니다.

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

앰퍼샌드(`&`)를 사용하면 여러 개의 필터를 하나의 요청에 결합할 수 있습니다. 요청에 추가 조건이 추가되면 AND 관계가 가정합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
