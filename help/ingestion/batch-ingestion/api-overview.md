---
keywords: Experience Platform;홈;인기 항목;일괄 처리 수집;일괄 처리 수집;수집;개발자 안내서;api 안내서;업로드;Parquet 수집;JSON 수집;
solution: Experience Platform
title: 일괄 처리 수집 API 안내서
description: 이 문서에서는 Adobe Experience Platform용 일괄 처리 수집 API를 사용하는 개발자를 위한 포괄적인 안내서를 제공합니다.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '2435'
ht-degree: 4%

---

# 일괄 처리 수집 개발자 안내서

이 문서는 Adobe Experience Platform에서 [일괄 처리 수집 API 끝점](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)을 사용하는 방법에 대한 포괄적인 안내서를 제공합니다. 사전 요구 사항 및 모범 사례를 포함한 일괄 처리 수집 API에 대한 개요를 보려면 [일괄 처리 수집 API 개요](overview.md)를 읽는 것부터 시작하십시오.

이 문서의 부록에서는 샘플 CSV 및 JSON 데이터 파일을 포함하여 [수집에 사용할 데이터 서식 지정](#data-transformation-for-batch-ingestion)에 대한 정보를 제공합니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [일괄 처리 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)의 일부입니다. 지원되는 객체 유형에 대해 기본 CRUD 작업을 수행할 수 있는 RESTful API를 통해 일괄 수집이 제공됩니다.

계속하기 전에 [일괄 처리 수집 API 개요](overview.md) 및 [시작 안내서](getting-started.md)를 검토하십시오.

## JSON 파일 수집

>[!NOTE]
>
>- 다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과 또는 요청 본문 크기 오류가 있는 경우 대용량 파일 업로드로 전환해야 합니다.
>
>- 일괄 처리 수집을 위한 입력으로 다중 라인 JSON 대신 단일 라인 JSON을 사용합니다. 한 줄 JSON을 사용하면 시스템에서 하나의 입력 파일을 여러 청크로 분할하여 병렬로 처리할 수 있으므로 성능이 향상되지만 여러 줄 JSON은 분할할 수 없습니다. 이를 통해 데이터 처리 비용을 크게 줄이고 일괄 처리 지연 시간을 개선할 수 있습니다.

### 일괄 처리 만들기

먼저 JSON을 입력 형식으로 한 일괄 처리를 만들어야 합니다. 배치를 생성할 때 데이터 세트 ID를 제공해야 합니다. 또한 배치의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 준수하는지 확인해야 합니다.

>[!NOTE]
>
>아래 예제는 단일 라인 JSON용입니다. 여러 줄 JSON을 수집하려면 `isMultiLineJson` 플래그를 설정해야 합니다. 자세한 내용은 [일괄 처리 수집 문제 해결 안내서](./troubleshooting.md)를 참조하십시오.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 참조 데이터 세트의 ID입니다. |

**응답**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |

### 파일 업로드

배치를 만들었으므로 이제 배치 생성 응답의 배치 ID를 사용하여 파일을 배치에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

>[!NOTE]
>
>올바른 형식의 JSON 데이터 파일에 대한 [예시](#data-transformation-for-batch-ingestion)는 부록 섹션을 참조하십시오.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출 중인 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!NOTE]
>
>API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `acme/customers/campaigns/summer.json`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었음을 알리고 배치를 승격할 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## Parquet 파일 수집 {#ingest-parquet-files}

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과 또는 요청 본문 크기 오류가 있는 경우 대용량 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저 Parquet를 입력 형식으로 하여 일괄 처리를 만들어야 합니다. 배치를 생성할 때 데이터 세트 ID를 제공해야 합니다. 또한 배치의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 준수하는지 확인해야 합니다.

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| 매개변수 | 설명 |
| --------- | ------------ |
| `{DATASET_ID}` | 참조 데이터 세트의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID입니다. |

### 파일 업로드

이제 일괄 처리를 만들었으므로 이전 의 `batchId`을(를) 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출 중인 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `acme/customers/campaigns/summer.parquet`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었음을 알리고 배치를 승격할 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호하려는 배치의 ID가 완료될 준비가 되었습니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 큰 Parquet 파일 수집

>[!NOTE]
>
>이 섹션에서는 256MB보다 큰 파일을 업로드하는 방법에 대해 자세히 설명합니다. 큰 파일은 청크로 업로드된 다음 API 신호를 통해 결합됩니다.

### 일괄 처리 만들기

먼저 Parquet를 입력 형식으로 하여 일괄 처리를 만들어야 합니다. 배치를 생성할 때 데이터 세트 ID를 제공해야 합니다. 또한 배치의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 준수하는지 확인해야 합니다.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 참조 데이터 세트의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID입니다. |

### 대용량 파일 초기화

일괄 처리를 작성한 후 일괄 처리에 청크를 업로드하기 전에 큰 파일을 초기화해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |
| `{FILE_NAME}` | 초기화하려는 파일의 이름입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
201 Created
```

### 큰 파일 청크 업로드

이제 파일이 생성되었으므로 파일의 각 섹션에 대해 하나씩 반복된 PATCH 요청을 수행하여 모든 후속 청크를 업로드할 수 있습니다.

**API 형식**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출 중인 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 정수에서 요청된 범위의 시작과 끝입니다. |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `acme/customers/campaigns/summer.json`). |


**응답**

```http
200 OK
```

### 전체 대형 파일

이제 일괄 처리를 만들었으므로 이전 의 `batchId`을(를) 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료를 신호 할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 완료를 표시할 파일의 이름입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
201 Created
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었음을 알리고 배치를 승격할 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호를 보내려는 배치 ID가 완료되었습니다. |


**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## CSV 파일 수집

CSV 파일을 수집하려면 CSV를 지원하는 클래스, 스키마 및 데이터 세트를 만들어야 합니다. 필요한 클래스와 스키마를 만드는 방법에 대한 자세한 내용은 [임시 스키마 만들기 자습서](../../xdm/api/ad-hoc.md)에 제공된 지침을 따르십시오.

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과 또는 요청 본문 크기 오류가 있는 경우 대용량 파일 업로드로 전환해야 합니다.

### 데이터 세트 만들기

위의 지침에 따라 필요한 클래스와 스키마를 만든 후에는 CSV를 지원할 수 있는 데이터 세트를 만들어야 합니다.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TENANT_ID}` | 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. |
| `{SCHEMA_ID}` | 생성한 스키마의 ID입니다. |

### 일괄 처리 만들기

그런 다음 CSV를 입력 형식으로 사용하여 일괄 처리를 만들어야 합니다. 배치를 생성할 때 데이터 세트 ID를 제공해야 합니다. 또한 배치의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 스키마를 준수하는지 확인해야 합니다.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 참조 데이터 세트의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID입니다. |

### 파일 업로드

이제 일괄 처리를 만들었으므로 이전 의 `batchId`을(를) 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

>[!NOTE]
>
>올바른 형식의 CSV 데이터 파일에 대한 [예시](#data-transformation-for-batch-ingestion)는 부록 섹션을 참조하십시오.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출 중인 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `acme/customers/campaigns/summer.csv`). |


**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었음을 알리고 배치를 승격할 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## 일괄 처리 취소

일괄 처리를 처리하는 동안 취소할 수 있습니다. 하지만 일괄 처리가 완료되면(예: 성공 또는 실패 상태) 일괄 처리를 취소할 수 없습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 취소할 일괄 처리의 ID입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 일괄 처리 삭제 {#delete-a-batch}

삭제할 일괄 처리의 ID에 대해 `action=REVERT` 쿼리 매개 변수로 다음 POST 요청을 수행하여 일괄 처리를 삭제할 수 있습니다. 배치가 &quot;비활성&quot;으로 표시되어 가비지 수집에 적합합니다. 배치는 비동기적으로 수집되며, 이 때 &quot;삭제됨&quot;으로 표시됩니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 삭제할 일괄 처리의 ID입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 일괄 처리 패치

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. Adobe Experience Platform은 업데이트 작업 또는 &quot;일괄 패치 작업&quot;을 통해 프로필 스토어 데이터의 업데이트 또는 패치를 지원합니다.

>[!NOTE]
>
>이러한 업데이트는 프로필 레코드에만 허용되며 경험 이벤트에는 허용되지 않습니다.

배치를 패치하려면 다음 조건을 충족해야 합니다.

- **프로필 및 특성 업데이트에 사용할 수 있는 데이터 집합입니다.** 이 작업은 데이터 세트 태그를 통해 수행되며 특정 `isUpsert:true` 태그를 `unifiedProfile` 배열에 추가해야 합니다. 데이터 집합을 만들거나 업데이트할 기존 데이터 집합을 구성하는 방법을 보여 주는 자세한 단계를 보려면 [프로필 업데이트에 대한 데이터 집합을 활성화](../../catalog/datasets/enable-upsert.md)하는 자습서를 따르십시오.
- **패치할 필드와 프로필의 ID 필드가 포함된 Parquet 파일입니다.** 일괄 처리를 패치하는 데이터 형식은 일반 일괄 처리 수집 프로세스와 유사합니다. 필요한 입력은 Parquet 파일이며, 업데이트할 필드 외에도 프로필 저장소의 데이터와 일치시키기 위해 업로드된 데이터에는 ID 필드가 포함되어야 합니다.

프로필 및 업데이트에 대한 데이터 세트를 사용할 수 있고, 패치할 필드와 필수 ID 필드가 포함된 Parquet 파일이 있으면 [Parquet 파일을 수집](#ingest-parquet-files)하는 단계에 따라 일괄 처리 수집을 통해 패치를 완료할 수 있습니다.

## 배치 재생

이미 수집된 배치를 바꾸려면 &quot;배치 재생&quot;을 사용합니다. 이 작업은 이전 배치를 삭제하고 대신 새 배치를 수집하는 것과 같습니다.

### 일괄 처리 만들기

먼저 JSON을 입력 형식으로 한 일괄 처리를 만들어야 합니다. 배치를 생성할 때 데이터 세트 ID를 제공해야 합니다. 또한 배치의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 준수하는지 확인해야 합니다. 또한 이전 배치를 재생 섹션에 참조로 제공해야 합니다. 아래 예에서는 ID가 `batchIdA` 및 `batchIdB`인 배치를 재생하고 있습니다.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| 매개변수 | 설명 |
| --------- | ----------- | 
| `{DATASET_ID}` | 참조 데이터 세트의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID입니다. |


### 파일 업로드

이제 일괄 처리를 만들었으므로 이전 의 `batchId`을(를) 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 배치 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출 중인 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다. curl -F 옵션은 기본적으로 API와 호환되지 않는 다중 파트 요청으로 설정되므로 사용하지 마십시오.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `acme/customers/campaigns/summer.json`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었음을 알리고 배치를 승격할 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료할 일괄 처리의 ID입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## 부록

다음 섹션에는 일괄 처리 수집을 사용하여 Experience Platform에서 데이터를 수집하기 위한 추가 정보가 포함되어 있습니다.

### 일괄 처리 수집을 위한 데이터 변환

데이터 파일을 [!DNL Experience Platform]&#x200B;(으)로 수집하려면 파일의 계층 구조가 업로드할 데이터 세트와 연결된 [XDM(Experience Data Model)](../../xdm/home.md) 스키마를 준수해야 합니다.

XDM 스키마를 준수하도록 CSV 파일을 매핑하는 방법에 대한 정보는 올바른 형식의 JSON 데이터 파일의 예제와 함께 [샘플 변형](../../etl/transformations.md) 문서에서 확인할 수 있습니다. 문서에 제공된 샘플 파일은 여기에서 찾을 수 있습니다.

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
