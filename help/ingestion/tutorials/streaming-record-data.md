---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스트리밍 레코드 데이터
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a371aab5435bac97f714e5cf96a93adf4aa0303
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 2%

---


# Adobe Experience Platform으로 레코드 데이터 스트리밍

이 자습서는 Adobe Experience Platform 데이터 통합 서비스 API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 됩니다.

## 시작하기

이 자습서에서는 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [XDM(Experience Data Model)](../../xdm/home.md): Platform이 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [실시간 고객 프로필](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.
- [스키마 레지스트리 개발자 가이드](../../xdm/api/getting-started.md): 스키마 레지스트리 API의 사용 가능한 각 끝점과 이러한 끝점에 대한 호출 방법을 다루는 포괄적인 안내서입니다. 여기에는 이 자습서 전체의 호출에 표시되는 사용자 `{TENANT_ID}`를 아는 것과 수렴을 위한 데이터 세트를 만드는 데 사용되는 스키마를 만드는 방법을 아는 것이 포함됩니다.

또한 이 자습서에서는 스트리밍 연결을 이미 만들어야 합니다. 스트리밍 연결 만들기에 대한 자세한 내용은 스트리밍 연결 [만들기 자습서를 참조하십시오](./create-streaming-connection.md).

다음 섹션에서는 스트리밍 통합 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

Platform API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: 무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## XDM 개별 프로필 클래스를 기반으로 스키마 작성

데이터 세트를 만들려면 먼저 XDM 개별 프로필 클래스를 구현하는 새 스키마를 만들어야 합니다. 스키마 생성 방법에 대한 자세한 내용은 스키마 [레지스트리 API 개발자 안내서를 참조하십시오](../../xdm/api/getting-started.md).

**API 형식**

```http
POST /schemaregistry/tenant/schemas
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `title` | 스키마에 사용할 이름입니다. 이 이름은 고유해야 합니다. |
| `description` | 만들고 있는 스키마에 대한 의미 있는 설명입니다. |
| `meta:immutableTags` | 이 예에서, `union` 태그는 데이터를 [실시간 고객 프로파일에 유지하는 데 사용됩니다](../../profile/home.md). |

**응답**

성공적인 응답은 새로 만든 스키마의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{TENANT_ID}` | 이 ID는 사용자가 만든 리소스가 IMS 조직 내에 올바르게 지정되고 포함되어 있는지 확인하는 데 사용됩니다. 테넌트 ID에 대한 자세한 내용은 [스키마 레지스트리 안내서를 참조하십시오](../../xdm/api/getting-started.md#know-your-tenant-id). |

데이터 세트 `$id` 를 만들 때 이 두 가지 모두 사용되므로 속성 `version` 및 특성을 참고하시기 바랍니다.

## 스키마에 대한 기본 ID 설명자 설정

그런 다음 작업 이메일 주소 속성을 기본 식별자로 사용하여 위에 만든 스키마에 [ID 설명자를](../../xdm/api/descriptors.md) 추가합니다. 이렇게 하면 두 가지 변경 사항이 발생합니다.

1. 회사 이메일 주소는 필수 필드가 됩니다. 즉, 이 필드 없이 보낸 메시지는 유효성 검사에 실패하며 인제스트되지 않습니다.

2. 실시간 고객 프로필은 회사 이메일 주소를 식별자로 사용하여 해당 개인에 대한 더 많은 정보를 연결하는 데 도움이 됩니다.

### 요청

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | 스키마를 작성할 때 이전에 받은 `$id` 내용입니다. 다음과 같이 표시되어야 합니다. `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B; ID 네임스페이스 코드&#x200B;****
>
> 코드가 유효한지 확인하십시오. 위의 예에서는 표준 ID 네임스페이스인 &quot;email&quot;을 사용합니다. 일반적으로 사용되는 기타 표준 ID 네임스페이스는 [Identity Service FAQ에서 찾을 수 있습니다](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 사용자 지정 네임스페이스를 만들려면 [ID 네임스페이스 개요에 설명된 단계를 따릅니다](../../identity-service/home.md).

**응답**

성공적인 응답은 스키마에 대해 새로 생성된 기본 ID 설명자에 대한 정보가 포함된 HTTP 상태 201을 반환합니다.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## 레코드 데이터를 위한 데이터 집합 만들기

스키마를 만들었으면 데이터 세트를 만들어 레코드 데이터를 인제스트해야 합니다.

>[!NOTE]
>
>이 데이터 세트는 **실시간 고객 프로필** 및 **ID 서비스에 대해 활성화됩니다**.

**API 형식**

```http
POST /catalog/dataSets
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**응답**

성공적인 응답은 HTTP 상태 201을 반환하고 새로 만든 데이터 집합의 ID가 포함된 배열을 형식으로 반환합니다 `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 스트리밍 연결에 레코드 데이터 인제스트

데이터 세트 및 스트리밍 연결을 통해 XDM 형식의 JSON 레코드를 인제스트하여 기록 데이터를 Platform에 인제스트할 수 있습니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |
| `synchronousValidation` | 개발 용도로 사용할 선택적 쿼리 매개 변수입니다. 로 설정된 `true`경우 즉시 피드백에 사용하여 요청이 성공적으로 전송되었는지 확인할 수 있습니다. 기본적으로 이 값은 로 설정됩니다 `false`. |

**요청**

>[!NOTE]
>
>다음 API 호출에는 인증 헤더가 필요하지 **않습니다** .

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

**응답**

성공적인 응답은 새로 스트리밍된 프로필에 대한 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 ID입니다. |
| `xactionId` | 방금 보낸 레코드에 대해 서버측에서 생성된 고유한 식별자입니다. 이 ID는 Adobe가 다양한 시스템과 디버깅을 통해 이 기록의 라이프사이클을 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청을 받은 시간을 표시하는 타임스탬프(밀리초 단위) |
| `synchronousValidation.status` | 쿼리 매개 변수가 `synchronousValidation=true` 추가되었으므로 이 값이 나타납니다. 유효성 검사에 성공하면 상태가 됩니다 `pass`. |

## 새로 인제스트한 레코드 데이터 검색

이전에 인제스트한 레코드의 유효성을 확인하려면 프로필 액세스 API를 [사용하여](../../profile/api/entities.md) 레코드 데이터를 검색할 수 있습니다.

>[!NOTE]
>
>병합 정책 ID가 정의되지 않고 스키마를 사용하는 경우</span>name 또는 relatedSchema</span>.name `_xdm.context.profile`은 프로필 액세스가 **모든** 관련 ID를 가져옵니다.

**API 형식**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `schema.name` | **필수 여부.** 액세스하는 스키마의 이름입니다. |
| `entityId` | 엔티티의 ID입니다. 제공된 경우 엔티티 네임스페이스도 제공해야 합니다. |
| `entityIdNS` | 검색하려는 ID의 네임스페이스입니다. |

**요청**

다음 GET 요청으로 이전에 인제스트한 레코드 데이터를 검토할 수 있습니다.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 개체에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다. 보시다시피, 이것은 일찍이 성공적으로 수집되었던 것과 동일한 레코드입니다.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## 다음 단계

이제 이 문서를 읽고 스트리밍 연결을 사용하여 레코드 데이터를 Platform으로 인제스트하는 방법을 알 수 있습니다. 다른 값으로 더 많은 호출을 만들고 업데이트된 값을 검색할 수 있습니다. 또한 Platform UI를 통해 인제스트된 데이터 모니터링을 시작할 수 있습니다. 자세한 내용은 [모니터링 데이터 수집](../quality/monitor-data-flows.md) 안내서를 참조하십시오.

일반적인 스트리밍 통합 방법에 대한 자세한 내용은 [스트리밍 통합 개요를 참조하십시오](../streaming-ingestion/overview.md).


