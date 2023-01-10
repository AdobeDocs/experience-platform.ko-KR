---
keywords: Experience Platform;홈;인기 항목;클라우드 스토리지 데이터
solution: Experience Platform
title: Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기
type: Tutorial
description: 이 자습서에서는 소스 커넥터 및 API를 사용하여 타사 클라우드 저장소에서 데이터를 검색하고 Platform으로 가져오는 단계를 설명합니다.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 1%

---

# 를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기 [!DNL Flow Service] API

이 자습서에서는 클라우드 스토리지 소스에서 데이터를 검색하고 다음을 사용하여 Platform으로 가져오는 단계를 설명합니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>데이터 흐름을 만들려면 이미 클라우드 저장소 소스와 유효한 기본 연결 ID가 있어야 합니다. 이 ID가 없다면 다음을 참조하십시오. [소스 개요](../../../home.md#cloud-storage) 을 사용하여 기본 연결을 만들 수 있는 클라우드 스토리지 소스 목록입니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 작성 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   - [스키마 레지스트리 개발자 안내서](../../../../xdm/api/getting-started.md): 스키마 레지스트리 API 호출을 성공적으로 수행하기 위해 알고 있어야 하는 중요한 정보를 포함합니다. 여기에는 다음이 포함됩니다 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청을 수행하는 데 필요한 헤더입니다(Accept 헤더와 가능한 값에 특별히 주의).
- [[!DNL Catalog Service]](../../../../catalog/home.md): 카탈로그는 Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): 배치 수집 API를 사용하면 데이터를 배치 파일로 Experience Platform에 수집할 수 있습니다.
- [샌드박스](../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../landing/api-guide.md).

## 소스 연결 만들기 {#source}

에 POST 요청을 수행하여 소스 연결을 만들 수 있습니다 `sourceConnections` 끝점 [!DNL Flow Service] 기본 연결 ID, 수집할 소스 파일의 경로 및 소스의 해당 연결 사양 ID를 제공하는 동안 API입니다.

소스 연결을 만들 때 데이터 형식 속성에 대한 열거형 값도 정의해야 합니다.

