---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;데이터 유형 레지스트리;스키마 레지스트리;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;만들기
solution: Experience Platform
title: 데이터 유형 API 끝점
description: 스키마 레지스트리 API의 /datatypes 종단점을 사용하면 경험 애플리케이션 내에서 XDM 데이터 유형을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 2%

---

# 데이터 유형 끝점

데이터 유형은 기본 리터럴 필드와 같은 방식으로 클래스 또는 스키마 필드 그룹에서 참조 형식 필드로 사용되며, 데이터 형식은 여러 하위 필드를 정의할 수 있다는 점에서 중요한 차이가 있습니다. 의 필드 그룹과 유사하지만, 여러 필드 구조를 일관되게 사용할 수 있다는 점에서 데이터 유형은 스키마 구조의 어느 곳에서든 포함할 수 있지만 필드 그룹은 루트 수준에서만 추가할 수 있으므로 보다 유연합니다. [!DNL Schema Registry] API의 `/datatypes` 종단점을 사용하면 경험 애플리케이션 내에서 데이터 유형을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 데이터 유형 목록 검색 {#list}

각각 `/global/datatypes` 또는 `/tenant/datatypes`에 GET 요청을 하여 `global` 또는 `tenant` 컨테이너 아래에 모든 데이터 유형을 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서에서 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 데이터 유형을 검색할 컨테이너:Adobe이 만든 데이터 유형의 경우 `global`, 조직이 소유한 데이터 유형의 경우 `tenant` 입니다. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록에 대해서는 [부록 document](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `tenant` 컨테이너에서 데이터 유형 목록을 검색하여 `orderby` 쿼리 매개 변수를 사용하여 `title` 속성으로 데이터 유형을 정렬합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 `Accept` 헤더는 목록 데이터 유형에 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 데이터 유형을 반환합니다. (제한:300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용하므로 응답에는 각 데이터 유형에 대한 `title`, `$id`, `meta:altId` 및 `version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 데이터 유형의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## 데이터 유형 조회 {#lookup}

GET 요청 경로에 데이터 유형의 ID를 포함하여 특정 데이터 유형을 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 데이터 유형이 들어 있는 컨테이너:Adobe이 만든 데이터 유형의 경우 `global`, 조직이 소유한 데이터 유형의 경우 `tenant` 입니다. |
| `{DATA_TYPE_ID}` | 조회하려는 데이터 유형의 `meta:altId` 또는 URL로 인코딩된 `$id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 경로에 제공된 `meta:altId` 값으로 데이터 유형을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청에는 `Accept` 헤더에 `version`이 포함되어야 합니다. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이 있는 Raw에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 그리고  `allOf` 해결됨 에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf` 가 있는 원시 형식의 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 그리고  `allOf` 해결되었습니다. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 그리고  `allOf` 설명자가 포함된 문제가 해결되었습니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 데이터 유형의 세부 정보를 반환합니다. 반환되는 필드는 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 데이터 유형 만들기 {#create}

POST 요청을 만들어 `tenant` 컨테이너 아래에 사용자 지정 데이터 유형을 정의할 수 있습니다.

**API 형식**

```http
POST /tenant/datatypes
```

**요청**

데이터 유형을 정의해도 `meta:extends` 또는 `meta:intendedToExtend` 필드가 필요하지 않으며, 충돌을 방지하기 위해 필드를 중첩할 필요가 없습니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          }
        } 
      }'
```

**응답**

성공적으로 응답하면 `$id`, `meta:altId` 및 `version`를 포함하여 새로 만든 데이터 유형의 세부 정보가 포함된 페이로드 및 HTTP 상태 201(생성됨)가 반환됩니다. 이 세 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 지정됩니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

이제 임차인 컨테이너에 있는 모든 데이터 형식](#list)에 대한 GET 요청을 수행하면 이제 속성 세부 사항 데이터 유형이 포함되거나, URL 인코딩된 `$id` URI를 사용하여 [조회(GET) 요청](#lookup)을 수행하여 새 데이터 유형을 직접 볼 수 있습니다.[

## 데이터 유형 업데이트 {#put}

기본적으로 리소스를 다시 작성하는 PUT 작업을 통해 전체 데이터 유형을 바꿀 수 있습니다. PUT 요청을 통해 데이터 유형을 업데이트할 때 본문에는 POST 요청에 [새 데이터 형식](#create)을 만들 때 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>데이터 형식을 완전히 바꾸는 대신 일부 데이터만 업데이트하려면 [데이터 형식](#patch)의 일부를 업데이트하는 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | 다시 쓸 데이터 형식의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 데이터 유형을 다시 작성하여 새 `floorSize` 필드를 추가합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**응답**

성공적인 응답은 업데이트된 데이터 유형의 세부 정보를 반환합니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 데이터 유형의 일부 업데이트 {#patch}

PATCH 요청을 사용하여 데이터 유형의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은 `add`, `remove` 및 `replace`를 비롯한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업](#put)을 사용하여 데이터 유형을 바꾸는 섹션을 참조하십시오.

**API 형식**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | 업데이트할 데이터 형식의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 기존 데이터 유형의 `description`을 업데이트하고 새 `floorSize` 필드를 추가합니다.

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`)이 포함되어 있으며, (`path`)에서 작업을 수행해야 하는 필드와 해당 작업에 포함해야 하는 정보가 포함됩니다(`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**응답**

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. `description`이(가) 업데이트되었으며 `definitions` 아래에 `floorSize`이(가) 추가되었습니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 데이터 유형 삭제 {#delete}

스키마 레지스트리에서 데이터 형식을 제거해야 하는 경우가 있을 수 있습니다. 이 작업은 경로에 제공된 데이터 유형 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | 삭제할 데이터 형식의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

데이터 유형에 [조회(GET) 요청](#lookup)을 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 데이터 형식이 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
