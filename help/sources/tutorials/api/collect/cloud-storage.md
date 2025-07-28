---
keywords: Experience Platform;홈;인기 항목;클라우드 스토리지 데이터
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기
type: Tutorial
description: 이 자습서에서는 소스 커넥터 및 API를 사용하여 서드파티 클라우드 스토리지에서 데이터를 검색하고 Experience Platform으로 가져오는 단계를 다룹니다.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: b184319f6c5f5430a5ae1e9de4728b5074bca9b8
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 클라우드 저장소 원본에 대한 데이터 흐름을 만듭니다.

이 튜토리얼에서는 클라우드 저장소 원본에서 데이터를 검색하고 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)을(를) 사용하여 Experience Platform으로 가져오는 단계를 다룹니다.

>[!NOTE]
>
>데이터 흐름을 만들려면 클라우드 스토리지 소스의 유효한 기본 연결 ID가 이미 있어야 합니다. 이 ID가 없는 경우 [소스 개요](../../../home.md#cloud-storage)에서 기본 연결을 만들 수 있는 클라우드 저장소 소스 목록을 참조하십시오.

## 시작

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 레지스트리 개발자 안내서](../../../../xdm/api/getting-started.md): 스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보가 포함되어 있습니다. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청을 하는 데 필요한 헤더가 포함됩니다(Accept 헤더 및 가능한 값에 특별한 주의를 기울임).
- [[!DNL Catalog Service]](../../../../catalog/home.md): 카탈로그는 Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): 일괄 처리 수집 API를 사용하면 데이터를 일괄 처리 파일로 Experience Platform에 수집할 수 있습니다.
- [샌드박스](../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 소스 연결 만들기 {#source}

기본 연결 ID, 수집할 소스 파일의 경로 및 소스의 해당 연결 사양 ID를 제공하는 동안 `sourceConnections` API의 [!DNL Flow Service] 끝점에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다.

소스 연결을 만들 때 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 소스에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분됨 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 원본의 경우 값을 `tabular`(으)로 설정하십시오.

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
          "type": "file",
          "cdcEnabled": true
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
| `data.format` | Experience Platform으로 가져올 데이터의 형식입니다. 지원되는 값은 `delimited`, `JSON` 및 `parquet`입니다. |
| `data.properties` | (선택 사항) 소스 연결을 만드는 동안 데이터에 적용할 수 있는 속성 세트입니다. |
| `data.properties.columnDelimiter` | (선택 사항) 플랫 파일을 수집할 때 지정할 수 있는 단일 문자 열 구분 기호입니다. 모든 단일 문자 값은 허용되는 열 구분 기호입니다. 지정하지 않으면 쉼표(`,`)가 기본값으로 사용됩니다. **참고**: `columnDelimiter` 속성은 구분된 파일을 수집할 때만 사용할 수 있습니다. |
| `data.properties.encoding` | (선택 사항) 데이터를 Experience Platform에 수집할 때 사용할 인코딩 유형을 정의하는 속성입니다. 지원되는 인코딩 유형은 `UTF-8` 및 `ISO-8859-1`입니다. **참고**: `encoding` 매개 변수는 구분된 CSV 파일을 수집할 때만 사용할 수 있습니다. 다른 파일 형식은 기본 인코딩 `UTF-8`을(를) 사용하여 수집됩니다. |
| `data.properties.compressionType` | (선택 사항) 수집을 위한 압축 파일 유형을 정의하는 속성입니다. 지원되는 압축 파일 형식은 `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` 및 `tar`입니다. **참고**: `compressionType` 속성은 구분된 파일 또는 JSON 파일을 수집할 때만 사용할 수 있습니다. |
| `params.path` | 액세스 중인 소스 파일의 경로입니다. 이 매개 변수는 개별 파일 또는 전체 폴더를 가리킵니다.  **참고**: 파일 이름 대신 별표를 사용하여 전체 폴더의 수집을 지정할 수 있습니다. 예를 들어 `/acme/summerCampaign/*.csv`은(는) 전체 `/acme/summerCampaign/` 폴더를 수집합니다. |
| `params.type` | 수집 중인 소스 데이터 파일의 파일 유형입니다. `file` 형식을 사용하여 개별 파일을 수집하고 `folder` 형식을 사용하여 전체 폴더를 수집합니다. |
| `params.cdcEnabled` | 변경 내역 캡처를 사용할지 여부를 나타내는 부울 값입니다. 이 속성은 다음 클라우드 스토리지 소스에서 지원됩니다. <ul><li>[!DNL Azure Blob]</li><li>[!DNL Data Landing Zone]</li><li>[!DNL Google Cloud Storage]</li><li>[!DNL SFTP]</li></ul> 자세한 내용은 [소스에서 데이터 캡처 변경](../change-data-capture.md)을 사용하는 방법에 대한 안내서를 참조하십시오. |
| `connectionSpec.id` | 특정 클라우드 스토리지 소스와 연결된 연결 사양 ID입니다. 연결 사양 ID 목록은 [부록](#appendix)을 참조하십시오. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 정규 표현식을 사용하여 수집할 특정 파일 세트를 선택합니다 {#regex}

소스 연결을 만들 때 정규 표현식을 사용하여 소스에서 Experience Platform으로 특정 파일 세트를 수집할 수 있습니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

아래 예에서 정규 표현식은 파일 경로에 `premium`이(가) 있는 모든 CSV 파일의 수집을 지정하는 데 사용됩니다.

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

소스 연결을 만들 때 `recursive` 매개 변수를 사용하여 깊게 중첩된 폴더에서 데이터를 수집할 수 있습니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

아래 예에서 `recursive: true` 매개 변수는 [!DNL Flow Service]에게 수집 프로세스 중에 모든 하위 폴더를 재귀적으로 읽도록 알립니다.

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

소스 데이터를 Experience Platform에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Experience Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오.

## 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하여 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 원본 데이터를 포함할 데이터 집합을 지정할 수 있습니다.

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
| `data.schema.id` | 대상 XDM 스키마의 `$id`. |
| `data.schema.version` | 스키마의 버전입니다. 이 값은 스키마의 최신 부 버전을 반환하는 `application/vnd.adobe.xed-full+json;version=1`(으)로 설정해야 합니다. |
| `params.dataSetId` | 이전 단계에서 생성된 대상 데이터 세트의 ID입니다. **참고**: 대상 연결을 만들 때 올바른 데이터 세트 ID를 제공해야 합니다. 잘못된 데이터 세트 ID로 인해 오류가 발생합니다. |
| `connectionSpec.id` | 데이터 레이크에 연결하는 데 사용되는 연결 사양 ID입니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다.

매핑 세트를 만들려면 대상 XDM 스키마 `mappingSets`과(와) 만들려는 매핑 세트의 세부 정보를 제공하는 동안 [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)의 `$id` 끝점에 대한 POST 요청을 수행하십시오.

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

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

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

데이터 흐름은 소스에서 데이터를 수집하고 이를 Experience Platform으로 가져오는 역할을 합니다. 데이터 흐름을 만들려면 먼저 클라우드 스토리지 데이터 수집을 담당하는 데이터 흐름 사양을 구해야 합니다.

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
>간결성을 위해 아래의 JSON 응답 페이로드가 숨겨집니다. 응답 페이로드를 보려면 &quot;페이로드&quot;를 선택합니다.

+++ 페이로드 보기

**응답**

성공적인 응답은 소스에서 Experience Platform으로 데이터를 가져오는 역할을 하는 데이터 흐름 사양의 세부 정보를 반환합니다. 응답에는 새 데이터 흐름을 만드는 데 필요한 고유한 흐름 사양 `id`이(가) 포함되어 있습니다.

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

클라우드 스토리지 데이터를 수집하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

- [Source 연결 ID](#source)
- [대상 연결 ID](#target)
- [ID 매핑](#mapping)
- [데이터 흐름 사양 ID](#specs)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

>[!NOTE]
>
>일괄 처리 수집을 위해 다음의 모든 데이터 흐름은 **마지막으로 수정한 날짜** 타임스탬프를 기반으로 소스에서 수집할 파일을 선택합니다. 즉, 일괄 처리 데이터 흐름은 마지막 데이터 흐름 실행 이후 새로 추가되었거나 수정된 파일을 소스에서 선택합니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 `once`, `minute`, `hour`, `day` 또는 `week` 옵션 중 하나로 설정해야 합니다. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하며 1회 수집을 만들 때 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 `15`보다 크거나 같게 설정해야 합니다.

>[!IMPORTANT]
>
>[FTP 커넥터](../../../connectors/cloud-storage/ftp.md)를 사용할 때 데이터 흐름을 일회성 수집으로 예약하는 것이 좋습니다.

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
        "name": "Cloud Storage flow to Experience Platform",
        "description": "Cloud Storage flow to Experience Platform",
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
| `flowSpec.id` | 이전 단계에서 검색된 [흐름 사양 ID](#specs)입니다. |
| `sourceConnectionIds` | 이전 단계에서 [원본 연결 ID](#source)을(를) 검색했습니다. |
| `targetConnectionIds` | 이전 단계에서 [대상 연결 ID](#target-connection)을(를) 검색했습니다. |
| `transformations.params.mappingId` | [매핑 ID](#mapping)이(가) 이전 단계에서 검색되었습니다. |
| `scheduleParams.startTime` | epoch 시간 내 데이터 흐름의 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 `once`, `minute`, `hour`, `day` 또는 `week`입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 각 주파수에 대해 허용되는 최소 간격 값은 다음과 같습니다.<ul><li>**한 번**: 해당 없음</li><li>**분**: 15</li><li>**시간**: 1</li><li>**일**: 1</li><li>**주**: 1</li></ul> |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [API에서 데이터 흐름 모니터링](../monitor.md)에 대한 자습서를 참조하십시오.

## 다음 단계

이 자습서에 따라 일정에 따라 클라우드 저장소에서 데이터를 수집하는 소스 커넥터를 만들었습니다. 이제 [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]과(와) 같은 다운스트림 Experience Platform 서비스에서 수신 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../profile/home.md)
- [데이터 과학 작업 영역 개요](../../../../data-science-workspace/home.md)

## 부록 {#appendix}

다음 섹션에서는 다양한 클라우드 스토리지 소스 커넥터와 해당 연결 사양을 나열합니다.

### 연결 사양

| 커넥터 이름 | 연결 사양 |
| -------------- | --------------- |
| [!DNL Amazon S3]&#x200B;(S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis]&#x200B;(Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob]&#x200B;(Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2]&#x200B;(ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs]&#x200B;(이벤트 허브) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
