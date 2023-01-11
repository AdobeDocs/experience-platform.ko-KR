---
keywords: Experience Platform;홈;인기 항목;일괄 처리 수집;일괄 처리 수집;부분 수집;오류 검색;오류 검색;부분 배치 수집;부분 배치 수집;수집;부분;수집;수집;오류 진단;오류 진단 검색;오류 진단 가져오기;오류 가져오기;오류 가져오기;오류 검색
solution: Experience Platform
title: 데이터 수집 오류 진단 검색
description: 이 문서에서는 배치 수집 모니터링, 부분 배치 수집 오류 관리 및 부분 배치 수집 유형에 대한 참조에 대해 설명합니다.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 2%

---

# 데이터 수집 오류 진단 검색

Adobe Experience Platform에서는 데이터를 업로드하고 수집하는 두 가지 방법을 제공합니다. 일괄 처리 수집을 사용할 수 있습니다. 이 통합 기능을 사용하면 다양한 파일 유형(예: CSV)을 사용하여 데이터를 삽입하거나 스트리밍 수집 기능을 사용하여 데이터를 삽입할 수 있습니다 [!DNL Platform] 스트리밍 끝점을 실시간으로 사용합니다.

이 문서에서는 배치 수집 모니터링, 부분 배치 수집 오류 관리 및 부분 배치 수집 유형에 대한 참조에 대해 설명합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): 데이터를 보낼 수 있는 메서드입니다 [!DNL Experience Platform].

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Schema Registry]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

## 오류 진단 다운로드 중 {#download-diagnostics}

Adobe Experience Platform을 사용하면 입력 파일에 대한 오류 진단 프로그램을 다운로드할 수 있습니다. 진단 프로그램은 [!DNL Platform] 최대 30일.

### 입력 파일 나열 {#list-files}

다음 요청은 완료된 배치에 제공된 모든 파일의 목록을 검색합니다.

**API 형식**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회 중인 배치의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

여러 입력 파일의 목록을 검색한 후에는 다음 요청을 사용하여 개별 파일의 진단 유틸리티를 검색할 수 있습니다.

**API 형식**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 조회 중인 배치의 ID입니다. |
| `{FILE}` | 액세스하는 파일의 이름입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음을 포함하는 JSON 개체를 반환합니다 `path` 진단 프로그램이 저장된 위치를 설명하는 개체입니다. 응답에서 `path` 개체 [JSON 라인](https://jsonlines.readthedocs.io/en/latest/) 형식 지정

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 배치 수집 오류 검색 {#retrieve-errors}

배치에 오류가 포함된 경우 데이터를 다시 수집할 수 있도록 이러한 오류에 대한 오류 정보를 검색해야 합니다.

### 상태 확인 {#check-status}

수집된 일괄 처리의 상태를 확인하려면 GET 요청의 경로에 일괄 처리의 ID를 제공해야 합니다. 이 API 호출 사용에 대한 자세한 내용은 [카탈로그 끝점 안내서](../../catalog/api/list-objects.md).

**API 형식**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 다음 `id` 상태를 확인할 배치의 값입니다. |
| `{FILTER}` | 응답에서 반환된 결과를 필터링하는 데 사용되는 쿼리 매개 변수입니다. 여러 매개 변수는 앰퍼샌드(`&`). 자세한 내용은 다음 안내서를 참조하십시오. [카탈로그 데이터 필터링](../../catalog/api/filter-data.md). |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**오류 없는 응답**

배치 상태에 대한 세부 정보와 함께 성공적인 응답이 반환됩니다.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 `inputRecordCount` 에서 `outputRecordCount`. 이 값은 `errorDiagnostics` 이 활성화되어 있습니다. |

**오류가 있는 응답**

배치에 하나 이상의 오류가 있고 오류 진단이 활성화된 경우 페이로드 자체 및 다운로드 가능한 오류 파일 내의 오류에 대한 자세한 정보가 응답에 반환됩니다. 오류가 포함된 배치의 상태는 여전히 성공 상태일 수 있습니다.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 `inputRecordCount` 에서 `outputRecordCount`. 이 값은 `errorDiagnostics` 이 활성화되어 있습니다. |
| `errors.recordCount` | 지정된 오류 코드에 대해 실패한 행 수입니다. 이 값은 **전용** 생성된 경우 `errorDiagnostics` 이 활성화되어 있습니다. |

>[!NOTE]
>
>오류 진단을 사용할 수 없으면 다음 오류 메시지가 대신 표시됩니다.
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

이 자습서에서는 부분 배치 수집 오류를 모니터링하는 방법을 다룹니다. 일괄 처리에 대한 자세한 내용은 [배치 수집 개발자 안내서](../batch-ingestion/api-overview.md).

## 부록 {#appendix}

이 섹션에서는 섭취 오류 유형에 대한 보충 정보를 제공합니다.

### 부분 배치 수집 오류 유형 {#partial-ingestion-types}

부분 배치 수집에는 데이터를 수집할 때 세 가지 다른 오류 유형이 있습니다.

- [읽을 수 없는 파일](#unreadable)
- [스키마 또는 헤더가 잘못되었습니다.](#schemas-headers)
- [구문 분석할 수 없는 행](#unparsable)

### 읽을 수 없는 파일 {#unreadable}

수집된 일괄 처리에 읽을 수 없는 파일이 있으면 일괄 처리 자체에 일괄 처리의 오류가 첨부됩니다. 실패한 배치 검색에 대한 자세한 내용은 [실패한 배치 가이드 검색](../quality/retrieve-failed-batches.md).

### 스키마 또는 헤더가 잘못되었습니다. {#schemas-headers}

수집된 일괄 처리에 잘못된 스키마나 잘못된 헤더가 있는 경우 일괄 처리 자체에 일괄 처리의 오류가 첨부됩니다. 실패한 배치 검색에 대한 자세한 내용은 [실패한 배치 가이드 검색](../quality/retrieve-failed-batches.md).

### 구문 분석할 수 없는 행 {#unparsable}

수집한 배치에 구문 분석할 수 없는 행이 있는 경우 다음 요청을 사용하여 오류가 포함된 파일 목록을 볼 수 있습니다.

**API 형식**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 다음 `id` 오류 정보를 검색하는 배치의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 오류가 있는 파일 목록이 반환됩니다.

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

그런 다음 를 사용하여 오류에 대한 세부 정보를 검색할 수 있습니다 [진단 검색 끝점](#retrieve-diagnostics).

오류 파일 검색에 대한 샘플 응답은 다음과 같습니다.

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
