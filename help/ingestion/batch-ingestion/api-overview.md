---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;ingestion;developer guide;api guide;upload;ingest parquet;ingest json;
solution: Experience Platform
title: 일괄 처리 통합 개발자 가이드
topic: developer guide
description: 이 문서에서는 일괄 처리 통합 API를 사용하는 방법에 대한 포괄적인 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '2675'
ht-degree: 5%

---


# 일괄 처리 통합 개발자 가이드

이 문서에서는 [일괄 처리 통합 API를 사용하는 방법에 대한 포괄적인 개요를 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

이 문서의 부록은 샘플 CSV 및 JSON 데이터 파일 등 인제스트에 [](#data-transformation-for-batch-ingestion)사용되는 데이터 서식 지정 정보를 제공합니다.

## 시작하기

데이터 수집은 지원되는 개체 유형에 대해 기본 CRUD 작업을 수행할 수 있는 RESTful API를 제공합니다.

다음 섹션에서는 배치 처리 API를 성공적으로 호출하기 위해 알아야 하거나 현재 가지고 있는 추가 정보를 제공합니다.

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

- [일괄 처리](./overview.md):데이터를 Adobe Experience Platform에 일괄 파일로 인제스트할 수 있습니다.
- [[!DNL Experience Data Model (XDM)] 시스템](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)을 포함하는 요청에는 추가 헤더가 필요할 수 `Content-Type` 있습니다. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

## 유형

데이터를 인제스트할 때는 XDM(Schemas Operating Data) [!DNL Experience Data Model] 개표의 작동 방식을 이해해야 합니다. XDM 필드 유형이 다른 포맷으로 매핑되는 방법에 대한 자세한 내용은 스키마 [레지스트리 개발자 안내서를 참조하십시오](../../xdm/api/getting-started.md).

데이터 인제스트 시 몇 가지 유연성이 있습니다. 유형이 대상 스키마의 유형과 일치하지 않으면 데이터는 표현된 대상 유형으로 변환됩니다. 그럴 수 없는 경우, 배치는 A로 실패합니다 `TypeCompatibilityException`.

예를 들어 JSON이나 CSV에는 날짜 또는 날짜 시간 유형이 없습니다. 그 결과, 이러한 값은 [ISO 8061 형식 문자열](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.00-08:00&quot;) 또는 Unix 시간(밀리초)(153126395 9000) 및 수집 시 대상 XDM 유형으로 변환됩니다.

아래 표는 데이터를 인제스트할 때 지원되는 전환을 보여줍니다.

| 인바운드(행)과 Target(열) 비교 | 문자열 | 바이트 | Short | 정수 | Long | 이중 | 날짜 | 날짜-시간 | 개체 | 맵 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 문자열 | X | X | X | X | X | X | X | X |  |  |
| 바이트 | X | X | X | X | X | X |  |  |  |  |
| Short | X | X | X | X | X | X |  |  |  |  |
| 정수 | X | X | X | X | X | X |  |  |  |  |
| Long | X | X | X | X | X | X | X | X |  |  |
| 이중 | X | X | X | X | X | X |  |  |  |  |
| 날짜 |  |  |  |  |  |  | X |  |  |  |
| 날짜-시간 |  |  |  |  |  |  |  | X |  |  |
| 개체 |  |  |  |  |  |  |  |  | X | X |
| 맵 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>부울 및 배열은 다른 형식으로 변환할 수 없습니다.

## 섭취 제한

일괄 데이터 수집에는 몇 가지 제한 사항이 있습니다.
- 일괄 처리당 최대 파일 수:1500년
- 최대 배치 크기:100GB
- 행당 최대 속성 또는 필드 수:1000
- 사용자당 분당 최대 배치 수:138년

## JSON 파일 인제스트

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 초과를 히트하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저 JSON을 입력 포맷으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

>[!NOTE]
>
>아래의 예는 단일 JSON용입니다. 다중 라인 JSON을 인제스트하려면 `isMultiLineJson` 플래그를 설정해야 합니다. 자세한 내용은 일괄 처리 [문제 해결 가이드를 참조하십시오](./troubleshooting.md).

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 참조 데이터 집합의 ID입니다. |

**응답**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |

### 파일 업로드

일괄 처리를 생성했으면 이전에 을 사용하여 파일을 일괄 `batchId` 에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

>[!NOTE]
>
>올바르게 서식이 지정된 JSON 데이터 파일의 [예는 부록 섹션을 참조하십시오](#data-transformation-for-batch-ingestion).

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 쪽에 저장될 위치입니다. |

**요청**

>[!NOTE]
>
>API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로(예: )입니다 `Users/sample-user/Downloads/sample.json`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분을 업로드한 후에는 데이터가 완전히 업로드되었고 일괄 처리가 홍보될 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## 인제스트 쪽모이 세공 파일

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 초과를 히트하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저, 입력 포맷으로 쪽모이 세공된 배치를 생성해야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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
| `{DATASET_ID}` | 참조 데이터 집합의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 파일 업로드

일괄 처리를 생성했으면 이전에 을 사용하여 파일을 일괄 `batchId` 에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 쪽에 저장될 위치입니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로(예: )입니다 `Users/sample-user/Downloads/sample.json`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분을 업로드한 후에는 데이터가 완전히 업로드되었고 일괄 처리가 홍보될 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호를 보내려는 배치의 ID가 완료될 준비가 되었습니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 대용량 쪽모이 세공 파일 인제스트

>[!NOTE]
>
>이 섹션에서는 256MB보다 큰 파일을 업로드하는 방법에 대해 자세히 설명합니다. 큰 파일은 청크로 업로드된 다음 API 신호를 통해 스티칭됩니다.

### 일괄 처리 만들기

먼저, 입력 포맷으로 쪽모이 세공된 배치를 생성해야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 참조 데이터 집합의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 큰 파일 초기화

일괄 처리를 만든 후 일괄 처리에 청크를 업로드하기 전에 큰 파일을 초기화해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |
| `{FILE_NAME}` | 초기화하려는 파일의 이름입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
201 Created
```

### 대용량 파일 업로드

이제 파일이 생성되었으므로 파일의 각 섹션에 대해 반복된 PATCH 요청을 수행하여 이후의 모든 청크를 업로드할 수 있습니다.

**API 형식**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 쪽에 저장될 위치입니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 정수에서 요청된 범위의 시작 및 끝. |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로(예: )입니다 `Users/sample-user/Downloads/sample.json`. |


**응답**

```http
200 OK
```

### 대용량 파일 작성

일괄 처리를 생성했으면 이전에 을 사용하여 파일을 일괄 `batchId` 에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료 신호를 보낼 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 완료 신호를 보낼 파일의 이름입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
201 Created
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분을 업로드한 후에는 데이터가 완전히 업로드되었고 일괄 처리가 홍보될 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호를 보내려는 일괄 처리 ID가 완료되었습니다. |


**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## CSV 파일 인제스트

CSV 파일을 인제스트하려면 CSV를 지원하는 클래스, 스키마 및 데이터 세트를 만들어야 합니다. 필요한 클래스 및 스키마를 만드는 방법에 대한 자세한 내용은 [임시 스키마 만들기 자습서에서 제공하는 지침을 따르십시오](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 초과를 히트하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TENANT_ID}` | 이 ID는 사용자가 만든 리소스가 IMS 조직 내에 올바르게 지정되고 포함되어 있는지 확인하는 데 사용됩니다. |
| `{SCHEMA_ID}` | 만든 스키마의 ID입니다. |

JSON 본문의 &quot;fileDescription&quot; 섹션의 다양한 부분이 아래에 표시될 수 있는 내용에 대한 설명입니다.

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `format` | 입력 파일의 형식이 아니라 마스터된 파일의 형식입니다. |
| `delimiters` | 구분 기호로 사용할 문자입니다. |
| `quotes` | 견적에 사용할 문자입니다. |
| `escapes` | 이스케이프 문자로 사용할 문자입니다. |
| `header` | 업로드된 파일은 헤더를 **포함해야** 합니다. 스키마 유효성 검사가 수행되므로 true로 설정해야 합니다. 헤더에 공백이 있으면 헤더에 공백이 **포함되지** 않을 수 있습니다. 헤더에 공백이 있으면 대신 밑줄로 바꾸십시오. |
| `charset` | 선택적 필드입니다. 기타 지원되는 문자로는 &quot;US-ASCII&quot; 및 &quot;ISO-8869-1&quot;이 있습니다. 비워 두면 기본적으로 UTF-8이 사용됩니다. |

참조된 데이터 집합은 위에 나열된 파일 설명 블록을 가지고 있어야 하며 레지스트리에서 올바른 스키마를 가리켜야 합니다. 그렇지 않으면 파일이 쪽모이 세공된 상태로 마스터되지 않습니다.

### 일괄 처리 만들기

그런 다음 CSV를 입력 포맷으로 사용한 배치를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 스키마를 따르는지 확인해야 합니다.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 참조 데이터 집합의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 파일 업로드

일괄 처리를 생성했으면 이전에 을 사용하여 파일을 일괄 `batchId` 에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

>[!NOTE]
>
>올바르게 서식이 지정된 CSV 데이터 파일의 [예는 부록 섹션을 참조하십시오](#data-transformation-for-batch-ingestion).

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 쪽에 저장될 위치입니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로(예: )입니다 `Users/sample-user/Downloads/sample.json`. |


**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분을 업로드한 후에는 데이터가 완전히 업로드되었고 일괄 처리가 홍보될 준비가 되었음을 표시해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## 배치 취소

배치를 처리하는 동안 취소할 수 있습니다. 하지만 배치가 완료되면(예: 성공 또는 실패 상태) 배치를 취소할 수 없습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 일괄 삭제 {#delete-a-batch}

삭제하려는 배치의 ID에 대한 `action=REVERT` 쿼리 매개 변수를 사용하여 다음 POST 요청을 수행하여 배치를 삭제할 수 있습니다. 일괄 처리는 &quot;비활성&quot;으로 표시되어 가비지 수집이 가능합니다. 일괄 처리는 비동기적으로 수집되며, 그 때 &quot;삭제됨&quot;으로 표시됩니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 삭제할 배치의 ID입니다. |

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

```http
200 OK
```

## 일괄 재생

이미 인제스트한 배치를 바꾸려는 경우 &quot;일괄 재생&quot;으로 바꿀 수 있습니다. 이 작업은 이전 일괄 처리를 삭제하고 대신 새 일괄 처리를 인제스트하는 것과 같습니다.

### 일괄 처리 만들기

먼저 JSON을 입력 포맷으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 또한 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다. 또한 재생 섹션에서 이전 배치를 참조로 제공해야 합니다. 아래 예에서 ID와 함께 배치를 다시 재생하고 `batchIdA` 있습니다 `batchIdB`.

**API 형식**

```http
POST /batches
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 참조 데이터 집합의 ID입니다. |

**응답**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 새로 생성된 일괄 처리에 대한 ID입니다. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID입니다. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |


### 파일 업로드

일괄 처리를 생성했으면 이전에 을 사용하여 파일을 일괄 `batchId` 에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID입니다. |
| `{DATASET_ID}` | 일괄 처리 참조 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 쪽에 저장될 위치입니다. |

**요청**

>[!CAUTION]
>
>이 API는 단일 부분 업로드를 지원합니다. content-type이 application/octet-stream인지 확인합니다. 기본적으로 API와 호환되지 않는 다중 부분 요청으로 설정되므로 curl -F 옵션을 사용하지 마십시오.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로(예: )입니다 `Users/sample-user/Downloads/sample.json`. |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분을 업로드한 후에는 데이터가 완전히 업로드되었고 일괄 처리가 홍보될 준비가 되었음을 표시해야 합니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```http
200 OK
```

## 부록

### 일괄 처리를 위한 데이터 변환

데이터 파일을 인제스트하려면 파일의 계층 구조 [!DNL Experience Platform]가 업로드되는 데이터 세트에 연결된 [경험 데이터 모델(XDM)](../../xdm/home.md) 스키마를 준수해야 합니다.

XDM 스키마를 따르도록 CSV 파일을 매핑하는 방법에 대한 자세한 내용은 [샘플 변형](../../etl/transformations.md) 문서 및 올바른 형식의 JSON 데이터 파일의 예를 참조하십시오. 문서에 제공된 샘플 파일은 다음 사이트에서 찾을 수 있습니다.

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)