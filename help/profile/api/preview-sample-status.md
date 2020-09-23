---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
title: 프로필 미리 보기 - 실시간 고객 프로필 API
description: Adobe Experience Platform을 사용하면 여러 소스에서 고객 데이터를 수집하여 개별 고객을 위한 강력한 통합 프로파일을 구축할 수 있습니다. 실시간 고객 프로파일에 대해 활성화된 데이터가 플랫폼으로 수집되므로 프로필 데이터 저장소 내에 저장됩니다. 프로필 저장소의 레코드 수가 늘어나거나 줄어들면서 데이터 저장소에 있는 프로필 조각 및 병합된 프로필 수에 대한 정보가 포함된 샘플 작업이 실행됩니다. 프로필 API를 사용하면 성공적인 최신 샘플뿐만 아니라 데이터 세트 및 ID 네임스페이스별로 프로필 배포를 나열할 수 있습니다.
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# 샘플 상태 끝점 미리 보기(프로필 미리 보기)

Adobe Experience Platform을 사용하면 여러 소스에서 고객 데이터를 수집하여 개별 고객을 위한 강력한 통합 프로파일을 구축할 수 있습니다. 실시간 고객 프로파일에 대해 활성화된 데이터가 인제스트되어 프로필 데이터 저장소 [!DNL Platform]에 저장됩니다.

프로필 스토어에 레코드 수집이 전체 프로필 수를 5% 이상 늘리거나 줄이면 작업이 트리거되어 카운트를 업데이트합니다. 스트리밍 데이터 워크플로우의 경우 시간별로 검사하여 5% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 이 경우 작업이 자동으로 트리거되어 카운트가 업데이트됩니다. 일괄 처리 수정의 경우, 배치를 성공적으로 프로필 스토어에 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업이 실행되어 카운트를 업데이트합니다. 프로필 API를 사용하면 성공적인 최신 샘플 작업을 미리 볼 수 있을 뿐만 아니라 데이터 세트 및 ID 네임스페이스별 프로필 배포를 나열할 수 있습니다.

이러한 지표는 Experience Platform UI의 [!UICONTROL 프로필] 섹션 내에서도 사용할 수 있습니다. UI를 사용하여 프로필 데이터에 액세스하는 방법에 대한 자세한 내용은 [[!DNL Profile] 사용자 안내서를 참조하십시오](../ui/user-guide.md).

## 시작하기

이 안내서에서 사용되는 API 끝점은 [[!DNL Real-time Customer Profile] API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). 계속하기 전에 [시작하기 가이드](getting-started.md) 에서 관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오 [!DNL Experience Platform] .

## 마지막 샘플 상태 보기 {#view-last-sample-status}

종단점에 대한 GET 요청을 수행하여 IMS 조직에 대해 실행된 마지막 성공 샘플 작업에 대한 세부 사항을 볼 수 있습니다. `/previewsamplestatus` 여기에는 샘플에 있는 총 프로필 수, 프로필 수 지표 또는 Experience Platform 내에 있는 조직의 총 프로필 수가 포함됩니다. 프로필 개수는 프로필 조각을 병합한 후 생성되어 각 개별 고객에 대한 단일 프로필을 형성합니다. 즉, 조직은 여러 채널에서 브랜드와 상호 작용하는 단일 고객과 관련된 여러 프로필 조각을 가질 수 있지만 이러한 조각은 기본 병합 정책에 따라 병합되며 &quot;1&quot; 프로필의 개수가 반환됩니다. 모두 동일한 개인과 관련되어 있기 때문입니다.

프로필 수에는 속성(레코드 데이터)이 있는 프로필 및 Adobe Analytics 프로필과 같은 시간 시리즈(이벤트) 데이터만 포함된 프로파일도 모두 포함됩니다. 플랫폼 내에서 최신 총 프로필 수를 제공하기 위해 프로필 데이터를 수집하므로 샘플 작업은 정기적으로 새로 고쳐집니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 IMS 조직에 대해 실행된 마지막 성공 샘플 작업에 대한 세부 정보가 포함됩니다.

>[!NOTE]
>
>이 예제 응답에서 `numRowsToRead` 는 `totalRows` 서로 같습니다. Experience Platform에 있는 조직의 프로필 수에 따라 이러한 경우가 해당될 수 있습니다. 그러나 일반적으로 이 두 숫자는 전체 프로필 수( `numRowsToRead``totalRows`)의 하위 집합으로 샘플을 나타내므로 더 작은 숫자가 되므로 차이가 있습니다.

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
| `numRowsToRead` | 샘플에 있는 병합된 프로필의 총 수입니다. |
| `sampleJobRunning` | 샘플 작업이 진행 중일 `true` 때 반환하는 부울 값입니다. 일괄 처리 파일이 프로필 스토어에 실제로 추가되는 시점까지 발생하는 지연에 대한 투명도를 제공합니다. |
| `cosmosDocCount` | Cosmos의 총 문서 수입니다. |
| `totalFragmentCount` | 프로필 저장소의 총 프로필 조각 수입니다. |
| `lastSuccessfulBatchTimestamp` | 마지막으로 성공한 일괄 처리 타임스탬프. |
| `streamingDriven` | *이 필드는 더 이상 사용되지 않으며 응답에 중요도가 없습니다.* |
| `totalRows` | &#39;프로필 수&#39;로도 알려진 경험 플랫폼의 병합된 총 프로필 수입니다. |
| `lastBatchId` | 마지막 일괄 처리 ID. |
| `status` | 마지막 샘플의 상태입니다. |
| `samplingRatio` | 십진수 형식의 백분율로 표현되는 병합된 프로필`numRowsToRead`(`totalRows`)의 전체 병합된 프로필입니다. |
| `mergeStrategy` | 샘플에 사용된 병합 전략입니다. |
| `lastSampledTimestamp` | 마지막으로 성공한 샘플 타임스탬프. |

