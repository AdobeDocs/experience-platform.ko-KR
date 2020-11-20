---
keywords: Experience Platform;home;popular topics;Collect eCommerce data;eCommerce data
solution: Experience Platform
title: 소스 커넥터 및 API를 통해 전자 상거래 데이터 수집
topic: overview
type: Tutorial
description: 이 자습서에서는 타사 e커머스 시스템에서 데이터를 검색하고 소스 커넥터 및 API를 통해 플랫폼으로 데이터를 인제하는 단계를 다룹니다.
translation-type: tm+mt
source-git-commit: a9d6c6dda560ec401bdf41319994153e7f2c0572
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 1%

---


# 소스 커넥터 및 API를 통해 전자 상거래 데이터 수집

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 타사 e커머스 **[!UICONTROL 시스템에서 데이터를 검색하고 소스 커넥터 및]** API를 통해 데이터를 인제스트하는 [!DNL Platform] [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 단계를 다룹니다.

## 시작하기

이 자습서에서는 올바른 연결을 통해 **[!UICONTROL eCommerce]** 시스템에 액세스하거나 가져올 파일(파일의 경로 및 구조 포함)에 대한 정보 [!DNL Platform] 를 필요로 합니다. 이 정보가 없는 경우 이 자습서를 시작하기 전에 Flow Service API를 사용하여 eCommerce 시스템을 [탐색하는 방법에 대한 자습서를](../explore/ecommerce.md) 참조하십시오.

또한 이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 레지스트리 API](../../../../xdm/api/getting-started.md):스키마 레지스트리 API에 대한 호출을 성공적으로 수행하는 방법을 알아봅니다. 여기에는 사용자 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청 시 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).
* [[!DNL Catalog Service]](../../../../catalog/home.md):카탈로그는 내부 데이터 위치 및 계열에 대한 기록 시스템이다 [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):일괄 처리 통합 API를 사용하면 데이터를 일괄 처리 파일 [!DNL Experience Platform] 로 인제스트할 수 있습니다.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 **[!UICONTROL API를 사용하여 전자 상거래]** [!DNL Flow Service] 시스템에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

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
        "name": "Shopify Source Connection demo",
        "baseConnectionId": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
        "description": "Shopify Source Connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "Shopify.Orders",
            "columns": [
                {
                    "name": "Email",
                    "type": "string"
                },
                {
                    "name": "Phone",
                    "type": "string"
                },
            ]
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | eCommerce 소스의 연결 **[!UICONTROL ID입니다]** . |
| `params.path` | 소스 파일의 경로입니다. |
| `connectionSpec.id` | eCommerce 소스의 **[!UICONTROL 연결 사양]** ID. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 타겟 연결을 만들려면 이후 단계에서 필요합니다.

```json
{
    "id": "c278ab14-acdf-440b-b67f-1265d15a7655",
    "etag": "\"10007c3f-0000-0200-0000-5fa9be720000\""
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
        "title": "Test Shopify schema",
        "description": "",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
    "meta:altId": "_{TENANT_ID}.schemas.854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Test shopify demo",
    "type": "object",
    "description": "",
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
    "meta:sandboxId": "6b36e130-c5d7-11e9-949c-0da8d50fcac1",
    "meta:sandboxType": "production",
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
    'https://platform.adobe.io/data/foundation/catalog/dataSet' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test Shopify Target Dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
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
    "@/dataSets/5fa9c083de62e418dd170b42"
]
```

## 대상 연결 만들기 {#target-connection}

대상 연결은 인제스트된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마의 고유한 식별자를 데이터 세트에 사용하고 데이터 호수에 대한 연결 사양 ID를 가집니다. API를 사용하여 [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트와 함께 이러한 식별자를 지정하여 대상 연결을 만들 수 있습니다.

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
    -d '{{
    "name": "Test Shopify Dataset Target Connection",
    "description": "Test Shopify Dataset Target Connection",
    "data": {
        "format": "parquet_xdm",
        "schema": {
            "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
            "version": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    },
    "params": {
        "dataSetId": "5fa9c083de62e418dd170b42"
    },
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `data.schema.id` | 대상 XDM 스키마 `$id` 의 이름입니다. |
| `params.dataSetId` | 대상 데이터 집합의 ID입니다. |
| `connectionSpec.id` | 데이터 레이크에 연결하는 데 사용되는 연결 사양 ID. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 데이터 흐름을 만들려면 이후 단계에서 필요합니다.

```json
{
    "id": "6c0ba537-a96b-4d74-8c95-450eb88baee8",
    "etag": "\"00005506-0000-0200-0000-5fa9c13c0000\""
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
        "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Shipping_Address_Phone",
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
    "id": "22922102bffd4369b6209c102a604062",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## 데이터 흐름 사양 검색 {#specs}

데이터 프롤은 소스에서 데이터를 수집하여 데이터 센터로 가져옵니다 [!DNL Platform]. 데이터 흐름을 만들려면 먼저 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다. 데이터 흐름 사양은 **[!UICONTROL 전자 상거래]** 소스에서 데이터를 수집하는 책임을 집니다.

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

성공적인 응답은 **[!UICONTROL eCommerce]** 소스에서 데이터를 데이터 [!DNL Platform]로 가져오는 작업을 담당하는 데이터 흐름 세부 정보의 내용을 반환합니다. 이 ID는 새 데이터 흐름을 만들려면 다음 단계에서 필요합니다.

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
        "name": "Test Shopify dataflow",
        "description": "Shopify With mapping ingestion",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c278ab14-acdf-440b-b67f-1265d15a7655"
        ],
        "targetConnectionIds": [
            "6c0ba537-a96b-4d74-8c95-450eb88baee8"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "22922102bffd4369b6209c102a604062",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1604961070",
            "frequency": "once"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `flowSpec.id` | 이전 단계에서 검색된 [흐름 사양](#specs) ID. |
| `sourceConnectionIds` | 이전 단계에서 검색된 [소스 연결](#source) ID입니다. |
| `targetConnectionIds` | 이전 단계에서 검색된 [대상 연결](#target-connection) ID입니다. |
| `transformations.params.mappingId` | 이전 단계에서 검색된 [매핑](#mapping) ID. |
| `transformations.params.mappingId` | 전자 상거래 원본과 연결된 **[!UICONTROL 매핑]** ID. |
| `scheduleParams.startTime` | epoch time의 데이터 흐름 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름 `frequency` 이 데이터를 수집하는 위치입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`또는 `week`를 선택합니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 간격이 으로 설정된 경우 `frequency` 는 필요하지 않으며 다른 `once` 값에 대해 `15` `frequency` 크거나 같아야 합니다. |

**응답**

성공적인 응답은 새로 만든 데이터 흐름 `id` 의 ID를 반환합니다.

```json
{
    "id": "20c115bc-46e3-40f3-bfe9-fb25abe4ba76",
    "etag": "\"030018cb-0000-0200-0000-5fa9c31a0000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름을 만든 후 데이터 흐름을 통해 인제스트되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름 모니터링 방법에 대한 자세한 내용은 API에서 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오 ](../monitor.md)

## 다음 단계

이 튜토리얼을 따라 데이터 전자 상거래 **[!UICONTROL 를 예약별로]** 수집하기 위한 소스 커넥터를 만들었습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../profile/home.md)
* [데이터 과학 작업 공간 개요](../../../../data-science-workspace/home.md)