---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;클래스 레지스트리;스키마 레지스트리;클래스;클래스;클래스;클래스;클래스;클래스;클래스;클래스;생성
solution: Experience Platform
title: 클래스 API 끝점
description: 스키마 레지스트리 API의 /classes 종단점을 사용하면 경험 애플리케이션 내에서 XDM 클래스를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 3%

---

# 클래스 끝점

모든 XDM(Experience Data Model) 스키마는 클래스를 기반으로 해야 합니다. 클래스는 해당 클래스를 기반으로 하는 모든 스키마에 포함해야 하는 공통 속성의 기본 구조와 이러한 스키마에서 사용할 수 있는 스키마 필드 그룹을 결정합니다. 또한 스키마의 클래스는 스키마에 포함할 데이터의 행동 측면을 결정하며, 이 양식은 두 가지 유형이 있습니다.

* **[!UICONTROL 레코드]**: 주체의 특성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**: 작업 수행 시 레코드 주체가 직접 또는 간접적으로 시스템의 스냅샷을 제공합니다.

>[!NOTE]
>
>스키마 구성에 영향을 주는 방식에 대한 데이터 동작에 대한 자세한 내용은 [스키마 구성 기본 사항](../schema/composition.md).

다음 `/classes` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 경험 애플리케이션 내의 클래스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 클래스 목록 검색 {#list}

모든 클래스를 `global` 또는 `tenant` 컨테이너에 GET 요청 `/global/classes` 또는 `/tenant/classes`각각 입니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 의 섹션을 참조하십시오. [쿼리 매개 변수](./appendix.md#query) 자세한 내용은 부록 문서에서 확인하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 클래스를 검색할 컨테이너: `global` Adobe에서 만든 클래스 또는 `tenant` 을 입력합니다. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [부록 문서](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `tenant` 컨테이너, `orderby` 쿼리 매개 변수를 사용하여 클래스 정렬 `title` 속성을 사용합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 다음 `Accept` 목록 클래스에 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 클래스 반환 `$ref` 및 `allOf` 포함됩니다. (제한: 300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서는 `application/vnd.adobe.xed-id+json` `Accept` 헤더. 따라서 응답에는 `title`, `$id`, `meta:altId`, 및 `version` 각 클래스에 대한 속성입니다. 다른 `Accept` 헤더 (`application/vnd.adobe.xed+json`)은 각 클래스의 모든 특성을 반환합니다. 적절한 `Accept` 헤더에서 사용할 수 있습니다.

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
| `{CONTAINER_ID}` | 검색할 클래스가 들어 있는 컨테이너: `global` Adobe에서 만든 클래스 또는 `tenant` 해당 조직이 소유한 클래스입니다. |
| `{CLASS_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 네가 찾아보고 싶은 수업들 말이야 |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 클래스를 `meta:altId` 경로에 제공된 값입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 모든 조회 요청에는 `version` 에 포함됨 `Accept` 헤더. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 원시 `$ref` 및 `allOf`에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 및 `allOf` 해결됨, 에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | 원시 `$ref` 및 `allOf`, 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 및 `allOf` 해결됨, 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 및 `allOf` 해결된 설명자가 포함되어 있습니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 클래스의 세부 정보를 반환합니다. 반환되는 필드는 `Accept` 헤더가 전송되었습니다. 다양한 실험 `Accept` 헤더를 사용하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

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

사용자 지정 클래스는 `tenant` POST 요청을 수행하여 컨테이너.

>[!IMPORTANT]
>
>정의한 사용자 정의 클래스를 기반으로 스키마를 작성할 때는 표준 필드 그룹을 사용할 수 없습니다. 각 필드 그룹은 해당 필드에서 호환되는 클래스를 정의합니다 `meta:intendedToExtend` 속성을 사용합니다. 새 클래스와 호환되는 필드 그룹을 정의했으면 `$id` 새 학급의 `meta:intendedToExtend` 필드 그룹의 필드)에서는 정의한 클래스를 구현하는 스키마를 정의할 때마다 해당 필드 그룹을 다시 사용할 수 있습니다. 의 섹션을 참조하십시오. [필드 그룹 만들기](./field-groups.md#create) 및 [스키마 만들기](./schemas.md#create) 를 참조하십시오.
>
>실시간 고객 프로필의 사용자 지정 클래스를 기반으로 하여 스키마를 사용하려는 경우, 결합 스키마가 동일한 클래스를 공유하는 스키마만 기반으로 구축된다는 점을 명심하십시오. 같은 다른 클래스에 대해 공용 구조체에 사용자 지정 클래스 스키마를 포함하려는 경우 [!UICONTROL XDM 개별 프로필] 또는 [!UICONTROL XDM ExperienceEvent]를 채울 때는 해당 클래스를 사용하는 다른 스키마와 관계를 설정해야 합니다. 다음에서 자습서를 참조하십시오. [api에서 두 스키마 간의 관계 설정](../tutorials/relationship-api.md) 추가 정보.

**API 형식**

```http
POST /tenant/classes
```

**요청**

클래스를 만드는(POST) 요청에는 `allOf` 를 포함하는 속성 `$ref` 다음 두 값 중 하나를 선택합니다. `https://ns.adobe.com/xdm/data/record` 또는 `https://ns.adobe.com/xdm/data/time-series`. 이러한 값은 클래스가 기반으로 하는 동작(레코드 또는 시계열)을 나타냅니다. 레코드 데이터와 시계열 데이터 간의 차이에 대한 자세한 내용은 [스키마 구성 기본 사항](../schema/composition.md).

클래스를 정의할 때 클래스 정의 내에 필드 그룹이나 사용자 정의 필드를 포함할 수도 있습니다. 이렇게 하면 추가된 필드 그룹 및 필드가 클래스를 구현하는 모든 스키마에 포함됩니다. 다음 예제 요청에서는 회사가 소유하거나 운영하는 다른 속성에 대한 정보를 캡처하는 &quot;Property&quot;라는 클래스를 정의합니다. 여기에는 다음이 포함됩니다 `propertyId` 클래스를 사용할 때마다 포함할 필드입니다.

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
| `_{TENANT_ID}` | 다음 `TENANT_ID` 조직의 네임스페이스. 조직에서 만든 모든 리소스에는 [!DNL Schema Registry]. |
| `allOf` | 새 클래스에서 속성을 상속할 리소스 목록입니다. 다음 중 하나 `$ref` 배열 내의 개체는 클래스의 동작을 정의합니다. 이 예제에서 클래스는 &quot;record&quot; 동작을 상속합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 HTTP 상태 201(Created)을 반환하고, `$id`, `meta:altId`, 및 `version`. 이 세 값은 읽기 전용이며 [!DNL Schema Registry].

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

에 GET 요청 수행 [모든 클래스 나열](#list) 에서 `tenant` 컨테이너에는 이제 속성 클래스가 포함됩니다. 다음을 수행할 수도 있습니다 [조회(GET) 요청 수행](#lookup) url로 인코딩된 `$id` 새 클래스를 직접 보려면

## 클래스 업데이트 {#put}

PUT 작업을 통해 전체 클래스를 바꿀 수 있으며, 기본적으로 리소스를 다시 쓸 수 있습니다. PUT 요청을 통해 클래스를 업데이트할 때는 본문에는 [새 클래스 만들기](#create) POST 요청.

>[!NOTE]
>
>클래스의 일부를 완전히 대체하지 않고 업데이트하려는 경우 [클래스의 일부 업데이트](#patch).

**API 형식**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 다시 쓰려는 클래스의 |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 클래스를 다시 작성하여 해당 클래스를 변경합니다 `description` 그리고 `title` 그 분야 중 하나.

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

PATCH 요청을 사용하여 클래스의 일부를 업데이트할 수 있습니다. 다음 [!DNL Schema Registry] 는 다음을 포함한 모든 표준 JSON 패치 작업을 지원합니다 `add`, `remove`, 및 `replace`. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업을 사용하여 클래스 바꾸기](#put).

**API 형식**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 업데이트하려는 클래스의 |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 를 업데이트합니다 `description` 기존 클래스 및 `title` 그 분야 중 하나.

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 객체에는 수행할 작업이 포함됩니다(`op`)에서 작업을 수행해야 하는 필드(`path`) 및 해당 작업에 포함해야 하는 정보(`value`).

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

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. 다음 `description` 과 함께 가 업데이트되었습니다. `title` 의 `propertyId` 필드.

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

스키마 레지스트리에서 클래스를 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 클래스 ID를 사용하여 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 삭제할 클래스 |

{style=&quot;table-layout:auto&quot;}

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

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

다음을 수행하여 삭제를 확인할 수 있습니다 [조회(GET) 요청](#lookup) Analytics Premium을 사용할 수 있습니다. 다음을 포함해야 합니다 `Accept` 헤더를 반환하지만 해당 클래스가 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
