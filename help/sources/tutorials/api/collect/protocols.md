---
keywords: Experience Platform;home;popular topics;Collect protocol data;protocol data
solution: Experience Platform
title: 소스 커넥터 및 API를 통해 프로토콜 데이터 수집
topic: overview
type: Tutorial
description: 이 자습서에서는 프로토콜 애플리케이션에서 데이터를 검색하고 소스 커넥터 및 API를 통해 플랫폼으로 데이터를 인제하는 단계를 다룹니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 1%

---


# 소스 커넥터 및 API를 통해 프로토콜 데이터 수집

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 타사 프로토콜 응용 프로그램에서 데이터를 검색하고 소스 커넥터 및 [!DNL Platform] [!DNL Flow Service] [API를 통해 데이터를 인제하는 단계를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 다룹니다.

## 시작하기

이 자습서에서는 테이블의 경로 및 구조를 [!DNL Platform]포함하여 가져올 파일에 대한 정보와 유효한 기본 연결을 통해 프로토콜 시스템에 액세스해야 합니다. 이 정보가 없는 경우 이 튜토리얼을 시작하기 전에 Flow Service API를 사용하여 프로토콜 시스템을 [탐색하는](../explore/protocols.md) 자습서를 참조하십시오.

* [[!DNL 경험 데이터 모델(XDM) 시스템]](../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 레지스트리 개발자 가이드](../../../../xdm/api/getting-started.md):스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보를 포함합니다. 여기에는 사용자 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청 시 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).
* [[!DNL 카탈로그 서비스]](../../../../catalog/home.md):카탈로그는 내부 데이터 위치 및 계열에 대한 기록 시스템이다 [!DNL Experience Platform].
* [[!DNL 일괄 처리]](../../../../ingestion/batch-ingestion/overview.md):일괄 처리 통합 API를 사용하면 데이터를 일괄 처리 파일 [!DNL Experience Platform] 로 인제스트할 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 프로토콜 애플리케이션에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 소스 연결 만들기 {#source}

API에 POST 요청을 만들어 소스 연결을 만들 수 [!DNL Flow Service] 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 커넥터에 다음과 같은 열거형 값을 사용하십시오.

| Data.format | 열거값 |
| ----------- | ---------- |
| 구분된 파일 | `delimited` |
| JSON 파일 | `json` |
| 쪽모이 세공 파일 | `parquet` |

모든 테이블 기반 커넥터의 경우 열거형 값을 사용합니다. `tabular`.

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
        "name": "Protocols source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Protocols source connection to ingest Orders",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Orders"
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 프로토콜 응용 프로그램의 연결 ID |
| `params.path` | 소스 파일의 경로입니다. |
| `connectionSpec.id` | 프로토콜 응용 프로그램의 연결 사양 ID. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 타겟 연결을 만들려면 이후 단계에서 필요합니다.

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

이전 단계에서는 소스 데이터를 구조화하기 위해 임시 XDM 스키마를 만들었습니다. 소스 데이터를 사용하려면 필요에 따라 소스 데이터 [!DNL Platform]를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 [!DNL Platform] 데이터 세트를 만듭니다. 이 대상 XDM 스키마도 XDM [!DNL Individual Profile] 클래스를 확장합니다.

대상 XDM 스키마는 스키마 레지스트리 API에 대한 POST 요청을 수행하여 [만들 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). 사용자 인터페이스를 에서 사용하려는 경우 스키마 편집기 자습서 [!DNL Experience Platform]는 스키마 편집기에서 유사한 작업 [](../../../../xdm/tutorials/create-schema-ui.md) 을 수행하기 위한 단계별 지침을 제공합니다.
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
        "title": "Target schema for protocols",
        "description": "Target schema for protocols",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Protocols target schema",
    "type": "object",
    "description": "Protocols target schema",
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
    "imsOrg": "7DC732555AECDB4C0A494036@AdobeOrg",
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
        "repo:createdDate": 1586124086523,
        "repo:lastModifiedDate": 1586124086523,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "8b281c23af03ff6a8b7d8061c62d73f7bcbfa1fc7dbabebfb4d8ca77130576ca"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 대상 데이터 세트 만들기

페이로드 내의 대상 스키마의 ID를 제공하여 [카탈로그 서비스 API에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)POST 요청을 수행하여 대상 데이터 집합을 만들 수 있습니다.

**API 형식**

```http
POST /dataSets
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
        "name": "Protocols target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef.id` | 대상 XDM 스키마 `$id` 의 이름입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 형식 `"@/datasets/{DATASET_ID}"`입니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다. 타겟 데이터 집합 ID를 나중에 타겟 연결 및 데이터 흐름을 만드는 데 필요한 만큼 저장합니다.

```json
[
    "@/dataSets/5e8a55ca53662c18af37a83a"
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
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
            "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `data.schema.id` | 대상 XDM 스키마 `$id` 의 이름입니다. |
| `params.dataSetId` | 대상 데이터 집합의 ID입니다. |
| `connectionSpec.id` | 데이터 호수에 대한 연결 사양 ID가 수정되었습니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 데이터 흐름을 만들려면 이후 단계에서 필요합니다.

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 요청 페이로드 내에 정의된 데이터 매핑과 함께 [전환 서비스 API에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) 대한 POST 요청을 수행하여 얻습니다.

**API 형식**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
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
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## 데이터 흐름 사양 검색 {#specs}

데이터 프롤은 소스에서 데이터를 수집하여 데이터 센터로 가져옵니다 [!DNL Platform]. 데이터 흐름을 만들려면 먼저 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다. 데이터 흐름 사양은 외부 프로토콜 애플리케이션에서 데이터를 수집합니다.

**API 형식**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 프로토콜 애플리케이션에서 데이터를 데이터 흐름 사양에 대한 세부 정보를 반환합니다 [!DNL Platform]. 이 ID는 새 데이터 흐름을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## 데이터 흐름 만들기

데이터 수집을 위한 마지막 단계는 데이터 흐름을 만드는 것입니다. 이때 다음 필수 값이 준비되어야 합니다.

* [원본 연결 ID](#source)
* [Target 연결 ID](#target)
* [매핑 ID](#mapping)
* [데이터 흐름 사양 ID](#specs)

데이터 프롤은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급한 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

질문을 예약하려면 먼저 시작 시간 값을 epoch time(초)으로 설정해야 합니다. 그런 다음 빈도 값을 5개 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`또는 `week`를 선택합니다. 간격 값은 연속된 두 시퀀스 사이의 기간을 지정하고 일회성 인제스트를 만들 때는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값이 같거나 크게 설정되어야 합니다 `15`.


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
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `flowSpec.id` | 이전 단계에서 검색된 [흐름 사양](#specs) ID. |
| `sourceConnectionIds` | 이전 단계에서 검색된 [소스 연결](#source) ID입니다. |
| `targetConnectionIds` | 이전 단계에서 검색된 [대상 연결](#target-connection) ID입니다. |
| `transformations.params.mappingId` | 이전 단계에서 검색된 [매핑](#mapping) ID. |
| `transformations.params.deltaColum` | 새 데이터와 기존 데이터를 구분하는 데 사용되는 지정된 열 선택한 열의 타임스탬프를 기반으로 증분 데이터를 인제스트합니다. 범용 OData를 사용할 `deltaColumn` 때 지원되는 형식입니다 `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | 데이터베이스와 연결된 매핑 ID. |
| `scheduleParams.startTime` | epoch time의 데이터 흐름 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름 데이터가 수집되는 빈도 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`또는 `week`를 선택합니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 주기를 다음으로 설정하고 다른 주파수 값에 대해 이보다 `once` 크거나 같아야 하는 경우 간격이 `15` 필요하지 않습니다. |

**응답**

성공적인 응답은 새로 만든 데이터 흐름 `id` 의 ID를 반환합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름을 만든 후 데이터 흐름을 통해 인제스트되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름 모니터링 방법에 대한 자세한 내용은 API에서 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오 ](../monitor.md)


## 다음 단계

이 튜토리얼을 따라 예약된 기준에 따라 프로토콜 애플리케이션에서 데이터를 수집하는 소스 커넥터를 만들었습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../profile/home.md)
* [데이터 과학 작업 공간 개요](../../../../data-science-workspace/home.md)