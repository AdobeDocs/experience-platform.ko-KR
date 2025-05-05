---
keywords: Experience Platform;홈;자주 찾는 주제;수집된 데이터;문제 해결;faq;수집;일괄 처리 수집;일괄 처리 수집;
solution: Experience Platform
title: 일괄 처리 수집 문제 해결 안내서
description: 이 설명서는 Adobe Experience Platform 배치 데이터 수집 API와 관련하여 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 37b241f15f297263cc7aa20f382c115a2d131c7e
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# 일괄 처리 수집 문제 해결 안내서

이 설명서는 Adobe Experience Platform [!DNL Batch Data Ingestion] API와 관련하여 자주 묻는 질문에 답변하는 데 도움이 됩니다.

## 일괄 처리 API 호출

### CompleteBatch API에서 HTTP 200 OK를 수신한 후 배치가 즉시 활성화됩니까?

API의 `200 OK` 응답은 일괄 처리가 처리에 수락되었음을 의미합니다. 활성 또는 실패와 같은 최종 상태로 전환되기 전까지는 활성화되지 않습니다.

### 실패한 후 CompleteBatch API 호출을 다시 시도하는 것이 안전합니까?

예 - API 호출을 다시 시도하는 것이 안전합니다. 실패에도 불구하고 작업이 실제로 성공하고 배치가 성공적으로 수락되었을 수 있습니다. 그러나 클라이언트는 API 실패 시 재시도 메커니즘이 있어야 하며 실제로 재시도하는 것이 좋습니다. 작업이 실제로 성공하면 API는 다시 시도한 후에도 성공을 반환합니다.

### 대용량 파일 업로드 API는 언제 사용해야 합니까?

