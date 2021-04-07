---
keywords: Experience Platform;홈;인기 항목;스트리밍 통합;기록 데이터;스트림 레코드 데이터;;home;popular topics;streaming ingestion;ingestion;record data;stream record data;
solution: Experience Platform
title: 스트리밍 통합 API를 사용한 스트림 레코드 데이터
topic: 자습서
type: 튜토리얼
description: 이 자습서는 Adobe Experience Platform 데이터 통합 서비스 API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 됩니다.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 2%

---

# 스트리밍 통합 API를 사용하여 데이터 스트리밍

이 자습서는 Adobe Experience Platform [!DNL Data Ingestion Service] API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 됩니다.

## 시작하기

이 자습서에서는 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.
- [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md):API의 사용 가능한 각 끝점과  [!DNL Schema Registry] API를 호출하는 방법을 다루는 포괄적인 안내서입니다. 여기에는 이 자습서 전체의 호출에 표시되는 `{TENANT_ID}`에 대해 알고 있을 뿐만 아니라 수집에 대한 데이터 세트를 만드는 데 사용되는 스키마를 만드는 방법에 대해서도 알고 있는 것이 포함됩니다.

또한 이 자습서에서는 스트리밍 연결을 이미 만들어야 합니다. 스트리밍 연결 만들기에 대한 자세한 내용은 [스트리밍 연결 자습서 만들기](./create-streaming-connection.md)를 참조하십시오.

다음 섹션에서는 스트리밍 통합 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## [!DNL XDM Individual Profile] 클래스를 기반으로 스키마 작성