## 데이터 세트별 프로필 배포 목록

데이터 세트별 프로필 배포를 보려면 종단점에 대한 GET 요청을 수행할 수 `/previewsamplestatus/report/dataset` 있습니다.

**API 형식**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 반환할 보고서 날짜를 지정합니다. 날짜에 여러 보고서가 실행되면 해당 날짜에 대한 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 존재하지 않으면 404 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식:YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청에서는 매개 변수를 사용하여 지정된 날짜에 대한 최신 보고서를 반환합니다. `date`

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 데이터 집합 개체 목록이 포함된 `data` 배열이 포함됩니다. 표시된 응답이 세 개의 데이터 세트를 표시하도록 잘렸습니다.

>[!NOTE]
>
>날짜에 여러 보고서가 존재하는 경우 최신 보고서만 반환됩니다. 데이터 집합 보고서가 제공된 날짜에 존재하지 않으면 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

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
| `sampleCount` | 이 데이터 집합 ID를 사용한 병합된 프로필의 총 수입니다. |
| `samplePercentage` | 병합된 프로필의 총 수( `sampleCount` 마지막 샘플 상태로 반환되는 `numRowsToRead` 값)에 대한 백분율로, 십진수 형식으로 표현됩니다 [](#view-last-sample-status). |
| `fullIDsCount` | 이 데이터 집합 ID를 가진 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | 병합된 프로필의 총 수( `fullIDsCount` 마지막 샘플 상태로 반환되는 `totalRows` 값)의 백분율로, 십진수 형식으로 표현됩니다 [](#view-last-sample-status). |
| `name` | 데이터 세트를 만드는 동안 제공된 데이터 세트의 이름입니다. |
| `description` | 데이터 세트를 만드는 동안 제공된 데이터 세트에 대한 설명입니다. |
| `value` | 데이터 세트의 ID입니다. |
| `streamingIngestionEnabled` | 데이터 세트에 스트리밍 통합 기능이 있는지 여부 |
| `createdUser` | 데이터 세트를 만든 사용자의 사용자 ID. |
| `reportTimestamp` | 보고서의 타임스탬프입니다. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜입니다. 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. `date` |



## 네임스페이스별 프로필 배포 목록

종단점에 대한 GET 요청을 수행하여 프로필 저장소의 병합된 모든 프로필에 대해 ID 네임스페이스별 분류를 볼 수 있습니다. `/previewsamplestatus/report/namespace` ID 네임스페이스는 고객 데이터와 관련된 컨텍스트의 지표로 사용되는 Adobe Experience Platform ID 서비스의 중요한 구성 요소입니다. 자세한 내용은 [ID 네임스페이스 개요를 참조하십시오](../../identity-service/namespaces.md).

>[!NOTE]
>
>네임스페이스별 총 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 항상 프로필 수 지표보다 높습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 해당 개별 고객과 여러 개의 네임스페이스가 연결됩니다.

**API 형식**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 반환할 보고서 날짜를 지정합니다. 날짜에 여러 보고서가 실행되면 해당 날짜에 대한 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 존재하지 않으면 404 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식:YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 매개 변수를 지정하지 않으므로 `date` 가장 최근 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 `data` 배열이 포함되며 각 네임스페이스에 대한 세부 정보가 들어 있습니다. 표시된 응답이 네 개의 네임스페이스를 표시하도록 잘렸습니다.

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
| `sampleCount` | 네임스페이스에 있는 샘플링된 병합된 프로필의 총 수입니다. |
| `samplePercentage` | 샘플링된 병합된 프로필 `sampleCount` 의 백분율( `numRowsToRead` 마지막 샘플 상태로 [](#view-last-sample-status)반환되는 값)으로서 소수점 형식으로 표시됩니다. |
| `reportTimestamp` | 보고서의 타임스탬프입니다. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜입니다. 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. `date` |
| `fullIDsFragmentCount` | 네임스페이스에 있는 총 프로필 조각 수입니다. |
| `fullIDsCount` | 네임스페이스에 있는 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | 병합된 전체 프로필 `fullIDsCount` 의 백분율( `totalRows` 마지막 샘플 상태로 반환되는 값 [](#view-last-sample-status))으로서 소수점 형식으로 표시됩니다. |
| `code` | 네임스페이스의 `code` 이름입니다. 이는 [Adobe Experience Platform ID 서비스 API를 사용하여 네임스페이스를](../../identity-service/api/list-namespaces.md) 사용하는 경우 찾을 수 있으며 Experience Platform UI에서 [!UICONTROL ID] 기호라고도 합니다. 자세한 내용은 [ID 네임스페이스 개요를 참조하십시오](../../identity-service/namespaces.md). |
| `value` | 네임스페이스의 `id` 값입니다. ID 서비스 API를 사용하여 네임스페이스를 사용하는 경우 이 [매개 변수를 찾을 수 있습니다](../../identity-service/api/list-namespaces.md). |

## 다음 단계

유사한 예측과 미리 보기를 사용하여 세그먼트 정의와 관련된 요약 수준 정보를 보고 예상 고객을 분리할 수도 있습니다. 세그먼트 미리 보기 및 [!DNL Adobe Experience Platform Segmentation Service] API를 사용한 예상 작업에 대한 자세한 단계를 살펴보려면 [API 개발자 안내서의 일부인](../../segmentation/api/previews-and-estimates.md)미리 보기 및 예측 엔드포인트 가이드를 [!DNL Segmentation] 참조하십시오.

