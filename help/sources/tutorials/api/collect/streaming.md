---
keywords: Experience Platform;home;popular topics;cloud storage data;streaming data;streaming
solution: Experience Platform
title: 소스 커넥터 및 API를 통해 스트리밍 데이터 수집
topic: overview
type: Tutorial
description: 이 자습서에서는 스트리밍 데이터를 검색하고 소스 커넥터 및 API를 통해 플랫폼에 가져오는 단계를 다룹니다.
translation-type: tm+mt
source-git-commit: a9d6c6dda560ec401bdf41319994153e7f2c0572
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 2%

---


# 소스 커넥터 및 API를 통해 스트리밍 데이터 수집

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 스트리밍 소스 커넥터에서 데이터를 검색하고 API [!DNL Experience Platform] 를 사용하여 데이터를 가져오는 단계를 [[!DNL Flow Service] 설명합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 시작하기

이 자습서에서는 스트리밍 커넥터에 대해 유효한 연결 ID가 있어야 합니다. 이 정보가 없는 경우 이 자습서를 시작하기 전에 스트리밍 소스 연결을 만드는 다음 자습서를 참조하십시오.

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../../../../ingestion/tutorials/create-streaming-connection.md)

또한 이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 레지스트리 개발자 가이드](../../../../xdm/api/getting-started.md):스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보를 포함합니다. 여기에는 사용자 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청 시 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).
- [[!DNL Catalog Service]](../../../../catalog/home.md):카탈로그는 내부 데이터 위치 및 계열에 대한 기록 시스템이다 [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md):스트리밍 방식 [!DNL Platform] 을 사용하면 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 전송할 수 [!DNL Experience Platform] 있습니다.
- [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 스트리밍 데이터를 성공적으로 수집하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

- `Content-Type: application/json`

## 소스 연결 만들기 {#source}

API에 POST 요청을 만들어 소스 연결을 만들 수 [!DNL Flow Service] 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 커넥터에 다음과 같은 열거형 값을 사용하십시오.

| 데이터 형식 | 열거값 |
| ----------- | ---------- |
| 구분 기호 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 커넥터의 경우 값을 로 설정합니다 `tabular`.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `providerId` | 스트리밍 커넥터의 공급자 ID입니다. |
| `connectionId` | 스트리밍 커넥터의 고유한 연결 ID입니다. |
| `connectionSpec.id` | 특정 스트리밍 커넥터와 연결된 연결 사양 ID입니다. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 데이터 흐름을 만들려면 이 ID가 나중에 필요합니다.

```json
{
    "id": "2abd97c4-91bb-4c93-bd97-c491bbfc933d",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 사용하려면 필요에 따라 소스 데이터 [!DNL Platform]를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 [!DNL Platform] 데이터 세트를 만듭니다. 이 대상 XDM 스키마도 XDM [!DNL Individual Profile] 클래스를 확장합니다.

대상 XDM 스키마는 스키마 레지스트리 API에 대한 POST 요청을 수행하여 [만들 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 예제 요청에서는 XDM 클래스를 확장하는 XDM 스키마를 [!DNL Individual Profile] 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공적인 응답은 고유한 식별자(`$id`)를 포함하여 새로 만든 스키마의 세부 정보를 반환합니다. 이 ID는 나중에 대상 데이터 집합, 매핑 및 데이터 흐름을 만들려면 필요합니다.

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
    "imsOrg": "{IMS_ORG}",
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

## 대상 데이터 세트 만들기

페이로드 내의 대상 스키마의 ID를 제공하여 [카탈로그 서비스 API에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)POST 요청을 수행하여 대상 데이터 집합을 만들 수 있습니다.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.1"
        },
        "fileDescription": {
            "format": "parquet"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        },
        "name": "Test streaming dataset"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `schemaRef.id` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 형식 `"@/datasets/{DATASET_ID}"`입니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다. 대상 연결 및 데이터 흐름을 만들려면 나중에 대상 데이터 집합 ID가 필요합니다.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 대상 연결 만들기 {#target-connection}

대상 연결은 인제스트된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 호수와 관련된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마의 고유한 식별자를 데이터 세트에 사용하고 데이터 호수에 대한 연결 사양 ID를 가집니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 소스 데이터를 포함할 데이터 세트를 지정할 수 있습니다.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `params.dataSetId` | 대상 데이터 집합의 ID입니다. |
| `connectionSpec.id` | 데이터 레이크에 연결하는 데 사용되는 연결 사양 ID. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 이후 단계에서 필요합니다.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 요청 페이로드 내에 정의된 데이터 매핑과 함께 전환 서비스에 대한 POST 요청을 수행하여 얻습니다.

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `xdmSchema` | 대상 XDM 스키마 `$id` 의 이름입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 데이터 흐름을 만들려면 이 ID가 나중에 필요합니다.

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

## 데이터 흐름 사양 검색 {#specs}

데이터 프롤은 소스에서 데이터를 수집하여 데이터 센터로 가져옵니다 [!DNL Platform]. 데이터 흐름을 만들려면 먼저 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다. 데이터 흐름 사양은 스트리밍 커넥터에서 데이터를 수집하는 책임을 집니다.
**API 형식**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답으로 스트리밍 커넥터의 데이터를 데이터 흐름 사양에 대한 세부 정보를 반환합니다 [!DNL Platform]. 이 ID는 새 데이터 흐름을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
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
        }
    ]
}
```

## 데이터 흐름 만들기

스트리밍 데이터를 수집하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 현재 다음과 같은 필수 값이 준비되었습니다.

- [원본 연결 ID](#source)
- [Target 연결 ID](#target)
- [매핑 ID](#mapping)
- [데이터 흐름 사양 ID](#specs)

데이터 프롤은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급한 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "2abd97c4-91bb-4c93-bd97-c491bbfc933d"
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
| `flowSpec.id` | 이전 단계에서 검색된 [흐름 사양](#specs) ID. |
| `sourceConnectionIds` | 이전 단계에서 검색된 [소스 연결](#source) ID입니다. |
| `targetConnectionIds` | 이전 단계에서 검색된 [대상 연결](#target-connection) ID입니다. |
| `transformations.params.mappingId` | 이전 단계에서 검색된 [매핑](#mapping) ID. |

**응답**

성공적인 응답은 새로 만든 데이터 흐름`id`의 ID를 반환합니다.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 다음 단계

이 튜토리얼을 따라 스트리밍 커넥터에서 스트리밍 데이터를 수집하는 데이터 흐름을 만들었습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../profile/home.md)
- [데이터 과학 작업 공간 개요](../../../../data-science-workspace/home.md)