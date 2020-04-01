---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 부분 일괄 처리 개요
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# 부분 일괄 처리

부분 일괄 처리란 오류가 포함된 데이터를 특정 임계값까지 인제스트하는 기능입니다. 이 기능을 사용하면 모든 올바른 데이터를 Adobe Experience Platform으로 성공적으로 인제스트할 수 있으며, 잘못된 모든 데이터를 잘못된 이유에 대한 세부 정보와 함께 별도로 일괄 처리할 수 있습니다.

이 문서에서는 부분 일괄 처리를 관리하는 자습서를 제공합니다.

또한 이 자습서의 [부록에서는](#partial-batch-ingestion-error-types) 부분 배치 처리 오류 유형에 대한 참조를 제공합니다.

## 시작하기

이 자습서에서는 부분 일괄 처리와 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 처리](./overview.md):플랫폼이 CSV 및 Partiquet과 같은 데이터 파일의 데이터를 인제스트 및 저장하는 방법입니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

## API에서 부분 일괄 처리를 위해 데이터 세트 활성화

>[!NOTE] 이 섹션에서는 API를 사용하여 부분 일괄 처리를 위한 데이터 세트 활성화에 대해 설명합니다. UI 사용에 대한 지침은 UI 단계에서 데이터 세트 [활성화를 참조하십시오](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) .

새 데이터 세트를 만들거나 부분 처리가 활성화된 기존 데이터 세트를 수정할 수 있습니다.

새로운 데이터 세트를 만들려면 데이터 세트 [만들기 자습서의](../../catalog/api/create-dataset.md)단계를 따릅니다. 데이터 세트 *만들기* 단계에 도달하면 요청 본문 내에 다음 필드를 추가합니다.

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `errorThresholdPercentage` | 전체 배치가 실패하기 전에 허용되는 오류 비율. |

마찬가지로 기존 데이터 세트를 수정하려면 카탈로그 개발자 안내서의 [단계를](../../catalog/api/update-object.md)따르십시오.

데이터 집합 내에서 위에 설명된 태그를 추가해야 합니다.

## UI에서 부분 일괄 처리를 위한 데이터 세트 활성화

>[!NOTE] 이 섹션에서는 UI를 사용하여 부분 일괄 처리를 위한 데이터 세트 활성화에 대해 설명합니다. API를 사용하여 부분 일괄 처리를 위해 이미 데이터 세트를 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

플랫폼 UI를 통해 데이터 세트를 부분 수집할 수 있도록 하려면 왼쪽 탐색 **영역에서 데이터** 세트를 클릭합니다. 새 데이터 세트를 [만들거나](#create-a-new-dataset-with-partial-batch-ingestion-enabled) 기존 데이터 세트를 [수정할 수 있습니다](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### 부분 일괄 처리가 활성화된 새 데이터 세트 만들기

새 데이터 세트를 만들려면 [데이터 세트 사용 안내서의](../../catalog/datasets/user-guide.md)단계를 따르십시오. 데이터 세트 구성 *단계에 도달하면 부분 통합* 및 *오류 진단* ** 필드를메모해둡니다.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

부분 *통합* 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 *진단* 토글은 부분 통합 토글이 꺼진 경우에만 ** 나타납니다. 이 기능을 사용하면 플랫폼에서 인제스트된 배치에 대한 자세한 오류 메시지를 생성할 수 있습니다. 부분 통합 *전환이* 켜져 있으면 향상된 오류 진단 기능이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

오류 *임계값을* 사용하면 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 세트를 수정하여 부분 일괄 처리 통합 활성화

기존 데이터 세트를 수정하려면 수정할 데이터 세트를 선택합니다. 오른쪽의 세로 막대는 데이터 세트에 대한 정보로 채워집니다.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

부분 *통합* 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 *임계값을* 사용하면 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 부분 일괄 처리 오류 검색

배치에 오류가 있는 경우 데이터를 다시 인제스트할 수 있도록 이러한 오류에 대한 오류 정보를 검색해야 합니다.

### 상태 확인

인제스트된 배치의 상태를 확인하려면 GET 요청 경로에 일괄 처리 ID를 제공해야 합니다.

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

**응답**

성공적인 응답은 일괄 처리의 상태에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
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
            "outputRecordCount": 497
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

일괄 처리에 오류가 있고 오류 진단을 활성화한 경우, 상태는 &quot;성공&quot;이며 다운로드 가능한 오류 파일에 제공된 오류에 대한 자세한 정보가 표시됩니다.

## 다음 단계

이 자습서에서는 데이터 세트를 만들거나 수정하여 부분 일괄 처리를 활성화하는 방법에 대해 다룹니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서를](./api-overview.md)참조하십시오.

## 부분 일괄 처리 오류 유형

데이터 인제스트 시 부분 일괄 처리에는 4가지 오류 유형이 있습니다.

- [읽을 수 없는 파일](#unreadable)
- [스키마 또는 헤더가 잘못되었습니다.](#schemas-headers)
- [구문 분석할 수 없는 행](#unparsable)
- [잘못된 XDM 변환](#conversion)

### 읽을 수 없는 파일 {#unreadable}

인제스트한 일괄 처리에 읽을 수 없는 파일이 있으면 일괄 처리 자체에 일괄 처리 오류가 첨부됩니다. 실패한 배치 [검색 안내서에서는](../quality/retrieve-failed-batches.md)실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다.

### 스키마 또는 헤더가 잘못되었습니다. {#schemas-headers}

일괄 인제스트된 항목에 잘못된 스키마나 잘못된 머리글이 있는 경우 일괄 처리 자체에 배치의 오류가 첨부됩니다. 실패한 배치 [검색 안내서에서는](../quality/retrieve-failed-batches.md)실패한 배치 검색에 대한 자세한 정보를 확인할 수 있습니다.

### 구문 분석할 수 없는 행 {#unparsable}

인제스트된 일괄 처리에 구문 분석할 수 없는 행이 있는 경우, 일괄 처리 오류는 아래에 설명된 끝점을 사용하여 액세스할 수 있는 파일에 저장됩니다.

**API 형식**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 오류 정보를 검색하는 배치의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 구문 분석할 수 없는 행에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### 잘못된 XDM 변환 {#conversion}

인제스트된 일괄 처리에 잘못된 XDM 전환이 있는 경우 다음 끝점을 사용하여 액세스할 수 있는 파일에 일괄 처리 오류가 저장됩니다.

**API 형식**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 오류 정보를 검색하는 배치의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 XDM 변환 시 발생한 오류에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
