---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 클래스 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba

---


# 클래스 만들기

스키마의 기본 빌딩 블록은 클래스입니다. 이 클래스에는 스키마의 핵심 데이터를 캡처하기 위해 정의해야 하는 최소 필드 집합이 포함되어 있습니다. 예를 들어 자동차와 트럭용 스키마를 디자인하는 경우 모든 차량의 기본 공통 속성을 설명하는 Vehicle이라는 클래스를 사용할 수 있습니다.

Adobe와 기타 Experience Platform 파트너가 제공하는 여러 개의 표준 클래스가 있지만, 고유한 클래스를 정의하여 스키마 레지스트리에 저장할 수도 있습니다. 그런 다음 만든 클래스를 구현하는 스키마를 구성하고 새로 정의된 클래스와 호환되는 혼합을 정의할 수 있습니다.

>[!NOTE] 정의한 클래스를 기반으로 스키마를 작성할 때 표준 혼합을 사용할 수 없습니다. 각 혼합은 해당 `meta:intendedToExtend` 특성과 호환되는 클래스를 정의합니다. 새 클래스와 호환되는 혼합을 정의하고 나면(믹스의 `$id` `meta:intendedToExtend` 필드에 새 클래스의 사용) 정의한 클래스를 구현하는 스키마를 정의할 때마다 이러한 혼합을 다시 사용할 수 있습니다. 자세한 내용은 믹싱 [생성](create-mixin.md) 및 스키마 [](create-schema.md) 만들기에 대한 섹션을 참조하십시오.

**API 형식**

```http
POST /tenant/classes
```

**요청**

클래스를 만들기 위한 요청(POST)에는 두 값 중 `allOf` `$ref` 하나를 포함하는 속성이 포함되어야 합니다. `https://ns.adobe.com/xdm/data/record` 또는 `https://ns.adobe.com/xdm/data/time-series`. 이러한 값은 클래스가 기반으로 하는 비헤이비어를 나타냅니다(각각 레코드 또는 시계열). 레코드 데이터와 시간 시리즈 데이터 간의 차이에 대한 자세한 내용은 스키마 컴포지션의 [기본 사항](../schema/composition.md)내에서 동작 유형에 대한 섹션을 참조하십시오.

클래스를 정의할 때 클래스 정의 내에 혼합이나 사용자 정의 필드를 포함할 수도 있습니다. 이로 인해 추가된 믹스와 필드가 클래스를 구현하는 모든 스키마에 포함됩니다. 다음 예제 요청은 회사가 소유하거나 운영하는 다른 속성에 대한 정보를 캡처하는 &quot;Property&quot;라는 클래스를 정의합니다. 여기에는 클래스가 사용될 때마다 포함할 `propertyId` 필드가 포함되어 있습니다.

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
| `_{TENANT_ID}` | 조직의 `TENANT_ID` 네임스페이스입니다. 조직에서 만든 모든 리소스에 이 속성이 포함되어야 스키마 레지스트리에 있는 다른 리소스와 충돌하지 않습니다. |
| `allOf` | 새 클래스에서 속성을 상속할 리소스의 목록입니다. 배열 내의 `$ref` 객체 중 하나는 클래스의 동작을 정의합니다. 이 예제에서 클래스는 &quot;record&quot; 비헤이비어를 상속합니다. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 클래스, `$id``meta:altId`및 `version`등의 세부 정보가 포함된 페이로드를 반환합니다. 이 세 개의 값은 읽기 전용이며 스키마 레지스트리에 지정됩니다.

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

테넌트 컨테이너의 모든 클래스를 나열하기 위한 GET 요청을 수행하면 이제 속성 클래스가 포함됩니다. URL 인코딩 URI를 사용하여 조회(GET) 요청을 수행하여 새 클래스를 직접 볼 `$id` 수도 있습니다. 조회 요청을 수행할 때 수락 `version` 헤더에 를 포함해야 합니다.
