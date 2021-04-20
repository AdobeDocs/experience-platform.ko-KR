---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 필드를 구성하는 방법
topic: guide
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 이 필드는 스키마 레지스트리 API를 사용하여 계산된 속성 필드를 포함할 스키마 및 사용자 정의 믹싱을 정의할 수 있습니다.
translation-type: tm+mt
source-git-commit: 2a4fb8af8cd29254c499bfa6bfb8b316a4834526
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# (알파) 스키마 레지스트리 API를 사용하여 계산된 속성 필드를 구성합니다.

>[!IMPORTANT]
>
>계산된 속성 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 이 필드는 스키마 레지스트리 API를 사용하여 계산된 속성 필드를 포함할 스키마 및 사용자 정의 믹싱을 정의할 수 있습니다. 계산된 특성으로 사용할 속성을 추가할 수 있는 별도의 &quot;계산된 특성&quot; 스키마 및 혼합을 만드는 것이 좋습니다. 이렇게 하면 조직에서 계산된 속성 스키마를 데이터 수집에 사용되는 다른 스키마와 깔끔하게 분리할 수 있습니다.

이 문서의 작업 과정은 스키마 레지스트리 API를 사용하여 사용자 정의 믹싱을 참조하는 프로필 사용 &quot;계산된 특성&quot; 스키마를 만드는 방법에 대해 설명합니다. 이 문서에는 계산된 속성과 관련된 샘플 코드가 포함되어 있지만 API를 사용하여 혼합과 스키마를 정의하는 방법에 대한 자세한 내용은 [스키마 레지스트리 API 안내서](../../xdm/api/overview.md)를 참조하십시오.

## 계산된 특성 혼합 만들기

스키마 레지스트리 API를 사용하여 믹싱을 만들려면 먼저 `/tenant/mixins` 끝점에 POST 요청을 하고 요청 본문에 혼합에 대한 세부 정보를 제공하는 방식으로 시작합니다. 스키마 레지스트리 API를 사용한 믹싱 작업에 대한 자세한 내용은 [믹싱 API 끝점 안내서](../../xdm/api/mixins.md)를 참조하십시오.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Mixin",
        "description":"Description of the mixin.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

| 속성 | 설명 |
|---|---|
| `title` | 만들고 있는 믹싱의 이름입니다. |
| `meta:intendedToExtend` | 혼합을 사용할 수 있는 XDM 클래스입니다. |

**응답**

요청이 성공하면 `$id`, `meta:altIt` 및 `version` 등 새로 만든 믹싱의 세부 정보가 포함된 응답 본문이 있는 HTTP 응답 상태 201(생성됨)이 반환됩니다. 이러한 값은 읽기 전용이며 스키마 레지스트리에 할당됩니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of the mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 추가 계산된 특성을 사용하여 믹신 업데이트

계산된 특성이 더 필요하므로, `/tenant/mixins` 끝점에 PUT 요청을 수행하여 계산된 특성 혼합을 추가 특성으로 업데이트할 수 있습니다. 이 요청을 수행하려면 경로에 만든 믹싱의 고유한 ID와 본문에 추가할 모든 새 필드를 포함해야 합니다.

스키마 레지스트리 API를 사용하여 믹스를 업데이트하는 방법에 대한 자세한 내용은 [믹싱 API 끝점 안내서](../../xdm/api/mixins.md)를 참조하십시오.

**API 형식**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

**요청**

이 요청은 `purchaseSummary` 정보와 관련된 새 필드를 추가합니다.

>[!NOTE]
>
>PUT 요청을 통해 믹싱을 업데이트할 때 본문에는 POST 요청에 새 믹싱을 만들 때 필요한 모든 필드가 포함되어야 합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Mixin",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of mixin.",
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

**응답**

성공적인 응답은 업데이트된 믹싱의 세부 정보를 반환합니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 프로필 사용 스키마 만들기

스키마 레지스트리 API를 사용하여 스키마를 만들려면 먼저 `/tenant/schemas` 끝점에 POST 요청을 하고 요청 본문에 스키마의 세부 정보를 제공하는 방식으로 시작합니다. 또한 스키마는 [!DNL Profile]에 대해 활성화되어야 하며 스키마 클래스에 대한 공용 스키마의 일부로 나타나야 합니다.

[!DNL Profile] 사용 가능한 스키마 및 결합 스키마에 대한 자세한 내용은 [[!DNL Schema Registry] API 안내서](../../xdm/api/overview.md) 및 [스키마 구성 기본 설명서](../../xdm/schema/composition.md)를 참조하십시오.

**API 형식**

```http
POST /tenants/schemas
```

**요청**

다음 요청은 이 문서에서 이전에 만든 `computedAttributesMixin`을(를) 참조하고(고유 ID 사용) `meta:immutableTags` 배열을 사용하여 프로필 조합 스키마에 대해 활성화되는 새 스키마를 만듭니다. 스키마 레지스트리 API를 사용하여 스키마를 만드는 방법에 대한 자세한 지침은 [스키마 API 끝점 안내서](../../xdm/api/schemas.md)를 참조하십시오.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 스키마의 `$id`, `meta:altId` 및 `version`을(를) 포함하여 세부 정보가 포함된 페이로드를 반환합니다. 이러한 값은 읽기 전용이며 스키마 레지스트리에 할당됩니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## 다음 단계

계산된 특성이 저장될 스키마와 혼합을 만들었으므로 이제 `/computedattributes` API 끝점을 사용하여 계산된 특성을 만들 수 있습니다. API에서 계산된 속성을 만드는 자세한 단계를 보려면 [계산된 특성 API 끝점 안내서](ca-api.md)에서 제공하는 단계를 따르십시오.