데이터 집합을 만들려면 먼저 [!DNL XDM Individual Profile] 클래스를 구현하는 새 스키마를 만들어야 합니다. 스키마 생성 방법에 대한 자세한 내용은 [스키마 레지스트리 API 개발자 가이드](../../xdm/api/getting-started.md)를 참조하십시오.

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
| `meta:immutableTags` | 이 예에서 `union` 태그는 데이터를 [[!DNL Real-time Customer Profile]](../../profile/home.md)에 유지하는 데 사용됩니다. |

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
| `{TENANT_ID}` | 이 ID는 사용자가 만든 리소스가 적절하게 대체되고 IMS 조직 내에 포함되도록 하는 데 사용됩니다. 테넌트 ID에 대한 자세한 내용은 [스키마 레지스트리 안내서](../../xdm/api/getting-started.md#know-your-tenant-id)를 참조하십시오. |

데이터 세트를 만들 때 이 두 가지가 모두 사용되므로 `$id` 및 `version` 특성을 참고하시기 바랍니다.

## 스키마에 대한 기본 ID 설명자 설정

그런 다음 작업 이메일 주소 특성을 기본 식별자로 사용하여 위에 만든 스키마에 [ID 설명자](../../xdm/api/descriptors.md)를 추가합니다. 이렇게 하면 두 가지 변경 사항이 발생합니다.

1. 작업 이메일 주소는 필수 필드가 됩니다. 즉, 이 필드 없이 전송된 메시지는 유효성 검사에 실패하며 인제스트되지 않습니다.

2. [!DNL Real-time Customer Profile] 는 해당 개인에 대한 자세한 정보를 연결하는 데 도움이 되도록 작업 이메일 주소를 식별자로 사용합니다.

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
| `{SCHEMA_REF_ID}` | 스키마를 작성할 때 이전에 받은 `$id`. 다음과 같이 표시됩니다.`"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;&#x200B;**ID 네임스페이스 코드**
>
> 코드가 유효한지 확인하십시오. 위의 예에서는 표준 ID 네임스페이스인 &quot;email&quot;을 사용합니다. 일반적으로 사용되는 다른 표준 ID 네임스페이스는 [Identity Service FAQ](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)에서 찾을 수 있습니다.
>
> 사용자 정의 네임스페이스를 만들려면 [identity 네임스페이스 개요](../../identity-service/home.md)에 설명된 단계를 따릅니다.

**응답**

성공적인 응답은 스키마에 대해 새로 만든 기본 ID 설명자에 대한 정보가 포함된 HTTP 상태 201을 반환합니다.

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

스키마를 만든 후에는 레코드 데이터를 인제스트할 데이터 세트를 만들어야 합니다.

>[!NOTE]
>
>이 데이터 집합은 **[!DNL Real-time Customer Profile]** 및 **[!DNL Identity Service]**&#x200B;에 대해 활성화됩니다.

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
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**응답**

성공적인 응답은 HTTP 상태 201을 반환하고 새로 만든 데이터 세트의 ID를 `@/dataSets/{DATASET_ID}` 형식으로 포함하는 배열을 반환합니다.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 스트리밍 연결 {#ingest-data}에 레코드 데이터를 인제스트합니다.

데이터 세트 및 스트리밍 연결을 적절히 사용하여 XDM 형식의 JSON 레코드를 인제스트하여 레코드 데이터를 [!DNL Platform]에 인제스트할 수 있습니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 `id` 값입니다. |
| `synchronousValidation` | 개발 목적으로 사용하기 위한 선택적 쿼리 매개 변수입니다. `true`으로 설정된 경우 즉시 피드백에 사용하여 요청이 성공적으로 전송되었는지 확인할 수 있습니다. 기본적으로 이 값은 `false`으로 설정됩니다. |

**요청**

소스 이름을 사용하거나 사용하지 않고 스트리밍 연결에 레코드 데이터를 인제스트할 수 있습니다.

아래의 예제 요청은 소스 이름이 누락된 레코드를 플랫폼에 인제스트합니다. 레코드에 소스 이름이 없으면 스트리밍 연결 정의에서 소스 ID가 추가됩니다.

>[!NOTE]
>
>다음 API 호출은 **인증 헤더가 필요하지 않습니다.**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
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

소스 이름을 포함하려는 경우 다음 예제에서는 소스 이름을 포함하는 방법을 보여 줍니다.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**응답**

성공적인 응답은 새로 스트리밍된 [!DNL Profile]에 대한 세부 사항과 함께 HTTP 상태 200을 반환합니다.

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
| `xactionId` | 방금 보낸 레코드에 대해 서버측에서 생성된 고유 식별자. 이 ID는 Adobe이 다양한 시스템과 디버깅을 통해 이 레코드의 주기를 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청을 받은 시간을 표시하는 타임스탬프(밀리초 단위)입니다. |
| `synchronousValidation.status` | 쿼리 매개 변수 `synchronousValidation=true`이(가) 추가되었으므로 이 값이 나타납니다. 유효성 검사에 성공한 경우 상태는 `pass`입니다. |

## 새로 인제스트한 레코드 데이터 검색

이전에 인제스트한 레코드의 유효성을 검사하려면 [[!DNL Profile Access API]](../../profile/api/entities.md)을 사용하여 레코드 데이터를 검색할 수 있습니다.

>[!NOTE]
>
>병합 정책 ID가 정의되지 않은 상태에서 `schema.name` 또는 `relatedSchema.name`이 `_xdm.context.profile`인 경우 [!DNL Profile Access]은(는) **모든** 관련 ID를 가져옵니다.

**API 형식**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `schema.name` | **필수 여부.** 액세스하는 스키마의 이름입니다. |
| `entityId` | 엔티티의 ID입니다. 제공된 경우 엔터티 네임스페이스도 제공해야 합니다. |
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

성공적으로 응답하면 요청된 엔티티의 세부 정보가 포함된 HTTP 상태 200이 반환됩니다. 보시다시피, 이것은 이전에 성공적으로 수집되었던 기록과 같습니다.

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

이제 스트리밍 연결을 사용하여 레코드 데이터를 [!DNL Platform]에 인제스트하는 방법을 알 수 있습니다. 값이 다른 호출을 더 만들고 업데이트된 값을 검색할 수 있습니다. 또한 [!DNL Platform] UI를 통해 인제스트된 데이터 모니터링을 시작할 수 있습니다. 자세한 내용은 [데이터 통합 모니터링](../quality/monitor-data-ingestion.md) 안내서를 참조하십시오.

일반적인 스트리밍 통합 관련 자세한 내용은 [스트리밍 통합 개요](../streaming-ingestion/overview.md)를 참조하십시오.
