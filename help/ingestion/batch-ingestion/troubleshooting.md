---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 일괄 처리 문제 해결 가이드
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 일괄 처리 문제 해결 가이드

이 설명서는 Adobe Experience Platform Batch Data Ingestion API와 관련된 FAQ에 대한 답변을 제공합니다.

## 일괄 처리 API 호출

### CompleteBatch API 파섹

API의 `200 OK` 응답은 일괄 처리가 승인되었음을 의미하며, 일괄 처리가 활성 또는 실패와 같은 최종 상태로 전환될 때까지 활성화되지 않습니다.

### CompleteBatch API 호출이 실패한 후 다시 시도해도 안전합니까?

예 - API 호출을 다시 시도해도 안전합니다. 실패 시 작업이 실제로 성공하여 일괄 처리가 성공적으로 수락될 수 있습니다. 그러나 API 실패 시 클라이언트는 다시 시도 메커니즘이 있어야 하며 실제로 다시 시도할 수 있습니다. 작업이 실제로 성공한 경우 API는 다시 시도해도 성공합니다.

### 대용량 파일 업로드 API는 언제 사용해야 합니까?

대용량 파일 업로드 API를 사용하는 데 권장되는 파일 크기는 256MB 이상입니다. 대용량 파일 업로드 API를 사용하는 방법에 대한 자세한 내용은 [여기에서](./api-overview.md#ingest-large-parquet-files)확인할 수 있습니다.

### 대용량 파일 전체 API 호출이 실패하는 이유는 무엇입니까?

큰 파일의 청크가 겹치거나 누락된 경우 서버는 HTTP 400 잘못된 요청으로 응답합니다. 파일 청크를 함께 결합할 때 범위 유효성 검사가 수행되므로 겹치는 청크를 업로드할 수 있기 때문에 이러한 문제가 발생할 수 있습니다.

## 통합 지원

### 지원되는 인제스트 포맷은 무엇입니까?

현재, Parentical 및 JSON이 모두 지원됩니다. CSV는 기존 기반으로 지원됩니다. 데이터는 마스터로 승격되고 예비 검사가 수행되지만 변환, 분할 또는 행 유효성 검사와 같은 최신 기능은 지원되지 않습니다.

### 배치 입력 형식을 어디에 지정해야 합니까?

입력 형식은 페이로드 내에서 일괄 생성 시 지정해야 합니다. 배치 입력 형식을 지정하는 방법의 예는 아래에 나와 있습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 다중 행 JSON은 어떻게 수집됩니까?

다중 행 JSON을 인제스트하려면 일괄 작성 시 플래그를 설정해야 합니다. `isMultiLineJson` 이 예제는 다음과 같습니다.

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON 라인(단일 행 JSON)과 다중 라인 JSON의 차이점은 무엇입니까?

JSON 라인의 경우 한 줄에 하나의 JSON 개체가 있습니다. 예:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

다중 행 JSON의 경우 하나의 개체가 여러 행을 차지하지만 모든 개체는 JSON 배열로 둘러싸여 있습니다. 예:

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

기본적으로 일괄 데이터 수집은 단일 행 JSON을 사용합니다.

### CSV 수집이 지원됩니까?

CSV 수집은 플랫 스키마에만 지원됩니다. 현재 CSV의 계층 데이터 인제스트는 지원되지 않습니다.

모든 데이터 통합 기능을 이용하려면 JSON 또는 쪽모이 세공 마루 포맷을 사용해야 합니다.

### 데이터에 대해 수행되는 유효성 검사 유형은 무엇입니까?

데이터에 대해 수행되는 유효성 검사에는 세 가지 수준이 있습니다.

- 스키마 - 일괄 처리를 통해 인제스트된 데이터의 스키마가 데이터 세트의 스키마와 일치하는지 확인할 수 있습니다.
- 데이터 유형 - 일괄 처리를 통해 인제스트된 각 필드의 유형이 데이터 세트 스키마에 정의된 유형과 일치하는지 확인합니다.
- 제약 조건 - 일괄 처리를 통해 &quot;필수&quot;, &quot;열거형&quot; 및 &quot;format&quot;과 같은 제약 조건을 스키마 정의에 올바르게 정의할 수 있습니다.

### 이미 인제스트된 배치를 어떻게 대체할 수 있습니까?

이미 인제스트된 배치를 배치 재생 기능을 사용하여 대체할 수 있습니다. 배치 재생에 대한 자세한 내용은 [여기에서](./api-overview.md#replay-a-batch)확인할 수 있습니다.

### 일괄 처리가 어떻게 모니터링됩니까?

일괄 처리 프로모션을 위해 일괄 처리를 전송하면 다음 요청을 통해 일괄 처리 진행 상태를 모니터링할 수 있습니다.

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

이 요청을 통해 다음과 유사한 응답을 받게 됩니다.

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

### 가능한 일괄 처리 상태는 무엇입니까?

일괄 처리는 라이프사이클에서 다음 상태를 처리할 수 있습니다.

| 상태 | 마스터에 기록된 데이터 | 설명 |
| ------ | ---------------------- | ----------- |
| 포기 |  | 클라이언트가 예상 기간에 배치를 완료하지 못했습니다. |
| 중단됨 |  | 클라이언트는 배치 데이터 통합 API를 통해 지정된 일괄 처리에 대한 중단 작업을 명시적으로 호출했습니다. 일괄 처리가 로드됨 상태에 있으면 일괄 처리를 중단할 수 없습니다. |
| 활성/성공 | x | 배치가 스테이지에서 마스터로 성공적으로 승격되었으며 이제 다운스트림 소비에 사용할 수 있습니다. **참고:** 활성 및 성공은 교환적으로 사용됩니다. |
| 보관 |  | 그 화분은 냉장 보관소에 보관되어 있다. |
| 실패/실패 |  | 잘못된 구성 및/또는 잘못된 데이터에서 발생하는 터미널 상태입니다. 클라이언트가 데이터를 수정하고 다시 제출할 수 있도록 일괄 처리와 함께 실행 가능한 오류가 기록됩니다. **참고:** 실패 및 실패가 혼용적으로 사용됩니다. |
| 비활성 | x | 배치가 성공적으로 승격되었지만 되돌려졌거나 만료되었습니다. 일괄 처리를 더 이상 다운스트림 소비에 사용할 수 없지만 기본 데이터는 보관, 보관 또는 다른 방법으로 삭제될 때까지 마스터에 남아 있습니다. |
| 로드 중 |  | 클라이언트는 현재 일괄 처리에 대한 데이터를 작성하고 있습니다. 이 시점에 배치가 프로모션할 준비가 **되지** 않았습니다. |
| 로드됨 |  | 클라이언트가 일괄 처리에 대한 데이터 작성을 완료했습니다. 배치가 홍보할 준비가 되었습니다. |
| 보존 |  | 이 데이터는 Master에서 제거되었으며 Adobe Data Lake의 지정된 보관소에 보관되었습니다. |
| 스테이징 |  | 클라이언트가 프로모션을 위해 배치를 성공적으로 신호를 보냈으며 다운스트림 소비를 위해 데이터를 준비 중입니다. |
| 다시 시도 중 |  | 클라이언트가 프로모션을 위해 배치를 표시했지만 오류로 인해 배치 모니터링 서비스에서 배치를 재시도합니다. 이 상태를 사용하여 데이터 인제스트가 지연될 수 있음을 클라이언트에 알릴 수 있습니다. |
| 중지됨 |  | 클라이언트가 일괄 프로모션을 위해 배치를 표시했지만 배치 모니터링 서비스에서 `n` 재시도 후 일괄 프로모션이 중단되었습니다. |

### 배치의 &quot;스테이징&quot;은 무엇을 의미합니까?

배치가 &quot;스테이징&quot;에 있을 때, 배치가 성공적으로 판촉 신호를 받았고 다운스트림 소비를 위해 데이터가 스테이징되고 있음을 의미합니다.

### 일괄 처리가 &quot;다시 시도 중&quot;일 때 의미하는 것은 무엇입니까?

일괄 처리가 &quot;다시 시도 중&quot;일 경우, 간헐적인 문제로 인해 일괄 처리 데이터 처리가 일시적으로 중단되었음을 의미합니다. 이러한 경우 고객의 개입이 필요하지 않습니다.

### 일괄 처리가 &quot;중단&quot;일 때 의미하는 것은 무엇입니까?

일괄 처리가 &quot;중단&quot;되면 데이터 통합 서비스에서 일괄 처리를 인제스트하는 데 어려움을 겪고 모든 재시도가 소진되었음을 의미합니다.

### 일괄 처리가 여전히 &quot;로드 중&quot;일 경우 이는 무엇을 의미합니까?

일괄 처리가 &quot;로드 중&quot;에 있을 때 일괄 처리를 홍보하기 위해 CompleteBatch API가 호출되지 않았음을 의미합니다.

### 일괄 처리가 성공적으로 수행되었는지 알 수 있는 방법이 있습니까?

배치 상태가 &quot;활성&quot;이면 배치가 성공적으로 인제스트되었습니다. 배치의 상태를 확인하려면 [앞서](#how-is-batch-ingestion-monitored)설명된 단계를 따르십시오.

### 일괄 처리에 실패한 후 어떻게 됩니까?

일괄 처리가 실패하면 페이로드 `errors` 섹션에서 실패 이유를 식별할 수 있습니다. 오류 예는 다음과 같습니다.

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

오류가 수정되면 일괄 처리를 다시 업로드할 수 있습니다.

## 일괄 지원

### 배치를 삭제하려면 어떻게 해야 합니까?

카탈로그에서 직접 삭제하는 대신 아래 제공된 방법 중 하나를 사용하여 배치를 제거해야 합니다.

1. 일괄 처리가 진행 중인 경우 일괄 처리가 취소되어야 합니다.
2. 배치가 성공적으로 마스터되면 배치를 되돌려야 합니다.

### 사용할 수 있는 일괄 수준 지표는 무엇입니까?

활성/성공 상태의 배치에는 다음 배치 수준 지표를 사용할 수 있습니다.

| 지표 | 설명 |
| ------ | ----------- |
| inputByteSize | 데이터 통합 서비스가 처리할 총 바이트 단계 수입니다. |
| inputRecordSize | Data Ingestion Services에서 처리할 총 단계 행 수입니다. |
| outputByteSize | 데이터 통합 서비스가 Data Lake로 출력한 총 바이트 수입니다. |
| outputRecordSize | 데이터 통합 서비스에서 Data Lake로 출력된 총 행 수입니다. |
| partitionCount | Data Lake에 기록된 총 파티션 수입니다. |

### 일부 배치에서 지표를 사용할 수 없는 이유는 무엇입니까?

일괄 처리에서 지표를 사용할 수 없는 이유는 두 가지가 있습니다.

1. 일괄 처리가 활성/성공 상태로 성공적으로 만들어지지 않았습니다.
2. CSV 수집과 같은 이전 프로모션 경로를 사용하여 일괄 처리가 승격되었습니다.

### 다른 상태 코드는 무엇을 의미합니까?

| 상태 코드 | 설명 |
| ----------- | ----------- |
| 106 | 데이터 집합 파일이 비어 있습니다. |
| 118 | CSV 파일에 빈 헤더 행이 있습니다. |
| 200 | 일괄 처리가 승인되었으며 활성 또는 실패와 같은 최종 상태로 전환됩니다. 제출하면 `GetBatch` 끝점을 사용하여 일괄 처리를 모니터링할 수 있습니다. |
| 400 | 잘못된 요청입니다. 일괄 처리에서 누락되거나 겹쳐진 청크가 있는 경우 반환됩니다. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
