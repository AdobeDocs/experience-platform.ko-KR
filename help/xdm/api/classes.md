---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;클래스 레지스트리;스키마 레지스트리;클래스;클래스;클래스;만들기
solution: Experience Platform
title: 클래스 API 끝점
description: 스키마 레지스트리 API의 /classes 끝점을 사용하면 experience 애플리케이션 내에서 XDM 클래스를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 1%

---

# 클래스 끝점

모든 XDM(경험 데이터 모델) 스키마는 클래스를 기반으로 해야 합니다. 클래스는 해당 클래스를 기반으로 하는 모든 스키마에 포함되어야 하는 공통 속성의 기본 구조와 해당 스키마에서 사용할 수 있는 스키마 필드 그룹을 결정합니다. 또한 스키마의 클래스는 스키마에 포함될 데이터의 동작 측면을 결정하며, 그 중 두 가지 유형이 있습니다.

* **[!UICONTROL 레코드]**: 제목의 특성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**: 레코드 주체가 직접 또는 간접적으로 작업을 수행한 시간에 시스템의 스냅숏을 제공합니다.

>[!NOTE]
>
>데이터 동작이 스키마 구성에 미치는 영향 측면에서 데이터 동작에 대한 자세한 내용은 [스키마 컴포지션의 기본 사항](../schema/composition.md)을 참조하세요.

