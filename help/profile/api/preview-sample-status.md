---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;미리 보기;샘플
title: 샘플 상태 미리 보기(프로필 미리 보기) API 끝점
description: Real-Time Customer Profile API의 샘플 상태 미리보기 엔드포인트를 사용하면 프로필 데이터의 최근 성공 샘플을 미리 보고, 데이터 세트 및 ID별로 프로필 분포를 나열하고, 데이터 세트 중복, ID 중복 및 연결되지 않은 프로필을 보여주는 보고서를 생성할 수 있습니다.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 1%

---

# 샘플 상태 끝점 미리 보기(프로필 미리 보기)

Adobe Experience Platform을 사용하면 여러 소스에서 고객 데이터를 수집하여 각 개별 고객을 위한 강력하고 통합된 프로필을 구축할 수 있습니다. 데이터가 Platform으로 수집되면 샘플 작업이 실행되어 프로필 수 및 기타 실시간 고객 프로필 데이터 관련 지표를 업데이트합니다.

이 샘플 작업의 결과는 `/previewsamplestatus` 실시간 고객 프로필 API의 일부인 종단점입니다. 이 끝점을 사용하여 데이터 세트와 ID 네임스페이스 모두로 프로필 분포를 나열할 수 있을 뿐만 아니라 조직의 프로필 스토어 구성에 대한 가시성을 확보할 수 있도록 여러 보고서를 생성할 수도 있습니다. 이 안내서에서는 다음을 사용하여 이러한 지표를 보는 데 필요한 단계를 안내합니다. `/previewsamplestatus` API 엔드포인트.

>[!NOTE]
>
>Adobe Experience Platform 세그먼테이션 서비스 API의 일부로 사용할 수 있는 예상 및 미리 보기 끝점이 있습니다. 이 끝점을 사용하면 세그먼트 정의에 대한 요약 수준 정보를 보고 예상 대상을 격리할 수 있습니다. 세그먼트 미리 보기 및 예상 끝점을 사용하는 작업에 대한 자세한 단계를 찾으려면 다음을 방문하십시오. [미리 보기 및 예상 끝점 안내서](../../segmentation/api/previews-and-estimates.md), 의 일부 [!DNL Segmentation] API 개발자 안내서.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). 계속하기 전에 다음을 검토하십시오. [시작 안내서](getting-started.md) 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내서 및 를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보 [!DNL Experience Platform] API.

## 프로필 조각과 병합된 프로필

이 안내서는 &quot;프로필 조각&quot;과 &quot;병합된 프로필&quot;을 모두 참조합니다. 진행하기 전에 이러한 용어 간의 차이점을 이해하는 것이 중요합니다.

각 개별 고객 프로필은 해당 고객에 대한 단일 보기를 형성하기 위해 병합된 여러 프로필 조각으로 구성됩니다. 예를 들어, 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 단일 고객과 관련된 여러 프로필 조각이 있을 수 있습니다.

프로필 조각을 Platform으로 수집하면 해당 고객을 위한 단일 프로필을 만들기 위해 프로필 조각이 병합 정책에 따라 함께 병합됩니다. 따라서 각 프로필이 여러 조각으로 구성되므로 총 프로필 조각 수는 병합된 프로필 총 수보다 항상 높을 수 있습니다.

Experience Platform 내에서 프로필 및 프로필의 역할에 대한 자세한 내용은 [실시간 고객 프로필 개요](../home.md).

## 샘플 작업이 트리거되는 방법

실시간 고객 프로필에 대해 활성화된 데이터를에 수집함 [!DNL Platform]: 프로필 데이터 저장소 내에 저장됩니다. 프로필 스토어로 레코드를 수집하면 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 트리거되어 수를 업데이트합니다. 샘플이 트리거되는 방법은 사용 중인 수집 유형에 따라 다릅니다.