파일 기반 소스에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분 기호 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 소스의 경우 값을 `tabular`.

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
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `baseConnectionId` | 클라우드 스토리지 소스의 기본 연결 ID입니다. |
| `data.format` | Platform으로 가져올 데이터의 형식입니다. 지원되는 값은 다음과 같습니다. `delimited`, `JSON`, 및 `parquet`. |
| `data.properties` | (선택 사항) 소스 연결을 만드는 동안 데이터에 적용할 수 있는 속성 세트입니다. |
| `data.properties.columnDelimiter` | (선택 사항) 플랫 파일을 수집할 때 지정할 수 있는 단일 문자 열 구분 기호입니다. 단일 문자 값은 허용 열 구분 기호입니다. 지정하지 않으면 쉼표( )를 입력합니다`,`)가 기본값으로 사용됩니다. **참고**: 다음 `columnDelimiter` 속성은 구분된 파일을 수집할 때만 사용할 수 있습니다. |
| `data.properties.encoding` | (선택 사항) 데이터를 Platform에 수집할 인코딩 유형을 정의하는 속성입니다. 지원되는 인코딩 유형은 다음과 같습니다. `UTF-8` 및 `ISO-8859-1`. **참고**: 다음 `encoding` 매개 변수는 구분된 CSV 파일을 수집할 때만 사용할 수 있습니다. 다른 파일 유형은 기본 인코딩으로 수집됩니다. `UTF-8`. |
| `data.properties.compressionType` | (선택 사항) 수집을 위한 압축 파일 유형을 정의하는 속성입니다. 지원되는 압축 파일 유형은 다음과 같습니다. `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, 및 `tar`. **참고**: 다음 `compressionType` 속성은 구분된 또는 JSON 파일을 수집할 때만 사용할 수 있습니다. |
| `params.path` | 액세스하는 소스 파일의 경로입니다. 이 매개 변수는 개별 파일 또는 전체 폴더를 가리킵니다.  **참고**: 파일 이름 대신 별표를 사용하여 전체 폴더의 수집을 지정할 수 있습니다. 예: `/acme/summerCampaign/*.csv` 전체 `/acme/summerCampaign/` 폴더를 입력합니다. |
| `params.type` | 수집 중인 소스 데이터 파일의 파일 유형입니다. 유형 사용 `file` 개별 파일을 수집하고 유형을 사용하려면 `folder` 전체 폴더를 수집하려면 다음을 수행하십시오. |
| `connectionSpec.id` | 특정 클라우드 스토리지 소스와 연결된 연결 사양 ID입니다. 자세한 내용은 [부록](#appendix) 연결 사양 ID 목록 |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 정규 표현식을 사용하여 수집을 위한 특정 파일 세트를 선택합니다 {#regex}

소스 연결을 만들 때 정규 표현식을 사용하여 소스에서 플랫폼으로 특정 파일 세트를 수집할 수 있습니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

아래 예에서는 파일 경로에 정규 표현식을 사용하여 모든 CSV 파일에 대한 수집을 지정합니다 `premium` 이름.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### 데이터를 재귀적으로 수집하도록 소스 연결 구성

소스 연결을 만들 때 `recursive` 깊이 중첩된 폴더에서 데이터를 수집할 매개 변수입니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

아래 예에서는 `recursive: true` 매개 변수 정보 [!DNL Flow Service] 수집 프로세스 중에 모든 하위 폴더를 재귀적으로 읽습니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## 대상 XDM 스키마 만들기 {#target-schema}

Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

대상 XDM 스키마는에 대한 POST 요청을 수행하여 만들 수 있습니다 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](../../../../xdm/api/schemas.md).

## 대상 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 대상 데이터 세트를 만들 수 있습니다 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공하는 것이 좋습니다.

대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../catalog/api/create-dataset.md).

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에서 대상 데이터 세트와 데이터 레이크에 대한 연결 사양 ID의 고유 식별자가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `data.schema.id` | 다음 `$id` 대상 XDM 스키마 중 하나입니다. |
| `data.schema.version` | 스키마 버전입니다. 이 값을 설정해야 합니다. `application/vnd.adobe.xed-full+json;version=1`는 스키마의 최신 부 버전을 반환합니다. |
| `params.dataSetId` | 대상 데이터 세트의 ID입니다. |
| `connectionSpec.id` | 데이터 레이크에 대한 고정 연결 사양 ID입니다. 이 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`). 이 ID는 이후 단계에서 필요합니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다.

매핑 세트를 만들려면, `mappingSets` 의 끝점 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) target XDM 스키마를 제공하는 동안 `$id` 생성하려는 매핑 세트의 세부 정보를 표시합니다.

>[!TIP]
>
>클라우드 저장소 소스 커넥터를 사용하여 JSON 파일의 배열과 같은 복잡한 데이터 유형을 매핑할 수 있습니다.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 값은 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 데이터 흐름 사양 검색 {#specs}

데이터 흐름은 소스에서 데이터를 수집하여 플랫폼으로 가져와야 합니다. 데이터 흐름을 만들려면 먼저 클라우드 스토리지 데이터 수집을 담당하는 데이터 흐름 사양을 가져와야 합니다.

**API 형식**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>아래의 JSON 응답 페이로드는 간결성을 위해 숨겨져 있습니다. 응답 페이로드를 보려면 &quot;페이로드&quot;를 선택합니다.

+++ 페이로드 보기

**응답**

성공적인 응답은 소스에서 플랫폼으로 데이터를 가져오는 데이터 흐름 사양의 세부 정보를 반환합니다. 응답에는 고유한 흐름 세부 사항이 포함됩니다 `id` 새 데이터 흐름을 만드는 데 필요합니다.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
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
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## 데이터 흐름 만들기

클라우드 스토리지 데이터를 수집하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 현재까지는 다음 필수 값이 준비되었습니다.

- [소스 연결 ID](#source)
- [Target 연결 ID](#target)
- [매핑 ID](#mapping)
- [데이터 흐름 사양 ID](#specs)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에서 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

>[!NOTE]
>
>다음의 모든 데이터 흐름에서는 일괄 처리를 위해 해당 파일을 기반으로 소스에서 수집할 파일을 선택합니다 **마지막 수정 날짜** timestamp. 즉, 일괄 처리 데이터 흐름은 마지막 데이터 흐름 실행 이후 새로 만들거나 수정한 소스에서 파일을 선택합니다.

수집을 예약하려면 먼저 시작 시간 값을 초 단위로 설정해야 합니다. 그런 다음 빈도 값을 다섯 가지 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`, 또는 `week`. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하고 1회 수집을 만들 때에는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 같거나 그 이상으로 설정해야 합니다 `15`.

>[!IMPORTANT]
>
>데이터 흐름을 사용할 때 일회성 수집으로 예약하는 것이 좋습니다 [FTP 커넥터](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `flowSpec.id` | 다음 [흐름 사양 ID](#specs) 이전 단계에서 검색됨. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source) 이전 단계에서 검색됨. |
| `targetConnectionIds` | 다음 [target 연결 ID](#target-connection) 이전 단계에서 검색됨. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 검색됨. |
| `scheduleParams.startTime` | epoch 시간의 데이터 흐름의 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름에서 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도가 로 설정된 경우 간격이 필요하지 않습니다 `once` 및 보다 크거나 같아야 합니다. `15` 다른 주파수 값에 사용할 수 있습니다. |

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름을 만든 후에는 데이터 흐름을 통해 수집 중인 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 다음 내용을 참조하십시오 [API에서 데이터 흐름 모니터링](../monitor.md)

## 다음 단계

이 자습서에 따라 예약된 대로 클라우드 스토리지에서 데이터를 수집하기 위한 소스 커넥터를 만들었습니다. 이제 와 같은 다운스트림 Platform 서비스에서 들어오는 데이터를 사용할 수 있습니다. [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../profile/home.md)
- [Data Science Workspace 개요](../../../../data-science-workspace/home.md)

## 부록 {#appendix}

다음 섹션에는 다양한 클라우드 스토리지 소스 커넥터 및 해당 연결 사양이 나와 있습니다.

### 연결 사양

| 커넥터 이름 | 연결 사양 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (이벤트 허브) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
