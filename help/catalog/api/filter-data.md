---
keywords: Experience Platform;홈;인기 항목;필터;필터;데이터 필터링;데이터 필터링;날짜 범위
solution: Experience Platform
title: 쿼리 매개 변수를 사용하여 카탈로그 데이터 필터링
description: 카탈로그 서비스 API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. 카탈로그에 대한 모범 사례의 일부는 API에 대한 로드를 줄이고 전체 성능을 개선하는 데 도움이 되므로 모든 API 호출에 필터를 사용하는 것입니다.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 75099d39fbdb9488105a9254bbbcca9b12349238
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 1%

---

# 쿼리 매개 변수를 사용하여 [!DNL Catalog] 데이터 필터링

[!DNL Catalog Service] API를 사용하면 요청 쿼리 매개 변수를 사용하여 응답 데이터를 필터링할 수 있습니다. [!DNL Catalog]에 대한 모범 사례의 일부는 API에 대한 로드를 줄이고 전체 성능을 개선하는 데 도움이 되므로 모든 API 호출에 필터를 사용하는 것입니다.

이 문서에서는 API에서 [!DNL Catalog] 개체를 필터링하는 가장 일반적인 방법에 대해 설명합니다. [!DNL Catalog] API와 상호 작용하는 방법에 대한 자세한 내용은 [카탈로그 개발자 안내서](getting-started.md)를 읽는 동안 이 문서를 참조하는 것이 좋습니다. [!DNL Catalog Service]에 대한 일반적인 정보는 [[!DNL Catalog] 개요](../home.md)를 참조하십시오.

## 반환되는 오브젝트 제한

`limit` 쿼리 매개 변수는 응답에서 반환되는 개체 수를 제한합니다. 구성된 제한에 따라 [!DNL Catalog] 응답이 자동으로 측정됩니다.

* `limit` 매개 변수를 지정하지 않으면 응답 페이로드당 최대 개체 수는 20개입니다.
* 데이터 세트 쿼리의 경우 `properties` 쿼리 매개 변수를 사용하여 `observableSchema`을(를) 요청하면 반환되는 최대 데이터 세트 수는 20개입니다.
* 다른 모든 카탈로그 쿼리에 대한 전역 제한은 100개입니다.
* `limit` 매개 변수가 잘못되면 `limit=0`을(를) 포함하여 적절한 범위의 윤곽을 나타내는 400개 수준의 오류 응답이 발생합니다.
* 쿼리 매개 변수로 전달된 제한 또는 오프셋은 헤더로 전달된 제한보다 우선합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | 반환할 개체 수를 나타내는 정수로, 1개에서 100개까지 지정할 수 있습니다. |

**요청**

다음 요청은 응답을 세 개의 객체로 제한하면서 데이터 세트 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답이 `limit` 쿼리 매개 변수로 표시된 숫자로 제한된 데이터 세트 목록을 반환합니다.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 표시된 속성 제한

`limit` 매개 변수를 사용하여 반환된 개체 수를 필터링하는 경우에도 반환된 개체 자체에는 실제로 필요한 것보다 더 많은 정보가 포함될 수 있습니다. 시스템의 로드를 추가로 줄이려면 필요한 속성만 포함하도록 응답을 필터링하는 것이 좋습니다.

`properties` 매개 변수는 지정된 속성 집합만 반환하도록 응답 개체를 필터링합니다. 매개 변수는 하나 이상의 속성을 반환하도록 설정할 수 있습니다.

`properties` 매개 변수는 모든 수준의 개체 속성을 사용할 수 있습니다. `?properties=subItem.sampleKey`을(를) 사용하여 `sampleKey`을(를) 추출할 수 있습니다.

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

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | 응답 본문에 포함할 속성의 이름입니다. |
| `{OBJECT_ID}` | 검색 중인 특정 [!DNL Catalog] 개체의 고유 식별자입니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색합니다. `properties` 매개 변수 아래에 제공된 쉼표로 구분된 속성 이름 목록은 응답에서 반환될 속성을 나타냅니다. 반환된 데이터 세트 수를 제한하는 `limit` 매개 변수도 포함됩니다. 요청에 `limit` 매개 변수가 포함되지 않은 경우 응답에는 최대 20개의 개체가 포함됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 요청된 속성만 표시된 [!DNL Catalog] 개체 목록을 반환합니다.

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

위의 응답을 기반으로 다음을 추론할 수 있습니다.

