---
title: API에서 XDM 필드 사용 중단
description: 스키마 레지스트리 API에서 XDM(Experience Data Model) 필드를 사용하지 않는 방법을 알아봅니다.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# API에서 XDM 필드 사용 중단

XDM(경험 데이터 모델)에서 다음을 사용하여 스키마 또는 사용자 지정 리소스 내의 필드를 사용하지 않을 수 있습니다. [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 필드를 사용하지 않으면 다음과 같은 다운스트림 UI에서 필드가 숨겨집니다. [!UICONTROL 프로필] 작업 공간 및 Customer Journey Analytics을 변경할 수 없지만 변경되지 않으며 기존 데이터 흐름에 부정적인 영향을 주지 않습니다.

이 문서에서는 다양한 XDM 리소스에 대한 필드를 사용하지 않는 방법을 다룹니다. Experience Platform 사용자 인터페이스에서 스키마 편집기를 사용하여 XDM 필드를 사용하지 않는 방법은 다음 자습서를 참조하십시오. [UI에서 XDM 필드 사용 중단](./field-deprecation-ui.md).

## 시작하기

이 자습서에서는 스키마 레지스트리 API를 호출해야 합니다. 다음을 검토하십시오. [개발자 안내서](../api/getting-started.md) 이러한 API를 호출하기 위해 알아야 하는 중요한 정보. 여기에는 다음 항목이 포함됩니다. `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청을 하는 데 필요한 헤더( `Accept` 헤더 및 가능한 값).

## 사용자 정의 필드 사용 안 함 {#custom}

사용자 지정 클래스, 필드 그룹 또는 데이터 형식의 필드를 사용하지 않으려면 PUT 또는 PATCH 요청을 통해 사용자 지정 리소스를 업데이트하고 특성을 추가합니다 `meta:status: deprecated` 을(를) 해당 필드에 보냅니다.

>[!NOTE]
>
>XDM에서 사용자 지정 리소스를 업데이트하는 방법에 대한 일반 정보는 다음 설명서를 참조하십시오.
>
>* [클래스 업데이트](../api/classes.md#patch)
>* [필드 그룹 업데이트](../api/field-groups.md#patch)
>* [데이터 유형 업데이트](../api/data-types.md#patch)


아래 예제 API 호출은 사용자 지정 데이터 유형의 필드를 사용하지 않습니다.

**API 형식**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**요청**

다음 요청은 `expansionArea` 부동산 속성을 설명하는 데이터 유형에 대한 필드.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**응답**

성공적인 응답은 사용자 지정 리소스의 업데이트 세부 정보를 반환하며 더 이상 사용되지 않는 필드에는 `meta:status` 값 `deprecated`. 아래 예제 응답은 공백으로 잘렸습니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
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

## 스키마의 표준 필드 사용 중단 {#standard}

표준 클래스, 필드 그룹 및 데이터 형식의 필드는 더 이상 사용하지 않을 수 없습니다. 대신 설명자를 사용하여 이러한 표준 리소스를 사용하는 개별 스키마에서 사용을 중단할 수 있습니다.

### 필드 사용 중단 설명자 만들기 {#create-descriptor}

POST 사용하지 않을 스키마 필드에 대한 설명자를 만들려면 `/tenant/descriptors` 엔드포인트.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 설명자 유형. 필드 사용 중단 설명자의 경우 이 값을 로 설정해야 합니다. `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 설명자를 적용 중인 스키마 의 입니다. |
| `xdm:sourceVersion` | 설명자를 적용 중인 스키마 버전입니다. 을(를) (으)로 설정해야 함 `1`. |
| `xdm:sourceProperty` | 설명자를 적용하는 스키마 내의 속성에 대한 경로입니다. 설명자를 여러 속성에 적용하려면 경로 목록을 배열 형식으로 제공할 수 있습니다(예: `["/firstName", "/lastName"]`). |

**응답**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### 사용되지 않는 필드 확인 {#verify-deprecation}

설명자가 적용된 후 해당 스키마를 조회하여 필드가 더 이상 사용되지 않는지 여부를 확인하고 적절한 옵션을 사용할 수 있습니다 `Accept` 머리글입니다.

>[!NOTE]
>
>현재 스키마를 나열할 때 더 이상 사용되지 않는 필드를 표시할 수 없습니다.

**API 형식**

```http
GET /tenant/schemas
```

**요청**

API 응답에 더 이상 사용되지 않는 필드에 대한 정보를 포함하려면 `Accept` 헤더 대상 `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**응답**

성공적인 응답은 더 이상 사용되지 않는 필드에 `meta:status` 값 `deprecated`. 아래 예제 응답은 공백으로 잘렸습니다.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## 다음 단계

이 문서에서는 스키마 레지스트리 API를 사용하여 XDM 필드를 사용하지 않는 방법에 대해 설명합니다. 사용자 지정 리소스에 대한 필드 구성에 대한 자세한 내용은 [api에서 XDM 필드 정의](./custom-fields-api.md). 설명자 관리에 대한 자세한 내용은 [descriptors 끝점 안내서](../api/descriptors.md).
