---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;ad-hoc;ad hoc;adhoc;Ad-hoc;Ad hoc;Adhoc;tutorial;Tutorial;create;Create;schema;Schema
solution: Experience Platform
title: 임시 스키마 만들기
description: 특정 상황에서 단일 데이터 세트에 의해서만 사용하도록 지정된 필드가 있는 XDM(경험 데이터 모델) 스키마를 만들어야 할 수 있습니다. 이를 "임시" 스키마라고 합니다. 애드혹 스키마는 CSV 파일 인제스트 및 특정 종류의 소스 연결 만들기를 포함하여 Experience Platform에 대한 다양한 데이터 처리 워크플로우에서 사용됩니다.
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---


# 임시 스키마 만들기

특정 상황에서 단일 데이터 세트에 의해서만 사용하도록 지정된 필드가 있는 [!DNL Experience Data Model] (XDM) 스키마를 만들어야 할 수 있습니다. 이를 &quot;임시&quot; 스키마라고 합니다. 애드혹 스키마는 CSV 파일 인제스트 및 특정 종류의 소스 연결 만들기를 [!DNL Experience Platform]포함하여 다양한 데이터 처리 워크플로우에서 사용됩니다.

이 문서에서는 스키마 레지스트리 API를 사용하여 임시 스키마를 만드는 일반적인 [단계를 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). 이 도구는 작업 과정의 일부로 임시 스키마를 만들어야 하는 다른 [!DNL Experience Platform] 자습서와 함께 사용됩니다. 이러한 각 문서는 특정 사용 사례에 대해 임시 스키마를 제대로 구성하는 방법에 대한 자세한 정보를 제공합니다.

## 시작하기

이 자습서에서는 [!DNL Experience Data Model] (XDM) 시스템에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 XDM 설명서를 검토하십시오.

- [XDM 시스템 개요](../home.md):XDM 및 XDM 구현에 대한 개요 [!DNL Experience Platform].
- [스키마 컴포지션의 기본 사항](../schema/composition.md):XDM 스키마의 기본 구성 요소에 대한 개요입니다.

이 자습서를 시작하기 전에 [개발자 가이드에서](../api/getting-started.md) API를 성공적으로 호출하기 위해 알아야 할 중요한 정보가 있는지 [!DNL Schema Registry] 확인하십시오. 여기에는 사용자 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청 시 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).

## 애드혹 클래스 만들기

XDM 스키마의 데이터 동작은 기본 클래스에 의해 결정됩니다. 임시 스키마를 만드는 첫 번째 단계는 동작을 기반으로 클래스를 만드는 `adhoc` 것입니다. 이것은 종단점에 POST 요청을 함으로써 `/tenant/classes` 수행됩니다.

**API 형식**

```http
POST /tenant/classes
```

**요청**

다음 요청은 페이로드에서 제공된 속성으로 구성된 새 XDM 클래스를 만듭니다. 배열 `$ref` 에 속성 `https://ns.adobe.com/xdm/data/adhoc` 을 제공하면 이 `allOf` 클래스는 `adhoc` 비헤이비어를 상속합니다. 또한 이 요청은 클래스에 대한 사용자 정의 필드가 포함된 `_adhoc` 개체를 정의합니다.

>[!NOTE]
>
>에 정의된 사용자 정의 필드는 `_adhoc` 임시 스키마의 사용 사례에 따라 다릅니다. 사용 사례에 따라 필요한 사용자 정의 필드에 대해서는 해당 자습서의 특정 워크플로우를 참조하십시오.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `$ref` | 새 클래스에 대한 데이터 동작입니다. 임시 클래스의 경우 이 값을 로 설정해야 합니다 `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | 필드 이름과 데이터 형식의 키 값 쌍으로 표현되는 클래스에 대한 사용자 정의 필드가 포함된 개체입니다. |

**응답**

성공적인 응답은 `properties._adhoc` 개체의 이름을 클래스에 대한 시스템에서 생성된 읽기 전용 고유 식별자인 GUID로 대체하여 새 클래스의 세부 사항을 반환합니다. 이 `meta:datasetNamespace` 속성은 자동으로 생성되어 응답에 포함됩니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `$id` | 시스템이 새 애드혹 클래스에 대해 생성된 읽기 전용 고유 식별자를 제공하는 URI입니다. 이 값은 임시 스키마를 만드는 다음 단계에서 사용됩니다. |

## 임시 스키마 만들기

애드혹 클래스를 만든 후에는 종단점에 POST 요청을 수행하여 해당 클래스를 구현하는 새 스키마를 만들 수 `/tenant/schemas` 있습니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 요청은 새 스키마를 만들어 페이로드에서 이전에 만든`$ref`애드혹 클래스 `$id` 의 참조에 제공합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**응답**

성공적인 응답은 시스템에서 생성된 읽기 전용 등 새로 생성된 스키마의 세부 사항을 반환합니다 `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## 전체 임시 스키마 보기

>[!NOTE]
>
>조건을 추가합니다. 임시 스키마의 필드 구조를 검사하지 않으려는 경우 이 자습서의 끝에 있는 [다음 단계](#next-steps) 섹션으로 건너뛸 수 있습니다.

임시 스키마가 생성되면 조회(GET) 요청을 만들어 확장 형식으로 스키마를 볼 수 있습니다. 이 작업은 아래에 설명된 대로 GET 요청에 적절한 수락 헤더를 사용하여 수행됩니다.

**API 형식**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 액세스하려는 임시 스키마의 URL 인코딩 `$id` URI `meta:altId` 또는 URL입니다. |

**요청**

다음 요청에서는 스키마의 확장된 양식을 반환하는 수락 헤더 `application/vnd.adobe.xed-full+json; version=1`를 사용합니다. 요청에서 특정 리소스를 검색할 때 요청 [!DNL Schema Registry]의 수락 헤더에 해당 리소스의 주요 버전이 포함되어야 합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 아래 중첩된 모든 필드를 포함하여 스키마의 세부 사항을 반환합니다 `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## 다음 단계 {#next-steps}

이 튜토리얼을 따라 새 임시 스키마를 만들었습니다. 이 문서를 다른 자습서의 일부로 가져온 경우, 이제 임시 스키마 `$id` 를 사용하여 지정된 대로 워크플로우를 완료할 수 있습니다.

API 작업에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 [안내서를 참조하십시오](../api/getting-started.md).