* 개체에 요청된 속성이 없는 경우 개체에 포함된 요청된 속성만 표시됩니다. (`Dataset1`)
* 개체에 요청된 속성이 포함되지 않으면 빈 개체로 표시됩니다. (`Dataset2`)
* 데이터 세트는 속성이 포함되어 있지만 값이 없는 경우 요청된 속성을 빈 개체로 반환할 수 있습니다. (`Dataset3`)
* 그렇지 않으면 데이터 세트에 요청된 모든 속성의 전체 값이 표시됩니다. (`Dataset4`)

>[!NOTE]
>
>각 데이터 집합에 대한 `schemaRef` 속성에서 버전 번호는 스키마의 최신 부 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.

## 응답 목록의 오프셋 시작 인덱스

`start` 쿼리 매개 변수는 0부터 시작하는 번호 매기기를 사용하여 지정된 번호만큼 응답 목록을 앞으로 오프셋합니다. 예를 들어 `start=2`은(는) 나열된 세 번째 개체에서 시작할 응답을 오프셋합니다.

`start` 매개 변수가 `limit` 매개 변수와 쌍을 이루지 않으면 반환되는 최대 개체 수는 20개입니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | 응답을 오프셋할 개체 수를 나타내는 정수입니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색하여 다섯 번째 개체(`start=4`)로 오프셋하고 응답을 두 개의 반환된 데이터 세트(`limit=2`)로 제한합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 각 데이터 세트 및 세부 정보에 대해 하나씩, 두 개의 최상위 수준 항목(`limit=2`)이 포함된 JSON 개체가 포함되어 있습니다(예제에 자세한 내용이 요약되었습니다). 응답이 4개(`start=4`)만큼 이동되었습니다. 즉, 표시된 데이터 세트가 시간 순서대로 5번과 6번입니다.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 태그로 필터링

일부 카탈로그 개체는 `tags` 특성 사용을 지원합니다. 태그는 오브젝트에 정보를 첨부한 다음 나중에 해당 오브젝트를 검색하는 데 사용할 수 있습니다. 사용할 태그와 적용 방법의 선택은 조직 프로세스에 따라 다릅니다.

태그를 사용할 때 고려해야 할 몇 가지 제한 사항이 있습니다.

* 현재 태그를 지원하는 유일한 카탈로그 개체는 데이터 세트, 배치 및 연결입니다.
* 태그 이름은 조직에 고유합니다.
* Adobe 프로세스는 특정 비헤이비어에 대해 태그를 활용할 수 있습니다. 이러한 태그의 이름 앞에는 &quot;adobe&quot;가 표준으로 붙습니다. 따라서 태그 이름을 선언할 때는 이 규칙을 사용하지 않아야 합니다.
* 다음 태그 이름은 [!DNL Experience Platform]에서 사용하도록 예약되어 있으므로 조직의 태그 이름으로 선언할 수 없습니다.
   * `unifiedProfile`: 이 태그 이름은 [[!DNL Real-Time Customer Profile]](../../profile/home.md)에서 수집할 데이터 세트에 예약되어 있습니다.
   * `unifiedIdentity`: 이 태그 이름은 [[!DNL Identity Service]](../../identity-service/home.md)에서 수집할 데이터 세트에 예약되어 있습니다.

다음은 `tags` 속성이 포함된 데이터 집합의 예입니다. 해당 속성 내의 태그는 키-값 쌍의 형태를 취하며 각 태그 값은 단일 문자열을 포함하는 배열로 표시됩니다.

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

`tags` 매개 변수의 값은 `{TAG_NAME}:{TAG_VALUE}` 형식을 사용하여 키-값 쌍의 형식을 취합니다. 여러 키-값 쌍을 쉼표로 구분된 목록 형태로 제공할 수 있습니다. 여러 개의 태그가 제공된 경우 AND 관계를 가정합니다.

매개 변수는 태그 값에 와일드카드 문자(`*`)를 지원합니다. 예를 들어 `test*`의 검색 문자열은 태그 값이 &quot;test&quot;로 시작하는 모든 개체를 반환합니다. 와일드카드로만 구성된 검색 문자열은 값에 관계없이 특정 태그가 포함되어 있는지 여부에 따라 객체를 필터링하는 데 사용할 수 있습니다.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 필터링 기준으로 사용할 태그의 이름입니다. |
| `{TAG_VALUE}` | 필터링 기준으로 사용할 태그의 값. 와일드카드 문자(`*`)를 지원합니다. |

