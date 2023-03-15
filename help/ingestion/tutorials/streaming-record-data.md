---
keywords: Experience Platform;홈;인기 항목;스트리밍 수집;수집;레코드 데이터;레코드 데이터 스트리밍;
solution: Experience Platform
title: 스트리밍 수집 API를 사용하여 레코드 데이터 스트리밍
type: Tutorial
description: 이 자습서는 Adobe Experience Platform 데이터 수집 서비스 API의 일부인 수집 API 스트리밍을 사용하는 데 도움이 됩니다.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 2%

---


# 스트리밍 수집 API를 사용하여 레코드 데이터 스트리밍

이 자습서는 Adobe Experience Platform의 일부인 수집 API 스트리밍을 사용하는 데 도움이 됩니다 [!DNL Data Ingestion Service] API.

## 시작하기

이 자습서에서는 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 경험 데이터를 구성합니다.
   - [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md): 의 사용 가능한 각 끝점을 다루는 포괄적인 안내서 [!DNL Schema Registry] API 및 호출 방법. 여기에는 다음 사항을 아는 것이 포함됩니다. `{TENANT_ID}`: 수집을 위한 데이터 세트를 만드는 데 사용되는 스키마를 만드는 방법을 알고 있을 뿐만 아니라 이 자습서 전체의 호출에 표시됩니다.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 소비자 프로필을 실시간으로 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../landing/api-guide.md).

## 다음을 기반으로 스키마 구성 [!DNL XDM Individual Profile] 클래스

