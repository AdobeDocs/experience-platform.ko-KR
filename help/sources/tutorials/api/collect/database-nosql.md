---
title: 흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 데이터 흐름을 만들고 데이터베이스에서 Experience Platform으로 데이터를 수집하는 방법을 알아봅니다.
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: b4f8d44c3ce9507ff158cf051b7a4b524b293c64
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 데이터베이스 원본에 대한 데이터 흐름 만들기

데이터 흐름을 만들고 [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 데이터베이스에서 Adobe Experience Platform으로 데이터를 수집하는 방법을 알아보려면 이 자습서를 참조하십시오.

>[!NOTE]
>
>* 데이터 흐름을 만들려면 데이터베이스 원본의 올바른 기본 연결 ID가 이미 있어야 합니다. 이 ID가 없는 경우 [소스 카탈로그](../../../home.md#database)를 방문하여 기본 연결을 만들 수 있는 데이터베이스 원본 목록을 보십시오.
>* Experience Platform이 데이터를 수집하려면 모든 테이블 기반 배치 소스의 시간대를 UTC로 구성해야 합니다. [[!DNL Snowflake] source](../../../connectors/databases/snowflake.md)에 대해 지원되는 타임스탬프는 UTC 시간이 있는 TIMESTAMP_NTZ뿐입니다.

## 시작

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 레지스트리 개발자 안내서](../../../../xdm/api/getting-started.md): 스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보가 포함되어 있습니다. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청을 하는 데 필요한 헤더가 포함됩니다(Accept 헤더 및 가능한 값에 특별한 주의를 기울임).
* [[!DNL Catalog Service]](../../../../catalog/home.md): 카탈로그는 Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): 일괄 처리 수집 API를 사용하면 데이터를 일괄 처리 파일로 Experience Platform에 수집할 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 소스 연결 만들기 {#source}

[!DNL Flow Service] API에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 커넥터에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분됨 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 커넥터의 경우 값을 `tabular`(으)로 설정합니다.

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
    "name": "Database source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "Database source connection",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "test1.Mytable",
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
      ],
      "cdcEnabled": true
    },
    "connectionSpec": {
      "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
      "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 데이터베이스 소스의 연결 ID입니다. |
| `params.tableName` | 소스 파일의 경로입니다. |
| `params.cdcEnabled` | 변경 내역 캡처를 사용할지 여부를 나타내는 부울 값입니다. 이 속성은 다음 데이터베이스 소스에서 지원됩니다. <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> 자세한 내용은 [소스에서 데이터 캡처 변경](../change-data-capture.md)을 사용하는 방법에 대한 안내서를 참조하십시오. |
| `connectionSpec.id` | 데이터베이스 소스의 연결 사양 ID입니다. 데이터베이스 사양 ID 목록은 [부록](#appendix)을 참조하십시오. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 대상 연결을 만드는 이후 단계에서 필요합니다.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 Experience Platform에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Experience Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오.

## 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하여 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다.

이제 타겟 스키마에 대한 고유 식별자, 타겟 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. [!DNL Flow Service] API를 사용하면 인바운드 원본 데이터를 포함할 데이터 세트와 함께 이러한 식별자를 지정하여 대상 연결을 만들 수 있습니다.

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
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `data.schema.id` | 대상 XDM 스키마의 `$id`. |
| `data.schema.version` | 스키마의 버전입니다. 이 값은 스키마의 최신 부 버전을 반환하는 `application/vnd.adobe.xed-full+json;version=1`(으)로 설정해야 합니다. |
| `params.dataSetId` | 이전 단계에서 생성된 대상 데이터 세트의 ID입니다. **참고**: 대상 연결을 만들 때 올바른 데이터 세트 ID를 제공해야 합니다. 잘못된 데이터 세트 ID로 인해 오류가 발생합니다. |
| `connectionSpec.id` | 데이터 레이크에 연결하는 데 사용되는 연결 사양 ID입니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다.

매핑 세트를 만들려면 대상 XDM 스키마 `mappingSets`과(와) 만들려는 매핑 세트의 세부 정보를 제공하는 동안 [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)의 `$id` 끝점에 대한 POST 요청을 수행하십시오.

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
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 데이터 흐름 사양 검색 {#specs}

데이터 흐름은 소스에서 데이터를 수집하고 Experience Platform으로 가져오는 역할을 합니다. 데이터 흐름을 만들려면 먼저 [!DNL Flow Service] API에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다. 데이터 흐름 사양은 외부 데이터베이스 또는 NoSQL 시스템에서 데이터를 수집하는 역할을 합니다.

**API 형식**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

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

>[!NOTE]
>
>간결성을 위해 아래의 JSON 응답 페이로드가 숨겨집니다. 응답 페이로드를 보려면 &quot;페이로드&quot;를 선택합니다.

+++ 페이로드 보기

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
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
    "221c7626-58f6-4eec-8ee2-042b0226f03b",
    "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
    "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
    "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
    "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
    "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
    "102706fb-a5cd-42ee-afe0-bc42f017ff43",
    "09182899-b429-40c9-a15a-bf3ddbc8ced7",
    "0479cc14-7651-4354-b233-7480606c2ac3",
    "d6b52d86-f0f8-475f-89d4-ce54c8527328",
    "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
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
  "transformationSpec": [
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
    }
}
```

+++

## 데이터 흐름 만들기

데이터 수집을 위한 마지막 단계는 데이터 흐름을 만드는 것입니다. 이 시점에서 다음 필수 값을 준비해야 합니다.

* [Source 연결 ID](#source)
* [대상 연결 ID](#target)
* [ID 매핑](#mapping)
* [데이터 흐름 사양 ID](#specs)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 요청 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 `once`, `minute`, `hour`, `day` 또는 `week` 옵션 중 하나로 설정해야 합니다. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하며 1회 수집을 만들 때 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 `15`보다 크거나 같게 설정해야 합니다.

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
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
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
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
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

+++

| 속성 | 설명 |
| -------- | ----------- |
| `flowSpec.id` | 이전 단계에서 검색된 [흐름 사양 ID](#specs)입니다. |
| `sourceConnectionIds` | 이전 단계에서 [원본 연결 ID](#source)을(를) 검색했습니다. |
| `targetConnectionIds` | 이전 단계에서 [대상 연결 ID](#target-connection)을(를) 검색했습니다. |
| `transformations.params.mappingId` | [매핑 ID](#mapping)이(가) 이전 단계에서 검색되었습니다. |
| `transformations.params.deltaColum` | 새 데이터와 기존 데이터를 구분하는 데 사용되는 지정된 열입니다. 증분 데이터는 선택한 열의 타임스탬프를 기반으로 수집됩니다. `deltaColumn`에 지원되는 날짜 형식은 `yyyy-MM-dd HH:mm:ss`입니다. Azure 테이블 저장소를 사용하는 경우 `deltaColumn`에 지원되는 형식은 `yyyy-MM-ddTHH:mm:ssZ`입니다. |
| `transformations.params.mappingId` | 데이터베이스와 연계된 매핑 ID. |
| `scheduleParams.startTime` | epoch 시간 내 데이터 흐름의 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 `once`, `minute`, `hour`, `day` 또는 `week`입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 각 주파수에 대해 허용되는 최소 간격 값은 다음과 같습니다.<ul><li>**한 번**: 해당 없음</li><li>**분**: 15</li><li>**시간**: 1</li><li>**일**: 1</li><li>**주**: 1</li></ul> |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [API에서 데이터 흐름 모니터링](../monitor.md)에 대한 자습서를 참조하십시오.

## 다음 단계

이 자습서에 따라 일정에 따라 데이터베이스에서 데이터를 수집하는 소스 커넥터를 만들었습니다. 이제 [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]과(와) 같은 다운스트림 Experience Platform 서비스에서 수신 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../profile/home.md)
* [데이터 과학 작업 영역 개요](../../../../data-science-workspace/home.md)

## 부록

다음 섹션에서는 다양한 클라우드 스토리지 소스 커넥터와 해당 연결 사양을 나열합니다.

### 연결 사양

| 커넥터 이름 | 연결 사양 ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive]의 [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark]의 [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |
