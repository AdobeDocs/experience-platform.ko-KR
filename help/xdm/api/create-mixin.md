---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: 혼합 만들기
topic: developer guide
description: 혼합은 "주소" 또는 "프로필 환경 설정"과 같은 특정 개념을 설명하는 데 사용되는 필드 집합입니다. 다양한 표준 혼합을 사용할 수 있으며, 조직 고유의 정보를 캡처하고자 할 때 직접 정의할 수 있습니다.
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 혼합 만들기

혼합은 &quot;주소&quot; 또는 &quot;프로필 환경 설정&quot;과 같은 특정 개념을 설명하는 데 사용되는 필드 집합입니다. 다양한 표준 혼합을 사용할 수 있으며, 조직 고유의 정보를 캡처하고자 할 때 직접 정의할 수 있습니다. 각 믹스인에는 믹싱과 호환되는 클래스를 나열하는 필드가 포함되어 있습니다. `meta:intendedToExtend`

각 영역에 포함된 필드에 익숙해지도록 사용 가능한 모든 혼합을 검토하는 것이 도움이 될 수 있습니다. 각 &quot;global&quot; 및 &quot;tenant&quot; 컨테이너에 대한 요청을 수행하여 특정 클래스와 호환되는 모든 믹스를 목록(GET)으로 표시할 수 있으며, &quot;meta:intendedToExtend&quot; 필드가 사용 중인 클래스와 일치하는 믹스만 반환합니다. 아래 예제는 [!DNL XDM Individual Profile] 클래스와 함께 사용할 수 있는 모든 혼합을 반환합니다.

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

아래의 예제 API 요청은 테넌트 컨테이너에 새 혼합을 만듭니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

새 혼합을 정의할 때는 `meta:intendedToExtend` 특성이 포함되어야 하며, 믹신이 호환되는 클래스 `$id` 의 목록이 나열됩니다. 이 예제에서 mixin은 이전에 정의한 속성 클래스와 호환됩니다. 사용자 정의 필드는 `_{TENANT_ID}` (예제와 같이) 클래스 스키마의 다른 믹스나 필드와 충돌하지 않도록 하려면 아래 중첩되어야 합니다. 이 필드는 `propertyConstruction` 이전 호출에서 만든 데이터 유형에 대한 참조입니다.

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

성공적인 응답은 HTTP 상태 201(만들음)과 새로 만든 믹싱에 대한 세부 사항을 포함하는 페이로드를 `$id`반환합니다. 여기에는, `meta:altId`및 `version`. 이러한 값은 읽기 전용이며, [!DNL Schema Registry]

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

테넌트 컨테이너에 모든 믹스를 나열하기 위한 GET 요청을 수행하면 이제 차량 세부 사항 믹싱이 포함되거나 URL 인코딩 URI를 사용하여 조회(GET) 요청을 수행하여 새 믹싱을 직접 볼 수 있습니다. `$id` 모든 조회 요청에 대한 수락 헤더 `version` 에 해당 항목을 포함해야 합니다.