[!DNL Schema Registry] API의 `/classes` 끝점을 사용하면 경험 응용 프로그램 내에서 클래스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 클래스 목록 검색 {#list}

`/global/classes` 또는 `/tenant/classes`에 각각 GET 요청을 하여 `global` 또는 `tenant` 컨테이너 아래에 모든 클래스를 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환되는 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서의 [쿼리 매개 변수](./appendix.md#query)에 대한 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | Adobe 생성 클래스의 경우 `global`에서 클래스를 검색하려는 컨테이너이거나 조직에서 소유한 클래스의 경우 `tenant`에서 클래스를 검색하려는 컨테이너입니다. |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록은 [부록 문서](./appendix.md#query)를 참조하십시오. |

{style="table-layout:auto"}

**요청**

다음 요청은 `orderby` 쿼리 매개 변수를 사용하여 클래스를 `title` 특성별로 정렬하여 `tenant` 컨테이너에서 클래스 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 클래스 목록에 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본 `$ref` 및 `allOf`이(가) 포함된 각 리소스에 대한 전체 JSON 클래스를 반환합니다. (제한: 300) |

{style="table-layout:auto"}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용했으므로 응답에는 각 클래스에 대한 `title`, `$id`, `meta:altId` 및 `version` 특성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 클래스의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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

## 클래스 조회 {#lookup}

GET 요청의 경로에 클래스 ID를 포함하여 특정 클래스를 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 클래스를 보관하는 컨테이너입니다. Adobe이 만든 클래스의 경우 `global`이고, 조직이 소유한 클래스의 경우 `tenant`입니다. |
| `{CLASS_ID}` | 조회할 클래스의 `meta:altId` 또는 URL로 인코딩된 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 경로에 제공된 `meta:altId` 값으로 클래스를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청에는 `Accept` 헤더에 `version`이(가) 포함되어야 합니다. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이(가) 있는 Raw에 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 및 `allOf`이(가) 확인되었으며 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf`이(가) 포함된 원시 버전이며 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 및 `allOf`이(가) 해결되었습니다. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 및 `allOf` 해결됨, 설명자가 포함됨. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 클래스의 세부 정보를 반환합니다. 반환되는 필드는 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

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
  "imsOrg":"{ORG_ID}",
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

POST 요청을 통해 `tenant` 컨테이너에서 사용자 지정 클래스를 정의할 수 있습니다.

>[!IMPORTANT]
>
>정의한 사용자 정의 클래스를 기반으로 스키마를 작성할 경우 표준 필드 그룹을 사용할 수 없습니다. 각 필드 그룹은 `meta:intendedToExtend` 특성에서 호환되는 클래스를 정의합니다. 필드 그룹의 `meta:intendedToExtend` 필드에서 새 클래스의 `$id`을(를) 사용하여 새 클래스와 호환되는 필드 그룹을 정의하면 정의한 클래스를 구현하는 스키마를 정의할 때마다 해당 필드 그룹을 재사용할 수 있습니다. 자세한 내용은 해당 엔드포인트 가이드의 [필드 그룹 만들기](./field-groups.md#create) 및 [스키마 만들기](./schemas.md#create)에 대한 섹션을 참조하십시오.
>
>실시간 고객 프로필의 사용자 지정 클래스를 기반으로 하는 스키마를 사용하려는 경우 유니온 스키마는 동일한 클래스를 공유하는 스키마를 기반으로 생성된다는 점도 유의해야 합니다. [!UICONTROL XDM 개별 프로필] 또는 [!UICONTROL XDM ExperienceEvent]과 같은 다른 클래스의 유니온에 사용자 지정 클래스 스키마를 포함하려면 해당 클래스를 사용하는 다른 스키마와의 관계를 설정해야 합니다. 자세한 내용은 [API의 두 스키마 간의 관계 설정](../tutorials/relationship-api.md)에 대한 자습서를 참조하십시오.

**API 형식**

```http
POST /tenant/classes
```

**요청**

클래스 만들기(POST) 요청에는 두 값 `https://ns.adobe.com/xdm/data/record` 또는 `https://ns.adobe.com/xdm/data/time-series` 중 하나에 대한 `$ref`을(를) 포함하는 `allOf` 특성이 포함되어야 합니다. 이 값은 클래스가 기반으로 하는 동작(각각 레코드 또는 시계열)을 나타냅니다. 레코드 데이터와 시계열 데이터 간의 차이점에 대한 자세한 내용은 [스키마 컴포지션의 기본 사항](../schema/composition.md) 내의 동작 유형에 대한 섹션을 참조하십시오.

클래스를 정의할 때 클래스 정의 내에 필드 그룹 또는 사용자 정의 필드를 포함할 수도 있습니다. 이렇게 하면 추가된 필드 그룹 및 필드가 클래스를 구현하는 모든 스키마에 포함됩니다. 다음 예제 요청은 &quot;Property&quot;라는 클래스를 정의하며, 이 클래스는 회사가 소유 및 운영하는 다른 속성에 대한 정보를 캡처합니다. 클래스를 사용할 때마다 포함될 `propertyId` 필드가 포함되어 있습니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | 조직의 `TENANT_ID` 네임스페이스입니다. 조직에서 만든 모든 리소스는 [!DNL Schema Registry]에 있는 다른 리소스와의 충돌을 방지하기 위해 이 속성을 포함해야 합니다. |
| `allOf` | 새 클래스에서 속성을 상속할 리소스의 목록입니다. 배열 내의 `$ref` 개체 중 하나가 클래스의 동작을 정의합니다. 이 예에서 클래스는 &quot;record&quot; 동작을 상속합니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 HTTP 상태 201(생성됨)과 `$id`, `meta:altId` 및 `version`을(를) 포함하여 새로 만든 클래스의 세부 정보를 포함하는 페이로드를 반환합니다. 이 세 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 할당됩니다.

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
  "imsOrg": "{ORG_ID}",
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

`tenant` 컨테이너의 [모든 클래스를 나열](#list)하는 GET 요청을 수행하면 이제 Property 클래스가 포함됩니다. URL로 인코딩된 `$id`을 사용하여 [조회(GET) 요청을 수행](#lookup)하여 새 클래스를 직접 볼 수도 있습니다.

## 클래스 업데이트 {#put}

PUT 작업을 통해 전체 클래스를 대체할 수 있으며 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 클래스를 업데이트할 때 본문에는 POST 요청에서 [새 클래스를 만들 때](#create)에 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>클래스의 일부를 완전히 바꾸지 않고 일부만 업데이트하려면 [클래스의 일부를 업데이트](#patch)하는 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 다시 쓸 클래스의 `meta:altId` 또는 URL로 인코딩된 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 클래스를 다시 작성하여 해당 `description` 및 해당 필드 중 하나의 `title`을(를) 변경합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 응답은 업데이트된 클래스의 세부 정보를 반환합니다.

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
  "imsOrg": "{ORG_ID}",
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

PATCH 요청을 사용하여 클래스의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은(는) `add`, `remove` 및 `replace`을(를) 포함한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 바꾸려면 [PUT 작업을 사용하여 클래스 바꾸기](#put)의 섹션을 참조하십시오.

**API 형식**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 매개변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 업데이트할 클래스의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

아래 예제 요청에서는 기존 클래스의 `description`을(를) 업데이트하고 필드 중 하나의 `title`을(를) 업데이트합니다.

요청 본문은 배열 형식을 취하며, 나열된 각 객체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`), 작업을 수행할 필드(`path`) 및 해당 작업에 포함할 정보(`value`)가 포함됩니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**응답**

응답은 두 작업이 모두 성공적으로 수행되었음을 보여 줍니다. `propertyId` 필드의 `title`과(와) 함께 `description`이(가) 업데이트되었습니다.

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
  "imsOrg": "{ORG_ID}",
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

스키마 레지스트리에서 클래스를 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 클래스 ID로 DELETE 요청을 수행함으로써 수행됩니다.

**API 형식**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 삭제할 클래스의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

클래스에 대해 [조회(GET) 요청](#lookup)을 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 스키마 레지스트리에서 클래스가 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