**요청**

다음 요청은 데이터 세트 목록을 검색하여 특정 값을 갖는 태그 하나와 존재하는 두 번째 태그로 필터링합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 값이 &quot;123456&quot;인 `sampleTag`과(와) 값이 있는 `secondTag`을(를) 포함하는 데이터 세트 목록을 반환합니다. 제한도 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

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
    }
}
```

## 날짜 범위로 필터링

[!DNL Catalog] API의 일부 끝점에는 광범위한 쿼리를 허용하는 쿼리 매개 변수가 있습니다(대부분의 경우 날짜의 경우).

**API 형식**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 매개변수 | 설명 |
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

성공한 응답에 지정된 날짜 범위에 속하는 [!DNL Catalog]개 개체 목록이 포함되어 있습니다. 제한도 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

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
    }
}
```

## 속성별 정렬

`orderBy` 쿼리 매개 변수를 사용하면 지정된 속성 값을 기준으로 응답 데이터를 정렬(순서 지정)할 수 있습니다. 이 매개 변수에는 &quot;direction&quot;(`asc`(오름차순) 또는 `desc`(내림차순) 다음에 콜론(`:`)을 추가한 다음 결과를 정렬할 속성이 필요합니다. 방향을 지정하지 않으면 기본 방향은 오름차순입니다.

여러 정렬 속성을 쉼표로 구분된 목록으로 제공할 수 있습니다. 첫 번째 정렬 속성이 해당 속성에 대해 동일한 값을 포함하는 여러 객체를 생성하는 경우 두 번째 정렬 속성을 사용하여 일치하는 객체를 추가로 정렬합니다.

예를 들어 `orderBy=name,desc:created` 쿼리를 생각해 보십시오. 결과는 첫 번째 정렬 속성 `name`을(를) 기준으로 오름차순으로 정렬됩니다. 여러 레코드가 동일한 `name` 속성을 공유하는 경우 일치하는 레코드는 두 번째 정렬 속성인 `created`에 따라 정렬됩니다. 반환된 레코드가 동일한 `name`을(를) 공유하지 않는 경우 `created` 속성은 정렬에 영향을 주지 않습니다.


**API 형식**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 결과를 정렬할 속성의 이름입니다. |

**요청**

다음 요청은 `name` 속성으로 정렬된 데이터 세트 목록을 검색합니다. 동일한 `name`을(를) 공유하는 데이터 세트가 있는 경우 해당 데이터 세트는 `updated` 속성에 따라 내림차순으로 정렬됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 `orderBy` 매개 변수에 따라 정렬된 [!DNL Catalog] 개체 목록이 포함되어 있습니다. 제한도 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

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
    }
}
```

## 속성으로 필터링

[!DNL Catalog]은(는) 속성별로 필터링하는 두 가지 방법을 제공합니다. 이 방법은 다음 섹션에 자세히 설명되어 있습니다.

* [단순 필터 사용](#using-simple-filters): 특정 속성이 특정 값과 일치하는지 여부를 기준으로 필터링합니다.
* [속성 매개 변수 사용](#using-the-property-parameter): 조건식을 사용하여 속성이 있는지 여부 또는 속성 값이 지정된 다른 값 또는 정규 표현식과 일치하는지, 근사화하는지 또는 비교하는지 여부를 기준으로 필터링합니다.

### 단순 필터 사용 {#using-simple-filters}

단순 필터를 사용하면 특정 속성 값을 기준으로 응답을 필터링할 수 있습니다. 단순 필터는 `{PROPERTY_NAME}={VALUE}` 형식을 사용합니다.

예를들어, `name=exampleName` 쿼리는 `name` 속성에 &quot;exampleName&quot; 값이 포함된 개체만 반환합니다. 반대로 `name=!exampleName` 쿼리는 `name` 속성이 **not** &quot;exampleName&quot;인 개체만 반환합니다.

또한 간단한 필터는 단일 속성에 대해 여러 값을 쿼리하는 기능을 지원합니다. 여러 값이 제공되면 응답은 속성이 제공된 목록의 값 **any**&#x200B;과(와) 일치하는 개체를 반환합니다. `!` 문자를 목록에 접두사로 추가하여 다중 값 쿼리를 반전하고 제공된 목록에서 속성 값이 **not**&#x200B;인 개체만 반환합니다(예: `name=!exampleName,anotherName`).

**API 형식**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 필터링 기준으로 사용할 값을 가진 속성의 이름입니다. |
| `{VALUE}` | 쿼리에 따라 포함(또는 제외)할 결과를 결정하는 속성 값입니다. |

**요청**

다음 요청은 `name` 속성의 값이 &quot;exampleName&quot; 또는 &quot;anotherName&quot;인 데이터 세트만 포함하도록 필터링된 데이터 세트 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 `name`이(가) &quot;exampleName&quot; 또는 &quot;anotherName&quot;인 데이터 세트를 제외한 데이터 세트 목록이 포함되어 있습니다. 제한도 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

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
    }
}
```

