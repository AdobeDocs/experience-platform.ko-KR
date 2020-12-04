---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Adobe Experience Platform 부분 배치 처리 개요
topic: overview
description: 이 문서에서는 일괄 처리 처리 통합 모니터링, 부분 배치 처리 오류 관리 및 부분 일괄 처리 처리 처리 유형에 대한 참조에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---


# 오류 진단 검색 중

Adobe Experience Platform은 데이터를 업로드하고 인제스트하는 두 가지 방법을 제공합니다. 다양한 파일 형식(예: CSV)을 사용하여 데이터를 삽입할 수 있는 일괄 처리 섭취 또는 스트리밍 끝점을 실시간으로 [!DNL Platform] 사용하는 데 데이터를 삽입할 수 있는 스트리밍 통합 기능을 사용할 수 있습니다.

이 문서에서는 일괄 처리 처리 통합 모니터링, 부분 배치 처리 오류 관리 및 부분 일괄 처리 처리 처리 유형에 대한 참조에 대해 설명합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):데이터를 보낼 수 있는 메서드입니다 [!DNL Experience Platform].

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Schema Registry]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## 다운로드 오류 진단 {#download-diagnostics}

Adobe Experience Platform을 사용하면 입력 파일에 대한 오류 진단을 다운로드할 수 있습니다. 진단 프로그램은 최대 30일 [!DNL Platform] 동안 유지됩니다.

### 입력 파일 나열 {#list-files}

다음 요청은 완료된 일괄 처리로 제공된 모든 파일의 목록을 검색합니다.

**API 형식**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회하고 있는 배치의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 진단이 저장된 위치를 설명하는 JSON 개체가 반환됩니다.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 입력 파일 진단 검색 {#retrieve-diagnostics}

서로 다른 모든 입력 파일 목록을 검색한 후에는 다음 요청을 사용하여 개별 파일의 진단을 검색할 수 있습니다.

**API 형식**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회하고 있는 배치의 ID입니다. |
| `{FILE}` | 액세스하는 파일의 이름입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 진단 기능이 저장된 위치를 설명하는 `path` 개체가 포함된 JSON 개체가 반환됩니다. 응답에서 JSON 라인 형식 `path` 으로 [개체를](https://jsonlines.org/) 반환합니다.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 일괄 처리 처리 오류 검색 {#retrieve-errors}

배치에 오류가 있는 경우 데이터를 다시 인제스트할 수 있도록 이러한 오류에 대한 오류 정보를 검색해야 합니다.

### 상태 확인 {#check-status}

인제스트된 배치의 상태를 확인하려면 GET 요청 경로에 배치의 ID를 제공해야 합니다.

**API 형식**

```http
GET /catalog/batches/{BATCH_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 상태를 확인할 배치의 `id` 값. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**오류 없는 응답**

배치 상태에 대한 자세한 정보가 포함된 성공적인 응답이 반환됩니다.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 에서 값을 빼서 파생될 수 `inputRecordCount` 있습니다 `outputRecordCount`. 이 값은 활성화되었는지 여부에 관계없이 모든 배치에서 `errorDiagnostics` 생성됩니다. |

**오류 발생 시 응답**

배치에 하나 이상의 오류가 있고 오류 진단을 사용할 수 있는 경우 응답에서는 페이로드 자체 및 다운로드 가능한 오류 파일 내에 있는 오류에 대한 자세한 정보를 반환합니다. 오류가 포함된 일괄 처리 상태는 여전히 성공 상태를 가질 수 있습니다.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 에서 값을 빼서 파생될 수 `inputRecordCount` 있습니다 `outputRecordCount`. 이 값은 활성화되었는지 여부에 관계없이 모든 배치에서 `errorDiagnostics` 생성됩니다. |
| `errors.recordCount` | 지정된 오류 코드에 실패한 행 수입니다. 이 값은 활성화된 **경우에만** `errorDiagnostics` 생성됩니다. |

>[!NOTE]
>
>오류 진단을 사용할 수 없는 경우 다음 오류 메시지가 대신 표시됩니다.
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 다음 단계 {#next-steps}

이 자습서에서는 부분 배치 처리 오류를 모니터링하는 방법을 다룹니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서를 참조하십시오](../batch-ingestion/api-overview.md).

## 부록 {#appendix}

이 섹션에서는 통합 오류 유형에 대한 보충 정보를 제공합니다.

### 부분 일괄 처리 오류 유형 {#partial-ingestion-types}

데이터 인제스트 시 부분 일괄 처리 문제에는 세 가지 다른 오류 유형이 있습니다.

- [읽을 수 없는 파일](#unreadable)
- [스키마 또는 헤더가 잘못되었습니다.](#schemas-headers)
- [구문 분석할 수 없는 행](#unparsable)

### 읽을 수 없는 파일 {#unreadable}

인제스트한 묶음에 읽을 수 없는 파일이 있는 경우 일괄 처리 자체에 배치 오류가 첨부됩니다. 실패한 배치 검색 [안내서에서는 실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다](../quality/retrieve-failed-batches.md).

### 스키마 또는 헤더가 잘못되었습니다. {#schemas-headers}

인제스트한 일괄 처리에 잘못된 스키마나 잘못된 머리글이 있는 경우 일괄 처리 자체에 배치의 오류가 첨부됩니다. 실패한 배치 검색 [안내서에서는 실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다](../quality/retrieve-failed-batches.md).

### 구문 분석할 수 없는 행 {#unparsable}

인제스트한 일괄 처리에서 구문 분석할 수 없는 행이 있는 경우 다음 요청을 사용하여 오류가 포함된 파일 목록을 볼 수 있습니다.

**API 형식**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 오류 정보를 검색하는 일괄 처리 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 오류가 있는 파일 목록을 반환합니다.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

그런 다음 진단 검색 끝점을 사용하여 오류에 대한 자세한 정보를 [검색할 수 있습니다](#retrieve-diagnostics).

오류 파일을 검색하는 샘플 응답은 아래에 나와 있습니다.

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
