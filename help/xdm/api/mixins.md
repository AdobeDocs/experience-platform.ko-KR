---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;혼합 레지스트리;스키마 레지스트리;mixin;Mixin;Mixin;Mixin;Mixin;Mixin;Mixin;Mixin;만들기
solution: Experience Platform
title: Mixin API 끝점
description: 스키마 레지스트리 API의 /mixin 종단점을 사용하면 경험 애플리케이션 내에서 XDM mixin을 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: 93ba2fe3-0277-4c06-acf6-f236cd33252e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 3%

---


# Mixin 끝점(더 이상 사용되지 않음)

>[!IMPORTANT]
>
>Mixin의 이름이 스키마 필드 그룹으로 변경되었으므로 `/mixins` 종단점은 `/fieldgroups` 종단점을 위해 더 이상 사용되지 않습니다.
>
>`/mixins`은(는) 기존 종단점으로 계속 유지되지만, 경험 애플리케이션에서 스키마 레지스트리 API의 새로운 구현에 `/fieldgroups`을 사용하는 것이 좋습니다. 자세한 내용은 [필드 그룹 엔드포인트 가이드](./field-groups.md)를 참조하십시오.

Mixins는 개별 사용자, 우편 주소 또는 웹 브라우저 환경과 같은 특정 개념을 나타내는 필드를 하나 이상 정의하는 재사용 가능한 구성 요소입니다. Mixin은 Mixin이 나타내는 데이터의 동작(레코드 또는 시계열)에 따라 호환 클래스를 구현하는 스키마의 일부로 포함되도록 합니다. [!DNL Schema Registry] API의 `/mixins` 종단점을 사용하면 경험 애플리케이션 내의 mixins를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## mixin 목록 검색 {#list}

각각 `/global/mixins` 또는 `/tenant/mixins`에 GET 요청을 하여 `global` 또는 `tenant` 컨테이너 아래에 모든 mixin을 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서에서 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | Mixin을 검색할 컨테이너: Adobe이 만든 mixin의 경우 `global`, 조직이 소유한 mixin의 경우 `tenant` 입니다. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록에 대해서는 [부록 document](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `tenant` 컨테이너에서 `orderby` 쿼리 매개 변수를 사용하여 mixin 목록을 검색하여 `title` 특성으로 정렬합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 `Accept` 헤더를 mixin 목록에 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON mixin을 반환합니다. (제한: 300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용하므로 응답에는 각 mixin에 대한 `title`, `$id`, `meta:altId` 및 `version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 mixin의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/mixins"
    }
  }
}
```

## 믹신을 찾아봐 {#lookup}

GET 요청 경로에 mixin의 ID를 포함하여 특정 mixin을 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 혼합기가 들어 있는 컨테이너: Adobe이 만든 mixin의 경우 `global`, 조직이 소유한 mixin의 경우 `tenant` 입니다. |
| `{MIXIN_ID}` | 조회할 mixin의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 경로에 제공된 `meta:altId` 값으로 mixin을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
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

성공적인 응답은 mixin의 세부 정보를 반환합니다. 반환되는 필드는 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
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

## mixin 만들기 {#create}

POST 요청을 만들어 `tenant` 컨테이너 아래에 사용자 지정 mixin을 정의할 수 있습니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

새 mixin을 정의할 때는 Mixin이 호환되는 클래스의 `meta:intendedToExtend` 속성을 포함해야 합니다. `$id` 이 예제에서 mixin은 이전에 정의된 `Property` 클래스와 호환됩니다. 사용자 지정 필드는 클래스 및 다른 mixin에서 제공하는 유사한 필드가 있는 충돌을 피하려면 `_{TENANT_ID}` 아래에 중첩되어야 합니다(예제에 표시된 대로).

>[!NOTE]
>
>mixin에 포함할 다른 필드 유형을 정의하는 방법에 대한 자세한 내용은 [필드 제한 가이드](../schema/field-constraints.md#define-fields)를 참조하십시오.

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

성공적으로 응답하면 `$id`, `meta:altId` 및 `version`를 포함하여 새로 만든 mixin의 세부 정보가 포함된 페이로드 및 HTTP 상태 201(생성됨)이 반환됩니다. 이러한 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 지정됩니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

이제 임차인 컨테이너에 있는 모든 mixin](#list)에 대한 GET 요청을 수행하면 속성 세부 사항 mixin이 포함되거나, URL로 인코딩된 `$id` URI를 사용하여 조회(GET) 요청](#lookup)을 수행하여 새 mixin을 직접 볼 수 있습니다.[[

## mixin 업데이트 {#put}

기본적으로 리소스를 다시 작성하는 PUT 작업을 통해 전체 mixin을 바꿀 수 있습니다. PUT 요청을 통해 mixin을 업데이트할 때는 본문에는 POST 요청에 [새 mixin](#create)을 만들 때 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>Mixin의 일부를 완전히 대체하지 않고 일부만 업데이트하려면 [mixin](#patch)의 일부를 업데이트하는 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 다시 쓸 mixin의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 mixin을 다시 작성하여 새 `propertyCountry` 필드를 추가합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**응답**

성공적인 응답은 업데이트된 mixin의 세부 정보를 반환합니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

## mixin 일부 업데이트 {#patch}

PATCH 요청을 사용하여 mixin 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은 `add`, `remove` 및 `replace`를 비롯한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업](#put)을 사용하여 mixin 바꾸기의 섹션을 참조하십시오.

**API 형식**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 업데이트할 mixin의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 기존 mixin의 `description`을 업데이트하고 새 `propertyCity` 필드를 추가합니다.

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`)이 포함되어 있으며, (`path`)에서 작업을 수행해야 하는 필드와 해당 작업에 포함해야 하는 정보가 포함됩니다(`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**응답**

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. `description`이(가) 업데이트되었으며 `definitions` 아래에 `propertyCountry`이(가) 추가되었습니다.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
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

## mixin 삭제 {#delete}

스키마 레지스트리에서 mixin을 제거해야 하는 경우가 있을 수 있습니다. 이 작업은 경로에 제공된 mixin ID를 사용하여 DELETE 요청을 수행함으로써 수행됩니다.

**API 형식**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 삭제할 mixin의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

mixin에 [조회(GET) 요청](#lookup)을 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 mixin이 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
