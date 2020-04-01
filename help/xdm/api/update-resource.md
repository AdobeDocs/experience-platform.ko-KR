---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 리소스 업데이트
topic: developer guide
translation-type: tm+mt
source-git-commit: 0d3bee939226d9ef4ac1672b71e0d240f32c5dcf

---


# 리소스 업데이트

PATCH 요청을 사용하여 테넌트 컨테이너의 리소스를 수정하거나 업데이트할 수 있습니다. 스키마 레지스트리는 추가, 제거 및 바꾸기를 비롯한 모든 표준 JSON 패치 작업을 지원합니다.

사용 가능한 작업을 포함한 JSON 패치에 대한 자세한 내용은 공식 JSON [패치 설명서를](http://jsonpatch.com/)참조하십시오.

>[!NOTE] 개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 PUT 작업을 [사용하여 리소스를](replace-resource.md)바꾸는 방법을 참조하십시오.

## 스키마에 믹스 추가

가장 일반적인 PATCH 작업 중 하나는 아래 예제와 같이 이전에 정의한 혼합을 XDM 스키마에 추가하는 것입니다.

**API 형식**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 업데이트할 리소스 유형입니다. 유효한 유형은 `datatypes`, `mixins`, `schemas`및 `classes`입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 `meta:altId` 리소스의 URL입니다. |

**요청**

PATCH 작업을 사용하여 스키마를 업데이트하여 이전에 만든 믹스에 정의된 필드를 포함할 수 있습니다. 이렇게 하려면 URL 인코딩 URI `meta:altId` 또는 URL을 사용하여 스키마에 대한 패치 요청을 수행해야 `$id` 합니다.

요청 본문에는 수행하려는 작업(`op`)과 작업을 수행하려는 위치, (`path`) 작업을 수행하려는 위치 및 작업에 포함할 정보(`value`)가 포함됩니다. 이 예에서는 대상 스키마에 대한 mixin의 `$id` 값이 `meta:extends` 및 `allOf` 필드 모두에 추가됩니다.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**응답**

이 응답에는 두 작업이 성공적으로 수행되었음을 보여줍니다. 혼합이 배열에 `$id` 추가되었으며, `meta:extends` 이제 혼합에 대한 참조(`$ref`)가 배열에 표시됩니다 `$id` `allOf` .

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 리소스의 개별 필드 업데이트

스키마 레지스트리 리소스 내에서 개별 필드를 여러 번 변경하는 PATCH 요청을 전송할 수도 있습니다.

**API 형식**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 업데이트할 리소스 유형입니다. 유효한 유형은 `datatypes`, `mixins`, `schemas`및 `classes`입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 `meta:altId` 리소스의 URL입니다. |

**요청**

요청 본문에는 믹스를 업데이트하는 데 필요한 작업(`op`), 위치(`path`) 및 정보(`value`)가 포함되어 있습니다. 이 요청은 속성 세부 사항 혼합을 업데이트하여 &quot;propertyCity&quot; 필드를 제거하고 주소 정보가 포함된 표준 데이터 형식을 참조하는 새 &quot;propertyAddress&quot; 필드를 추가합니다. 또한 이메일 정보가 포함된 표준 데이터 유형을 참조하는 새로운 &quot;emailAddress&quot; 필드를 추가합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**응답**

성공적인 응답은 새 필드가 있고 &quot;propertyCity&quot; 필드가 제거되었기 때문에 작업이 성공적으로 완료되었음을 나타냅니다.

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
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
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
