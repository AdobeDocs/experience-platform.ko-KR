---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;미리 보기;샘플
title: 샘플 상태 미리 보기(프로필 미리 보기) API 끝점
description: Real-Time Customer Profile API의 샘플 상태 미리보기 엔드포인트를 사용하면 프로필 데이터의 최근 성공 샘플을 미리 보고, 데이터 세트 및 ID별로 프로필 분포를 나열하고, 데이터 세트 중복, ID 중복 및 연결되지 않은 프로필을 보여주는 보고서를 생성할 수 있습니다.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 399b76f260732015f691fd199c977d6f7e772b01
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 1%

---

# 샘플 상태 끝점 미리 보기(프로필 미리 보기)

Adobe Experience Platform을 사용하면 여러 소스에서 고객 데이터를 수집하여 각 개별 고객을 위한 강력하고 통합된 프로필을 구축할 수 있습니다. 데이터가 Experience Platform에 수집되면 샘플 작업이 실행되어 프로필 수 및 기타 실시간 고객 프로필 데이터 관련 지표를 업데이트합니다.

이 샘플 작업의 결과는 실시간 고객 프로필 API의 일부인 `/previewsamplestatus` 끝점을 사용하여 볼 수 있습니다. 이 끝점을 사용하여 데이터 세트와 ID 네임스페이스 모두로 프로필 분포를 나열할 수 있을 뿐만 아니라 조직의 프로필 저장소 구성을 가시적으로 확인할 수 있도록 여러 보고서를 생성할 수도 있습니다. 이 안내서에서는 `/previewsamplestatus` API 끝점을 사용하여 이러한 지표를 보는 데 필요한 단계를 안내합니다.

>[!NOTE]
>
>Adobe Experience Platform 세그먼테이션 서비스 API의 일부로 사용할 수 있는 예상 및 미리 보기 끝점이 있습니다. 이 끝점을 사용하면 세그먼트 정의에 대한 요약 수준 정보를 보고 예상 대상을 격리할 수 있습니다. 미리 보기 및 예상 끝점을 사용하는 작업에 대한 자세한 단계를 찾으려면 [ API 개발자 가이드의 일부인 ](../../segmentation/api/previews-and-estimates.md)미리 보기 및 예상 끝점 안내서[!DNL Segmentation]를 참조하십시오.

## 시작

