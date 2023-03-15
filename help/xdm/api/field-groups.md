---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;필드 그룹;필드 그룹;필드 그룹;만들기
solution: Experience Platform
title: 필드 그룹 API 끝점
description: Schema Registry API의 /fieldgroups 엔드포인트를 사용하면 experience 애플리케이션 내에서 XDM 스키마 필드 그룹을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 2%

---

# 스키마 필드 그룹 엔드포인트

스키마 필드 그룹은 개별 사용자, 메일링 주소 또는 웹 브라우저 환경과 같이 특정 개념을 나타내는 하나 이상의 필드를 정의하는 재사용 가능한 구성 요소입니다. 필드 그룹은 나타내는 데이터(레코드 또는 시계열)의 비헤이비어에 따라 호환되는 클래스를 구현하는 스키마의 일부로 포함되어야 합니다. 다음 `/fieldgroups` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 경험 애플리케이션 내에서 필드 그룹을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 필드 그룹 목록 검색 {#list}

아래에 모든 필드 그룹을 나열할 수 있습니다. `global` 또는 `tenant` 에 대한 GET 요청을 하여 컨테이너 `/global/fieldgroups` 또는 `/tenant/fieldgroups`, 각각

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환되는 리소스 수를 줄이는 것이 좋습니다. 의 섹션을 참조하십시오. [쿼리 매개 변수](./appendix.md#query) 자세한 내용은 부록 문서를 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 필드 그룹을 검색할 컨테이너: `global` Adobe 생성 필드 그룹 또는 `tenant` (조직에서 소유한 필드 그룹). |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 다음을 참조하십시오. [부록 문서](./appendix.md#query) 사용 가능한 매개 변수 목록입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 다음에서 필드 그룹 목록을 검색합니다. `tenant` 컨테이너, 사용 `orderby` 쿼리 매개 변수를 사용하여 필드 그룹을 기준으로 정렬 `title` 특성.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 다음에 따라 다릅니다. `Accept` 헤더가 요청에서 전송되었습니다. 다음 `Accept` 헤더는 필드 그룹을 나열하는 데 사용할 수 있습니다.

| `Accept` 머리글 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 필드 그룹을 반환합니다. `$ref` 및 `allOf` 포함. (제한: 300) |

{style="table-layout:auto"}

**응답**

위의 요청은 `application/vnd.adobe.xed-id+json` `Accept` 따라서 응답에는 다음만 포함됩니다. `title`, `$id`, `meta:altId`, 및 `version` 각 필드 그룹의 속성입니다. 다른 항목 사용 `Accept` 헤더 (`application/vnd.adobe.xed+json`)는 각 필드 그룹의 모든 속성을 반환합니다. 적절한 항목 선택 `Accept` 응답에 필요한 정보에 따라 다릅니다.

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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## 필드 그룹 조회 {#lookup}

GET 요청의 경로에 필드 그룹의 ID를 포함하여 특정 필드 그룹을 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 필드 그룹을 저장하는 컨테이너입니다. `global` Adobe 생성 필드 그룹 또는 `tenant` (조직이 소유한 필드 그룹). |
| `{FIELD_GROUP_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 조회할 필드 그룹의 이름입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 다음으로 필드 그룹을 검색합니다. `meta:altId` 경로에 제공된 값입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 다음에 따라 다릅니다. `Accept` 헤더가 요청에서 전송되었습니다. 모든 조회 요청에는 `version` 에 포함 `Accept` 머리글입니다. 다음 `Accept` 머리글을 사용할 수 있습니다.

| `Accept` 머리글 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 원시 `$ref` 및 `allOf`에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 및 `allOf` 해결됨, 제목 및 설명 포함. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 원시 `$ref` 및 `allOf`, 제목 또는 설명 없음. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 및 `allOf` 해결됨, 제목 또는 설명 없음. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 및 `allOf` 해결됨, 설명자가 포함됨. |

{style="table-layout:auto"}

**응답**

성공한 응답은 필드 그룹의 세부 정보를 반환합니다. 반환되는 필드는 다음에 따라 다릅니다 `Accept` 헤더가 요청에서 전송되었습니다. 다른 실험 `Accept` 응답 비교와 사용 사례에 가장 적합한 헤더를 결정하는 헤더입니다.

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

## 필드 그룹 만들기 {#create}

아래에서 사용자 정의 필드 그룹을 정의할 수 있습니다. `tenant` POST 요청을 하여 컨테이너를 작성합니다.

**API 형식**

```http
POST /tenant/fieldgroups
```

**요청**

새 필드 그룹을 정의할 때 다음을 포함해야 합니다. `meta:intendedToExtend` 속성, 목록 `$id` 필드 그룹이 호환되는 클래스에서 사용됩니다. 이 예에서 필드 그룹은 와 호환됩니다. `Property` 이전에 정의된 클래스입니다. 사용자 정의 필드는 아래에 중첩되어야 합니다. `_{TENANT_ID}` (예제에 표시된 대로) 클래스와 다른 필드 그룹에서 제공하는 유사한 필드와의 충돌을 피합니다.

>[!NOTE]
>
>필드 그룹에 포함할 다양한 필드 유형을 정의하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [api에서 사용자 정의 필드 정의](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공적인 응답은 HTTP 상태 201(생성됨) 및 다음을 포함하여 새로 생성된 필드 그룹의 세부 사항이 포함된 페이로드를 반환합니다. `$id`, `meta:altId`, 및 `version`. 이 값은 읽기 전용이며 [!DNL Schema Registry].

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

에 대한 GET 요청 수행 [모든 필드 그룹 나열](#list) 이제 테넌트 컨테이너에 속성 세부 정보 필드 그룹이 포함되거나 [조회(GET) 요청 수행](#lookup) url 인코딩 사용 `$id` 새 필드 그룹을 바로 볼 수 있는 URI입니다.

## 필드 그룹 업데이트 {#put}

PUT 작업을 통해 전체 필드 그룹을 바꿀 수 있으며, 기본적으로 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 필드 그룹을 업데이트할 때 본문에는 다음과 같은 경우에 필요한 모든 필드가 포함되어야 합니다. [새 필드 그룹 만들기](#create) POST 요청에서.

>[!NOTE]
>
>필드 그룹의 일부를 완전히 대체하지 않고 일부만 업데이트하려면 [필드 그룹의 일부 업데이트](#patch).

**API 형식**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 다시 쓸 필드 그룹의 이름입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 필드 그룹을 다시 작성하여 새 필드 그룹을 추가합니다. `propertyCountry` 필드.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 응답은 업데이트된 필드 그룹의 세부 정보를 반환합니다.

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

## 필드 그룹의 일부 업데이트 {#patch}

PATCH 요청을 사용하여 필드 그룹의 일부를 업데이트할 수 있습니다. 다음 [!DNL Schema Registry] 는 다음을 포함한 모든 표준 JSON 패치 작업을 지원합니다. `add`, `remove`, 및 `replace`. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 바꾸려면 [PUT 작업을 사용하여 필드 그룹 바꾸기](#put).

**API 형식**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{FIELD_GROUP_ID}` | URL로 인코딩됨 `$id` URI 또는 `meta:altId` 업데이트하려는 필드 그룹의 이름입니다. |

{style="table-layout:auto"}

**요청**

아래의 예제 요청은 `description` 기존 필드 그룹 및 추가 `propertyCity` 필드.

요청 본문은 배열 형식을 취하며, 나열된 각 객체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 객체에는 수행할 작업이 포함됩니다(`op`) 작업을 수행할 필드(`path`) 및 해당 작업에 포함해야 하는 정보(`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

응답은 두 작업이 모두 성공적으로 수행되었음을 보여 줍니다. 다음 `description` 이(가) 업데이트되었습니다. `propertyCountry` 이(가) 아래에 추가되었습니다. `definitions`.

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

## 필드 그룹 삭제 {#delete}

스키마 레지스트리에서 필드 그룹을 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 필드 그룹 ID로 DELETE 요청을 수행함으로써 수행됩니다.

**API 형식**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{FIELD_GROUP_ID}` | URL로 인코딩됨 `$id` URI 또는 `meta:altId` 을(를) 삭제하려는 필드 그룹의 일부로 지정합니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

다음을 시도하여 삭제를 확인할 수 있습니다. [조회(GET) 요청](#lookup) 필드 그룹으로 이동합니다. 다음을 포함해야 합니다. `Accept` 요청에 헤더가 있지만 필드 그룹이 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
