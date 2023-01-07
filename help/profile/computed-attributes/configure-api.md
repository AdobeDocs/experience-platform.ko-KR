---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 필드를 구성하는 방법
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 계산된 속성을 구성하려면 먼저 계산된 속성 값을 가질 필드를 식별해야 합니다. 스키마 레지스트리 API를 사용하여 이 필드를 만들어 계산된 속성 필드를 포함할 스키마와 사용자 지정 필드 그룹을 정의할 수 있습니다.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---

# (알파) 스키마 레지스트리 API를 사용하여 계산된 속성 필드를 구성합니다

>[!IMPORTANT]
>
>계산된 특성 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 구성하려면 먼저 계산된 속성 값을 가질 필드를 식별해야 합니다. 스키마 레지스트리 API를 사용하여 이 필드를 만들어 계산된 속성 필드를 포함할 스키마와 사용자 지정 스키마 필드 그룹을 정의할 수 있습니다. 계산된 속성으로 사용할 속성을 조직에서 추가할 수 있는 별도의 &quot;계산된 속성&quot; 스키마 및 필드 그룹을 만드는 것이 좋습니다. 이렇게 하면 조직에서 계산된 속성 스키마를 데이터 처리에 사용 중인 다른 스키마와 완전히 분리할 수 있습니다.

이 문서의 워크플로우에서는 스키마 레지스트리 API를 사용하여 사용자 지정 필드 그룹을 참조하는 프로필 사용 &quot;계산된 속성&quot; 스키마를 만드는 방법을 간략하게 설명합니다. 이 문서에는 계산된 속성과 관련된 샘플 코드가 포함되어 있지만 [스키마 레지스트리 API 안내서](../../xdm/api/overview.md) api를 사용하여 필드 그룹 및 스키마를 정의하는 방법에 대한 자세한 정보.

## 계산된 속성 필드 그룹 만들기

스키마 레지스트리 API를 사용하여 필드 그룹을 만들려면 먼저 `/tenant/fieldgroups` endpoint 및 request body에 필드 그룹의 세부 정보를 제공합니다. 스키마 레지스트리 API를 사용하는 필드 그룹 작업에 대한 자세한 내용은 [필드 그룹 API 엔드포인트 안내서](../../xdm/api/field-groups.md).

**API 형식**

```http
POST /tenant/fieldgroups
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| 속성 | 설명 |
|---|---|
| `title` | 생성 중인 필드 그룹의 이름입니다. |
| `meta:intendedToExtend` | 필드 그룹을 사용할 수 있는 XDM 클래스입니다. |

**응답**

성공적인 요청은 HTTP 응답 상태 201(생성됨)을 반환하며 이 반환에는 다음을 포함하여 새로 만든 필드 그룹의 세부 사항이 포함됩니다 `$id`, `meta:altIt`, 및 `version`. 이러한 값은 읽기 전용이며 스키마 레지스트리에 의해 지정됩니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
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

## 추가 계산된 속성으로 필드 그룹 업데이트

계산된 속성이 더 필요한 경우, `/tenant/fieldgroups` 엔드포인트. 이 요청을 수행하려면 경로에서 만든 필드 그룹의 고유 ID와 본문에 추가할 모든 새 필드를 포함해야 합니다.

스키마 레지스트리 API를 사용하여 필드 그룹을 업데이트하는 방법에 대한 자세한 내용은 [필드 그룹 API 엔드포인트 안내서](../../xdm/api/field-groups.md).

**API 형식**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**요청**

이 요청은 와 관련된 새 필드를 추가합니다 `purchaseSummary` 정보.

>[!NOTE]
>
>PUT 요청을 통해 필드 그룹을 업데이트할 때 본문에는 POST 요청에 새 필드 그룹을 만들 때 필요한 모든 필드가 포함되어야 합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**응답**

성공적인 응답은 업데이트된 필드 그룹의 세부 정보를 반환합니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
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

스키마 레지스트리 API를 사용하여 스키마를 만들려면 다음을 POST 요청하여 시작하십시오 `/tenant/schemas` endpoint 및 요청 본문에 스키마 세부 정보 제공 스키마가에 대해서도 활성화되어 있어야 합니다 [!DNL Profile] 스키마 클래스에 대한 결합 스키마의 일부로 나타납니다.

자세한 내용은 [!DNL Profile]-사용 가능한 스키마 및 결합 스키마를 확인하십시오. [[!DNL Schema Registry] API 안내서](../../xdm/api/overview.md) 그리고 [스키마 구성 기본 사항 설명서](../../xdm/schema/composition.md).

**API 형식**

```http
POST /tenants/schemas
```

**요청**

다음 요청은 를 참조하는 새 스키마를 만듭니다 `computedAttributesFieldGroup` 이 문서(고유 ID 사용)에서 앞에서 생성되었으며 ( `meta:immutableTags` 배열)을 참조하십시오. 스키마 레지스트리 API를 사용하여 스키마를 만드는 방법에 대한 자세한 지침은 [스키마 API 엔드포인트 안내서](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공적인 응답은 HTTP 상태 201(작성됨) 및 를 포함하여 새로 만든 스키마의 세부 사항이 포함된 페이로드를 반환합니다. `$id`, `meta:altId`, 및 `version`. 이러한 값은 읽기 전용이며 스키마 레지스트리에 의해 지정됩니다.

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
  "imsOrg": "{ORG_ID}",
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

이제 계산된 속성이 저장되는 스키마와 필드 그룹을 만들었으므로 `/computedattributes` API 엔드포인트. API에서 계산된 속성을 만드는 자세한 단계는 [계산된 특성 API 끝점 안내서](ca-api.md).
