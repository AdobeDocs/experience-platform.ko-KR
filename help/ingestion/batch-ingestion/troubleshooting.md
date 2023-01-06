---
keywords: Experience Platform;홈;인기 항목;수집된 데이터;문제 해결;faq;수집;일괄 처리 수집;일괄 처리 수집
solution: Experience Platform
title: 배치 수집 문제 해결 안내서
description: 이 설명서는 Adobe Experience Platform 배치 데이터 수집 API와 관련된 FAQ에 대한 답변을 제공하는 데 도움이 됩니다.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 일괄 수집 문제 해결 안내서

이 설명서는 Adobe Experience Platform과 관련된 FAQ에 답변하는 데 도움이 됩니다 [!DNL Batch Data Ingestion] API.

## 배치 API 호출

### CompleteBatch API에서 HTTP 200 OK를 받은 후 배치가 즉시 활성화됩니까?

다음 `200 OK` API의 응답은 일괄 처리가 수락되었음을 의미합니다. 활성 또는 실패와 같은 최종 상태로 전환될 때까지 활성화되지 않습니다.

### CompleteBatch API 호출이 실패한 후 다시 시도해도 안전합니까?

예 - API 호출을 다시 시도하는 것이 안전합니다. 실패 시 작업이 실제로 성공하고 일괄 처리가 성공적으로 수락되었을 수 있습니다. 그러나 클라이언트는 API 실패 시 재시도 메커니즘이 있어야 하며 실제로 다시 시도하는 것이 좋습니다. 작업이 실제로 성공하면 API가 재시도한 후에도 성공을 반환합니다.

### 대용량 파일 업로드 API는 언제 사용해야 합니까?

