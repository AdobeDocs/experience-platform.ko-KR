---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;ad-hoc;ad hoc;ad hoc;ad hoc;Ad hoc;Adhoc;자습서;자습서;만들기;만들기;스키마;스키마
solution: Experience Platform
title: 임시 스키마 만들기
description: 특정 상황에서 단일 데이터 세트에서만 사용할 수 있도록 네임스페이스가 지정된 필드가 있는 XDM(Experience Data Model) 스키마를 만들어야 할 수 있습니다. 이를 "임시" 스키마라고 합니다. 임시 스키마는 CSV 파일 수집 및 특정 종류의 소스 연결 생성 등 Experience Platform을 위한 다양한 데이터 수집 워크플로우에서 사용됩니다.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# 임시 스키마 만들기

특정 상황에서는 단일 데이터 집합에서만 사용할 수 있도록 네임스페이스가 지정된 필드가 있는 [!DNL Experience Data Model] (XDM) 스키마를 만들어야 할 수 있습니다. 이를 &quot;임시&quot; 스키마라고 합니다. 임시 스키마는 CSV 파일 수집 및 특정 종류의 소스 연결 생성을 포함하여 [!DNL Experience Platform]의 다양한 데이터 수집 워크플로우에서 사용됩니다.

이 문서에서는 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)를 사용하여 임시 스키마를 만드는 일반적인 단계를 제공합니다. 임시 스키마를 워크플로의 일부로 만들어야 하는 다른 [!DNL Experience Platform] 튜토리얼과 함께 사용됩니다. 이러한 각 문서에서는 특정 사용 사례에 맞게 임시 스키마를 올바르게 구성하는 방법에 대한 자세한 정보를 제공합니다.

## 시작하기

이 자습서에서는 [!DNL Experience Data Model] (XDM) 시스템에 대한 작업 이해가 필요합니다. 이 자습서를 시작하기 전에 다음 XDM 설명서를 검토하십시오.

- [XDM 시스템 개요](../home.md): [!DNL Experience Platform]의 XDM 및 해당 구현에 대한 높은 수준의 개요입니다.
- [스키마 컴포지션의 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소에 대한 개요입니다.

이 자습서를 시작하기 전에 [개발자 안내서](../api/getting-started.md)에서 [!DNL Schema Registry] API를 성공적으로 호출하기 위해 알아야 할 중요한 정보를 검토하십시오. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청을 하는 데 필요한 헤더가 포함됩니다(Accept 헤더 및 가능한 값에 특별한 주의를 기울임).

## 임시 클래스 만들기

XDM 스키마의 데이터 동작은 기본 클래스에 의해 결정됩니다. 임시 스키마를 만드는 첫 번째 단계는 `adhoc` 동작을 기반으로 클래스를 만드는 것입니다. 이 작업은 `/tenant/classes` 끝점에 대한 POST 요청을 통해 수행됩니다.

**API 형식**

```http
POST /tenant/classes
```

**요청**

다음 요청은 페이로드에 제공된 특성으로 구성된 새 XDM 클래스를 만듭니다. `allOf` 배열에서 `https://ns.adobe.com/xdm/data/adhoc`(으)로 설정된 `$ref` 속성을 제공하면 이 클래스는 `adhoc` 동작을 상속합니다. 이 요청은 클래스에 대한 사용자 지정 필드가 포함된 `_adhoc` 개체도 정의합니다.

>[!NOTE]
>
>`_adhoc`에 정의된 사용자 지정 필드는 임시 스키마의 사용 사례에 따라 다릅니다. 사용 사례에 따라 필요한 사용자 정의 필드에 대해서는 해당 자습서의 특정 워크플로우를 참조하십시오.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `$ref` | 새 클래스의 데이터 비헤이비어입니다. 임시 클래스의 경우 이 값을 `https://ns.adobe.com/xdm/data/adhoc`(으)로 설정해야 합니다. |
| `properties._adhoc` | 필드 이름과 데이터 형식의 키-값 쌍으로 표현되는 클래스에 대한 사용자 지정 필드를 포함하는 개체입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새 클래스의 세부 정보를 반환하며 `properties._adhoc` 개체의 이름을 클래스에 대한 시스템 생성 읽기 전용 고유 식별자인 GUID로 바꿉니다. `meta:datasetNamespace` 특성도 자동으로 생성되고 응답에 포함됩니다.

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
    "imsOrg": "{ORG_ID}",
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
| `$id` | 새 임시 클래스에 대해 시스템에서 생성한 읽기 전용 고유 식별자 역할을 하는 URI입니다. 이 값은 다음 임시 스키마 생성 단계에서 사용됩니다. |

{style="table-layout:auto"}

## 임시 스키마 만들기

임시 클래스를 만든 후에는 `/tenant/schemas` 끝점에 대한 POST 요청을 수행하여 해당 클래스를 구현하는 새 스키마를 만들 수 있습니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 요청은 페이로드에서 이전에 만든 임시 클래스의 `$id`에 대한 참조(`$ref`)를 제공하는 새 스키마를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 응답은 새로 만든 스키마의 세부 정보를 반환합니다(시스템 생성, 읽기 전용 `$id` 포함).

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
    "imsOrg": "{ORG_ID}",
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
>조건을 추가합니다. 임시 스키마의 필드 구조를 검사하지 않으려면 이 자습서를 마친 후 [다음 단계](#next-steps) 섹션으로 건너뛸 수 있습니다.

임시 스키마가 만들어지면 조회(GET) 요청을 만들어 확장된 형식으로 스키마를 볼 수 있습니다. 이 작업은 아래 표시된 대로 GET 요청에서 적절한 Accept 헤더를 사용하여 수행됩니다.

**API 형식**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 액세스할 임시 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 확장된 스키마 형식을 반환하는 Accept 헤더 `application/vnd.adobe.xed-full+json; version=1`을(를) 사용합니다. [!DNL Schema Registry]에서 특정 리소스를 검색할 때 요청의 Accept 헤더에 해당 리소스의 주 버전이 포함되어야 합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답이 성공하면 `properties` 아래에 중첩된 모든 필드를 포함하여 스키마의 세부 정보가 반환됩니다.

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
    "imsOrg": "{ORG_ID}",
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

이 자습서에 따라 새 임시 스키마를 만들었습니다. 다른 자습서의 일부로 이 문서를 가져온 경우 이제 임시 스키마의 `$id`을(를) 사용하여 지시된 대로 워크플로우를 완료할 수 있습니다.

[!DNL Schema Registry] API 작업에 대한 자세한 내용은 [개발자 안내서](../api/getting-started.md)를 참조하십시오.