데이터 세트를 만들려면 먼저 를 구현하는 새 스키마를 만들어야 합니다 [!DNL XDM Individual Profile] 클래스. 스키마를 만드는 방법에 대한 자세한 내용은 [스키마 레지스트리 API 개발자 안내서](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `description` | 생성 중인 스키마에 대한 의미 있는 설명입니다. |
| `meta:immutableTags` | 이 예에서는 `union` 태그는 데이터를 지속하는 데 사용됩니다. [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**응답**

성공적인 응답은 새로 생성된 스키마의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 IMS 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. 테넌트 ID에 대한 자세한 내용은 [스키마 레지스트리 안내서](../../xdm/api/getting-started.md#know-your-tenant-id). |

다음 사항을 적어 주십시오. `$id` 및 `version` 특성(이 두 가지 모두 데이터 세트를 만들 때 사용됨)입니다.

## 스키마에 대한 기본 ID 설명자 설정

그런 다음 을(를) 추가합니다. [id 설명자](../../xdm/api/descriptors.md) 회사 이메일 주소 속성을 기본 식별자로 사용하여 위에서 만든 스키마에 매핑합니다. 이렇게 하면 다음 두 가지 사항이 변경됩니다.

1. 회사 이메일 주소는 필수 필드가 됩니다. 즉, 이 필드 없이 전송된 메시지는 유효성 검사에 실패하고 수집되지 않습니다.

2. [!DNL Real-Time Customer Profile] 은(는) 회사 이메일 주소를 식별자로 사용하여 해당 개인에 대한 자세한 정보를 결합합니다.

### 요청

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | 다음 `$id` 이전에 스키마를 구성할 때 받은 것입니다. 다음과 같이 표시되어야 합니다. `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**ID 네임스페이스 코드**
>
> 코드가 유효한지 확인하십시오. 위의 예에서는 표준 ID 네임스페이스인 &quot;이메일&quot;을 사용합니다. 다른 일반적으로 사용되는 표준 ID 네임스페이스는 [ID 서비스 FAQ](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 사용자 지정 네임스페이스를 만들려면 [id 네임스페이스 개요](../../identity-service/home.md).

**응답**

성공적인 응답은 스키마에 대해 새로 생성된 기본 ID 설명자에 대한 정보와 함께 HTTP 상태 201을 반환합니다.

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
    "imsOrg": "{ORG_ID}"
}
```

## 레코드 데이터에 대한 데이터 세트 만들기

스키마를 만든 후에는 레코드 데이터를 수집하기 위한 데이터 세트를 만들어야 합니다.

>[!NOTE]
>
>이 데이터 세트는 다음에 대해 활성화됩니다. **[!DNL Real-Time Customer Profile]** 및 **[!DNL Identity Service]**.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 응답은 HTTP 상태 201과 새로 만든 데이터 세트의 ID가 포함된 배열을 형식으로 반환합니다 `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 스트리밍 연결 만들기

스키마와 데이터 세트를 만든 후 스트리밍 연결을 만들 수 있습니다

스트리밍 연결 만들기에 대한 자세한 내용은 [스트리밍 연결 튜토리얼 만들기](./create-streaming-connection.md).

## 스트리밍 연결로 레코드 데이터 수집 {#ingest-data}

데이터 세트 및 스트리밍 연결을 통해 XDM 형식의 JSON 레코드를 수집하여 레코드 데이터를에 수집할 수 있습니다 [!DNL Platform].

**API 형식**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 다음 `inletId` 이전에 만든 스트리밍 연결의 값입니다. |
| `syncValidation` | 개발 목적을 위한 선택적 쿼리 매개 변수입니다. 로 설정된 경우 `true`: 요청이 성공적으로 전송되었는지 확인하기 위해 즉각적인 피드백에 사용될 수 있습니다. 기본적으로 이 값은 로 설정됩니다. `false`. 이 쿼리 매개 변수를 로 설정하면 `true` 요청이 분당 60회로 제한됨 `CONNECTION_ID`. |

**요청**

레코드 데이터를 스트리밍 연결로 수집하는 작업은 소스 이름을 사용하거나 사용하지 않고 수행할 수 있습니다.

아래 예제 요청은 소스 이름이 누락된 레코드를 Platform으로 수집합니다. 레코드에 소스 이름이 없는 경우 스트리밍 연결 정의에서 소스 ID가 추가됩니다.

>[!NOTE]
>
>다음 API 호출은 **아님** 모든 인증 헤더가 필요합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
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

소스 이름을 포함하려면 다음 예제를 통해 소스 이름을 포함하는 방법을 보여 줍니다.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**응답**

성공적인 응답은 새로 스트리밍된 데이터의 세부 정보와 함께 HTTP 상태 200을 반환합니다 [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 ID입니다. |
| `xactionId` | 방금 전송한 레코드에 대해 서버측에서 생성된 고유 식별자입니다. 이 ID는 Adobe이 다양한 시스템을 통해 디버깅을 사용하여 이 레코드의 라이프사이클을 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청이 수신된 시간을 보여 주는 타임스탬프(시간(밀리초 단위))입니다. |
| `syncValidation.status` | 쿼리 매개 변수 이후 `syncValidation=true` 이(가) 추가되었습니다. 이 값이 표시됩니다. 유효성 검사가 성공하면 상태는 다음과 같습니다. `pass`. |

## 새로 수집된 레코드 데이터 검색

이전에 수집된 레코드의 유효성을 검사하려면 [[!DNL Profile Access API]](../../profile/api/entities.md) 레코드 데이터를 검색합니다.

>[!NOTE]
>
>병합 정책 ID가 정의되지 않은 경우 및 `schema.name` 또는 `relatedSchema.name` 은(는) `_xdm.context.profile`, [!DNL Profile Access] 가져오기 **모두** 관련 id.

**API 형식**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `schema.name` | **필수 여부.** 액세스 중인 스키마의 이름입니다. |
| `entityId` | 엔티티의 ID입니다. 제공된 경우 엔티티 네임스페이스도 제공해야 합니다. |
| `entityIdNS` | 검색하려는 ID의 네임스페이스입니다. |

**요청**

다음 GET 요청으로 이전에 수집된 레코드 데이터를 검토할 수 있습니다.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 엔터티의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 보시다시피, 이것은 이전에 성공적으로 수집된 레코드와 동일합니다.

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

이제 이 문서를 읽고 기록 데이터를 로 수집하는 방법을 이해할 수 있습니다 [!DNL Platform] 스트리밍 연결을 사용합니다. 다른 값으로 더 많은 호출을 하고 업데이트된 값을 검색해 볼 수 있습니다. 또한 다음을 통해 수집된 데이터의 모니터링을 시작할 수 있습니다. [!DNL Platform] UI. 자세한 내용은 다음을 참조하십시오. [데이터 수집 모니터링](../quality/monitor-data-ingestion.md) 가이드.

일반적인 스트리밍 수집에 대한 자세한 내용은 [스트리밍 수집 개요](../streaming-ingestion/overview.md).
