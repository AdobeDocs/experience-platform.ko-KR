---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;클래스 레지스트리;스키마 레지스트리;클래스;클래스;클래스;클래스;클래스;클래스;클래스;클래스;생성
solution: Experience Platform
title: 클래스 API 끝점
description: 스키마 레지스트리 API의 /classes 종단점을 사용하면 경험 애플리케이션 내에서 XDM 클래스를 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 1%

---

# 클래스 끝점

모든 XDM(Experience Data Model) 스키마는 클래스를 기반으로 해야 합니다. 클래스는 해당 클래스를 기반으로 하는 모든 스키마에 포함해야 하는 공통 속성의 기본 구조와 이러한 스키마에서 사용할 수 있는 스키마 필드 그룹을 결정합니다. 또한 스키마의 클래스는 스키마에 포함할 데이터의 행동 측면을 결정하며, 이 양식은 두 가지 유형이 있습니다.

* **[!UICONTROL 레코드]**:주체의 특성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**:작업 수행 시 레코드 주체가 직접 또는 간접적으로 시스템의 스냅샷을 제공합니다.

>[!NOTE]
>
>스키마 구성에 영향을 주는 방식에 대한 데이터 동작에 대한 자세한 내용은 스키마 구성](../schema/composition.md)의 [기본 사항을 참조하십시오.

[!DNL Schema Registry] API의 `/classes` 종단점을 사용하면 경험 애플리케이션 내의 클래스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 클래스 목록 검색 {#list}

각각 `/global/classes` 또는 `/tenant/classes`에 GET 요청을 수행하여 `global` 또는 `tenant` 컨테이너 아래에 모든 클래스를 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서에서 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 클래스를 검색할 컨테이너:`global`(Adobe 생성 클래스의 경우) 또는 조직이 소유한 클래스의 `tenant`. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록에 대해서는 [부록 document](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `tenant` 컨테이너에서 클래스 목록을 검색하여 `orderby` 쿼리 매개 변수를 사용하여 `title` 속성으로 클래스를 정렬합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 `Accept` 헤더를 목록 클래스에 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 클래스를 반환합니다. (제한:300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용하므로 응답에는 각 클래스에 대한 `title`, `$id`, `meta:altId` 및 `version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 클래스의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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

## 수업을 찾아보세요 {#lookup}

GET 요청 경로에 클래스의 ID를 포함하여 특정 클래스를 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 클래스가 들어 있는 컨테이너:Adobe이 만든 클래스의 `global` 또는 조직이 소유한 클래스의 `tenant`. |
| `{CLASS_ID}` | 조회하려는 클래스의 `meta:altId` 또는 URL로 인코딩된 `$id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 경로에 제공된 `meta:altId` 값으로 클래스를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

성공적인 응답은 클래스의 세부 정보를 반환합니다. 반환되는 필드는 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

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

POST 요청을 수행하여 `tenant` 컨테이너 아래에 사용자 지정 클래스를 정의할 수 있습니다.

>[!IMPORTANT]
>
>정의한 사용자 정의 클래스를 기반으로 스키마를 작성할 때는 표준 필드 그룹을 사용할 수 없습니다. 각 필드 그룹은 `meta:intendedToExtend` 속성에서 호환되는 클래스를 정의합니다. 새 클래스와 호환되는 필드 그룹을 정의하면(필드 그룹의 `meta:intendedToExtend` 필드에서 새 클래스의 `$id` 사용) 정의한 클래스를 구현하는 스키마를 정의할 때마다 해당 필드 그룹을 다시 사용할 수 있습니다. 자세한 내용은 각 끝점 안내서에서 [필드 그룹 만들기](./field-groups.md#create) 및 [스키마 만들기](./schemas.md#create)의 섹션을 참조하십시오.
>
>실시간 고객 프로필의 사용자 지정 클래스를 기반으로 하여 스키마를 사용하려는 경우, 결합 스키마가 동일한 클래스를 공유하는 스키마만 기반으로 구축된다는 점을 명심하십시오. [!UICONTROL XDM 개별 프로필] 또는 [!UICONTROL XDM ExperienceEvent]와 같은 다른 클래스에 대한 사용자 지정 클래스 스키마를 합계에 포함하려면 해당 클래스를 사용하는 다른 스키마와 관계를 설정해야 합니다. 자세한 내용은 API](../tutorials/relationship-api.md)에서 두 스키마 간의 관계 설정 관련 자습서를 참조하십시오.[

**API 형식**

```http
POST /tenant/classes
```

**요청**

클래스 만들기(POST) 요청에는 두 값 중 하나에 `$ref`를 포함하는 `allOf` 속성이 포함되어야 합니다.`https://ns.adobe.com/xdm/data/record` 또는 `https://ns.adobe.com/xdm/data/time-series`. 이러한 값은 클래스가 기반으로 하는 동작(레코드 또는 시계열)을 나타냅니다. 레코드 데이터와 시계열 데이터의 차이점에 대한 자세한 내용은 스키마 구성](../schema/composition.md)의 [기본 사항 내의 동작 유형 섹션을 참조하십시오.

클래스를 정의할 때 클래스 정의 내에 필드 그룹이나 사용자 정의 필드를 포함할 수도 있습니다. 이렇게 하면 추가된 필드 그룹 및 필드가 클래스를 구현하는 모든 스키마에 포함됩니다. 다음 예제 요청에서는 회사가 소유하거나 운영하는 다른 속성에 대한 정보를 캡처하는 &quot;Property&quot;라는 클래스를 정의합니다. 여기에는 클래스를 사용할 때마다 포함할 `propertyId` 필드가 포함되어 있습니다.

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
| `_{TENANT_ID}` | 조직의 `TENANT_ID` 네임스페이스. 조직에서 만든 모든 리소스는 [!DNL Schema Registry]에 있는 다른 리소스와 충돌을 피하려면 이 속성을 포함해야 합니다. |
| `allOf` | 새 클래스에서 속성을 상속할 리소스 목록입니다. 배열 내의 `$ref` 개체 중 하나는 클래스의 동작을 정의합니다. 이 예제에서 클래스는 &quot;record&quot; 동작을 상속합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 클래스의 세부 정보가 포함된 페이로드를 `$id`, `meta:altId` 및 `version`를 반환합니다. 이 세 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 지정됩니다.

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

이제 [에 GET 요청을 수행하면 `tenant` 컨테이너의 모든 클래스](#list)에 속성 클래스가 포함됩니다. [URL로 인코딩된 `$id`을 사용하여 조회(GET) 요청](#lookup)을 수행하여 새 클래스를 직접 볼 수도 있습니다.

## 클래스 업데이트 {#put}

PUT 작업을 통해 전체 클래스를 바꿀 수 있으며, 기본적으로 리소스를 다시 쓸 수 있습니다. PUT 요청을 통해 클래스를 업데이트할 때 본문에는 POST 요청에 새 클래스](#create)를 만들 때 필요한 모든 필드가 포함되어야 합니다.[

>[!NOTE]
>
>클래스의 일부를 완전히 대체하지 않고 업데이트하려는 경우 [클래스의 일부를 업데이트하는 섹션을 참조하십시오](#patch).

**API 형식**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 다시 쓸 클래스의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 클래스를 다시 작성하여 해당 필드 중 하나의 `description` 및 `title`을 변경합니다.

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

PATCH 요청을 사용하여 클래스의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은 `add`, `remove` 및 `replace`를 비롯한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업](#put)을 사용하여 클래스를 바꾸는 섹션을 참조하십시오.

**API 형식**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 업데이트할 클래스의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 기존 클래스의 `description` 및 해당 필드 중 하나의 `title`를 업데이트합니다.

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`)이 포함되어 있으며, (`path`)에서 작업을 수행해야 하는 필드와 해당 작업에 포함해야 하는 정보가 포함됩니다(`value`).

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

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. `description`이(가) `propertyId` 필드의 `title`과(와) 함께 업데이트되었습니다.

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

스키마 레지스트리에서 클래스를 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 클래스 ID를 사용하여 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 삭제할 클래스의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

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

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

클래스에 대해 [조회(GET) 요청](#lookup)을 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 이 클래스가 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
