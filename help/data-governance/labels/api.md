---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api
solution: Experience Platform
title: 'API를 사용하여 데이터 사용 레이블 관리 '
topic-legacy: developer guide
description: 데이터 집합 서비스 API를 사용하여 데이터 집합에 대한 사용 레이블을 적용하고 편집할 수 있습니다. 이것은 Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와는 별개입니다.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 2%

---


# API를 사용하여 데이터 사용 레이블 관리

이 문서에서는 [!DNL Policy Service] API 및 [!DNL Dataset Service] API를 사용하여 데이터 사용 레이블을 관리하는 방법에 대해 설명합니다.

[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)에서는 조직의 데이터 사용 레이블을 만들고 관리할 수 있는 여러 끝점을 제공합니다.

[!DNL Dataset Service] API를 사용하여 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. 이것은 Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 [!DNL Catalog Service] API와는 별개입니다.

## 시작하기

이 안내서를 읽기 전에 카탈로그 개발자 안내서의 [시작하기 섹션](../../catalog/api/getting-started.md)에 설명된 단계에 따라 [!DNL Platform] API를 호출하는 데 필요한 자격 증명을 수집합니다.

이 문서에 나와 있는 [!DNL Dataset Service] 끝점을 호출하려면 특정 데이터 세트에 대한 고유한 `id` 값이 있어야 합니다. 이 값이 없는 경우 [카탈로그 개체 목록](../../catalog/api/list-objects.md)의 안내서를 참조하여 기존 데이터 세트의 ID를 찾습니다.

## 모든 레이블 목록 {#list-labels}

[!DNL Policy Service] API를 사용하여 각각 `/labels/core` 또는 `/labels/custom`에 GET 요청을 하여 모든 `core` 또는 `custom` 레이블을 나열할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 시스템에서 검색된 사용자 지정 레이블 목록을 반환합니다. 위의 예제 요청이 `/labels/custom`에 수행되었으므로 아래 응답에는 사용자 지정 레이블만 표시됩니다.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 레이블 {#look-up-label} 검색

[!DNL Policy Service] API에 대한 GET 요청 경로에 해당 레이블의 `name` 속성을 포함하여 특정 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 조회할 사용자 지정 레이블의 `name` 속성. |

**요청**

다음 요청은 경로에 지정된 사용자 지정 레이블 `L2`을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

## 사용자 지정 레이블 {#create-update-label} 만들기 또는 업데이트

사용자 지정 레이블을 만들거나 업데이트하려면 [!DNL Policy Service] API에 PUT 요청을 해야 합니다.

**API 형식**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 사용자 지정 레이블의 `name` 속성입니다. 이 이름의 사용자 지정 레이블이 없으면 새 레이블이 만들어집니다. 레이블이 있으면 해당 레이블이 업데이트됩니다. |

**요청**

다음 요청은 고객의 선택된 결제 계획과 관련된 정보가 포함된 데이터를 설명하는 새 레이블인 `L3`을 만듭니다.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 레이블에 대한 고유한 문자열 식별자입니다. 이 값은 조회 목적으로 사용되며 데이터 세트 및 필드에 레이블을 적용할 때 짧고 간결한 것이 좋습니다. |
| `category` | 레이블의 카테고리. 사용자 지정 레이블에 대한 고유한 카테고리를 만들 수 있지만 UI에 레이블을 표시하려면 `Custom`을 사용하는 것이 좋습니다. |
| `friendlyName` | 표시 목적으로 사용되는 레이블의 친숙한 이름입니다. |
| `description` | (선택 사항) 추가 컨텍스트를 제공하는 레이블의 설명입니다. |

**응답**

성공적인 응답은 기존 레이블이 업데이트된 경우 HTTP 코드 200(OK)을 사용하는 사용자 지정 레이블의 세부 사항을 반환하고 새 레이블을 만든 경우에는 201(만들기)을 반환합니다.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

## 데이터 세트 {#look-up-dataset-labels} 레이블 찾기

[!DNL Dataset Service] API에 GET 요청을 하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 조회하려는 데이터 세트의 고유한 `id` 값. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트에 적용된 데이터 사용 레이블을 반환합니다.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `optionalLabels` | 데이터 사용 레이블이 적용된 데이터 세트 내의 개별 필드 목록입니다. <br/><br/>`option` 하위 속성이 필요합니다.필드의 [!DNL Experience Data Model](XDM) 특성을 포함하는 객체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`:필드와  `$id` 연결된 스키마의 URI 값입니다.</li><li>`contentType`:스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.</li><li>`schemaPath`:JSON Porintersyntax에서 작성된 문제의 스키마  [속성 ](../../landing/api-fundamentals.md#json-pointer) 경로입니다.</li></ul>`labels`:필드에 추가할 데이터 사용 레이블 목록입니다. |

- id:데이터 세트가 기반으로 하는 XDM 스키마의 URI $id 값입니다.
- contentType:스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.
- schemaPath:[JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 구문으로 작성된 해당 스키마 속성의 경로입니다.

## 데이터 세트 {#apply-dataset-labels}에 레이블 적용

POST 또는 PUT 요청의 페이로드나 [!DNL Dataset Service] API에 레이블을 제공하여 데이터 세트에 대한 레이블 세트를 만들 수 있습니다. 이 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에서 제공되는 레이블로 바꿉니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 세트의 고유한 `id` 값. |

**요청**

다음 POST 요청은 데이터 세트 내의 특정 필드뿐만 아니라 데이터 세트에 일련의 레이블을 추가합니다. 페이로드에서 제공되는 필드는 PUT 요청에 필요한 필드와 같습니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 <br/><br/>`option` 속성이 있어야 합니다.필드의 [!DNL Experience Data Model](XDM) 특성을 포함하는 객체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>`id`:필드와  `$id` 연결된 스키마의 URI 값입니다.</li><li>`contentType`:스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오.</li><li>`schemaPath`:JSON Porintersyntax에서 작성된 문제의 스키마  [속성 ](../../landing/api-fundamentals.md#json-pointer) 경로입니다.</li></ul>`labels`:필드에 추가할 데이터 사용 레이블 목록입니다. |

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

## 데이터 집합 {#remove-dataset-labels}에서 레이블 제거

[!DNL Dataset Service] API에 DELETE 요청을 하여 데이터 세트에 적용된 레이블을 제거할 수 있습니다.

**API 형식**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 제거할 데이터 세트의 고유한 `id` 값. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

레이블이 제거되었음을 나타내는 성공적인 응답 HTTP 상태 200(확인)입니다. 이를 확인하기 위해 별도의 호출에서 데이터 세트에 대한 기존 레이블](#look-up-dataset-labels)을(를) 찾을 수 있습니다.[

## 다음 단계

이 문서를 읽음으로써 API를 사용하여 데이터 사용 레이블을 관리하는 방법을 알아보았습니다.

데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가하면 데이터를 [!DNL Experience Platform]에 인제스트할 수 있습니다. 자세한 내용을 보려면 [데이터 통합 문서](../../ingestion/home.md)를 읽으십시오.

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요](../policies/overview.md)를 참조하십시오.

[!DNL Experience Platform]의 데이터 집합 관리에 대한 자세한 내용은 [데이터 집합 개요](../../catalog/datasets/overview.md)를 참조하십시오.