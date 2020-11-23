---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 클래스 만들기
description: 스키마 레지스트리 API의 /classes 끝점을 사용하면 경험 응용 프로그램 내에서 XDM 클래스를 프로그래밍 방식으로 관리할 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---


# 클래스 끝점

모든 XDM(경험 데이터 모델) 스키마는 클래스를 기반으로 해야 합니다. 클래스는 해당 클래스를 기반으로 하는 모든 스키마는 포함해야 하는 공통 속성의 기본 구조와 이러한 스키마에서 사용할 수 있는 믹스인을 결정합니다. 또한, 스키마의 클래스는 스키마에는 포함할 데이터의 동작 측면을 결정하며, 이 데이터에는 두 가지 유형이 있습니다.

* **[!UICONTROL 기록]**:제목 속성에 대한 정보를 제공합니다. 대상은 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**:작업을 직접 또는 간접적으로 레코드 제목에 의해 수행한 시점에 시스템의 스냅샷을 제공합니다.

>[!NOTE]
>
>데이터 동작이 스키마 구성에 미치는 영향에 대한 자세한 내용은 스키마 컴포지션의 [기본 사항을 참조하십시오](../schema/composition.md).

API의 `/classes` 종점을 사용하면 [!DNL Schema Registry] 경험 애플리케이션 내의 클래스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 끝점은 [[!DNL Schema Registry] API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). 계속하기 전에 [시작하기 가이드](./getting-started.md) (관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서)와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 클래스 목록 검색 {#list}

GET을 각각 또는 `global` 로 요청하여 `tenant` 또는 `/global/classes` 컨테이너 아래에 모든 클래스를 나열할 수 `/tenant/classes`있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 넘는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가적인 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서의 [쿼리 매개 변수](./appendix.md#query) 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 클래스를 검색할 컨테이너: `global` adobe에서 만든 클래스 또는 조직이 소유한 클래스 `tenant` 에 대해 지정합니다. |
| `{QUERY_PARAMS}` | 결과를 필터링하는 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록은 [부록 문서를](./appendix.md#query) 참조하십시오. |

**요청**

다음 요청은 쿼리 매개 변수를 사용하여 `tenant` 컨테이너에서 클래스 목록을 검색하여 `orderby` 해당 `title` 속성별로 클래스를 정렬합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 클래스 목록 `Accept` 에 다음 헤더를 사용할 수 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원본 및 포함된 각 리소스에 대한 전체 JSON 클래스 `$ref` 를 `allOf` 반환합니다. (제한:300) |

**응답**

위의 요청에서는 `application/vnd.adobe.xed-id+json``Accept` 헤더를 사용하므로 응답에는 `title`각 클래스에 대한 속성 `$id`과 `meta:altId`속성만 포함됩니다 `version` . 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 클래스의 모든 속성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## 수업 찾기 {#lookup}

GET 요청 경로에 클래스의 ID를 포함하여 특정 클래스를 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 클래스가 들어 있는 컨테이너: `global` adobe에서 만든 클래스 또는 조직이 소유한 클래스 `tenant` 에 대해 지정합니다. |
| `{CLASS_ID}` | 조회하려는 클래스 `meta:altId` 의 `$id` 또는 URL 인코딩입니다. |

**요청**

다음 요청은 경로에 제공된 값으로 클래스를 `meta:altId` 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청은 헤더에 `version` 포함되어야 `Accept` 합니다. The following `Accept` headers are available:

| `Accept` header | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw 및 `$ref` 와 `allOf`함께 사용할 수 있으며 제목 및 설명이 포함되어 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 그리고 `allOf` 해결되었습니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 제목 또는 설명 `$ref` `allOf`이 없는 Raw |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 제목 또는 설명이 없는 문제를 `allOf` 해결했습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 설명자가 포함된 `allOf` 문제를 해결했습니다. |

**응답**

성공적인 응답은 클래스의 세부 사항을 반환합니다. 반환되는 필드는 요청에 전송된 `Accept` 헤더에 따라 다릅니다. 다양한 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## 클래스 만들기 {#create}

POST 요청을 수행하여 컨테이너 아래에 사용자 지정 클래스를 `tenant` 정의할 수 있습니다.

>[!IMPORTANT]
>
>정의한 사용자 지정 클래스를 기반으로 스키마를 작성할 때 표준 혼합을 사용할 수 없습니다. 각 혼합은 특성이 서로 호환되는 클래스를 `meta:intendedToExtend` 정의합니다. 새 클래스와 호환되는 혼합을 정의하고 나면(믹신 `$id` `meta:intendedToExtend` 필드에 새 클래스의 조합을 사용) 정의된 클래스를 구현하는 스키마를 정의할 때마다 이러한 혼합을 재사용할 수 있습니다. 자세한 내용은 해당 종단점 안내서에서 [믹싱](./mixins.md#create) 만들기 [및 스키마](./schemas.md#create) 를만드는 방법에 대한 섹션을 참조하십시오.
>
>실시간 고객 프로필의 사용자 지정 클래스를 기반으로 스키마를 사용하려는 경우, 조합 스키마는 동일한 클래스를 공유하는 스키마만 기반으로 구성된다는 점을 염두에 두어야 합니다. XDM 개인 프로필 [!UICONTROL 또는] XDM ExperienceEvent와 같은 다른 클래스에 대한 사용자 지정 클래스 스키마를 [!UICONTROL 조합으로 포함하려면 해당 클래스를 사용하는 다른 스키마와의 관계를 설정해야 합니다]. 자세한 내용은 API에서 두 스키마 간 관계 [설정에 대한 자습서를](../tutorials/relationship-api.md) 참조하십시오.

**API 형식**

```http
POST /tenant/classes
```

**요청**

클래스 만들기(POST) 요청에는 두 값 중 하나를 포함하는 `allOf` 속성 `$ref` 이 포함되어야 합니다. `https://ns.adobe.com/xdm/data/record` 또는 `https://ns.adobe.com/xdm/data/time-series`. 이러한 값은 클래스가 기반으로 하는 비헤이비어를 나타냅니다(각각 레코드 또는 시계열). 레코드 데이터와 시간 시리즈 데이터 간의 차이에 대한 자세한 내용은 스키마 컴포지션의 [기본 사항 내에서 동작 유형에 대한 섹션을 참조하십시오](../schema/composition.md).

클래스를 정의할 때 클래스 정의 내에 혼합이나 사용자 정의 필드를 포함할 수도 있습니다. 이로 인해 클래스를 구현하는 모든 스키마에 추가된 혼합과 필드가 포함됩니다. 다음 예제 요청은 회사가 소유하거나 운영하는 다른 속성에 대한 정보를 캡처하는 &quot;Property&quot;라는 클래스를 정의합니다. 여기에는 클래스가 사용될 때마다 포함할 필드가 포함되어 있습니다. `propertyId`

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `_{TENANT_ID}` | 조직의 `TENANT_ID` 네임스페이스입니다. 조직에서 만든 모든 리소스에 이 속성이 포함되어야 다른 리소스와 충돌을 방지할 수 있습니다 [!DNL Schema Registry]. |
| `allOf` | 새 클래스에서 속성을 상속할 리소스 목록입니다. 배열 내의 `$ref` 개체 중 하나는 클래스의 동작을 정의합니다. 이 예에서 클래스는 &quot;record&quot; 동작을 상속합니다. |

**응답**

성공적인 응답은 HTTP 상태 201(만들음)과 새로 만든 클래스, `$id`및 `meta:altId`등의 세부 정보가 포함된 페이로드를 반환합니다 `version`. 이 세 개의 값은 읽기 전용이며 [!DNL Schema Registry]

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

GET 요청을 [수행하여 컨테이너에 있는 모든 클래스](#list) 를 `tenant` 나열합니다. URL 인코딩을 사용하여 조회(GET) 요청을 [수행하여](#lookup) 새 클래스를 직접 `$id` 볼 수도 있습니다.

## 클래스 업데이트 {#put}

PUT 작업을 통해 전체 클래스를 바꿀 수 있으며, 기본적으로 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 클래스를 업데이트하는 경우 본문에는 POST 요청에서 새 클래스를 [만들 때 필요한 모든 필드가 포함되어야](#create) 합니다.

>[!NOTE]
>
>완전히 대체하지 않고 클래스의 일부만 업데이트하려면 클래스의 부분 [업데이트 섹션을 참조하십시오](#patch).

**API 형식**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 다시 쓰려는 클래스 `meta:altId` 의 `$id` 또는 URL 인코딩입니다. |

**요청**

다음 요청은 기존 클래스를 다시 작성하여 해당 클래스 `description` 와 해당 필드 중 `title` 하나를 변경합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**응답**

성공적인 응답은 업데이트된 클래스의 세부 정보를 반환합니다.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 클래스의 일부 업데이트 {#patch}

PATCH 요청을 사용하여 클래스의 일부를 업데이트할 수 있습니다. 이 [!DNL Schema Registry] 는 `add`, `remove`및 `replace`등 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서를 참조하십시오](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하지 않고 전체 리소스를 새 값으로 대체하려면 PUT 작업을 사용하여 클래스 [교체 섹션을 참조하십시오](#put).

**API 형식**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 업데이트할 클래스 `$id` `meta:altId` 의 URL 인코딩 URI 또는 URL입니다. |

**요청**

아래 예제 요청에서는 기존 클래스 `description` 와 해당 필드 중 `title` 하나를 업데이트합니다.

요청 본문은 배열 형태를 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경을 나타냅니다. 각 객체에는 수행할 작업(`op`)과 작업을 수행할 필드(`path`)와 해당 작업에 포함되어야 하는 정보(`value`)가 포함됩니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**응답**

이 응답에는 두 작업이 성공적으로 수행되었음을 보여줍니다. 필드 `description` 와 함께 필드 `title` 가 `propertyId` 업데이트되었습니다.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 클래스 삭제 {#delete}

스키마 레지스트리에서 클래스를 제거해야 하는 경우도 있습니다. 이 작업은 경로에 제공된 클래스 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 삭제할 클래스의 URL 인코딩 `$id` URI `meta:altId` 입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

클래스에 대한 [조회(GET) 요청을](#lookup) 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 이 클래스가 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.