이 가이드에 사용된 API 끝점은 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)의 일부입니다. 계속하기 전에 [시작 안내서](getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 [!DNL Experience Platform] API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 프로필 조각과 병합된 프로필

이 안내서는 &quot;프로필 조각&quot;과 &quot;병합된 프로필&quot;을 모두 참조합니다. 진행하기 전에 이러한 용어 간의 차이점을 이해하는 것이 중요합니다.

각 개별 고객 프로필은 해당 고객에 대한 단일 보기를 형성하기 위해 병합된 여러 프로필 조각으로 구성됩니다. 예를 들어, 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 단일 고객과 관련된 여러 프로필 조각이 있을 수 있습니다.

프로필 조각을 Experience Platform에 수집하면 해당 고객을 위한 단일 프로필을 만들기 위해 프로필 조각이 함께 병합 정책에 따라 병합됩니다. 따라서 각 프로필이 여러 조각으로 구성되므로 총 프로필 조각 수는 병합된 프로필 총 수보다 항상 높을 수 있습니다.

Experience Platform에서 프로필 및 프로필의 역할에 대해 자세히 알아보려면 [실시간 고객 프로필 개요](../home.md)를 읽어 보십시오.

## 샘플 작업이 트리거되는 방법

실시간 고객 프로필에 대해 활성화된 데이터가 [!DNL Experience Platform]에 수집되면 프로필 데이터 저장소 내에 저장됩니다. 프로필 스토어로 레코드를 수집하면 총 프로필 수가 3% 이상 증가하거나 감소하면 샘플링 작업이 트리거되어 수를 업데이트합니다. 샘플이 트리거되는 방법은 사용 중인 수집 유형에 따라 다릅니다.

* **스트리밍 데이터 워크플로**&#x200B;의 경우 매시간 3% 증가 또는 감소 임계값이 충족되었는지 확인합니다. 샘플 작업이 있는 경우, 샘플 작업이 자동으로 트리거되어 카운트를 업데이트합니다.
* **일괄 처리 수집**&#x200B;의 경우, 일괄 처리를 프로필 스토어로 성공적으로 수집한 후 15분 이내에 3% 증가 또는 감소 임계값에 도달하면 카운트를 업데이트하는 작업이 실행됩니다. 프로필 API를 사용하면 최근에 성공한 샘플 작업을 미리 볼 수 있으며, 데이터 세트 및 ID 네임스페이스별로 프로필 분포를 나열할 수 있습니다.

네임스페이스 지표별 프로필 개수 및 프로필은 Experience Platform UI의 [!UICONTROL Profiles] 섹션 내에서도 사용할 수 있습니다. UI를 사용하여 프로필 데이터에 액세스하는 방법에 대한 자세한 내용은 [[!DNL Profile] UI 안내서](../ui/user-guide.md)를 참조하십시오.

## 마지막 샘플 상태 보기 {#view-last-sample-status}

`/previewsamplestatus` 끝점에 대한 GET 요청을 수행하여 조직에 대해 마지막으로 실행된 성공적인 샘플 작업에 대한 세부 정보를 볼 수 있습니다. 이 보고서에는 샘플에 있는 총 프로필 수와 프로필 수 지표 또는 조직이 Experience Platform 내에 있는 총 프로필 수가 포함됩니다.

프로필 수는 프로필 조각을 병합하여 각 개별 고객에 대한 단일 프로필을 형성한 후 생성됩니다. 즉, 프로필 조각이 함께 병합되면 모두 동일한 개인과 관련되므로 &quot;1&quot; 프로필 수를 반환합니다.

프로필 카운트에는 속성이 있는 프로필(레코드 데이터)과 Adobe Analytics 프로필과 같이 시계열(이벤트) 데이터만 포함된 프로필이 모두 포함됩니다. Experience Platform 내에서 최신 총 프로필 수를 제공하기 위해 프로필 데이터가 수집되면 샘플 작업이 정기적으로 새로 고쳐집니다.

**API 형식**

```http
GET /previewsamplestatus
```

**요청**

+++ 마지막 샘플 상태를 보기 위한 샘플 요청입니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**응답**

성공적인 응답은 HTTP 상태 200을 반환하며, 조직에 대해 실행된 마지막으로 성공한 샘플 작업에 대한 세부 정보를 포함합니다.

+++ 마지막 샘플 상태가 포함된 샘플 응답입니다.

>[!NOTE]
>
>이 예제 응답에서 `numRowsToRead`과(와) `totalRows`은(는) 서로 같습니다. 조직이 Experience Platform에 보유하고 있는 프로필 수에 따라 달라질 수 있습니다. 그러나 일반적으로 이 두 숫자는 다릅니다. `numRowsToRead`은(는) 샘플을 총 프로필 수(`totalRows`)의 하위 집합으로 나타내므로 더 작은 숫자입니다.

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | 샘플에서 병합된 총 프로필 수입니다. |
| `sampleJobRunning` | 샘플 작업이 진행 중일 때 `true`을(를) 반환하는 부울 값입니다. 일괄 처리 파일이 업로드된 시점부터 실제로 프로필 저장소에 추가될 때까지의 지연 시간을 투명하게 제공합니다. |
| `docCount` | 데이터베이스의 총 문서 수입니다. |
| `totalFragmentCount` | 프로필 저장소의 총 프로필 조각 수입니다. |
| `lastSuccessfulBatchTimestamp` | 마지막으로 성공한 일괄 처리 수집 타임스탬프. |
| `streamingDriven` | *이 필드는 더 이상 사용되지 않으며 응답에 대한 중요도가 없습니다.* |
| `totalRows` | Experience Platform에서 병합된 총 프로필 수이며 프로필 수라고도 합니다. |
| `lastBatchId` | 마지막 일괄 처리 수집 ID. |
| `status` | 마지막 샘플 상태. |
| `samplingRatio` | 샘플링된 병합 프로필(`numRowsToRead`)과 병합된 총 프로필(`totalRows`)의 비율(십진수 형식으로 백분율 표시). |
| `mergeStrategy` | 샘플에 사용된 병합 전략입니다. |
| `lastSampledTimestamp` | 마지막으로 성공한 샘플 타임스탬프. |

+++

## 데이터 세트별 목록 프로필 분포

`/previewsamplestatus/report/dataset` 끝점에 대한 GET 요청을 통해 데이터 세트별 프로필 분포를 볼 수 있습니다.

**API 형식**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 쿼리 매개변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `date` | 반환할 보고서의 날짜를 지정합니다. 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. | `date=2024-12-31` |

**요청**

다음 요청은 `date` 매개 변수를 사용하여 지정된 날짜에 대한 가장 최근 보고서를 반환합니다.

+++ 데이터 세트별 프로필 분포를 검색하기 위한 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**응답**

>[!NOTE]
>
>날짜에 여러 보고서가 있는 경우 최신 보고서만 반환됩니다. 입력한 날짜에 데이터 세트 보고서가 없는 경우 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

성공적인 응답은 HTTP 상태 200을 반환하며 데이터 집합 개체 목록이 포함된 `data` 배열을 포함합니다.

+++ 최신 데이터 세트 개체가 포함된 샘플 응답입니다.

>[!NOTE]
>
>표시된 다음 응답은 3개의 데이터 세트를 표시하도록 잘렸습니다.

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
| -------- | ----------- |
| `sampleCount` | 이 데이터 세트 ID로 샘플링된 병합된 프로필의 총 수입니다. |
| `samplePercentage` | `sampleCount`은(는) 십진수 형식으로 표현되는, 샘플링된 병합된 프로필의 총 수(`numRowsToRead`마지막 샘플 상태[에서 반환된 ](#view-last-sample-status) 값)의 백분율입니다. |
| `fullIDsCount` | 이 데이터 세트 ID를 가진 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | `fullIDsCount`은(는) 10진수 형식으로 표현되는 병합된 프로필 총 수(`totalRows`마지막 샘플 상태[에서 반환된 ](#view-last-sample-status) 값)의 백분율입니다. |
| `name` | 데이터 세트 생성 시 제공된 데이터 세트의 이름입니다. |
| `description` | 데이터 세트 생성 중 제공된 데이터 세트에 대한 설명입니다. |
| `value` | 데이터 세트의 ID입니다. |
| `streamingIngestionEnabled` | 스트리밍 수집에 데이터 세트를 사용할 수 있는지 여부입니다. |
| `createdUser` | 데이터 세트를 만든 사용자의 사용자 ID입니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜에 대한 것입니다. `date` 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. |

+++

## ID 네임스페이스별 목록 프로필 배포

`/previewsamplestatus/report/namespace` 엔드포인트에 대한 GET 요청을 수행하여 프로필 스토어에 있는 모든 병합된 프로필의 ID 네임스페이스별 분류를 볼 수 있습니다. 여기에는 Adobe에서 제공하는 표준 ID와 조직에서 정의한 사용자 정의 ID가 모두 포함됩니다.

ID 네임스페이스는 고객 데이터와 관련된 컨텍스트의 지표 역할을 하는 Adobe Experience Platform ID 서비스의 중요한 구성 요소입니다. 자세한 내용을 보려면 [ID 네임스페이스 개요](../../identity-service/features/namespaces.md)를 읽는 것부터 시작하십시오.

>[!NOTE]
>
>하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 네임스페이스별 총 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 프로필 수 지표보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

**API 형식**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 쿼리 매개변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `date` | 반환할 보고서의 날짜를 지정합니다. 날짜에 여러 보고서가 실행된 경우 해당 날짜에 대한 가장 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 없으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: `YYYY-MM-DD`. | `date=2025-6-20` |

**요청**

다음 요청은 `date` 매개 변수를 지정하지 않으며 가장 최근 보고서를 반환합니다.

+++ 네임스페이스별 프로필 배포에 대한 최신 보고서를 반환하는 샘플 요청입니다. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**응답**

성공적인 응답은 HTTP 상태 200을 반환하고 `data` 배열을 포함하며, 개별 개체에는 각 네임스페이스에 대한 세부 정보가 들어 있습니다. 표시된 응답이 4개의 네임스페이스를 표시하도록 잘렸습니다.

+++ 샘플 응답에는 네임스페이스별 프로필 배포에 대한 정보가 포함되어 있습니다.

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
| -------- | ----------- |
| `sampleCount` | 네임스페이스에서 샘플링된 병합된 프로필의 총 수입니다. |
| `samplePercentage` | `sampleCount`은(는) 십진수 형식으로 표현되는 샘플링된 병합 프로필(`numRowsToRead`마지막 샘플 상태[에서 반환된 ](#view-last-sample-status) 값)의 백분율입니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜에 대한 것입니다. `date` 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. |
| `fullIDsFragmentCount` | 네임스페이스의 총 프로필 조각 수입니다. |
| `fullIDsCount` | 네임스페이스에 병합된 총 프로필 수입니다. |
| `fullIDsPercentage` | `fullIDsCount`은(는) 10진수 형식으로 표현되는 총 병합 프로필 비율(`totalRows`마지막 샘플 상태[에서 반환된 ](#view-last-sample-status) 값)입니다. |
| `code` | 네임스페이스에 대한 `code`입니다. 이 ID는 [Adobe Experience Platform ID 서비스 API](../../identity-service/api/list-namespaces.md)를 사용하여 네임스페이스로 작업할 때 찾을 수 있으며 Experience Platform UI에서 [!UICONTROL Identity symbol]이라고도 합니다. 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/features/namespaces.md)를 참조하세요. |
| `value` | 네임스페이스에 대한 `id` 값입니다. [ID 서비스 API](../../identity-service/api/list-namespaces.md)를 사용하여 네임스페이스로 작업할 때 찾을 수 있습니다. |

+++

## 데이터 세트 통계 나열 {#dataset-stats}

`/previewsamplestatus/report/dataset_stats` 끝점에 GET 요청을 하여 데이터 집합에 대한 통계를 제공하는 보고서를 생성할 수 있습니다.

**API 형식**

```http
GET /previewsamplestatus/report/dataset_stats
```

**요청**

+++ 데이터 세트 통계 보고서를 생성하기 위한 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**응답**

성공적인 응답은 데이터 세트의 통계에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 데이터 세트의 통계에 대한 정보가 포함된 샘플 응답입니다.

>[!NOTE]
>
>다음 응답은 3개의 데이터 세트를 표시하도록 잘렸습니다.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `120days` | 120일의 데이터 만료 후 데이터 집합에 남아 있는 레코드 수입니다. |
| `14days` | 14일의 데이터 만료 후 데이터 집합에 남아 있는 레코드 수입니다. |
| `30days` | 30일 데이터 만료 후 데이터 집합에 남아 있는 레코드 수입니다. |
| `365days` | 365일의 데이터 만료 후 데이터 집합에 남아 있는 레코드 수입니다. |
| `60days` | 데이터 만료 후 60일이 지나면 데이터 세트에 남아 있게 되는 레코드 수입니다. |
| `7days` | 데이터 만료 후 7일이 지나면 데이터 세트에 남아 있게 되는 레코드 수입니다. |
| `90days` | 데이터 만료 후 90일 동안 데이터 집합에 남아 있는 레코드 수입니다. |
| `datasetId` | 데이터 세트의 ID입니다. |
| `datasetType` | 데이터 세트 유형. 이 값은 `Profiles` 또는 `ExperienceEvents`일 수 있습니다. |
| `percentEvents` | 데이터 세트 내에 있는 경험 이벤트 레코드의 백분율입니다. |
| `percentProfiles` | 데이터 세트 내에 있는 프로필 레코드의 백분율입니다. |
| `profileFragments` | 데이터 세트에 있는 총 프로필 조각 수입니다. |
| `records` | 데이터 세트에 수집된 총 프로필 레코드 수입니다. |
| `totalProfiles` | 데이터 세트에 수집된 총 프로필 수입니다. |

+++

## 다음 단계

이제 프로필 저장소에서 샘플 데이터를 미리 보고 데이터에 대한 여러 보고서를 실행하는 방법을 알았으므로, 세그먼테이션 서비스 API의 예상 및 미리 보기 끝점을 사용하여 세그먼트 정의와 관련된 요약 수준 정보를 볼 수도 있습니다. 다음은 예상 대상을 격리하는 데 유용한 정보입니다. Segmentation API를 사용하여 미리 보기 및 예상 작업을 수행하는 방법에 대한 자세한 내용은 [미리 보기 및 예상 끝점 안내서](../../segmentation/api/previews-and-estimates.md)를 참조하십시오.