### `property` 매개 변수 사용 {#using-the-property-parameter}

`property` 쿼리 매개 변수는 간단한 필터보다 속성 기반 필터링에 더 많은 유연성을 제공합니다. `property` 매개 변수는 속성에 특정 값이 있는지 여부에 따라 필터링할 뿐만 아니라 다른 비교 연산자(예: &quot;extenda&quot;(`>`) 및 &quot;less-than&quot;(`<`))와 정규식을 사용하여 속성 값으로 필터링할 수 있습니다. 또한 속성의 값에 관계없이 속성의 존재 여부에 따라 필터링할 수도 있습니다.

`property` 매개 변수는 모든 수준의 개체 속성을 사용할 수 있습니다. `sampleKey`은(는) `?properties=subItem.sampleKey`을(를) 사용하여 필터링하는 데 사용할 수 있습니다.

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

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | 쿼리할 속성 및 해당 값의 평가 방법을 나타내는 조건부 식입니다. 예제는 아래에 나와 있습니다. |

`property` 매개 변수의 값은 여러 종류의 조건부 표현식을 지원합니다. 다음 표에서는 지원되는 표현식에 대한 기본 구문을 간략하게 설명합니다.

| 기호 | 설명 | 예 |
| --- | --- | --- |
| (없음) | 연산자가 없는 속성 이름을 입력하면 해당 값에 관계없이 속성이 있는 객체만 반환됩니다. | `property=name` |
| ! | `property` 매개 변수의 값에 &quot;`!`&quot;을(를) 접두사로 사용하면 속성이 **not**&#x200B;인 개체만 반환됩니다. | `property=!name` |
| ~ | 속성 값(문자열)이 물결표(`~`) 기호 뒤에 제공된 정규식과 일치하는 개체만 반환합니다. | `property=name~^example` |
| == | 속성 값이 double-equals 기호(`==`) 뒤에 제공된 문자열과 정확히 일치하는 개체만 반환합니다. | `property=name==exampleName` |
| != | 같지 않음 기호(`!=`) 뒤에 제공된 문자열과 일치하는 속성 값이 **not**&#x200B;인 개체만 반환합니다. | `property=name!=exampleName` |
| &lt; | 속성 값이 지정된 양보다 작지만 같지 않은 개체만 반환합니다. | `property=version<1.0.0` |
| &lt;= | 속성 값이 지정된 양보다 작거나 같은 개체만 반환합니다. | `property=version<=1.0.0` |
| > | 속성 값이 지정된 양보다 큰(하지만 같지 않은) 개체만 반환합니다. | `property=version>1.0.0` |
| >= | 속성 값이 지정된 양보다 크거나 같은 개체만 반환합니다. | `property=version>=1.0.0` |

>[!NOTE]
>
>`name` 속성은 전체 검색 문자열로서 또는 와일드카드 `*`의 일부로 사용할 수 있도록 지원합니다. 와일드카드는 빈 문자를 일치시키므로 검색 문자열 `te*st`은(는) 값 &quot;test&quot;와(과) 일치합니다. 별표를 두 배로 늘려 이스케이프 처리합니다(`**`). 검색 문자열의 이중 별표는 리터럴 문자열로 단일 별표를 나타냅니다.

**요청**

다음 요청은 버전 번호가 1.0.3보다 큰 모든 데이터 세트를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 버전 번호가 1.0.3보다 큰 데이터 세트 목록이 포함되어 있습니다. 제한도 지정하지 않는 한 응답에는 최대 20개의 개체가 포함됩니다.

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
    }
}
```

## 여러 필터 결합

앰퍼샌드(`&`)를 사용하여 하나의 요청에 여러 필터를 결합할 수 있습니다. 요청에 추가 조건이 추가되면 AND 관계가 간주됩니다.

**API 형식**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