대용량 파일 업로드 API 사용에 권장되는 파일 크기는 256MB 이상입니다. 대용량 파일 업로드 API 사용 방법에 대한 자세한 내용은 [여기](./api-overview.md#ingest-large-parquet-files).

### 큰 파일 전체 API 호출이 실패하는 이유는 무엇입니까?

큰 파일의 청크가 겹치거나 누락된 경우 서버가 HTTP 400 잘못된 요청으로 응답합니다. 이 문제는 파일 청크가 함께 결합될 때 범위 유효성 검사가 수행되므로 겹치는 청크를 업로드할 수 있으므로 발생할 수 있습니다.

## 수집 지원

### 지원되는 수집 형식은 무엇입니까?

현재 Parquet과 JSON이 모두 지원됩니다. CSV는 이전 기반으로 지원됩니다. 데이터는 마스터로 승격되고 사전 검사는 수행됩니다. 하지만 전환, 분할 또는 행 유효성 검사와 같은 최신 기능은 지원되지 않습니다.

### 배치 입력 형식을 지정할 위치

입력 형식은 페이로드 내에서 일괄 생성 시 지정해야 합니다. 배치 입력 형식을 지정하는 방법의 예는 다음과 같습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 업로드된 데이터가 데이터 세트에 표시되지 않는 이유는 무엇입니까?

데이터가 데이터 집합에 표시되려면 일괄 처리가 완료로 표시되어야 합니다. 일괄 처리를 완료로 표시하기 전에 수집하려는 모든 파일을 업로드해야 합니다. 일괄 처리를 완료로 표시하는 예는 다음과 같습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 여러 줄 JSON을 어떻게 수집할 수 있습니까?

여러 줄 JSON을 수집하려면 `isMultiLineJson` 플래그는 배치를 만들 때 설정해야 합니다. 이 방법의 예는 다음과 같습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON 라인(단일 행 JSON)과 다중 라인 JSON의 차이점은 무엇입니까?

JSON 라인의 경우 행당 하나의 JSON 개체가 있습니다. 예:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

여러 줄 JSON의 경우 한 개체가 여러 행을 차지할 수 있지만 모든 개체는 JSON 배열에 래핑됩니다. 예:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

기본적으로 [!DNL Batch Data Ingestion] 에서는 단일 행 JSON을 사용합니다.

### CSV 수집이 지원됩니까?

CSV 수집은 플랫 스키마에만 지원됩니다. 현재 CSV로 계층 데이터를 섭취하는 것은 지원되지 않습니다.

모든 데이터 수집 기능을 사용하려면 JSON 또는 Parquet 형식을 사용해야 합니다.

### 데이터에 대해 어떤 유형의 유효성 검사가 수행됩니까?

데이터에 대해 수행된 세 가지 수준의 유효성 검사가 있습니다.

- 스키마 - 배치 수집을 사용하면 수집된 데이터의 스키마가 데이터 세트의 스키마와 일치하도록 합니다.
- 데이터 유형 - 일괄 처리를 통해 수집된 각 필드의 유형이 데이터 집합 스키마에 정의된 유형과 일치하는지 확인할 수 있습니다.
- 제한 - 배치 수집 기능을 사용하면 스키마 정의에 &quot;필수&quot;, &quot;열거형&quot; 및 &quot;형식&quot;과 같은 제한이 제대로 정의되어 있을 수 있습니다.

### 이미 수집된 배치를 어떻게 대체할 수 있습니까?

이미 수집된 일괄 처리는 [일괄 재생] 기능을 사용하여 대체할 수 있습니다. 배치 재생에 대한 자세한 내용은 [여기](./api-overview.md#replay-a-batch).

### 일괄 처리는 어떻게 모니터링됩니까?

일괄 처리 프로모션에 대해 일괄 처리를 시그널링했으면 다음 요청으로 배치 수집 진행 상황을 모니터링할 수 있습니다.

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

이 요청을 사용하면 다음과 유사한 응답을 받게 됩니다.

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## 배치 상태

### 가능한 배치 상태는 무엇입니까?

배치는 해당 라이프사이클에서 다음 상태를 진행할 수 있습니다.

| 상태 | 기본으로 작성된 데이터 | 설명 |
| ------ | ---------------------- | ----------- |
| 포기 |  | 클라이언트가 예상 기간에 배치를 완료하지 못했습니다. |
| 중단됨 |  | 클라이언트가 을 통해 명시적으로 를 호출했습니다. [!DNL Batch Data Ingestion] API, 지정된 배치에 대한 중단 작업. 일괄 처리가 로드된 상태이면 일괄 처리를 중단할 수 없습니다. |
| 활성/성공 | x | 일괄 처리가 단계에서 마스터로 성공적으로 승격되었으며, 이제 다운스트림 소비에 사용할 수 있습니다. **참고:** 활성 과 성공 은 서로 교환하여 사용됩니다. |
| 보관됨 |  | 일괄 처리가 냉장 저장고에 보관되었다. |
| 실패/실패 |  | 잘못된 구성 및/또는 잘못된 데이터에서 발생하는 터미널 상태입니다. 클라이언트가 데이터를 수정하고 다시 제출할 수 있도록 조치 가능한 오류가 배치와 함께 기록됩니다. **참고:** 실패 및 실패 가 서로 교환하여 사용됩니다. |
| 비활성 | x | 일괄 처리가 성공적으로 승격되었지만 복귀되었거나 만료되었습니다. 일괄 처리는 더 이상 다운스트림 소비에 사용할 수 없지만 기본 데이터는 유지, 보관 또는 삭제할 때까지 기본으로 유지됩니다. |
| 로드 중 |  | 클라이언트가 현재 배치에 대한 데이터를 쓰고 있습니다. 일괄 처리가 **not** 이 시점에서 승격 준비 |
| 로드됨 |  | 클라이언트가 일괄 처리에 대한 데이터 작성을 완료했습니다. 배치가 승진을 위해 준비되었습니다. |
| 보존됨 |  | 데이터는 기본에서, 그리고 Adobe Data Lake의 지정된 보관소에 있습니다. |
| 스테이징 |  | 클라이언트가 프로모션용 배치를 성공적으로 시그널링했으며 다운스트림으로 소비를 위해 데이터가 준비 중입니다. |
| 다시 시도 중 |  | 클라이언트가 프로모션용 배치를 알리는 신호를 보냈지만, 오류로 인해 배치 모니터링 서비스에 의해 일괄 처리가 재시도됩니다. 이 상태는 클라이언트의 데이터 섭취가 지연될 수 있음을 알리는 데 사용할 수 있습니다. |
| 정지된 상태 |  | 클라이언트가 프로모션 배치를 표시했지만, 이후 `n` 배치 모니터링 서비스별 다시 시도, 배치 프로모션이 중단되었습니다. |

### 배치의 &quot;스테이징&quot;은 무엇을 의미합니까?

일괄 처리가 &quot;스테이징&quot;에 있는 경우, 일괄 처리가 성공적으로 판촉 신호를 보냈으며, 다운스트림으로 소비를 위해 데이터가 스테이징되고 있음을 의미합니다.

### 일괄 처리가 &quot;재시도&quot;일 때 의미하는 것은 무엇입니까?

일괄 처리가 &quot;재시도 중&quot;에 있으면 일시적인 문제로 인해 일괄 처리의 데이터 처리가 일시적으로 중단되었음을 의미합니다. 이러한 경우 고객의 개입이 필요하지 않습니다.

### 배치가 &quot;정지됨&quot;일 때 어떤 의미입니까?

일괄 처리가 &quot;정지됨&quot;에 있으면, [!DNL Data Ingestion Services] 일괄 처리를 섭취하는 데 어려움을 겪고 있으며 모든 다시 시도 작업이 모두 소진되었습니다.

### 배치가 여전히 &quot;로드 중&quot;이면 어떤 의미입니까?

일괄 처리가 &quot;로드 중&quot;에 있으면 일괄 처리를 프로모션하기 위해 CompleteBatch API가 호출되지 않았음을 의미합니다.

### 일괄 처리가 성공적으로 수집되었는지 확인하는 방법이 있습니까?

배치 상태가 &quot;활성&quot;이면 성공적으로 배치를 수집했습니다. 배치의 상태를 확인하려면 상세 단계를 수행합니다 [이전](#how-is-batch-ingestion-monitored).

### 배치에 실패하면 어떻게 됩니까?

배치가 실패하면, `errors` 섹션에 있는 마지막 항목이 될 필요가 없습니다. 오류의 예는 다음과 같습니다.

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

오류가 수정되면 배치를 다시 업로드할 수 있습니다.

## 일괄 지원

### 배치를 삭제하려면 어떻게 해야 합니까?

에서 직접 삭제하는 대신 [!DNL Catalog], 배치는 아래에 제공된 방법 중 하나를 사용하여 제거해야 합니다.

1. 일괄 처리가 진행 중인 경우 일괄 처리가 중단됩니다.
2. 배치가 성공적으로 마스터되면 배치를 되돌려야 합니다.

### 사용할 수 있는 배치 수준 지표는 무엇입니까?

활성/성공 상태의 배치에는 다음 배치 수준 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| ------ | ----------- |
| inputByteSize | 에 대해 준비된 총 바이트 수 [!DNL Data Ingestion Services] 처리합니다. |
| inputRecordSize | 에 대해 준비된 총 행 수 [!DNL Data Ingestion Services] 처리합니다. |
| outputByteSize | 보낸 총 바이트 수 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| outputRecordSize | 에 의해 출력되는 총 행 수 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| partitionCount | 에 작성된 총 파티션 수 [!DNL Data Lake]. |

### 일부 배치에서 지표를 사용할 수 없는 이유는 무엇입니까?

일괄 처리에서 지표를 사용할 수 없는 두 가지 이유가 있습니다.

1. 일괄 처리가 활성/성공 상태로 성공적으로 설정되지 않았습니다.
2. 일괄 처리가 CSV 수집과 같은 이전 프로모션 경로를 사용하여 승격되었습니다.

### 다른 상태 코드는 무엇을 의미합니까?

| 상태 코드 | 설명 |
| ----------- | ----------- |
| 106 | 데이터 집합 파일이 비어 있습니다. |
| 118 | CSV 파일에 빈 머리글 행이 포함되어 있습니다. |
| 200 | 일괄 처리가 승인되었으며, 활성 또는 실패와 같은 최종 상태로 전환됩니다. 제출되면 배치를 `GetBatch` 엔드포인트. |
| 400 | 잘못된 요청. 일괄 처리에 청크가 없거나 겹치는 경우 반환됩니다. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
