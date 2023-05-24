---
keywords: Experience Platform;홈;자주 찾는 항목;클라우드 스토리지 데이터;스트리밍 데이터;스트리밍
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 원시 데이터에 대한 스트리밍 데이터 흐름 만들기
type: Tutorial
description: 이 튜토리얼에서는 소스 커넥터 및 API를 사용하여 스트리밍 데이터를 검색하고 이를 플랫폼으로 가져오는 단계를 다룹니다.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 2%

---

# 를 사용하여 원시 데이터에 대한 스트리밍 데이터 흐름 만들기 [!DNL Flow Service] API

이 자습서에서는 스트리밍 소스 커넥터에서 원시 데이터를 검색하고 를 사용하여 Experience Platform 상태로 가져오는 단계를 다룹니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 레지스트리 개발자 안내서](../../../../xdm/api/getting-started.md): 스키마 레지스트리 API 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보가 포함되어 있습니다. 여기에는 다음 항목이 포함됩니다. `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청을 하는 데 필요한 헤더(Accept 헤더 및 가능한 값에 특별한 주의 필요).
- [[!DNL Catalog Service]](../../../../catalog/home.md): 카탈로그는 Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): Platform용 스트리밍 수집은 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송하는 방법을 사용자에게 제공합니다.
- [샌드박스](../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../landing/api-guide.md).

### 소스 연결 만들기 {#source}

또한 이 자습서에서는 스트리밍 커넥터에 대해 유효한 소스 연결 ID가 있어야 합니다. 이 정보가 없는 경우 이 자습서를 시도하기 전에 스트리밍 소스 연결 만들기에 대한 다음 자습서를 참조하십시오.

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다. 이 대상 XDM 스키마는 XDM도 확장합니다 [!DNL Individual Profile] 클래스.

POST 대상 XDM 스키마를 생성하려면 `/schemas` 의 엔드포인트 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 예제 요청은 XDM을 확장하는 XDM 스키마를 만듭니다 [!DNL Individual Profile] 클래스.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 스키마의 세부 정보를 반환합니다.`$id`). 이 ID는 대상 데이터 세트, 매핑 및 데이터 흐름을 만드는 데 필요한 이후 단계입니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 타겟 데이터 세트 만들기

대상 XDM 스키마 및 고유 포함 `$id` 이제 소스 데이터를 포함할 타겟 데이터 세트를 만들 수 있습니다. POST 타겟 데이터 세트를 만들려면 다음을 수행하십시오. `dataSets` 의 엔드포인트 [카탈로그 서비스 API](https://www.adobe.io/experience-platform-apis/references/catalog/)페이로드 내에 대상 스키마의 ID를 제공합니다.

**API 형식**

```http
POST /catalog/dataSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 생성할 데이터 세트의 이름입니다. |
| `schemaRef.id` | URI `$id` xdm 스키마의 경우 데이터 세트가 기반으로 삼게 됩니다. |
| `schemaRef.contentType` | 스키마의 버전입니다. 이 값은 다음으로 설정해야 합니다. `application/vnd.adobe.xed-full-notext+json;version=1`최신 부 버전의 스키마를 반환합니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오. |

**응답**

성공적인 응답은 새로 생성된 데이터 세트의 ID가 포함된 배열을 형식으로 반환합니다 `"@/datasets/{DATASET_ID}"`. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다. 대상 연결 및 데이터 흐름을 만들려면 대상 데이터 세트 ID가 이후 단계에서 필요합니다.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 대상 연결 만들기 {#target-connection}

Target 연결은 플랫폼 또는 전송된 데이터가 도착하는 모든 위치에 대한 대상 연결을 만들고 관리합니다. Target 연결에는 데이터 대상, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 대상 연결 ID에 대한 정보가 포함되어 있습니다. Target 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

POST 대상 연결을 만들려면 `/targetConnections` 의 엔드포인트 [!DNL Flow Service] API. 요청의 일부로 데이터 형식인 `dataSetId` 이전 단계에서 검색되고 고정 연결 사양 ID가 연결됨 [!DNL Data Lake]. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API 형식**

```http
POST /targetConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `connectionSpec.id` | 에 연결하는 데 사용되는 연결 사양 ID [!DNL Data Lake]. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 가져오려는 데이터의 지정된 형식 [!DNL Data Lake]. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트의 ID입니다. |

**응답**

성공적인 응답은 새 타겟 연결의 고유 식별자( )를 반환합니다.`id`). 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다.

POST 매핑 세트를 만들려면 `mappingSets` 의 엔드포인트 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) target XDM 스키마를 제공하는 동안 `$id` 만들려는 매핑 세트의 세부 정보.

**API 형식**

```http
POST /mappingSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `xdmSchema` | 다음 `$id` 대상 XDM 스키마. |

**응답**

성공적인 응답은 고유한 식별자( )를 포함하여 새로 생성된 매핑의 세부 정보를 반환합니다.`id`). 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 데이터 흐름 사양 목록 검색 {#specs}

데이터 흐름은 소스에서 데이터를 수집하고 플랫폼으로 가져오는 역할을 합니다. 데이터 흐름을 만들려면 먼저 다음에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다 [!DNL Flow Service] API.

**API 형식**

```http
GET /flowSpecs
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 흐름 사양 목록을 반환합니다. 다음 중 하나를 사용하여 데이터 흐름을 만들기 위해 검색해야 하는 데이터 흐름 사양 ID [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], 또는  [!DNL Google PubSub],: `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## 데이터 흐름 만들기

스트리밍 데이터를 수집하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

- [소스 연결 ID](#source)
- [Target 연결 ID](#target)
- [ID 매핑](#mapping)
- [데이터 흐름 사양 ID](#specs)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `flowSpec.id` | 다음 [흐름 사양 ID](#specs) 이전 단계에서 검색되었습니다. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source) 이전 단계에서 검색되었습니다. |
| `targetConnectionIds` | 다음 [대상 연결 ID](#target-connection) 이전 단계에서 검색되었습니다. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 검색되었습니다. |

**응답**

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 다음 단계

이 자습서에 따라 스트리밍 커넥터에서 스트리밍 데이터를 수집하는 데이터 흐름을 만들었습니다. 이제 다음과 같은 다운스트림 플랫폼 서비스에서 수신 데이터를 사용할 수 있습니다. [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../profile/home.md)
- [데이터 과학 작업 영역 개요](../../../../data-science-workspace/home.md)