대용량 파일 업로드 API 사용에 권장되는 파일 크기는 256MB 이상입니다. 대용량 파일 업로드 API를 사용하는 방법에 대한 자세한 내용은 [여기](./api-overview.md#ingest-large-parquet-files)에서 확인할 수 있습니다.

### 대형 파일 완료 API 호출이 실패한 이유는 무엇입니까?

큰 파일의 청크가 겹치거나 누락된 것으로 확인되면 서버는 HTTP 400 잘못된 요청에 응답합니다. 파일 청크를 함께 결합할 때 파일 완료 시 범위 유효성 검사가 수행되므로 겹치는 청크를 업로드할 수 있으므로 이러한 문제가 발생할 수 있습니다.

## 수집 지원

### 지원되는 수집 형식은 무엇입니까?

현재 Parquet과 JSON이 모두 지원됩니다. CSV는 기존 방식으로 지원됩니다. 데이터가 마스터로 승격되고 사전 검사가 수행되는 동안 전환, 파티션 나누기 또는 행 유효성 검사와 같은 최신 기능은 지원되지 않습니다.

### 배치 입력 형식은 어디에서 지정해야 합니까?

페이로드 내에서 일괄 생성 시 입력 형식을 지정해야 합니다. 배치 입력 형식을 지정하는 방법의 예는 아래에서 확인할 수 있습니다.

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

데이터가 데이터 세트에 표시되도록 하려면 배치를 완료로 표시해야 합니다. 수집하려는 모든 파일을 업로드한 후에 배치를 완료로 표시해야 합니다. 배치를 완료로 표시하는 예는 아래에서 확인할 수 있습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 멀티라인 JSON은 어떻게 수집됩니까?

여러 줄 JSON을 수집하려면 일괄 처리를 만들 때 `isMultiLineJson` 플래그를 설정해야 합니다. 이에 대한 예는 아래에서 확인할 수 있습니다.

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

### JSON 라인(단일 라인 JSON)과 다중 라인 JSON 간의 차이점은 무엇입니까?

JSON 라인의 경우 라인당 JSON 오브젝트가 한 개 있습니다. 예:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

여러 줄 JSON의 경우 한 개체가 여러 줄을 차지할 수 있지만 모든 개체는 JSON 배열에 래핑됩니다. 예:

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

기본적으로 [!DNL Batch Data Ingestion]은(는) 한 줄 JSON을 사용합니다.

### CSV 수집이 지원됩니까?

CSV 수집은 플랫 스키마에 대해서만 지원됩니다. 현재 CSV로 계층 데이터 수집은 지원되지 않습니다.

모든 데이터 수집 기능을 가져오려면 JSON 또는 Parquet 형식을 사용해야 합니다.

### 데이터에 대해 수행되는 유효성 검사 유형

데이터에 대해 세 가지 수준의 유효성 검사가 수행됩니다.

- 스키마 - 일괄 처리 수집은 수집된 데이터의 스키마가 데이터 세트의 스키마와 일치하는지 확인합니다.
- 데이터 유형 - 일괄 처리 수집을 통해 수집된 각 필드의 유형이 데이터 세트의 스키마에 정의된 유형과 일치하는지 확인합니다.
- 제한 - 일괄 처리 수집을 통해 &quot;필수&quot;, &quot;열거형&quot; 및 &quot;형식&quot;과 같은 제한이 스키마 정의에 올바르게 정의되도록 합니다.

### 이미 수집된 일괄 처리를 어떻게 대체할 수 있습니까?

이미 수집된 배치는 배치 재생 기능을 사용하여 대체할 수 있습니다. 배치 재생에 대한 자세한 내용은 [여기](./api-overview.md#replay-a-batch)를 참조하십시오.

### 일괄 처리 수집은 어떻게 모니터링됩니까?

배치 판촉에 대한 배치의 신호를 받으면 다음 요청으로 배치 수집 진행률을 모니터링할 수 있습니다.

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

## 일괄 처리 상태

### 가능한 배치 상태는 무엇입니까?

배치는 해당 수명 주기에서 다음 상태를 거칠 수 있습니다.

| 상태 | 기본으로 기록된 데이터 | 설명 |
| ------ | ---------------------- | ----------- |
| 포기 | | 클라이언트가 예상 기간에 일괄 처리를 완료하지 못했습니다. |
| 중단됨 | | 클라이언트가 [!DNL Batch Data Ingestion] API를 통해 지정된 일괄 처리에 대한 중단 작업을 명시적으로 호출했습니다. 배치가 로드된 상태이면 배치를 중단할 수 없습니다. |
| 활성/성공 | x | 배치가 스테이지에서 마스터로 성공적으로 승격되었으며 이제 다운스트림 소비에 사용할 수 있습니다. **참고:** Active와 Success는 서로 다르게 사용됩니다. |
| 보관 | | 배치가 냉동 보관소에 보관되었습니다. |
| 실패/실패 | | 잘못된 구성 및/또는 잘못된 데이터로 인한 터미널 상태입니다. 실행 가능한 오류는 배치와 함께 기록되어 클라이언트가 데이터를 수정하고 다시 제출할 수 있습니다. **참고:**&#x200B;이(가) 실패했으며 실패는 서로 교환하여 사용됩니다. |
| 비활성 | x | 배치가 정상적으로 홍보되었지만, 되돌리거나 만료되었습니다. 배치를 더 이상 다운스트림 소비에 사용할 수 없지만 기본 데이터는 유지, 보관 또는 삭제될 때까지 기본으로 유지됩니다. |
| 로드 중 | | 클라이언트가 현재 배치에 대한 데이터를 쓰고 있습니다. 이 시점에서 일괄 처리를 승격할 준비가 **되지 않음**&#x200B;되었습니다. |
| 로드됨 | | 클라이언트가 배치에 대한 데이터 쓰기를 완료했습니다. 배치를 승격할 준비가 되었습니다. |
| 유지됨 | | 데이터는 기본으로 제거되고 Adobe 데이터 레이크의 지정된 아카이브에 있습니다. |
| 스테이징 | | 클라이언트가 프로모션을 위해 배치의 신호를 성공적으로 보냈으며, 데이터는 소비 다운스트림용으로 스테이징되고 있습니다. |
| 재시도 | | 클라이언트가 프로모션을 위해 배치에 신호를 보냈지만 오류로 인해 배치 모니터링 서비스에서 배치를 재시도합니다. 이 상태는 데이터 수집이 지연될 수 있음을 클라이언트에게 알리는 데 사용할 수 있습니다. |
| 정지됨 | | 클라이언트가 승격용 일괄 처리에 신호를 보냈지만 일괄 모니터링 서비스에서 `n`번 다시 시도한 후 일괄 처리 승격이 중지되었습니다. |

### 일괄 처리에 대한 &quot;스테이징&quot;은 무엇을 의미합니까?

배치가 &quot;스테이징&quot;에 있는 경우, 배치는 프로모션용 신호를 성공적으로 받았으며 데이터는 소비 다운스트림용 스테이징됨을 의미합니다.

### 일괄 처리가 &quot;재시도&quot;될 때 무엇을 의미합니까?

일괄 처리가 &quot;재시도 중&quot;이면 일시적인 문제로 인해 일괄 처리의 데이터 수집이 일시적으로 중단되었음을 의미합니다. 이 경우 고객의 개입이 필요하지 않습니다.

### 일괄 처리가 &quot;정지됨&quot;일 때 무엇을 의미합니까?

일괄 처리가 &quot;정지됨&quot;이면 [!DNL Data Ingestion Services]에서 일괄 처리를 수집하는 데 문제가 발생하고 있으며 모든 다시 시도가 모두 완료되었음을 의미합니다.

### 일괄 처리가 여전히 &quot;로드 중&quot;인 경우 무엇을 의미합니까?

일괄 처리가 &quot;로드 중&quot;이면 일괄 처리를 승격하기 위해 CompleteBatch API가 호출되지 않았음을 의미합니다.

### 배치가 성공적으로 수집되었는지 확인할 수 있는 방법이 있습니까?

예. 일괄 처리 상태가 &quot;활성&quot;이면 일괄 처리가 정상적으로 수집되었습니다. 일괄 처리 상태를 확인하려면 자세한 [이전](#how-is-batch-ingestion-monitored) 단계를 따르세요.

### 일괄 처리가 실패하면 어떻게 됩니까? {#what-if-a-batch-fails}

일괄 처리가 실패하면 프로세스가 중지되고 `Failure` 상태가 반환됩니다. 실패한 이유는 페이로드의 `errors` 섹션에서 확인할 수 있습니다. 오류의 예는 아래에서 확인할 수 있습니다.

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

### 일괄 처리를 삭제하려면 어떻게 해야 합니까?

[!DNL Catalog]에서 직접 삭제하는 대신 아래에 제공된 방법 중 하나를 사용하여 배치를 제거해야 합니다.

1. 배치가 진행 중인 경우 배치를 중단해야 합니다.
2. 배치가 성공적으로 마스터되면 배치를 되돌려야 합니다.

### 어떤 배치 수준 지표를 사용할 수 있습니까?

다음 배치 수준 지표는 활성/성공 상태의 배치에 사용할 수 있습니다.

| 지표 | 설명 |
| ------ | ----------- |
| 입력 바이트 크기 | 처리할 [!DNL Data Ingestion Services]에 대해 준비된 총 바이트 수입니다. |
| 입력 레코드 크기 | 처리할 [!DNL Data Ingestion Services]의 준비된 총 행 수입니다. |
| 출력 바이트 크기 | [!DNL Data Ingestion Services]에서 [!DNL Data Lake] (으)로 출력한 총 바이트 수입니다. |
| 출력 레코드 크기 | [!DNL Data Ingestion Services]에서 [!DNL Data Lake] (으)로 출력하는 총 행 수입니다. |
| partitionCount | [!DNL Data Lake]에 기록된 총 파티션 수입니다. |

### 일부 배치에서 지표를 사용할 수 없는 이유는 무엇입니까?

배치에서 지표를 사용할 수 없는 이유는 두 가지가 있습니다.

1. 배치가 성공적으로 활성/성공 상태가 되지 않았습니다.
2. 배치가 CSV 수집과 같은 레거시 프로모션 경로를 사용하여 홍보되었습니다.

### 다양한 상태 코드는 무엇을 의미합니까?

| 상태 코드 | 설명 |
| ----------- | ----------- |
| 106 | 데이터 세트 파일이 비어 있습니다. |
| 118 | CSV 파일에 빈 헤더 행이 포함되어 있습니다. |
| 200 | 배치가 처리에 수락되었으며 활성 또는 실패와 같은 최종 상태로 전환됩니다. 제출되면 `GetBatch` 끝점을 사용하여 일괄 처리를 모니터링할 수 있습니다. |
| 400 | 잘못된 요청. 일괄 처리에 누락되거나 겹치는 청크가 있는 경우 반환됩니다. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
