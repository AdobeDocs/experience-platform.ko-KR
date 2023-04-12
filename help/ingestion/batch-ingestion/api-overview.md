---
keywords: Experience Platform;홈;인기 항목;일괄 처리 수집;수집;수집;개발자 안내서;api 안내서;업로드;Parquet 수집;json 수집
solution: Experience Platform
title: 배치 수집 API 안내서
description: 이 문서에서는 Adobe Experience Platform용 배치 수집 API를 사용하는 개발자를 위한 포괄적인 안내서를 제공합니다.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 4%

---

# 일괄 수집 개발자 안내서

이 문서에서는 [배치 수집 API 엔드포인트](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) Adobe Experience Platform. 사전 요구 사항 및 우수 사례를 포함한 배치 수집 API에 대한 개요를 알려면 다음을 읽어 보십시오. [배치 수집 API 개요](overview.md).

이 문서의 부록에는 [처리에 사용할 데이터 형식 지정](#data-transformation-for-batch-ingestion): 샘플 CSV 및 JSON 데이터 파일 포함.

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [배치 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 일괄 처리는 RESTful API를 통해 제공되며, 이 RESTful API에서는 지원되는 개체 유형에 대해 기본 CRUD 작업을 수행할 수 있습니다.

계속하기 전에 [배치 수집 API 개요](overview.md) 그리고 [시작 안내서](getting-started.md).

## JSON 파일 수집

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과나 요청 본문 크기 오류가 발생하면 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저 JSON을 입력 형식으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

>[!NOTE]
>
>아래 예제는 단일 JSON입니다. 여러 줄 JSON을 수집하려면 `isMultiLineJson` 플래그를 설정해야 합니다. 자세한 내용은 [배치 수집 문제 해결 가이드](./troubleshooting.md).

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

| 매개 변수 | 설명 |
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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |

### 파일 업로드

이제 일괄 처리를 생성했으므로 일괄 처리 생성 응답의 배치 ID를 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 배치에 업로드할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 부록 섹션을 참조하십시오. [올바른 형식의 JSON 데이터 파일의 예](#data-transformation-for-batch-ingestion).

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출할 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!NOTE]
>
>API는 단일 부분 업로드를 지원합니다. content-type 이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 다음과 같은 로컬 파일 경로입니다 `acme/customers/campaigns/summer.json`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었으며 일괄 처리가 프로모션될 준비가 되었음을 알리는 신호가 있어야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
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

## Ingest Parquet 파일 {#ingest-parquet-files}

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과나 요청 본문 크기 오류가 발생하면 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저 일괄 처리를 생성한 후 Parquet을 입력 형식으로 입력해야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

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

| 매개 변수 | 설명 |
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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |
| `{USER_ID}` | 배치를 생성한 사용자의 ID입니다. |

### 파일 업로드

배치를 생성했으므로 다음을 사용할 수 있습니다 `batchId` 파일을 배치에 업로드하기 전에서까지입니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출할 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type 이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 다음과 같은 로컬 파일 경로입니다 `acme/customers/campaigns/summer.parquet`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었으며 일괄 처리가 프로모션될 준비가 되었음을 알리는 신호가 있어야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호할 배치의 ID가 완료될 준비가 되었습니다. |

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

## 대형 Parquet 파일 수집

>[!NOTE]
>
>이 섹션에서는 256MB보다 큰 파일을 업로드하는 방법을 자세히 설명합니다. 큰 파일은 청크로 업로드된 다음 API 신호를 통해 결합됩니다.

### 일괄 처리 만들기

먼저 일괄 처리를 생성한 후 Parquet을 입력 형식으로 입력해야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

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

| 매개 변수 | 설명 |
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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |
| `{USER_ID}` | 배치를 생성한 사용자의 ID입니다. |

### 큰 파일 초기화

배치를 만든 후 일괄 처리를 업로드하기 전에 큰 파일을 초기화해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |
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

파일이 만들어졌으므로 이제 파일의 각 섹션에 대해 하나씩 반복되는 PATCH 요청을 수행하여 후속 청크를 모두 업로드할 수 있습니다.

**API 형식**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출할 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type 이 application/octet-stream인지 확인합니다.

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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 정수로, 요청된 범위의 시작 및 끝. |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 다음과 같은 로컬 파일 경로입니다 `acme/customers/campaigns/summer.json`. |


**응답**

```http
200 OK
```

### 전체 대용량 파일

배치를 생성했으므로 다음을 사용할 수 있습니다 `batchId` 파일을 배치에 업로드하기 전에서까지입니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료 신호를 보낼 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 완료 신호를 보낼 파일의 이름입니다. |

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

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었으며 일괄 처리가 프로모션될 준비가 되었음을 알리는 신호가 있어야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호하려는 일괄 처리의 ID가 완료되었습니다. |


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

CSV 파일을 수집하려면 CSV를 지원하는 클래스, 스키마 및 데이터 세트를 만들어야 합니다. 필요한 클래스 및 스키마를 만드는 방법에 대한 자세한 내용은 [ad-hoc 스키마 만들기 튜토리얼](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용할 수 있습니다. 게이트웨이 시간 초과나 요청 본문 크기 오류가 발생하면 큰 파일 업로드로 전환해야 합니다.

### 데이터 세트 만들기

위의 지침에 따라 필요한 클래스 및 스키마를 만든 후 CSV를 지원할 수 있는 데이터 세트를 만들어야 합니다.

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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TENANT_ID}` | 이 ID는 사용자가 만드는 리소스가 제대로 식별되고 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. |
| `{SCHEMA_ID}` | 생성한 스키마의 ID입니다. |

### 일괄 처리 만들기

다음으로, CSV를 입력 형식으로 사용한 배치를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 스키마를 따르는지 확인해야 합니다.

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

| 매개 변수 | 설명 |
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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |
| `{USER_ID}` | 배치를 생성한 사용자의 ID입니다. |

### 파일 업로드

배치를 생성했으므로 다음을 사용할 수 있습니다 `batchId` 파일을 배치에 업로드하기 전에서까지입니다. 여러 파일을 배치에 업로드할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 부록 섹션을 참조하십시오. [올바른 형식의 CSV 데이터 파일의 예](#data-transformation-for-batch-ingestion).

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출할 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type 이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 다음과 같은 로컬 파일 경로입니다 `acme/customers/campaigns/summer.csv`. |


**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었으며 일괄 처리가 프로모션될 준비가 되었음을 알리는 신호가 있어야 합니다.

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

## 배치 취소

일괄 처리가 처리되는 동안 여전히 취소할 수 있습니다. 그러나 배치가 완료되면(성공 또는 실패 상태 등) 배치를 취소할 수 없습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 취소할 배치의 ID입니다. |

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

## 배치 삭제 {#delete-a-batch}

다음과 같은 POST 요청을 수행하여 배치를 삭제할 수 있습니다 `action=REVERT` 삭제할 배치 ID에 대한 쿼리 매개 변수입니다. 일괄 처리가 &quot;비활성&quot;으로 표시되어 가비지 수집에 적합합니다. 일괄 처리가 비동기적으로 수집되며 이때 일괄 처리가 &quot;삭제&quot;로 표시됩니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 매개 변수 | 설명 |
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

## 일괄 처리

간혹 조직의 프로필 저장소에서 데이터를 업데이트해야 할 수 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. Adobe Experience Platform은 업데이트 작업 또는 &quot;일괄 처리&quot;를 통해 프로필 저장소 데이터의 업데이트 또는 패치를 지원합니다.

>[!NOTE]
>
>이러한 업데이트는 경험 이벤트가 아니라 프로필 레코드에서만 허용됩니다.

배치를 패치하려면 다음 사항이 필요합니다.

- **프로필 및 속성 업데이트에 대해 활성화된 데이터 세트입니다.** 데이터 세트 태그를 통해 수행되며 특정 `isUpsert:true` 태그에 추가 `unifiedProfile` 배열입니다. 데이터 세트를 만들거나 업데이트할 기존 데이터 세트를 구성하는 방법을 보여주는 자세한 단계는 에 대한 자습서를 따르십시오 [프로필 업데이트에 대한 데이터 세트 활성화](../../catalog/datasets/enable-upsert.md).
- **패치할 필드와 프로파일의 ID 필드가 포함된 Parquet 파일입니다.** 일괄 처리를 패치하기 위한 데이터 형식은 일반 배치 수집 프로세스와 유사합니다. 필요한 입력은 Parquet 파일이며, 업데이트할 필드 외에 업로드된 데이터에는 ID 필드가 포함되어야 Profile Store의 데이터와 일치할 수 있습니다.

프로필 및 업데이트에 대해 데이터 세트를 활성화하고, 패치할 필드뿐만 아니라 필요한 ID 필드가 포함된 Parquet 파일이 있으면 다음 단계를 수행할 수 있습니다 [Parquet 파일 수집](#ingest-parquet-files) 배치 수집을 통해 패치를 완료하기 위해.

## 배치 재생

이미 수집된 일괄 처리를 대체하려면 &quot;일괄 재생&quot;으로 할 수 있습니다. 이 작업은 이전 일괄 처리를 삭제하고 대신 새 일괄 처리를 수집하는 것과 같습니다.

### 일괄 처리 만들기

먼저 JSON을 입력 형식으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다. 또한 재생 섹션에서 참조할 수 있도록 이전 배치를 제공해야 합니다. 아래 예에서는 ID가 있는 배치를 다시 재생하고 있습니다 `batchIdA` 및 `batchIdB`.

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

| 매개 변수 | 설명 |
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

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 배치의 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 세트의 ID입니다. |
| `{USER_ID}` | 배치를 생성한 사용자의 ID입니다. |


### 파일 업로드

배치를 생성했으므로 다음을 사용할 수 있습니다 `batchId` 파일을 배치에 업로드하기 전에서까지입니다. 여러 파일을 배치에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 일괄 처리의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트에 대한 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 제출할 파일 배치에 대해 다른 파일과 충돌하지 않도록 고유한 파일 이름을 사용해야 합니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type 이 application/octet-stream인지 확인합니다. curl -F 옵션은 기본적으로 API와 호환되지 않는 다중 부분 요청으로 설정되므로 사용하지 마십시오.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 다음과 같은 로컬 파일 경로입니다 `acme/customers/campaigns/summer.json`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 여러 부분을 모두 업로드했으면 데이터가 완전히 업로드되었으며 일괄 처리가 프로모션될 준비가 되었음을 알리는 신호가 있어야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료하려는 일괄 처리의 ID입니다. |

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

다음 섹션에는 배치 수집을 사용하여 Experience Platform에서 데이터를 수집하기 위한 추가 정보가 포함되어 있습니다.

### 일괄 처리를 위한 데이터 변환

데이터 파일을에 수집하려면 [!DNL Experience Platform]로 지정하는 경우 파일의 계층 구조는 [XDM(경험 데이터 모델)](../../xdm/home.md) 업로드 중인 데이터 세트와 연관된 스키마입니다.

XDM 스키마를 준수하도록 CSV 파일을 매핑하는 방법에 대한 자세한 내용은 [샘플 변형](../../etl/transformations.md) 적절한 형식의 JSON 데이터 파일의 예와 함께 문서에 첨부합니다. 문서에 제공된 샘플 파일은 다음과 같습니다.

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