* 대상 **스트리밍 데이터 워크플로**&#x200B;는 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사됩니다. 샘플 작업이 있는 경우, 샘플 작업이 자동으로 트리거되어 카운트를 업데이트합니다.
* 대상 **일괄 처리 수집**, 일괄 처리를 프로필 스토어에 성공적으로 수집한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 카운트를 업데이트하는 작업이 실행됩니다. 프로필 API를 사용하면 최근에 성공한 샘플 작업을 미리 볼 수 있으며, 데이터 세트 및 ID 네임스페이스별로 프로필 분포를 나열할 수 있습니다.

네임스페이스 지표별 프로필 개수 및 프로필은 [!UICONTROL 프로필] Experience Platform UI의 섹션입니다. UI를 사용하여 프로필 데이터에 액세스하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Profile] UI 안내서](../ui/user-guide.md).

## 마지막 샘플 상태 보기 {#view-last-sample-status}

에 대한 GET 요청을 수행할 수 있습니다. `/previewsamplestatus` 조직에 대해 마지막으로 성공한 샘플 작업에 대한 세부 정보를 보기 위한 끝점입니다. 여기에는 샘플의 총 프로필 수와 프로필 수 지표 또는 조직이 Experience Platform 내에 보유한 총 프로필 수가 포함됩니다.

프로필 수는 프로필 조각을 병합하여 각 개별 고객에 대한 단일 프로필을 형성한 후 생성됩니다. 즉, 프로필 조각이 함께 병합되면 모두 동일한 개인과 관련되므로 &quot;1&quot; 프로필 수를 반환합니다.

프로필 카운트에는 속성이 있는 프로필(레코드 데이터)과 Adobe Analytics 프로필과 같이 시계열(이벤트) 데이터만 포함된 프로필이 모두 포함됩니다. Platform 내에서 최신 총 프로필 수를 제공하기 위해 프로필 데이터가 수집되면 샘플 작업이 정기적으로 새로 고쳐집니다.

**API 형식**

```http
GET /previewsamplestatus
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 조직에 대해 마지막으로 실행된 성공적인 샘플 작업에 대한 세부 정보가 포함됩니다.

>[!NOTE]
>
>이 예제 응답에서는 `numRowsToRead` 및 `totalRows` 은 서로 같습니다. 조직이 Experience Platform 중인 프로필의 수에 따라 다를 수 있습니다. 그러나 일반적으로 이 두 숫자는 `numRowsToRead` 샘플을 총 프로필 수의 하위 집합으로 나타내므로 더 작은 수가 됩니다(`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| 속성 | 설명 |
|---|---|
| `numRowsToRead` | 샘플에서 병합된 총 프로필 수입니다. |
| `sampleJobRunning` | 를 반환하는 부울 값 `true` 샘플 작업이 진행 중인 경우. 배치 파일이 업로드된 시점부터 실제 프로필 스토어에 추가될 때까지의 지연 시간을 투명하게 제공합니다. |
| `cosmosDocCount` | Cosmos의 총 문서 개수. |
| `totalFragmentCount` | 프로필 저장소의 총 프로필 조각 수입니다. |
| `lastSuccessfulBatchTimestamp` | 마지막으로 성공한 일괄 처리 수집 타임스탬프. |
| `streamingDriven` | *이 필드는 더 이상 사용되지 않으며 응답에 대한 중요도를 포함하지 않습니다.* |
| `totalRows` | &#39;프로필 수&#39;라고도 하는 Experience Platform의 병합된 총 프로필 수입니다. |
| `lastBatchId` | 마지막 일괄 처리 수집 ID. |
| `status` | 마지막 샘플 상태. |
| `samplingRatio` | 샘플링된 병합된 프로필의 비율(`numRowsToRead`)을 클릭하여 병합된 총 프로필(`totalRows`), 십진수 형식의 백분율로 표시됩니다. |
| `mergeStrategy` | 샘플에 사용된 병합 전략입니다. |
| `lastSampledTimestamp` | 마지막으로 성공한 샘플 타임스탬프. |

