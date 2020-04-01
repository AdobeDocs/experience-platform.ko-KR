---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 혼합 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8

---


# 혼합 만들기

혼합은 &quot;주소&quot; 또는 &quot;프로필 환경 설정&quot;과 같은 특정 개념을 설명하는 데 사용되는 필드 세트입니다. 다양한 표준 혼합을 사용할 수 있으며 조직에 고유한 정보를 캡처하려는 경우 직접 정의할 수 있습니다. 각 믹스인에는 혼합과 호환되는 클래스를 나열하는 `meta:intendedToExtend` 필드가 포함되어 있습니다.

사용 가능한 모든 혼합을 검토하여 각 필드에 포함된 필드에 익숙해질 수 있습니다. 각 &quot;global&quot; 및 &quot;tenant&quot; 컨테이너에 대한 요청을 수행하여 특정 클래스와 호환되는 모든 믹스를 나열하고 &quot;meta:intendToExtend&quot; 필드가 사용 중인 클래스와 일치하는 믹스만 반환할 수 있습니다. 아래 예제는 XDM 개별 프로필 클래스에서 사용할 수 있는 모든 혼합을 반환합니다.

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

아래의 예제 API 요청은 임차인 컨테이너에 새 혼합을 만듭니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

새 혼합을 정의할 때는 `meta:intendedToExtend` 특성이 포함되어야 하며, mixin과 호환되는 `$id` 클래스의 목록이 나열됩니다. 이 예제에서 mixin은 이전에 정의한 Property 클래스와 호환됩니다. 사용자 정의 필드는 `_{TENANT_ID}` 예제와 같이 클래스 스키마에서 다른 혼합이나 필드와 충돌하지 않도록 하려면 아래에 중첩되어야 합니다. 이 `propertyConstruction` 필드는 이전 호출에서 만든 데이터 유형에 대한 참조입니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**응답**

성공적인 응답은 HTTP 상태 201(작성됨)과 새로 만든 믹스의 세부 사항을 포함하는 페이로드를 `$id`반환하고, `meta:altId`및 `version`를 포함합니다. 이러한 값은 읽기 전용이며 스키마 레지스트리에 지정됩니다.

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
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
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
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

테넌트 컨테이너에 모든 믹스를 나열하기 위한 GET 요청을 수행하면 이제 차량 세부 사항 믹스가 포함되거나 URL 인코딩 URI를 사용하여 조회(GET) 요청을 수행하여 새 믹싱을 직접 볼 `$id` 수 있습니다. 모든 조회 요청에 대해 수락 `version` 헤더에 를 포함해야 합니다.
