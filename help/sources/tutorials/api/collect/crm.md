---
title: CRM의 데이터를 Experience Platform으로 수집하는 데이터 흐름을 만듭니다.
description: 흐름 서비스 API를 사용하여 데이터 흐름을 만들고 소스 데이터를 Experience Platform으로 수집하는 방법을 알아봅니다.
exl-id: b07dd640-bce6-4699-9d2b-b7096746934a
source-git-commit: b4f8d44c3ce9507ff158cf051b7a4b524b293c64
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 1%

---

# CRM에서 Experience Platform으로 데이터를 수집하는 데이터 흐름을 만듭니다.

데이터 흐름을 만들고 [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 Adobe Experience Platform으로 데이터를 수집하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [일괄 처리 수집](../../../../ingestion/batch-ingestion/overview.md): 대량의 데이터를 빠르고 효율적으로 일괄 업로드하는 방법을 알아봅니다.
* [카탈로그 서비스](../../../../catalog/datasets/overview.md): Experience Platform에서 데이터 세트를 구성하고 추적합니다.
* [데이터 준비](../../../../data-prep/home.md): 들어오는 데이터를 스키마 요구 사항과 일치하도록 변환하고 매핑합니다.
* [데이터 흐름](../../../../dataflows/home.md): 데이터를 소스에서 대상으로 이동하는 파이프라인을 설정하고 관리합니다.
* [XDM(경험 데이터 모델) 스키마](../../../../xdm/home.md): Experience Platform에서 사용할 수 있도록 XDM 스키마를 사용하여 데이터를 구조화합니다.
* [샌드박스](../../../../sandboxes/home.md): 프로덕션 데이터에 영향을 주지 않고 격리된 환경에서 안전하게 테스트하고 개발하십시오.
* [소스](../../../home.md): 외부 데이터 소스를 Experience Platform에 연결하는 방법을 알아봅니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 기본 연결 만들기 {#base}

소스에 대한 데이터 흐름을 만들려면 완전히 인증된 소스 계정과 해당 기본 연결 ID가 필요합니다. 이 ID가 없는 경우 [소스 카탈로그](../../../home.md)를 방문하여 기본 연결을 만들 수 있는 소스 목록을 찾으십시오.

### 대상 XDM 스키마 만들기 {#target-schema}

XDM(경험 데이터 모델) 스키마는 Experience Platform 내에서 고객 경험 데이터를 구성하고 설명하는 표준화된 방법을 제공합니다. 소스 데이터를 Experience Platform에 수집하려면 먼저 수집하려는 데이터의 구조와 유형을 정의하는 대상 XDM 스키마를 만들어야 합니다. 이 스키마는 수집된 데이터가 위치할 Experience Platform 데이터 세트에 대한 블루프린트 역할을 합니다.

[스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 안내서를 참조하십시오.

* [API를 사용하여 스키마를 만듭니다](../../../../xdm/api/schemas.md).
* [UI를 사용하여 스키마를 만듭니다](../../../../xdm/tutorials/create-schema-ui.md).

만든 후에는 대상 데이터 세트 및 매핑에 대상 XDM 스키마 `$id`이(가) 필요합니다.

### 타겟 데이터 세트 만들기 {#target-dataset}

데이터 집합은 일반적으로 열(스키마) 및 행(필드)이 있는 테이블처럼 구성된 데이터 수집을 위한 저장 및 관리 구성입니다. Experience Platform에 성공적으로 수집된 데이터는 데이터 세트로 데이터 레이크 내에 저장됩니다. 이 단계에서는 새 데이터 세트를 만들거나 기존 데이터 세트를 사용할 수 있습니다.

페이로드 내에 대상 스키마의 ID를 제공하면서 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 하여 대상 데이터 집합을 만들 수 있습니다. 대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../catalog/api/create-dataset.md)에 대한 안내서를 참조하십시오.

>[!TIP]
>
>데이터를 실시간 고객 프로필로 수집하려면 대상 XDM 스키마와 대상 데이터 세트가 모두 프로필에 대해 활성화되었는지 확인해야 합니다.

+++예를 보려면 선택

**API 형식**

```HTTP
POST /dataSets
```

**요청**

다음 예제에서는 실시간 고객 프로필 수집을 위해 활성화된 타겟 데이터 세트를 만드는 방법을 보여줍니다. 이 요청에서 `unifiedProfile` 속성이 `true` 개체 아래의 `tags`(으)로 설정되어 Experience Platform에 실시간 고객 프로필에 데이터 세트를 포함하도록 지시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 대상 데이터 세트에 대한 수사적 이름입니다. 명확하고 고유한 이름을 사용하여 향후 작업에서 데이터 세트를 보다 쉽게 식별하고 관리할 수 있습니다. |
| `schemaRef.id` | 대상 XDM 스키마의 ID입니다. |
| `tags.unifiedProfile` | Experience Platform에 데이터를 실시간 고객 프로필로 수집해야 하는지 여부를 알려주는 부울 값입니다. |

**응답**

성공적인 응답은 대상 데이터 세트의 ID를 반환합니다. 이 ID는 나중에 대상 연결을 만드는 데 필요합니다.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## 소스 연결 만들기 {#source}

소스 연결은 외부 소스에서 Experience Platform으로 데이터를 가져오는 방법을 정의합니다. 소스 시스템과 들어오는 데이터의 형식을 모두 지정하며 인증 세부 정보를 포함하는 기본 연결을 참조합니다. 각 소스 연결은 조직에 고유합니다.

* 파일 기반 소스(예: 클라우드 저장소)의 경우 소스 연결에는 열 구분 기호, 인코딩 유형, 압축 유형, 파일 선택을 위한 정규 표현식 및 파일을 재귀적으로 수집할지 여부 등의 설정이 포함될 수 있습니다.
* 테이블 기반 소스(예: 데이터베이스, CRM 및 마케팅 자동화 공급자)의 경우 소스 연결에서 테이블 이름 및 열 매핑과 같은 세부 사항을 지정할 수 있습니다.

소스 연결을 만들려면 `/sourceConnections` API의 [!DNL Flow Service] 끝점에 대한 POST 요청을 만들고 기본 연결 ID, 연결 사양 ID 및 소스 데이터 파일에 대한 경로를 제공합니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME source connection",
    "description": "A source connection for ACME contact data",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ]
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결을 설명하는 이름입니다. 명확하고 고유한 이름을 사용하여 향후 작업에서 연결을 보다 쉽게 식별하고 관리할 수 있습니다. |
| `description` | 소스 연결에 대한 추가 정보를 제공하기 위해 추가할 수 있는 선택적 설명입니다. |
| `baseConnectionId` | 기본 연결의 `id`입니다. [!DNL Flow Service] API를 사용하여 Experience Platform에 대한 소스를 인증하여 이 ID를 검색할 수 있습니다. |
| `data.format` | 데이터의 형식입니다. 테이블 기반 원본(예: 데이터베이스, CRM 및 마케팅 자동화 공급자)에 대해 이 값을 `tabular`(으)로 설정하십시오. |
| `params.tableName` | Experience Platform으로 수집할 소스 계정의 테이블 이름입니다. |
| `params.columns` | Experience Platform에 수집할 데이터의 특정 테이블 열입니다. |
| `connectionSpec.id` | 사용 중인 소스의 연결 사양 ID입니다. |

**응답**

성공한 응답은 소스 연결의 ID를 반환합니다. 이 ID는 데이터 흐름을 만들고 데이터를 수집하는 데 필요합니다.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 대상 연결 만들기 {#target}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다.

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 대상 연결을 설명하는 이름입니다. 명확하고 고유한 이름을 사용하여 향후 작업에서 연결을 보다 쉽게 식별하고 관리할 수 있습니다. |
| `description` | 대상 연결에 대한 추가 정보를 제공하기 위해 추가할 수 있는 선택적 설명입니다. |
| `data.schema.id` | 대상 XDM 스키마의 ID입니다. |
| `params.dataSetId` | 대상 데이터 세트의 ID입니다. |
| `connectionSpec.id` | 데이터 레이크의 연결 사양 ID입니다. 이 ID는 수정되었습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## 매핑 {#mapping}

그런 다음 소스 데이터를 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑합니다. 매핑을 만들려면 `mappingSets`API[[!DNL Data Prep] 의 ](https://developer.adobe.com/experience-platform-apis/references/data-prep/) 끝점에 대한 POST 요청을 만듭니다. 대상 XDM 스키마 ID와 만들려는 매핑 세트에 대한 세부 사항을 포함합니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "destinationXdmPath": "_id",
              "sourceAttribute": "TestID",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.fullName",
              "sourceAttribute": "Name",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.birthDate",
              "sourceAttribute": "Datefield",
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
| `xdmSchema` | 대상 XDM 스키마의 `$id`. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 데이터 흐름 사양 검색 {#flow-specs}

데이터 흐름을 만들려면 먼저 소스에 해당하는 데이터 흐름 사양을 검색해야 합니다. 이 정보를 검색하려면 `/flowSpecs` API의 [!DNL Flow Service] 끝점에 대한 GET 요청을 만드십시오.

**API 형식**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `property=name=="{NAME}"` | 데이터 흐름 사양의 이름입니다. <ul><li>파일 기반 소스(예: 클라우드 저장소)의 경우 이 값을 `CloudStorageToAEP`(으)로 설정하십시오.</li><li>테이블 기반 소스(예: 데이터베이스, CRM 및 마케팅 자동화 공급자)의 경우 이 값을 `CRMToAEP`(으)로 설정합니다.</li></ul> |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 소스에서 Experience Platform으로 데이터를 가져오는 역할을 하는 데이터 흐름 사양의 세부 정보를 반환합니다. 응답에는 새 데이터 흐름을 만드는 데 필요한 고유한 흐름 사양 `id`이(가) 포함되어 있습니다.

올바른 데이터 흐름 사양을 사용하고 있는지 확인하려면 응답에서 `items.sourceConnectionSpecIds` 배열을 확인하십시오. 소스에 대한 연결 사양 ID가 이 목록에 포함되어 있는지 확인합니다.

+++보려면 선택

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "runSpec": {
                "name": "ProviderParams",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines various params required for creating flow run.",
                    "properties": {
                        "startTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
                        },
                        "windowStartTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "windowEndTime": {
                            "type": "integer",
                            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "deltaColumn": {
                            "type": "object",
                            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
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
                        "startTime",
                        "windowStartTime",
                        "windowEndTime",
                        "deltaColumn"
                    ]
                }
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## 데이터 흐름 만들기 {#dataflow}

데이터 흐름은 Experience Platform 서비스 간에 데이터를 전송하는 구성된 파이프라인입니다. 데이터가 외부 소스(예: 데이터베이스, 클라우드 스토리지 또는 API)에서 수집되고, 처리되고, 대상 데이터 세트로 라우팅되는 방법을 정의합니다. 그런 다음 활성화 및 분석을 위해 ID 서비스, 실시간 고객 프로필 및 대상 과 같은 서비스에서 이러한 데이터 세트를 사용합니다.

데이터 흐름을 만들려면 다음 항목에 대한 값을 제공해야 합니다.

* [Source 연결 ID](#source)
* [대상 연결 ID](#target)
* [ID 매핑](#mapping)
* [데이터 흐름 사양 ID](#flow-specs)

이 단계에서는 `scheduleParams`에서 다음 매개 변수를 사용하여 데이터 흐름에 대한 수집 일정을 구성할 수 있습니다.

| 예약 매개 변수 | 설명 |
| --- | --- |
| `startTime` | 데이터 흐름이 시작되어야 하는 에포크 시간(초)입니다. |
| `frequency` | 수집 빈도. 데이터 흐름이 실행되는 빈도를 구성하십시오. 빈도를 다음과 같이 설정할 수 있습니다. <ul><li>`once`: 빈도를 `once`(으)로 설정하여 일회성 수집을 만듭니다. 간격 및 채우기 설정은 일회성 수집 작업에 사용할 수 없습니다. 기본적으로 예약 빈도는 한 번으로 설정됩니다.</li><li>`minute`: 빈도를 `minute`(으)로 설정하여 분 단위로 데이터를 수집하도록 데이터 흐름을 예약합니다.</li><li>`hour`: 빈도를 `hour`(으)로 설정하여 시간당 기준으로 데이터를 수집하도록 데이터 흐름을 예약합니다.</li><li>`day`: 빈도를 `day`(으)로 설정하여 하루 단위로 데이터를 수집하도록 데이터 흐름을 예약합니다.</li><li>`week`: 주별로 데이터를 수집하도록 데이터 흐름을 예약하려면 빈도를 `week`(으)로 설정하십시오.</li></ul> |
| `interval` | 연속 수집 사이의 간격입니다(`once`을(를) 제외한 모든 빈도에 필요). 간격 설정을 구성하여 모든 수집 사이에 시간대를 설정합니다. 예를 들어 빈도를 일로 설정하고 간격을 15로 설정하면 데이터 흐름이 15일마다 실행됩니다. 간격을 0으로 설정할 수 없습니다. 각 주파수에 대해 허용되는 최소 간격 값은 다음과 같습니다.<ul><li>`once`: 해당 없음</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | `startTime` 전에 이전 데이터를 수집할지 여부를 나타냅니다. |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
      "flowSpec": {
          "id": "14518937-270c-4525-bdec-c2ba7cce3860",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "b7581b59-c603-4df1-a689-d23d7ac440f3"
      ],
      "targetConnectionIds": [
          "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
      ],
      "transformations": [
          {
              "name": "Copy",
              "params": {
                  "deltaColumn": {
                      "name": "Datefield",
                      "dateFormat": "YYYY-MM-DD",
                      "timezone": "UTC"
                  }
              }
          },
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1612310466",
          "frequency":"minute",
          "interval":"15",
          "backfill": "true"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름을 설명하는 이름입니다. 명확하고 고유한 이름을 사용하여 향후 작업에서 데이터 흐름을 보다 쉽게 식별하고 관리할 수 있습니다. |
| `description` | 데이터 흐름에 추가 정보를 제공하기 위해 추가할 수 있는 선택적 설명입니다. |
| `flowSpec.id` | 소스에 해당하는 흐름 사양의 ID입니다. |
| `sourceConnectionIds` | 이전 단계에서 생성된 소스 연결 ID입니다. |
| `targetConnectionIds` | 이전 단계에서 생성된 대상 연결 ID입니다. |
| `transformations.params.deltaColum` | 새 데이터와 기존 데이터를 구분하는 데 사용되는 지정된 열입니다. 증분 데이터는 선택한 열의 타임스탬프를 기반으로 수집됩니다. `deltaColumn`에 지원되는 형식은 `yyyy-MM-dd HH:mm:ss`입니다. [!DNL Microsoft Dynamics]의 경우 `deltaColumn`에 지원되는 형식은 `yyyy-MM-ddTHH:mm:ssZ`입니다. |
| `transformations.params.deltaColumn.dateFormat` | 델타 열에 따를 날짜 형식입니다. |
| `transformations.params.deltaColumn.timeZone` | 델타 열의 값을 해석할 때 사용할 시간대입니다. |
| `transformations.params.mappingId` | 이전 단계에서 생성된 매핑 ID. |
| `scheduleParams.startTime` | epoch 시간 단위 데이터 흐름의 시작 시간(Unix epoch 이후 초)입니다. 데이터 흐름이 첫 번째 실행을 시작하는 시기를 결정합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 실행되는 빈도입니다. 허용되는 값은 `once`, `minute`, `hour`, `day` 또는 `week`입니다. |
| `scheduleParams.interval` | 선택한 빈도를 기반으로 연속 데이터 흐름 실행 사이의 간격을 설정합니다. 0이 아닌 정수여야 합니다. 예를 들어 빈도를 분으로 설정하고 간격을 15로 설정하면 데이터 흐름이 15분마다 실행됩니다. |
| `scheduleParams.backfill` | 데이터 흐름을 처음 만들 때 기록 데이터(채우기)를 수집할지 여부를 결정하는 부울 값(`true` 또는 `false`)입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### UI를 사용하여 API 워크플로의 유효성을 검사합니다 {#validate-in-ui}

Experience Platform 사용자 인터페이스를 사용하여 데이터 흐름 생성의 유효성을 검사할 수 있습니다. Experience Platform UI에서 *[!UICONTROL 소스]* 카탈로그로 이동한 다음 헤더 탭에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다. 그런 다음 [!UICONTROL 데이터 흐름 이름] 열을 사용하고 [!DNL Flow Service] API를 사용하여 만든 데이터 흐름을 찾습니다.

![Experience Platform UI에서 원본 작업 영역의 데이터 흐름 인터페이스](../../../images/tutorials/validations/dataflows-interface.png)

[!UICONTROL 데이터 흐름 활동] 인터페이스를 통해 데이터 흐름의 유효성을 추가로 확인할 수 있습니다. 오른쪽 레일을 사용하여 데이터 흐름의 [!UICONTROL API 사용] 정보를 봅니다. 이 섹션에는 [!DNL Flow Service]에서 데이터 흐름 만들기 프로세스 중에 생성된 동일한 데이터 흐름 ID, 데이터 집합 ID 및 매핑 ID가 표시됩니다.

![원본 작업 영역의 데이터 흐름 보기 페이지입니다.](../../../images/tutorials/validations/api-usage.png)

## 다음 단계

이 튜토리얼에서는 [!DNL Flow Service] API를 사용하여 Experience Platform에서 데이터 흐름을 만드는 과정을 안내했습니다. 대상 XDM 스키마, 데이터 세트, 소스 연결, 대상 연결 및 데이터 흐름 자체를 포함하여 필요한 구성 요소를 만들고 구성하는 방법에 대해 배웠습니다. 이러한 단계를 수행하면 외부 소스에서 Experience Platform으로 데이터 수집을 자동화하여 실시간 고객 프로필 및 대상과 같은 다운스트림 서비스에서 수집된 데이터를 고급 사용 사례에 활용할 수 있습니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 Experience Platform UI에서 직접 성능을 모니터링할 수 있습니다. 여기에는 수집 비율, 성공 지표 및 발생하는 모든 오류 추적이 포함됩니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [계정 및 데이터 흐름 모니터링](../../../../dataflows/ui/monitor-sources.md)에 대한 자습서를 참조하십시오.

### 데이터 흐름 업데이트

데이터 흐름 예약, 매핑 또는 일반 정보에 대한 구성을 업데이트하려면 [원본 데이터 흐름 업데이트](../../api/update-dataflows.md)의 자습서를 참조하십시오.

## 데이터 흐름 삭제

**[!UICONTROL 데이터 흐름]** 작업 영역에서 사용할 수 있는 **[!UICONTROL Delete]** 함수를 사용하여 더 이상 필요하지 않거나 잘못 만들어진 데이터 흐름을 삭제할 수 있습니다. 데이터 흐름을 삭제하는 방법에 대한 자세한 내용은 [데이터 흐름 삭제](../../api/delete.md)에 대한 자습서를 참조하십시오.