## 데이터 세트별 목록 프로필 분포

데이터 세트별 프로필 분포를 보려면 다음을 위한 GET 요청을 수행할 수 있습니다 `/previewsamplestatus/report/dataset` 엔드포인트.

**API 형식**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
|---|---|
| `date` | 반환할 보고서의 날짜를 지정합니다. 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 `date` 지정된 날짜에 대한 가장 최근 보고서를 반환하는 매개 변수입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 다음이 포함됩니다. `data` 데이터 세트 개체 목록이 포함된 배열. 표시된 응답이 잘려서 3개의 데이터 세트를 표시합니다.

>[!NOTE]
>
>날짜에 여러 보고서가 있는 경우 최신 보고서만 반환됩니다. 입력한 날짜에 데이터 세트 보고서가 없는 경우 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 속성 | 설명 |
|---|---|
| `sampleCount` | 이 데이터 세트 ID로 샘플링된 병합된 프로필의 총 수입니다. |
| `samplePercentage` | 다음 `sampleCount` 샘플링된 병합된 프로필의 총 수에 대한 백분율로 나타낸 것입니다(다음 항목 포함). `numRowsToRead` 에 반환된 값 [마지막 샘플 상태](#view-last-sample-status)), 10진수 형식으로 표시됩니다. |
| `fullIDsCount` | 이 데이터 세트 ID를 가진 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | 다음 `fullIDsCount` 병합된 총 프로필 수에 대한 백분율로 나타낸 것입니다(다음 값: `totalRows` 에 반환된 값 [마지막 샘플 상태](#view-last-sample-status)), 10진수 형식으로 표시됩니다. |
| `name` | 데이터 세트 생성 시 제공된 데이터 세트의 이름입니다. |
| `description` | 데이터 세트 생성 중 제공된 데이터 세트에 대한 설명입니다. |
| `value` | 데이터 세트의 ID입니다. |
| `streamingIngestionEnabled` | 스트리밍 수집에 데이터 세트를 사용할 수 있는지 여부입니다. |
| `createdUser` | 데이터 세트를 만든 사용자의 사용자 ID입니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 다음과 같은 경우 `date` 매개 변수가 요청 중에 제공되었습니다. 반환된 보고서는 제공된 날짜에 대한 것입니다. 없는 경우 `date` 매개 변수가 제공되면 가장 최근 보고서가 반환됩니다. |

## ID 네임스페이스별 목록 프로필 배포

에 대한 GET 요청을 수행할 수 있습니다. `/previewsamplestatus/report/namespace` 프로필 스토어에 병합된 모든 프로필의 id 네임스페이스별 분류를 보는 엔드포인트입니다. 여기에는 Adobe에서 제공하는 표준 ID와 조직에서 정의한 사용자 정의 ID가 모두 포함됩니다.

ID 네임스페이스는 고객 데이터와 관련된 컨텍스트의 지표 역할을 하는 Adobe Experience Platform ID 서비스의 중요한 구성 요소입니다. 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md).

>[!NOTE]
>
>하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 네임스페이스별 총 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 프로필 수 지표보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

**API 형식**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
|---|---|
| `date` | 반환할 보고서의 날짜를 지정합니다. 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 `date` 매개 변수 및 는 따라서 가장 최근 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 다음이 포함됩니다. `data` 각 네임스페이스에 대한 세부 정보가 포함된 개별 객체가 포함된 배열 표시된 응답이 4개의 네임스페이스를 표시하도록 잘렸습니다.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 속성 | 설명 |
|---|---|
| `sampleCount` | 네임스페이스에서 샘플링된 병합된 프로필의 총 수입니다. |
| `samplePercentage` | 다음 `sampleCount` 샘플링된 병합 프로필의 백분율로(다음) `numRowsToRead` 에 반환된 값 [마지막 샘플 상태](#view-last-sample-status)), 10진수 형식으로 표시됩니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 다음과 같은 경우 `date` 매개 변수가 요청 중에 제공되었습니다. 반환된 보고서는 제공된 날짜에 대한 것입니다. 없는 경우 `date` 매개 변수가 제공되면 가장 최근 보고서가 반환됩니다. |
| `fullIDsFragmentCount` | 네임스페이스의 총 프로필 조각 수입니다. |
| `fullIDsCount` | 네임스페이스에 병합된 총 프로필 수입니다. |
| `fullIDsPercentage` | 다음 `fullIDsCount` 병합된 총 프로필의 백분율로 표시( `totalRows` 에 반환된 값 [마지막 샘플 상태](#view-last-sample-status)), 10진수 형식으로 표시됩니다. |
| `code` | 다음 `code` 네임스페이스에 사용됩니다. 이 로그는 를 사용하여 네임스페이스로 작업할 때 찾을 수 있습니다. [Adobe Experience Platform ID 서비스 API](../../identity-service/api/list-namespaces.md) 및 를 &quot;다음&quot;이라고도 합니다. [!UICONTROL ID 심볼] Experience Platform UI에서 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md). |
| `value` | 다음 `id` 네임스페이스에 대한 값입니다. 이 로그는 를 사용하여 네임스페이스로 작업할 때 찾을 수 있습니다. [ID 서비스 API](../../identity-service/api/list-namespaces.md). |

## 데이터 세트 중복 보고서 생성

데이터 세트 겹치기 보고서는 주소 지정 가능한 대상(병합된 프로필)에 가장 많이 기여하는 데이터 세트를 노출하여 조직의 프로필 저장소 구성을 볼 수 있도록 합니다. 이 보고서는 데이터에 대한 통찰력을 제공하는 것 외에도 특정 데이터 세트에 대한 만료 설정과 같은 라이선스 사용을 최적화하는 작업을 수행하는 데 도움이 될 수 있습니다.

에 대한 GET 요청을 수행하여 데이터 세트 중복 보고서를 생성할 수 있습니다. `/previewsamplestatus/report/dataset/overlap` 엔드포인트.

명령줄 또는 Postman UI를 사용하여 데이터 세트 중복 보고서를 생성하는 방법에 대한 단계별 지침은 다음을 참조하십시오. [데이터 세트 중복 보고서 튜토리얼 생성](../tutorials/dataset-overlap-report.md).

**API 형식**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
|---|---|
| `date` | 반환할 보고서의 날짜를 지정합니다. 동일한 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 `date` 지정된 날짜에 대한 가장 최근 보고서를 반환하는 매개 변수입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 데이터 세트 겹치기 보고서가 반환됩니다.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| 속성 | 설명 |
|---|---|
| `data` | 다음 `data` 객체에는 쉼표로 구분된 데이터 세트 목록과 해당 프로필 수가 포함되어 있습니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 다음과 같은 경우 `date` 매개 변수가 요청 중에 제공되었습니다. 반환된 보고서는 제공된 날짜에 대한 것입니다. 없는 경우 `date` 매개 변수가 제공되면 가장 최근 보고서가 반환됩니다. |

### 데이터 세트 중복 보고서 해석

응답의 데이터 세트 및 프로필 카운트에서 보고서 결과를 해석할 수 있습니다. 다음 예제 보고서를 고려하십시오 `data` 개체:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

이 보고서는 다음 정보를 제공합니다.

* 다음 데이터 세트에서 오는 데이터로 구성된 123개의 프로필이 있습니다. `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 다음 두 데이터 세트에서 오는 데이터로 구성된 454,412개의 프로필이 있습니다. `5d92921872831c163452edc8` 및 `5eb2cdc6fa3f9a18a7592a98`.
* 데이터 세트의 데이터로만 구성된 프로필은 107개입니다 `5eeda0032af7bb19162172a7`.
* 조직에 총 454,642개의 프로필이 있습니다.

## ID 네임스페이스 중복 보고서 생성 {#identity-overlap-report}

ID 네임스페이스 중복 보고서는 주소 지정 가능한 대상(병합된 프로필)에 가장 많은 영향을 주는 ID 네임스페이스를 노출하여 조직의 프로필 저장소 구성을 볼 수 있도록 합니다. 여기에는 Adobe에서 제공하는 표준 ID 네임스페이스와 조직에서 정의한 사용자 정의 ID 네임스페이스가 모두 포함됩니다.

에 대한 GET 요청을 수행하여 ID 네임스페이스 중복 보고서를 생성할 수 있습니다. `/previewsamplestatus/report/namespace/overlap` 엔드포인트.

**API 형식**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
|---|---|
| `date` | 반환할 보고서의 날짜를 지정합니다. 동일한 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 `date` 지정된 날짜에 대한 가장 최근 보고서를 반환하는 매개 변수입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 ID 네임스페이스 중복 보고서가 반환됩니다.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| 속성 | 설명 |
|---|---|
| `data` | 다음 `data` 객체에는 id 네임스페이스 코드와 해당 프로필 카운트의 고유한 조합이 있는 쉼표로 구분된 목록이 포함되어 있습니다. |
| 네임스페이스 코드 | 다음 `code` 는 각 id 네임스페이스 이름에 대한 약식입니다. 각 의 매핑 `code` 로 `name` 을 사용하여 찾을 수 있음 [Adobe Experience Platform ID 서비스 API](../../identity-service/api/list-namespaces.md). 다음 `code` 를 &quot;다음&quot;이라고도 합니다 [!UICONTROL ID 심볼] Experience Platform UI에서 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md). |
| `reportTimestamp` | 보고서의 타임스탬프. 다음과 같은 경우 `date` 매개 변수가 요청 중에 제공되었습니다. 반환된 보고서는 제공된 날짜에 대한 것입니다. 없는 경우 `date` 매개 변수가 제공되면 가장 최근 보고서가 반환됩니다. |

### ID 네임스페이스 중복 보고서 해석

보고서의 결과는 응답의 ID 및 프로필 카운트에서 해석될 수 있습니다. 각 행의 숫자 값은 표준 및 사용자 정의 ID 네임스페이스의 정확한 조합으로 구성된 프로필 수를 알려줍니다.

다음에서 발췌한 내용을 고려하십시오 `data` 개체:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

이 보고서는 다음 정보를 제공합니다.

* 다음으로 구성된 142개의 프로필이 있습니다. `AAID`, `ECID`, 및 `Email` 표준 id 및 사용자 지정 `crmid` id 네임스페이스.
* 다음으로 구성된 24개의 프로필이 있습니다. `AAID` 및 `ECID` id 네임스페이스.
* 다음과 같은 항목만 포함하는 6,565개의 프로필이 있습니다. `ECID` 신원.

## 연결되지 않은 프로필 보고서 생성

연결되지 않은 프로필 보고서를 통해 조직의 프로필 스토어 구성에 대한 가시성을 확보할 수 있습니다. &quot;연결되지 않은&quot; 프로필은 하나의 프로필 조각만 포함하는 프로필입니다. &quot;알 수 없는&quot; 프로필은 다음과 같은 익명 ID 네임스페이스와 연결된 프로필입니다. `ECID` 및 `AAID`. 알 수 없는 프로필은 비활성 상태이며, 이는 지정된 기간 동안 새로운 이벤트를 추가하지 않았음을 의미합니다. 연결되지 않은 프로필 보고서는 7, 30, 60, 90 및 120일 동안의 프로필 분류를 제공합니다.

에 대한 GET 요청을 수행하여 연결되지 않은 프로필 보고서를 생성할 수 있습니다. `/previewsamplestatus/report/unstitchedProfiles` 엔드포인트.

**API 형식**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**요청**

다음 요청은 연결되지 않은 프로필 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 연결되지 않은 프로필 보고서가 반환됩니다.

>[!NOTE]
>
>이 안내서에서는 보고서만 포함하도록 잘렸습니다 `"120days"` 및 &quot;`7days`&quot;기간. 전체 연결되지 않은 프로필 보고서는 7, 30, 60, 90 및 120일 동안의 프로필 분류를 제공합니다.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| 속성 | 설명 |
|---|---|
| `data` | 다음 `data` 개체에는 연결되지 않은 프로필 보고서에 대해 반환된 정보가 포함되어 있습니다. |
| `totalNumberOfProfiles` | 프로필 스토어의 총 고유 프로필 수입니다. 이는 대응 가능 대상 수와 동일합니다. 여기에는 알려진 프로필과 연결되지 않은 프로필이 모두 포함됩니다. |
| `totalNumberOfEvents` | 프로필 스토어의 총 ExperienceEvents 수입니다. |
| `unstitchedProfiles` | 기간별로 연결되지 않은 프로필의 분류가 포함된 객체입니다. 연결되지 않은 프로필 보고서는 7, 30, 60, 90 및 120일 기간 동안의 프로필 분류를 제공합니다. |
| `countOfProfiles` | 해당 기간에 대해 연결되지 않은 프로필 수 또는 네임스페이스에 대해 연결되지 않은 프로필 수. |
| `eventsAssociated` | 시간 범위에 대한 ExperienceEvents 수 또는 네임스페이스에 대한 이벤트 수입니다. |
| `nsDistribution` | 각 네임스페이스에 대해 연결되지 않은 프로필 및 이벤트가 배포된 개별 ID 네임스페이스를 포함하는 개체입니다. 참고: 합계를 함께 추가합니다. `countOfProfiles` 의 각 id 네임스페이스에 대해 `nsDistribution` 개체가 `countOfProfiles` 기간 동안. 에 대해서도 마찬가지입니다 `eventsAssociated` 네임스페이스당 및 합계 `eventsAssociated` 기간당. |
| `reportTimestamp` | 보고서의 타임스탬프. |

### 연결되지 않은 프로필 보고서 해석

보고서 결과는 조직이 프로필 스토어 내에 보유하고 있는 연결되지 않은 프로필 및 비활성 프로필 수에 대한 통찰력을 제공할 수 있습니다.

다음에서 발췌한 내용을 고려하십시오 `data` 개체:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

이 보고서는 다음 정보를 제공합니다.

* 프로필 조각이 하나만 포함되어 있고 지난 7일 동안 새 이벤트가 없는 1,782개의 프로필이 있습니다.
* 연결되지 않은 1,782개의 프로필과 연결된 29,151개의 ExperienceEvent가 있습니다.
* ECID의 ID 네임스페이스에서 단일 프로필 조각을 포함하는 연결되지 않은 프로필은 1,734개입니다.
* ECID의 ID 네임스페이스에서 단일 프로필 조각을 포함하는 1,734개의 연결되지 않은 프로필과 연결된 28,591개의 이벤트가 있습니다.

## 다음 단계

이제 프로필 스토어에서 샘플 데이터를 미리 보고 데이터에 대한 여러 보고서를 실행하는 방법을 알았으므로, 세그멘테이션 서비스 API의 예상 및 미리 보기 끝점을 사용하여 세그먼트 정의와 관련된 요약 수준 정보를 볼 수도 있습니다. 이 정보는 세그먼트에서 예상되는 대상자를 격리하는 데 도움이 됩니다. Segmentation API를 사용하여 세그먼트 미리 보기 및 예상 작업에 대해 자세히 알아보려면 다음을 방문하십시오. [끝점 미리 보기 및 예상 안내서](../../segmentation/api/previews-and-estimates.md).

