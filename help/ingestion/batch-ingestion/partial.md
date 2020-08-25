---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 부분 배치 처리 개요
topic: overview
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---



# 부분 일괄 처리

부분 일괄 처리란 오류가 포함된 데이터를 특정 임계값까지 인제스트하는 기능입니다. 이 기능을 사용하면 사용자가 모든 올바른 데이터를 Adobe Experience Platform으로 성공적으로 인제스트할 수 있으며 모든 잘못된 데이터가 잘못된 이유에 대한 세부 정보와 함께 별도로 일괄적으로 묶을 수 있습니다.

이 문서에서는 부분 일괄 처리 처리를 관리하는 자습서를 제공합니다.

또한 이 자습서의 [부록은](#appendix) 부분 배치 처리 오류 유형에 대한 참조를 제공합니다.

## 시작하기

이 자습서에서는 부분 일괄 처리에 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 처리](./overview.md):CSV 및 [!DNL Platform] Portable과 같은 데이터 파일의 데이터를 인제하고 저장하는 방법입니다.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## API에서 부분 일괄 처리를 활성화합니다. {#enable-api}

>[!NOTE]
>
>이 섹션에서는 API를 사용하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. UI 사용에 대한 지침은 UI [단계에서 부분 일괄 처리를 위한 일괄 처리](#enable-ui) 활성화를 참조하십시오.

부분 처리가 활성화된 새 배치를 만들 수 있습니다.

새 배치를 만들려면 일괄 처리 통합 개발자 안내서의 [단계를 따릅니다](./api-overview.md). 배치 **[!UICONTROL 생성]** 단계에 도달하면 요청 본문 내에 다음 필드를 추가합니다.

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 일괄 처리에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있는 플래그. |
| `partialIngestionPercentage` | 전체 배치가 실패하기 전에 허용되는 오류 비율. 따라서 이 예에서는 일괄 처리가 실패하기 전에 최대 5%의 일괄 처리를 오류가 발생할 수 있습니다. |


## UI에서 부분 일괄 처리를 위한 일괄 처리 활성화 {#enable-ui}

>[!NOTE]
>
>이 섹션에서는 UI를 사용하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. API를 사용하여 부분 일괄 처리를 이미 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

UI를 통해 부분 섭취에 대한 배치를 활성화하려면 소스 연결을 통해 새 배치를 만들거나 기존 데이터 세트에 새 배치를 만들거나 &quot;CSV를 [!DNL Platform] XDM 플로우에 매핑&quot;을 통해 새 배치를 만들 수 있습니다.

### 새 소스 연결 만들기 {#new-source}

새 소스 연결을 만들려면 소스 [개요에 나열된 단계를 따릅니다](../../sources/home.md). 데이터 흐름 세부 **[!UICONTROL 정보]** 단계에 도달하면 **[!UICONTROL 부분 섭취]** 및 **[!UICONTROL 오류 진단]** 필드를참고합니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 *[!UICONTROL 통합]* 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 세트 사용 {#existing-dataset}

기존 데이터 세트를 사용하려면 먼저 데이터 세트를 선택합니다. 오른쪽의 세로 막대는 데이터 세트에 대한 정보를 채웁니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 **[!UICONTROL 통합]** 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

이제 데이터 **추가** 단추를 사용하여 데이터를 업로드할 수 있으며 부분 섭싱을 사용하여 인제스트됩니다.

### &quot;XDM 스키마에[!UICONTROL CSV 매핑&quot; 흐름을]사용하십시오 {#map-flow}

&quot;[!UICONTROL CSV를 XDM 스키마에]매핑&quot; 흐름을 사용하려면 CSV 파일 [매핑 자습서에 나열된 단계를 따르십시오](../tutorials/map-a-csv-file.md). 데이터 **[!UICONTROL 추가]** 단계에 도달하면 **[!UICONTROL 부분 섭취]** 및 **[!UICONTROL 오류 진단]** 필드를참고하십시오.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 **[!UICONTROL 통합]** 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 파일 수준 메타데이터 다운로드 {#download-metadata}

Adobe Experience Platform을 사용하면 입력 파일의 메타데이터를 다운로드할 수 있습니다. 메타데이터는 최대 30일 동안 [!DNL Platform] 유지됩니다.

### 입력 파일 나열 {#list-files}

다음 요청을 통해 완성된 배치로 제공된 모든 파일의 목록을 볼 수 있습니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 메타데이터가 저장된 위치를 설명하는 경로 개체가 포함된 JSON 개체가 있는 HTTP 상태 200이 반환됩니다.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 입력 파일 메타데이터 검색 {#retrieve-metadata}

서로 다른 모든 입력 파일 목록을 검색한 후에는 다음 끝점을 사용하여 개별 파일의 메타데이터를 검색할 수 있습니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 메타데이터가 저장된 위치를 설명하는 경로 개체가 포함된 JSON 개체가 있는 HTTP 상태 200이 반환됩니다.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 부분 일괄 처리 처리 오류 검색 {#retrieve-errors}

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**오류 없는 응답**

성공적인 응답은 일괄 처리 상태에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 에서 값을 빼서 파생될 수 `inputRecordCount` 있습니다 `outputRecordCount`. 이 값은 활성화되었는지에 관계없이 모든 배치에서 `errorDiagnostics` 생성됩니다. |

**오류 발생 시 응답**

일괄 처리에서 하나 이상의 오류가 발생하고 오류 진단을 사용할 수 있는 경우 상태 `success` 에 응답에 제공된 오류와 다운로드 가능한 오류 파일에 모두 대한 자세한 정보가 표시됩니다.

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
| `metrics.failedRecordCount` | 구문 분석, 변환 또는 유효성 검사로 인해 처리할 수 없는 행 수입니다. 이 값은 에서 값을 빼서 파생될 수 `inputRecordCount` 있습니다 `outputRecordCount`. 이 값은 활성화되었는지에 관계없이 모든 배치에서 `errorDiagnostics` 생성됩니다. |
| `errors.recordCount` | 지정된 오류 코드에 실패한 행 수입니다. 이 값은 활성화된 **경우에만** `errorDiagnostics` 생성됩니다. |

>[!NOTE]
>
>오류 진단을 사용할 수 없는 경우 다음 오류 메시지가 대신 표시됩니다.
>
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## 다음 단계 {#next-steps}

이 자습서에서는 데이터 세트를 만들거나 수정하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서를 참조하십시오](./api-overview.md).

## 부분 일괄 처리 오류 유형 {#appendix}

데이터를 인제스트할 때 부분 일괄 처리에는 세 가지 다른 오류 유형이 있습니다.

- [읽을 수 없는 파일](#unreadable)
- [스키마 또는 헤더가 잘못되었습니다.](#schemas-headers)
- [구문 분석할 수 없는 행](#unparsable)

### 읽을 수 없는 파일 {#unreadable}

인제스트한 묶음에 읽을 수 없는 파일이 있는 경우 일괄 처리 자체에 배치 오류가 첨부됩니다. 실패한 배치 검색 [안내서에서는 실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다](../quality/retrieve-failed-batches.md).

### 스키마 또는 헤더가 잘못되었습니다. {#schemas-headers}

인제스트한 일괄 처리에 잘못된 스키마나 잘못된 머리글이 있는 경우 일괄 처리 자체에 배치의 오류가 첨부됩니다. 실패한 배치 검색 [안내서에서는 실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다](../quality/retrieve-failed-batches.md).

### 구문 분석할 수 없는 행 {#unparsable}

인제스트한 일괄 처리에서 구문 분석할 수 없는 행이 있는 경우 다음 끝점을 사용하여 오류가 포함된 파일 목록을 볼 수 있습니다.

**API 형식**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 오류 정보를 검색하는 일괄 처리 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 오류가 있는 파일 목록과 함께 HTTP 상태 200을 반환합니다.

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

그런 다음 [메타데이터 검색 끝점을 사용하여 오류에 대한 자세한 정보를 검색할 수 있습니다](#retrieve-metadata).

오류 파일을 검색하는 샘플 응답은 아래에 나와 있습니다.

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
