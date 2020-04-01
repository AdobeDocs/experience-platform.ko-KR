---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 임시 스키마 만들기
topic: tutorials
translation-type: tm+mt
source-git-commit: 956d1e5b4a994c9ea52d818f3dd6d3ff88cb16b6

---


# 임시 스키마 만들기

특정 상황에서 단일 데이터 세트에서만 사용하도록 지정된 필드가 있는 XDM(경험 데이터 모델) 스키마를 만들어야 할 수 있습니다. 이를 &quot;임시&quot; 스키마라고 합니다. 애드혹 스키마는 CSV 파일 인제스트 및 특정 종류의 소스 연결 만들기를 포함하여, 경험 플랫폼의 다양한 데이터 통합 워크플로우에 사용됩니다.

이 문서에서는 스키마 레지스트리 API를 사용하여 임시 스키마를 만드는 일반적인 [단계를 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Adobe Experience Platform 튜토리얼과 함께 사용하기 위해 마련된 Adobe Experience Platform(임시 스키마)을 워크플로우의 일부로 만들어야 합니다. 이러한 각 문서는 특정 사용 사례에 대해 임시 스키마를 제대로 구성하는 방법에 대한 자세한 정보를 제공합니다.

## 시작하기

이 자습서에서는 XDM(Experience Data Model) 시스템에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 XDM 설명서를 참조하십시오.

- [XDM 시스템 개요](../home.md):XDM 및 Experience Platform의 구현에 대한 개요
- [스키마 컴포지션의](../schema/composition.md)기본 사항:XDM 스키마의 기본 구성 요소에 대한 개요입니다.

이 자습서를 시작하기 전에 스키마 레지스트리 API를 성공적으로 호출하려면 [개발자 안내서를](../api/getting-started.md) 참조하십시오. 여기에는 사용자 `{TENANT_ID}`및 &quot;컨테이너&quot;의 개념, 요청을 수행하는 데 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).

## 애드혹 클래스 만들기

XDM 스키마의 데이터 동작은 기본 클래스에 의해 결정됩니다. 임시 스키마를 만드는 첫 번째 단계는 `adhoc` 동작을 기반으로 클래스를 만드는 것입니다. 이 작업은 `/tenant/classes` 끝점에 POST 요청을 수행하여 수행됩니다.

**API 형식**

```http
POST /tenant/classes
```

**요청**

다음 요청은 페이로드에 제공된 속성으로 구성된 새 XDM 클래스를 만듭니다. 이 클래스는 `$ref` 배열에 속성 세트를 `https://ns.adobe.com/xdm/data/adhoc` 제공하여 동작을 상속합니다 `allOf` `adhoc` . 또한 이 요청에는 클래스의 사용자 정의 필드가 포함된 `_adhoc` 개체가 정의되어 있습니다.

>[!NOTE] 에 정의된 사용자 정의 필드는 임시 스키마의 사용 사례에 따라 `_adhoc` 다릅니다. 사용 사례에 따라 필요한 사용자 정의 필드에 대해서는 해당 자습서의 특정 워크플로우를 참조하십시오.

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
| `$ref` | 새 클래스에 대한 데이터 동작입니다. 애드혹 클래스의 경우 이 값을 로 설정해야 합니다 `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | 필드 이름 및 데이터 유형의 키-값 쌍으로 표현되는 클래스의 사용자 정의 필드를 포함하는 객체입니다. |

**응답**

성공적인 응답은 새 클래스의 세부 사항을 반환하고, `properties._adhoc` 개체의 이름을 시스템에 의해 생성된 읽기 전용 고유 식별자인 GUID로 바꿉니다. 이 `meta:datasetNamespace` 속성은 자동으로 생성되어 응답에 포함됩니다.

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

애드혹 클래스를 만든 후에는 `/tenant/schemas` 종단점에 POST 요청을 수행하여 해당 클래스를 구현하는 새 스키마를 만들 수 있습니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 요청은 새 스키마를 만들어 페이로드에서 이전에 만든 애드혹 클래스의 참조(`$ref`) `$id` 를 제공합니다.

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

성공적인 응답은 시스템 생성, 읽기 전용 등 새로 생성된 스키마의 세부 사항을 반환합니다 `$id`.

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

>[!NOTE] 이 단계는 선택 사항입니다. 임시 스키마의 필드 구조를 검사하지 않으려면 이 자습서의 끝 부분에 있는 [다음 단계](#next-steps) 섹션으로 건너뛸 수 있습니다.

애드혹 스키마가 생성되면 GET(조회) 요청을 만들어 확장된 형식으로 스키마를 볼 수 있습니다. 이 작업은 아래에 설명된 대로 GET 요청에서 적절한 수락 헤더를 사용하여 수행됩니다.

**API 형식**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 액세스하려는 URL 인코딩 `$id` URI 또는 `meta:altId` 임시 스키마의 URL |

**요청**

다음 요청에서는 스키마의 확장된 양식을 반환하는 수락 헤더를 `application/vnd.adobe.xed-full+json; version=1`사용합니다. 스키마 레지스트리에서 특정 리소스를 검색할 때 요청의 수락 헤더에 해당 리소스의 주 버전이 포함되어야 합니다.

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

성공적인 응답은 아래 중첩된 모든 필드를 포함하여 스키마의 세부 사항을 `properties`반환합니다.

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

이 자습서를 따라 새 임시 스키마를 만들었습니다. 이 문서를 다른 자습서의 일부로 가져온 경우 이제 임시 `$id` 스키마의 기능을 사용하여 지시에 따라 워크플로우를 완료할 수 있습니다.

스키마 레지스트리 API 작업에 대한 자세한 내용은 [개발자 안내서를](../api/getting-started.md)참조하십시오.