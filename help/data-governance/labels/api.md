---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api
solution: Experience Platform
title: API를 사용하여 데이터 사용 레이블 관리
description: 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와 별개입니다.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 2%

---


# API를 사용하여 데이터 사용 레이블 관리

이 문서에서는 [!DNL Policy Service] API 및 [!DNL Dataset Service] API를 사용하여 데이터 사용 레이블을 관리하는 방법에 대한 단계를 제공합니다.

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)은(는) 조직의 데이터 사용 레이블을 만들고 관리할 수 있는 여러 끝점을 제공합니다.

[!DNL Dataset Service] API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 [!DNL Catalog Service] API와 별개입니다.

## 시작하기

이 안내서를 읽기 전에 카탈로그 개발자 안내서의 [시작 섹션](../../catalog/api/getting-started.md)에 설명된 단계에 따라 [!DNL Platform] API를 호출하는 데 필요한 자격 증명을 수집합니다.

이 문서에 설명된 [!DNL Dataset Service] 끝점을 호출하려면 특정 데이터 세트에 대해 고유한 `id` 값이 있어야 합니다. 이 값이 없으면 [카탈로그 개체 나열](../../catalog/api/list-objects.md)에 대한 안내서를 참조하여 기존 데이터 세트의 ID를 찾으십시오.

## 모든 레이블 나열 {#list-labels}

[!DNL Policy Service] API를 사용하면 `/labels/core` 또는 `/labels/custom`에 각각 GET 요청을 하여 `core` 또는 `custom` 레이블을 모두 나열할 수 있습니다.

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

성공적인 응답은 시스템에서 검색된 사용자 지정 레이블 목록을 반환합니다. 위의 예제 요청이 `/labels/custom`에 대해 수행되었으므로 아래 응답에는 사용자 지정 레이블만 표시됩니다.

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

[!DNL Policy Service] API에 대한 GET 요청 경로에 해당 레이블의 `name` 속성을 포함하여 특정 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 조회할 사용자 지정 레이블의 `name` 속성입니다. |

**요청**

다음 요청은 경로에 표시된 대로 사용자 지정 레이블 `L2`을(를) 검색합니다.

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

사용자 지정 레이블을 만들거나 업데이트하려면 [!DNL Policy Service] API에 대한 PUT 요청을 수행해야 합니다.

**API 형식**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 사용자 지정 레이블의 `name` 속성입니다. 이 이름을 가진 사용자 지정 레이블이 없으면 새 레이블이 만들어집니다. 레이블이 있으면 해당 레이블이 업데이트됩니다. |

**요청**

다음 요청은 고객이 선택한 결제 플랜과 관련된 정보가 포함된 데이터를 설명하는 것을 목적으로 하는 새 레이블 `L3`을(를) 만듭니다.

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
| `category` | 레이블의 카테고리입니다. 사용자 지정 레이블에 대해 고유한 범주를 만들 수 있지만, 레이블을 UI에 표시하려면 `Custom`을(를) 사용하는 것이 좋습니다. |
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

[!DNL Dataset Service] API에 대한 GET 요청을 통해 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 조회할 데이터 세트의 고유한 `id` 값입니다. |

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
| `optionalLabels` | 데이터 세트 내에 데이터 사용 레이블이 적용된 개별 필드의 목록입니다. 다음 하위 속성이 필요합니다.<br/><br/>`option`: 필드의 [!DNL Experience Data Model](XDM) 특성을 포함하는 개체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`: 필드와 연결된 스키마의 URI `$id` 값입니다.</li><li>`contentType`: 스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.</li><li>`schemaPath`: [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문으로 작성된 해당 스키마 속성의 경로입니다.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

- id: 데이터 세트의 기반이 되는 XDM 스키마의 URI $id 값입니다.
- contentType: 스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.
- schemaPath: [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문으로 작성된 해당 스키마 속성의 경로입니다.

## 데이터 세트에 레이블 적용 {#apply-dataset-labels}

[!DNL Dataset Service] API에 POST 또는 PUT 요청의 페이로드에 제공하여 데이터 세트에 대한 레이블 집합을 만들 수 있습니다. 이러한 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에 제공된 레이블로 교체합니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 집합의 고유한 `id` 값입니다. |

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
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다.<br/><br/>`option`: 필드의 [!DNL Experience Data Model](XDM) 특성을 포함하는 개체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`: 필드와 연결된 스키마의 URI `$id` 값입니다.</li><li>`contentType`: 스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.</li><li>`schemaPath`: [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문으로 작성된 해당 스키마 속성의 경로입니다.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

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

[!DNL Dataset Service] API에 대한 DELETE 요청을 통해 데이터 집합에 적용된 레이블을 제거할 수 있습니다.

**API 형식**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 제거할 데이터 집합의 고유한 `id` 값입니다. |

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

레이블이 제거되었음을 나타내는 성공적인 응답 HTTP 상태 200(OK). 별도의 호출에서 데이터 집합에 대한 기존 레이블을 [조회](#look-up-dataset-labels)하여 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 API를 사용하여 데이터 사용 레이블을 관리하는 방법을 배웠습니다.

데이터 집합 및 필드 수준에서 데이터 사용 레이블을 추가하면 데이터를 [!DNL Experience Platform](으)로 수집할 수 있습니다. 자세한 내용을 보려면 먼저 [데이터 수집 설명서](../../ingestion/home.md)를 읽어 보세요.

이제 적용한 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요](../policies/overview.md)를 참조하세요.

[!DNL Experience Platform]의 데이터 세트 관리에 대한 자세한 내용은 [데이터 세트 개요](../../catalog/datasets/overview.md)를 참조하십시오.