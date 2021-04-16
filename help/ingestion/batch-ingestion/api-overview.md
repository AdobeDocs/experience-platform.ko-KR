---
keywords: Experience Platform;home;popular topics;batch ingestion;통합;통합;개발자 가이드;api guide;upload;ingest Portable;ingest json
solution: Experience Platform
title: 일괄 처리 통합 API 안내서
topic: 개발자 가이드
description: 이 문서에서는 일괄 처리 통합 API 사용에 대한 포괄적인 개요를 제공합니다.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 6%

---

# 일괄 처리 통합 API 안내서

이 문서에서는 [일괄 처리 통합 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) 사용에 대한 포괄적인 개요를 제공합니다.

이 문서의 부록은 샘플 CSV 및 JSON 데이터 파일을 포함하여 통합](#data-transformation-for-batch-ingestion)에 사용할 [서식 데이터에 대한 정보를 제공합니다.

## 시작하기

데이터 수집은 지원되는 개체 유형에 대해 기본 CRUD 작업을 수행할 수 있는 RESTful API를 제공합니다.

다음 섹션에서는 배치 통합 API를 성공적으로 호출하기 위해 알아야 하거나 현재 가지고 있는 추가 정보를 제공합니다.

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [일괄 처리](./overview.md):데이터를 Adobe Experience Platform에 일괄 파일로 인제스트할 수 있습니다.
- [[!DNL Experience Data Model (XDM)] 시스템](../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 요청에는 추가 `Content-Type` 헤더가 필요할 수 있습니다. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

## 유형

데이터를 인제스트할 때는 [!DNL Experience Data Model](XDM) 스키마가 작동하는 방식을 이해하는 것이 중요합니다. XDM 필드 유형이 다른 형식에 매핑되는 방법에 대한 자세한 내용은 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)를 참조하십시오.

데이터를 인제스트할 때 유연성이 있습니다. 유형이 대상 스키마의 유형과 일치하지 않으면 데이터가 표현된 대상 유형으로 변환됩니다. 그럴 수 없는 경우 `TypeCompatibilityException`으로 일괄 처리가 실패합니다.

예를 들어 JSON과 CSV에는 날짜 또는 날짜 시간 유형이 없습니다. 따라서 이러한 값은 [ISO 8061 형식 문자열](https://www.iso.org/iso-8601-date-and-time-format.html)(&quot;2018-07-10T15:05:59.000-08:00&quot;) 또는 Unix 시간(밀리초)을 사용하여 표현되며 통합 시 대상 XDM 유형으로 변환됩니다.

아래 표는 데이터를 인제스트할 때 지원되는 전환을 보여줍니다.

| 인바운드(행)과 Target(열) 비교 | 문자열 | 바이트 | Short | 정수 | Long | 이중 | Date | 날짜-시간 | 개체 | 맵 |
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

## 통합 제한

일괄 데이터 수집에는 몇 가지 제한 사항이 있습니다.
- 일괄 처리당 최대 파일 수:1500년
- 최대 일괄 처리 크기:100GB
- 행당 최대 속성 또는 필드 수:10000
- 사용자당 분당 최대 배치 수:138년

## JSON 파일 인제스트

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 제한에 도달하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저 JSON을 입력 포맷으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

>[!NOTE]
>
>아래의 예는 단일 JSON용입니다. 여러 줄 JSON을 인제스트하려면 `isMultiLineJson` 플래그를 설정해야 합니다. 자세한 내용은 [일괄 처리 통합 문제 해결 안내서](./troubleshooting.md)를 참조하십시오.

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
| `{DATASET_ID}` | 참조 데이터 집합의 ID. |

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
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |

### 파일 업로드

이제 일괄 처리를 만들었으므로 이전에 `batchId`을 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

>[!NOTE]
>
>올바른 형식의 JSON 데이터 파일](#data-transformation-for-batch-ingestion)의 [예제에 대한 부록 섹션을 참조하십시오.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 측면에 저장될 위치입니다. |

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
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `Users/sample-user/Downloads/sample.json`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분 업로드를 완료하고 나면 데이터가 완전히 업로드되었다는 것과 배치가 홍보할 준비가 되었다는 신호를 보내야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |

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
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 제한에 도달하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

### 일괄 처리 만들기

먼저, 입력 포맷으로 Pencil을 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

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
| `{DATASET_ID}` | 참조 데이터 집합의 ID. |

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
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 파일 업로드

이제 일괄 처리를 만들었으므로 이전에 `batchId`을 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 측면에 저장될 위치입니다. |

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
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `Users/sample-user/Downloads/sample.json`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분 업로드를 완료하고 나면 데이터가 완전히 업로드되었다는 것과 배치가 홍보할 준비가 되었다는 신호를 보내야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 신호를 보내려는 일괄 처리 ID가 완료될 준비가 되었습니다. |

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

먼저, 입력 포맷으로 Pencil을 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다.

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
| `{DATASET_ID}` | 참조 데이터 집합의 ID. |

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
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 큰 파일 초기화

일괄 처리를 만든 후 일괄 처리에 청크를 업로드하기 전에 큰 파일을 초기화해야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |
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

### 대용량 파일 청크 업로드

이제 파일이 만들어졌으므로, 파일의 각 섹션에 대해 PATCH 요청을 반복하여 모든 후속 청크를 업로드할 수 있습니다.

**API 형식**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 측면에 저장될 위치입니다. |

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
| `{CONTENT_RANGE}` | 정수로, 요청된 범위의 시작 및 끝. |
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `Users/sample-user/Downloads/sample.json`). |


**응답**

```http
200 OK
```

### 큰 파일 완료

이제 일괄 처리를 만들었으므로 이전에 `batchId`을 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료 신호를 보내려는 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
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

파일의 서로 다른 모든 부분 업로드를 완료하고 나면 데이터가 완전히 업로드되었다는 것과 배치가 홍보할 준비가 되었다는 신호를 보내야 합니다.

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

CSV 파일을 인제스트하려면 CSV를 지원하는 클래스, 스키마 및 데이터 세트를 만들어야 합니다. 필요한 클래스 및 스키마를 만드는 방법에 대한 자세한 내용은 [애드혹 스키마 만들기 자습서](../../xdm/api/ad-hoc.md)에 제공된 지침을 따르십시오.

>[!NOTE]
>
>다음 단계는 작은 파일(256MB 이하)에 적용됩니다. 게이트웨이 시간 제한에 도달하거나 본문 크기 오류를 요청하는 경우 큰 파일 업로드로 전환해야 합니다.

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
      }
  }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TENANT_ID}` | 이 ID는 사용자가 만든 리소스가 적절하게 대체되고 IMS 조직 내에 포함되도록 하는 데 사용됩니다. |
| `{SCHEMA_ID}` | 만든 스키마의 ID. |

### 일괄 처리 만들기

그런 다음 CSV를 입력 형식으로 포함하는 배치를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 스키마를 따르는지 확인해야 합니다.

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
| `{DATASET_ID}` | 참조 데이터 집합의 ID. |

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
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |

### 파일 업로드

이제 일괄 처리를 만들었으므로 이전에 `batchId`을 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

>[!NOTE]
>
>올바른 형식의 CSV 데이터 파일](#data-transformation-for-batch-ingestion)의 [예제에 대한 부록 섹션을 참조하십시오.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 측면에 저장될 위치입니다. |

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
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `Users/sample-user/Downloads/sample.json`). |


**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 다른 모든 부분 업로드를 완료하고 나면 데이터가 완전히 업로드되었다는 신호를 보내고 일괄 처리가 홍보될 준비가 되었음을 알려야 합니다.

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

## 일괄 처리 취소

배치를 처리하는 동안 여전히 취소할 수 있습니다. 하지만 일단 배치가 완료되면(예: 성공 또는 실패 상태) 배치를 취소할 수 없습니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 취소할 일괄 처리의 ID. |

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

## 일괄 처리 {#delete-a-batch} 삭제

일괄 처리는 삭제하려는 일괄 처리의 ID에 대해 `action=REVERT` 쿼리 매개 변수를 사용하여 다음 POST 요청을 수행하여 삭제할 수 있습니다. 일괄 처리는 &quot;비활성&quot;으로 표시되어 가비지 수집을 사용할 수 있습니다. 일괄 처리는 비동기적으로 수집되며, 이때 &quot;삭제됨&quot;으로 표시됩니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 삭제할 배치의 ID. |

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

먼저 JSON을 입력 포맷으로 사용하여 일괄 처리를 만들어야 합니다. 일괄 처리를 만들 때 데이터 세트 ID를 제공해야 합니다. 일괄 처리의 일부로 업로드된 모든 파일이 제공된 데이터 세트에 연결된 XDM 스키마를 따르는지 확인해야 합니다. 또한 재생 섹션에 참조로 이전 배치를 제공해야 합니다. 아래 예에서 ID가 `batchIdA` 및 `batchIdB`인 배치를 다시 재생하고 있습니다.

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
| `{DATASET_ID}` | 참조 데이터 집합의 ID. |

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
| `{BATCH_ID}` | 새로 생성된 일괄 처리의 ID. |
| `{DATASET_ID}` | 참조된 데이터 집합의 ID. |
| `{USER_ID}` | 배치를 만든 사용자의 ID. |


### 파일 업로드

이제 일괄 처리를 만들었으므로 이전에 `batchId`을 사용하여 파일을 일괄 처리에 업로드할 수 있습니다. 여러 파일을 일괄 처리에 업로드할 수 있습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 업로드할 배치의 ID. |
| `{DATASET_ID}` | 일괄 처리의 참조 데이터 세트 ID입니다. |
| `{FILE_NAME}` | 업로드할 파일의 이름입니다. 이 파일 경로는 파일이 Adobe 측면에 저장될 위치입니다. |

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
| `{FILE_PATH_AND_NAME}` | 업로드하려는 파일의 전체 경로 및 이름입니다. 이 파일 경로는 로컬 파일 경로입니다(예: `Users/sample-user/Downloads/sample.json`). |

**응답**

```http
200 OK
```

### 일괄 처리 완료

파일의 서로 다른 모든 부분 업로드를 완료하고 나면 데이터가 완전히 업로드되었다는 것과 배치가 홍보할 준비가 되었다는 신호를 보내야 합니다.

**API 형식**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 완료하려는 일괄 처리의 ID. |

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

데이터 파일을 [!DNL Experience Platform]에 인제스트하려면 파일의 계층 구조가 업로드되는 데이터 집합과 관련된 [경험 데이터 모델(XDM)](../../xdm/home.md) 스키마를 준수해야 합니다.

XDM 스키마를 따르도록 CSV 파일을 매핑하는 방법에 대한 자세한 내용은 올바른 형식의 JSON 데이터 파일의 예와 함께 [sample transformations](../../etl/transformations.md) 문서를 참조하십시오. 문서에 제공되는 샘플 파일은 다음 URL에서 찾을 수 있습니다.

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
