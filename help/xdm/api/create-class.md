---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 클래스 만들기
description: 스키마의 기본 빌딩 블록은 클래스입니다. 이 클래스에는 스키마의 핵심 데이터를 캡처하기 위해 정의해야 하는 최소 필드 집합이 포함되어 있습니다. 예를 들어, 여러분이 자동차와 트럭용 스키마를 설계하고 있다면, 그들은 모든 자동차의 기본적인 공통 속성을 설명한 Vehicle이라는 클래스를 사용할 것입니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 클래스 만들기

스키마의 기본 빌딩 블록은 클래스입니다. 이 클래스에는 스키마의 핵심 데이터를 캡처하기 위해 정의해야 하는 최소 필드 집합이 포함되어 있습니다. 예를 들어, 여러분이 자동차와 트럭용 스키마를 설계하고 있다면, 그들은 모든 자동차의 기본적인 공통 속성을 설명한 Vehicle이라는 클래스를 사용할 것입니다.

Adobe 및 기타 [!DNL Experience Platform] 파트너가 제공하는 표준 클래스는 몇 가지가 있지만, 고유한 클래스를 정의하고 클래스에 저장할 수도 있습니다 [!DNL Schema Registry]. 그런 다음 만든 클래스를 구현하는 스키마를 구성하고 새로 정의된 클래스와 호환되는 혼합을 정의할 수 있습니다.

>[!NOTE]
>
>정의한 클래스를 기반으로 스키마를 작성할 때 표준 믹스를 사용할 수 없습니다. 각 혼합은 특성이 서로 호환되는 클래스를 `meta:intendedToExtend` 정의합니다. 새 클래스와 호환되는 혼합을 정의하고 나면(믹신 `$id` `meta:intendedToExtend` 필드에 새 클래스의 조합을 사용) 정의된 클래스를 구현하는 스키마를 정의할 때마다 이러한 혼합을 재사용할 수 있습니다. 자세한 내용은 믹싱 [생성](create-mixin.md) 및 스키마 [를 만드는](create-schema.md) 섹션을 참조하십시오.

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

테넌트 컨테이너의 모든 클래스를 나열하기 위한 GET 요청을 수행하면 이제 속성 클래스가 포함됩니다. 또한 URL 인코딩 URI를 사용하여 조회(GET) `$id` 요청을 수행하여 새 클래스를 직접 볼 수도 있습니다. 조회 요청을 수행할 때 수락 헤더 `version` 에 해당 코드를 포함해야 합니다.
