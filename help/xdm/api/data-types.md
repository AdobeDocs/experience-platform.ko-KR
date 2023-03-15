---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;데이터 유형 레지스트리;스키마 레지스트리;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;만들기
solution: Experience Platform
title: 데이터 유형 API 끝점
description: 스키마 레지스트리 API의 /datatypes 끝점을 사용하면 경험 애플리케이션 내에서 XDM 데이터 유형을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 342da62b83d0d804b31744a580bcd3e38412ea51
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 2%

---

# 데이터 유형 엔드포인트

데이터 형식은 기본 리터럴 필드와 같은 방식으로 클래스나 스키마 필드 그룹에서 참조 형식 필드로 사용되며 주요 차이점은 데이터 형식이 여러 하위 필드를 정의할 수 있다는 것입니다. 데이터 유형은 다중 필드 구조를 일관되게 사용할 수 있다는 점에서 필드 그룹과 유사하지만 스키마 구조의 모든 위치에 포함될 수 있으므로 보다 유연하지만 필드 그룹은 루트 수준에서만 추가할 수 있습니다. 다음 `/datatypes` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 경험 애플리케이션 내에서 데이터 유형을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 데이터 유형 목록 검색 {#list}

아래에 모든 데이터 형식을 나열할 수 있습니다. `global` 또는 `tenant` 에 대한 GET 요청을 하여 컨테이너 `/global/datatypes` 또는 `/tenant/datatypes`, 각각

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환되는 리소스 수를 줄이는 것이 좋습니다. 의 섹션을 참조하십시오. [쿼리 매개 변수](./appendix.md#query) 자세한 내용은 부록 문서를 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 데이터 형식을 검색할 컨테이너: `global` Adobe 생성 데이터 유형 또는 `tenant` 조직 소유의 데이터 유형. |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 다음을 참조하십시오. [부록 문서](./appendix.md#query) 사용 가능한 매개 변수 목록입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 다음에서 데이터 유형 목록을 검색합니다. `tenant` 컨테이너, 사용 `orderby` 쿼리 매개 변수를 사용하여 데이터 형식을 `title` 특성.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 다음에 따라 다릅니다. `Accept` 헤더가 요청에서 전송되었습니다. 다음 `Accept` 헤더는 데이터 유형 목록에 사용할 수 있습니다.

| `Accept` 머리글 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 데이터 유형을 반환합니다. `$ref` 및 `allOf` 포함. (제한: 300) |

{style="table-layout:auto"}

**응답**

위의 요청은 `application/vnd.adobe.xed-id+json` `Accept` 따라서 응답에는 다음만 포함됩니다. `title`, `$id`, `meta:altId`, 및 `version` 각 데이터 유형에 대한 속성입니다. 다른 항목 사용 `Accept` 헤더 (`application/vnd.adobe.xed+json`)는 각 데이터 유형의 모든 속성을 반환합니다. 적절한 항목 선택 `Accept` 응답에 필요한 정보에 따라 다릅니다.

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

GET 요청의 경로에 데이터 유형의 ID를 포함하여 특정 데이터 유형을 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 데이터 형식을 저장하는 컨테이너입니다. `global` Adobe 생성 데이터 유형 또는 `tenant` 조직에서 소유한 데이터 유형입니다. |
| `{DATA_TYPE_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 조회할 데이터 유형. |

{style="table-layout:auto"}

**요청**

다음 요청은 다음을 기준으로 데이터 형식을 검색합니다. `meta:altId` 경로에 제공된 값입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 다음에 따라 다릅니다. `Accept` 헤더가 요청에서 전송되었습니다. 모든 조회 요청에는 `version` 에 포함 `Accept` 머리글입니다. 다음 `Accept` 머리글을 사용할 수 있습니다.

| `Accept` 머리글 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 원시 `$ref` 및 `allOf`에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 및 `allOf` 해결됨, 제목 및 설명 포함. |
| `application/vnd.adobe.xed-notext+json; version=1` | 원시 `$ref` 및 `allOf`, 제목 또는 설명 없음. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 및 `allOf` 해결됨, 제목 또는 설명 없음. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 및 `allOf` 해결됨, 설명자가 포함됨. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 데이터 유형의 세부 정보를 반환합니다. 반환되는 필드는 다음에 따라 다릅니다 `Accept` 헤더가 요청에서 전송되었습니다. 다른 실험 `Accept` 응답 비교와 사용 사례에 가장 적합한 헤더를 결정하는 헤더입니다.

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
  "imsOrg": "{ORG_ID}",
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

아래에서 사용자 지정 데이터 유형을 정의할 수 있습니다. `tenant` POST 요청을 하여 컨테이너를 작성합니다.

**API 형식**

```http
POST /tenant/datatypes
```

**요청**

필드 그룹과 달리 데이터 형식을 정의할 필요는 없습니다 `meta:extends` 또는 `meta:intendedToExtend` 충돌을 방지하기 위해 필드를 중첩하지 않아도 됩니다.

데이터 유형 자체의 필드 구조를 정의하는 경우 다음과 같은 기본 유형을 사용할 수 있습니다 `string` 또는 `object`) 또는 다음을 통해 다른 기존 데이터 유형을 참조할 수 있습니다. `$ref` 속성. 다음 안내서를 참조하십시오 [api에서 사용자 지정 XDM 필드 정의](../tutorials/custom-fields-api.md) 다른 XDM 필드 유형의 예상 형식에 대한 자세한 지침을 제공합니다.

다음 요청은 하위 속성이 있는 &quot;속성 구성&quot; 객체 데이터 유형을 만듭니다 `yearBuilt`, `propertyType`, 및 `location`:

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
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
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과, 다음을 포함하여 새로 생성된 데이터 유형의 세부 사항이 포함된 페이로드를 반환합니다. `$id`, `meta:altId`, 및 `version`. 이 세 가지 값은 읽기 전용이며 [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
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
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

에 대한 GET 요청 수행 [모든 데이터 유형 나열](#list) 이제 테넌트 컨테이너에 속성 세부 정보 데이터 형식이 포함되거나 [조회(GET) 요청 수행](#lookup) url 인코딩 사용 `$id` 새 데이터 형식을 직접 볼 수 있는 URI입니다.

## 데이터 유형 업데이트 {#put}

PUT 작업을 통해 전체 데이터 유형을 바꾸고 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 데이터 형식을 업데이트할 때에는 본문에 다음과 같은 경우에 필요한 모든 필드를 포함해야 합니다. [새 데이터 유형 만들기](#create) POST 요청에서.

>[!NOTE]
>
>데이터 형식을 완전히 대체하지 않고 일부만 업데이트하려면 [데이터 유형의 일부 업데이트](#patch).

**API 형식**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 다시 쓸 데이터 형식 |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 데이터 유형을 다시 작성하여 새 데이터 유형을 추가합니다 `floorSize` 필드.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
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

성공한 응답은 업데이트된 데이터 유형의 세부 정보를 반환합니다.

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
  "imsOrg": "{ORG_ID}",
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

PATCH 요청을 사용하여 데이터 유형의 일부를 업데이트할 수 있습니다. 다음 [!DNL Schema Registry] 는 다음을 포함한 모든 표준 JSON 패치 작업을 지원합니다. `add`, `remove`, 및 `replace`. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 바꾸려면 [PUT 작업을 사용하여 데이터 유형 바꾸기](#put).

**API 형식**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL로 인코딩됨 `$id` URI 또는 `meta:altId` 업데이트할 데이터 형식의 입니다. |

{style="table-layout:auto"}

**요청**

아래의 예제 요청은 `description` 및 가 새 데이터 형식을 추가함 `floorSize` 필드.

요청 본문은 배열 형식을 취하며, 나열된 각 객체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 객체에는 수행할 작업이 포함됩니다(`op`) 작업을 수행할 필드(`path`) 및 해당 작업에 포함해야 하는 정보(`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

응답은 두 작업이 모두 성공적으로 수행되었음을 보여 줍니다. 다음 `description` 이(가) 업데이트되었습니다. `floorSize` 이(가) 아래에 추가되었습니다. `definitions`.

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
        "type": "object",
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
  "imsOrg": "{ORG_ID}",
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

스키마 레지스트리에서 데이터 유형을 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 데이터 유형 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL로 인코딩됨 `$id` URI 또는 `meta:altId` 삭제할 데이터 형식의 입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

다음을 시도하여 삭제를 확인할 수 있습니다. [조회(GET) 요청](#lookup) 데이터 형식에 매핑할 수도 있습니다. 다음을 포함해야 합니다. `Accept` 요청의 헤더이지만 데이터 형식이 스키마 레지스트리에서 제거되었으므로 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
