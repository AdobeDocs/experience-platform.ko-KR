---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;mixin registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: 혼합 만들기
description: 스키마 레지스트리 API의 /mixins 종단점을 사용하면 경험 응용 프로그램 내에서 XDM 믹스를 프로그래밍 방식으로 관리할 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---


# 혼합 끝점

믹스는 개별 사용자, 우편 주소 또는 웹 브라우저 환경과 같은 특정 개념을 나타내는 하나 이상의 필드를 정의하는 구성 요소를 재사용할 수 있습니다. 믹스는 호환 클래스를 구현하는 스키마의 일부로 포함되도록 합니다. 이때, 이 클래스는 데이터(레코드 또는 시간 시리즈)의 동작에 따라 달라집니다. [!DNL Schema Registry] API의 `/mixins` 종단점을 사용하면 경험 애플리케이션 내의 믹스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, Experience Platform API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## {#list} 혼합 목록 검색

각각 `/global/mixins` 또는 `/tenant/mixins`에 GET 요청을 하여 `global` 또는 `tenant` 컨테이너 아래에 모든 믹스를 표시할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 집합을 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 결과를 필터링하고 반환된 리소스 수를 줄이기 위해 추가 쿼리 매개 변수를 사용하는 것이 좋습니다. 자세한 내용은 부록 문서의 [쿼리 매개 변수](./appendix.md#query)에 대한 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 믹스를 검색할 컨테이너:Adobe에서 만든 믹스인 경우 `global`, 조직에서 소유한 믹스의 경우 `tenant` |
| `{QUERY_PARAMS}` | 결과를 필터링하는 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록은 [부록 문서](./appendix.md#query)를 참조하십시오. |

**요청**

다음 요청은 `tenant` 컨테이너에서 `orderby` 쿼리 매개 변수를 사용하여 믹스를 `title` 특성으로 정렬하는 믹싱 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 달라집니다. 다음 `Accept` 헤더는 믹스를 나열하는 데 사용할 수 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원본 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 믹싱을 반환합니다. (제한:300) |

**응답**

위의 요청은 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용하므로 응답에는 각 믹스에 대한 `title`, `$id`, `meta:altId` 및 `version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 믹스의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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

## {#lookup} 혼합 찾기

GET 요청 경로에 믹스의 ID를 포함하여 특정 믹싱을 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 혼합물을 포함하는 컨테이너:Adobe에서 만든 믹싱의 경우 `global`, 조직의 소유인 혼합의 경우 `tenant`. |
| `{MIXIN_ID}` | 찾아볼 믹스의 `meta:altId` 또는 URL 인코딩 `$id`. |

**요청**

다음 요청은 경로에 제공된 `meta:altId` 값으로 믹싱을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 달라집니다. 모든 조회 요청에는 `Accept` 헤더에 `version`이 포함되어야 합니다. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` header | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | `$ref` 및 `allOf`이(가) 있는 Raw에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 그리고  `allOf` 해결되었습니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | `$ref` 및 `allOf`이 있는 Raw에 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 제목 또는 설명 없이  `allOf` 해결되었습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 설명자가 포함된  `allOf` 문제가 해결되었습니다. |

**응답**

성공적인 응답은 믹싱의 세부 사항을 반환합니다. 반환되는 필드는 요청에 전송된 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

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

## {#create} 혼합 만들기

POST 요청을 수행하여 `tenant` 컨테이너 아래에 사용자 정의 믹싱을 정의할 수 있습니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

새 믹싱을 정의할 때는 `meta:intendedToExtend` 특성이 포함되어야 믹신이 호환되는 클래스의 `$id`이(가) 나열됩니다. 이 예제에서 mixin은 이전에 정의된 `Property` 클래스와 호환됩니다. 예제와 같이 사용자 정의 필드는 클래스 및 기타 믹싱에서 제공하는 유사한 필드와 충돌을 피하려면 `_{TENANT_ID}` 아래에 중첩되어야 합니다.

>[!NOTE]
>
>혼합에 포함할 다른 필드 유형을 정의하는 방법에 대한 자세한 내용은 [필드 제한 조건 안내](../schema/field-constraints.md#define-fields)를 참조하십시오.

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

성공적인 응답은 HTTP 상태 201(만들어짐)과 새로 만든 믹싱에 대한 `$id`, `meta:altId` 및 `version` 등의 세부 정보가 포함된 페이로드를 반환합니다. 이러한 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 할당됩니다.

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

이제 임차인 컨테이너에서 [모든 믹싱](#list)에 대한 GET 요청을 수행하면 속성 세부 사항 믹싱이 포함되거나 URL 인코딩 `$id` URI를 사용하여 [조회(GET) 요청](#lookup)을 수행하여 새 믹싱을 직접 볼 수 있습니다.

## 믹신 {#put} 업데이트

PUT 작업을 통해 전체 믹싱을 교체할 수 있으며 기본적으로 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 믹싱을 업데이트할 때 본문에는 POST 요청에 [새 믹신](#create)을 만들 때 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>완전히 대체하지 않고 믹스의 일부만 업데이트하려면 [믹스의 일부 업데이트](#patch)에 대한 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 다시 쓰려는 믹스의 `meta:altId` 또는 URL 인코딩 `$id`. |

**요청**

다음 요청은 기존 믹싱을 다시 작성하여 새 `propertyCountry` 필드를 추가합니다.

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

성공적인 응답은 업데이트된 믹싱의 세부 정보를 반환합니다.

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

## {#patch} 믹스의 일부 업데이트

PATCH 요청을 사용하여 믹스의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은 `add`, `remove` 및 `replace`을(를) 비롯한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 가이드](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 PUT 작업](#put)을 사용하여 믹싱을 교체하는 [의 섹션을 참조하십시오.

**API 형식**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 업데이트할 믹스의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

**요청**

아래 예제 요청에서는 기존 믹스의 `description`을 업데이트하고 새 `propertyCity` 필드를 추가합니다.

요청 본문은 배열 형식을 사용하며, 나열된 각 객체는 개별 필드에 대한 특정 변경을 나타냅니다. 각 개체에는 수행할 작업(`op`)이 포함되어 있으며, (`path`)에서 작업을 수행해야 하는 필드와 해당 작업에 포함할 정보(`value`)는 무엇입니까?

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

이 응답에는 두 작업이 성공적으로 수행되었음을 보여줍니다. `description`이(가) 업데이트되었으며 `definitions` 아래에 `propertyCountry`이(가) 추가되었습니다.

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

## {#delete} 혼합 삭제

스키마 레지스트리에서 믹싱을 제거해야 하는 경우도 있습니다. 이 작업은 경로에 제공된 혼합 ID를 사용하여 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MIXIN_ID}` | 삭제할 믹스의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

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

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

[조회(GET) 요청](#lookup)을 믹싱에 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 혼합이 스키마 레지스트리에서 제거되었으므로 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.