---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api
solution: Experience Platform
title: API를 사용하여 데이터 사용 레이블 관리
description: 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와 별개입니다.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# API를 사용하여 데이터 사용 레이블 관리

이 문서에서는 다음을 사용하여 데이터 사용 레이블을 관리하는 방법에 대한 단계를 제공합니다. [!DNL Policy Service] API 및 [!DNL Dataset Service] API.

다음 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 는 조직의 데이터 사용 레이블을 만들고 관리할 수 있는 몇 가지 끝점을 제공합니다.

다음 [!DNL Dataset Service] API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 과는 별개입니다 [!DNL Catalog Service] 데이터 세트 메타데이터를 관리하는 API.

## 시작하기

이 안내서를 읽기 전에 [시작 섹션](../../catalog/api/getting-started.md) 를 호출하는 데 필요한 자격 증명을 수집하려면 카탈로그 개발자 안내서에서 를 참조하십시오. [!DNL Platform] API.

를 호출하기 위해 [!DNL Dataset Service] 이 문서에 요약된 끝점에는 `id` 특정 데이터 세트에 대한 값입니다. 이 값이 없는 경우 의 안내서를 참조하십시오. [카탈로그 개체 나열](../../catalog/api/list-objects.md) 기존 데이터 세트의 ID를 찾습니다.

## 모든 레이블 나열 {#list-labels}

사용 [!DNL Policy Service] API를 사용하여 모든 항목을 나열할 수 있습니다. `core` 또는 `custom` 에 GET 요청을 하여 레이블 지정 `/labels/core` 또는 `/labels/custom`, 각각

**API 형식**

```http
GET /labels/core
GET /labels/custom
```

**요청**

다음 요청은 조직에서 만든 모든 사용자 지정 레이블을 나열합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 시스템에서 검색된 사용자 지정 레이블 목록을 반환합니다. 위의 예제 요청이에 대해 수행되었으므로 `/labels/custom`: 아래 응답은 사용자 지정 레이블만 표시합니다.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 레이블 조회 {#look-up-label}

해당 레이블을 포함하여 특정 레이블을 조회할 수 있습니다. `name` 에 대한 GET 요청 경로의 속성 [!DNL Policy Service] API.

**API 형식**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 다음 `name` 조회할 사용자 지정 레이블의 속성입니다. |

**요청**

다음 요청은 사용자 지정 레이블을 검색합니다 `L2`경로에 표시된 대로 를 클릭합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용자 지정 레이블의 세부 정보를 반환합니다.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 사용자 지정 레이블 만들기 또는 업데이트 {#create-update-label}

PUT 사용자 지정 레이블을 만들거나 업데이트하려면 [!DNL Policy Service] API.

**API 형식**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 다음 `name` 사용자 지정 레이블의 속성입니다. 이 이름을 가진 사용자 지정 레이블이 없으면 새 레이블이 만들어집니다. 레이블이 있으면 해당 레이블이 업데이트됩니다. |

**요청**

다음 요청은 새 레이블을 만듭니다. `L3`는 고객이 선택한 결제 플랜과 관련된 정보가 포함된 데이터를 설명하는 것을 목적으로 합니다.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 레이블에 대한 고유 문자열 식별자. 이 값은 조회 목적으로 사용되고 데이터 세트 및 필드에 레이블을 적용하므로 짧고 간결한 것이 좋습니다. |
| `category` | 레이블의 카테고리입니다. 사용자 지정 레이블에 대해 고유한 범주를 만들 수 있지만, `Custom` UI에 레이블을 표시하려면 다음을 수행하십시오. |
| `friendlyName` | 표시용으로 사용되는 레이블의 이름입니다. |
| `description` | (선택 사항) 추가 컨텍스트를 제공하기 위한 레이블에 대한 설명입니다. |

**응답**

성공적인 응답은 기존 레이블이 업데이트된 경우 HTTP 코드 200(OK), 새 레이블이 만들어진 경우 201(Created)과 함께 사용자 지정 레이블의 세부 사항을 반환합니다.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 데이터 세트에 대한 레이블 조회 {#look-up-dataset-labels}

에 GET 요청을 하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다. [!DNL Dataset Service] API.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 조회할 데이터 세트의 값입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트에 적용된 데이터 사용 레이블을 반환합니다.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `labels` | 데이터 세트에 적용된 데이터 사용 레이블 목록입니다. |
| `optionalLabels` | 데이터 세트 내에 데이터 사용 레이블이 적용된 개별 필드의 목록입니다. 다음 하위 속성이 필요합니다.<br/><br/>`option`: 다음을 포함하는 개체 [!DNL Experience Data Model] (XDM) 필드 속성입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`: URI `$id` 필드와 연계된 스키마 값.</li><li>`contentType`: 스키마의 형식 및 버전을 나타냅니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오.</li><li>`schemaPath`: 해당 스키마 속성에 대한 경로로, 다음에서 작성됨 [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

- id: 데이터 세트의 기반이 되는 XDM 스키마의 URI $id 값입니다.
- contentType: 스키마의 형식 및 버전을 나타냅니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오.
- schemaPath: 해당 스키마 속성에 대한 경로로, [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문.

## 데이터 세트에 레이블 적용 {#apply-dataset-labels}

POST 또는 PUT 요청의 페이로드에 제공하여 데이터 세트에 대한 레이블 집합을 생성할 수 있습니다. [!DNL Dataset Service] API. 이러한 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에 제공된 레이블로 교체합니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 만드는 데이터 세트의 값입니다. |

**요청**

다음 POST 요청은 일련의 레이블을 데이터 세트와 해당 데이터 세트 내의 특정 필드에 추가합니다. 페이로드에 제공된 필드는 PUT 요청에 필요한 것과 동일합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `labels` | 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다.<br/><br/>`option`: 다음을 포함하는 개체 [!DNL Experience Data Model] (XDM) 필드 속성입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`: URI `$id` 필드와 연계된 스키마 값.</li><li>`contentType`: 스키마의 형식 및 버전을 나타냅니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오.</li><li>`schemaPath`: 해당 스키마 속성에 대한 경로로, 다음에서 작성됨 [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

**응답**

성공적인 응답은 데이터 세트에 추가된 레이블을 반환합니다.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## 데이터 세트에서 레이블 제거 {#remove-dataset-labels}

에 DELETE 요청을 하여 데이터 세트에 적용된 레이블을 제거할 수 있습니다. [!DNL Dataset Service] API.

**API 형식**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 제거할 데이터 세트의 값입니다. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

레이블이 제거되었음을 나타내는 성공적인 응답 HTTP 상태 200(OK). 다음을 수행할 수 있습니다. [기존 레이블 조회](#look-up-dataset-labels) 을(를) 확인하기 위해 별도의 호출에서 데이터 세트에 대해 를 참조하십시오.

## 다음 단계

이 문서를 읽고 API를 사용하여 데이터 사용 레이블을 관리하는 방법을 배웠습니다.

데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가한 후에는 데이터 수집을 시작할 수 있습니다. [!DNL Experience Platform]. 자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md).

이제 적용한 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요](../policies/overview.md).

에서 데이터 세트 관리에 대한 자세한 내용 [!DNL Experience Platform], 다음을 참조하십시오. [데이터 세트 개요](../../catalog/datasets/overview.md).