---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;미리 보기;sample
title: 미리 보기 샘플 상태(프로필 미리 보기) API 끝점
description: 실시간 고객 프로필 API의 일부인 미리 보기 샘플 상태 끝점을 사용하면 성공적인 최신 프로필 데이터 샘플을 미리 보고 데이터 세트 및 ID별로 프로필 배포를 나열하고 데이터 세트 오버랩 보고서를 생성할 수 있습니다.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 459eb626101b7382b8fe497835cc19f7d7adc6b2
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 1%

---

# 샘플 상태 끝점 미리 보기(프로필 미리 보기)

Adobe Experience Platform을 사용하면 고객 데이터를 여러 소스에서 인제스트하여 각 개별 고객을 위한 강력하고 통합된 프로파일을 구축할 수 있습니다. 데이터를 플랫폼에 수집하면 샘플 작업이 실행되어 프로필 수 및 기타 프로필 관련 지표를 업데이트합니다.

실시간 고객 프로필 API의 `/previewsamplestatus` 끝점을 사용하여 이 샘플 작업의 결과를 볼 수 있습니다. 또한 이 끝점은 데이터 세트와 ID 네임스페이스로 프로필 배포를 나열하는 데 사용할 수 있으며, 조직의 프로필 저장소 구성을 확인할 수 있도록 데이터 집합 오버랩 보고서를 생성하는 데 사용할 수 있습니다. 이 안내서에서는 `/previewsamplestatus` API 끝점을 사용하여 이러한 지표를 보는 데 필요한 단계를 안내합니다.

>[!NOTE]
>
>예상 대상을 분리하는 데 도움이 되도록 세그먼트 정의와 관련된 요약 수준 정보를 볼 수 있는 Adobe Experience Platform 세그멘테이션 서비스 API의 일부로 사용할 수 있는 예측 및 미리 보기 끝점이 있습니다. 세그먼트 미리 보기 및 예상 끝점을 사용하여 작업하는 자세한 단계를 보려면 [!DNL Segmentation] API 개발자 안내서의 일부인 [미리 보기 및 예상 끝점 안내서](../../segmentation/api/previews-and-estimates.md)를 참조하십시오.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 프로필 조각과 병합된 프로필 비교

이 안내서는 &quot;프로필 조각&quot;과 &quot;병합된 프로필&quot;을 모두 참조합니다. 계속하기 전에 이러한 용어 간의 차이를 이해하는 것이 중요합니다.

각 개별 고객 프로필은 여러 프로필 조각으로 구성되며, 병합되어 해당 고객에 대한 단일 보기를 형성합니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직은 여러 데이터 세트에 나타나는 해당 단일 고객과 관련된 여러 프로필 조각을 가질 수 있습니다.

프로필 조각을 Platform(플랫폼)으로 인제스트하면 병합 정책을 기반으로 하여 해당 고객에 대한 단일 프로필을 만들기 위해 함께 병합됩니다. 따라서 각 프로파일이 여러 조각으로 구성되므로 전체 프로필 조각 수는 항상 병합된 프로필의 총 수보다 클 수 있습니다.

Experience Platform 내 프로필 및 역할에 대한 자세한 내용은 [실시간 고객 프로필 개요](../home.md)를 읽으십시오.

## 샘플 작업이 트리거되는 방식

실시간 고객 프로파일에 대해 활성화된 데이터를 [!DNL Platform]으로 인제스트하면 프로필 데이터 저장소 내에 저장됩니다. 프로필 스토어에 레코드를 수집하면 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 시작되어 카운트가 업데이트됩니다. 샘플이 트리거되는 방법은 사용되는 섭취 유형에 따라 달라집니다.

* **스트리밍 데이터 워크플로우**&#x200B;의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 확인이 수행됩니다. 있을 경우 샘플 작업이 자동으로 트리거되어 카운트를 업데이트합니다.
* **일괄 처리 통합**&#x200B;의 경우, 배치를 프로필 스토어에 성공적으로 인제스트한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 작업을 실행하여 카운트를 업데이트합니다. 프로필 API를 사용하면 성공적인 최신 샘플 작업을 미리 볼 수 있을 뿐만 아니라 데이터 세트 및 ID 네임스페이스별 프로필 배포를 나열할 수 있습니다.

네임스페이스 지표별 프로필 수 및 프로필은 Experience Platform UI의 [!UICONTROL 프로필] 섹션 내에서도 사용할 수 있습니다. UI를 사용하여 프로필 데이터에 액세스하는 방법에 대한 자세한 내용은 [[!DNL Profile] UI 안내서](../ui/user-guide.md)를 참조하십시오.

## 마지막 샘플 상태 보기 {#view-last-sample-status}

`/previewsamplestatus` 끝점에 대한 GET 요청을 수행하여 IMS 조직에 대해 실행된 마지막으로 성공한 샘플 작업에 대한 세부 정보를 볼 수 있습니다. 여기에는 샘플에 있는 총 프로필 수, 프로필 수 지표 또는 Experience Platform 내에 있는 총 프로필 수가 포함됩니다.

프로필 개수는 프로필 조각을 병합한 후 생성되어 각 개별 고객에 대한 단일 프로필을 형성합니다. 즉, 프로필 조각을 함께 병합하면 모두 동일한 개인과 관련되어 있으므로 &quot;1&quot; 프로필 수가 반환됩니다.

프로필 수에는 속성(레코드 데이터)이 있는 프로필 및 Adobe Analytics 프로필과 같은 시간 시리즈(이벤트) 데이터만 포함된 프로파일도 모두 포함됩니다. Platform(플랫폼) 내에서 최신 총 프로필 수를 제공하기 위해 프로필 데이터를 인제스트할 때 샘플 작업은 정기적으로 새로 고쳐집니다.

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

응답에는 조직에 대해 실행된 마지막 성공적인 샘플 작업에 대한 세부 사항이 포함됩니다.

>[!NOTE]
>
>이 예제 응답에서 `numRowsToRead` 및 `totalRows`는 서로 같습니다. Experience Platform에 있는 프로필 수에 따라 이러한 경우가 발생할 수 있습니다. 그러나 일반적으로 이러한 두 숫자는 서로 다르며, 샘플이 전체 프로필 수(`totalRows`)의 하위 집합으로 표시되기 때문에 `numRowsToRead`은 더 작은 숫자입니다.

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
| `numRowsToRead` | 샘플에 병합된 프로필의 총 수입니다. |
| `sampleJobRunning` | 샘플 작업이 진행 중일 때 `true`을 반환하는 부울 값입니다. 일괄 처리 파일이 프로필 스토어에 실제로 추가될 때까지 지연이 발생하는 지연에 대한 투명도를 제공합니다. |
| `cosmosDocCount` | Cosmos의 총 문서 수입니다. |
| `totalFragmentCount` | 프로필 저장소의 총 프로필 조각 수입니다. |
| `lastSuccessfulBatchTimestamp` | 마지막으로 성공한 일괄 처리 통합 타임스탬프. |
| `streamingDriven` | *이 필드는 사용되지 않으며 응답에 대한 중요도가 없습니다.* |
| `totalRows` | Experience Platform에서 병합된 프로필의 총 수입니다. &#39;프로필 수&#39;로도 알려져 있습니다. |
| `lastBatchId` | 마지막 일괄 처리 ID. |
| `status` | 마지막 샘플의 상태입니다. |
| `samplingRatio` | 총 병합된 프로필(`numRowsToRead`)에 대한 병합된 프로필 비율(`totalRows`)은 소수 형식으로 표현됩니다. |
| `mergeStrategy` | 샘플에 사용된 병합 전략입니다. |
| `lastSampledTimestamp` | 마지막으로 성공한 샘플 타임스탬프. |

## 데이터 세트별 프로필 배포 목록

데이터 집합별 프로필 배포를 보려면 `/previewsamplestatus/report/dataset` 끝점에 대한 GET 요청을 수행할 수 있습니다.

**API 형식**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 보고서 반환 날짜를 지정합니다. 날짜에 여러 보고서가 실행되면 해당 날짜에 대한 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 존재하지 않으면 404 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식:YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청에서는 `date` 매개 변수를 사용하여 지정된 날짜에 대한 최신 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 데이터 집합 개체 목록이 포함된 `data` 배열이 포함됩니다. 표시된 응답이 3개의 데이터 세트를 표시하도록 잘렸습니다.

>[!NOTE]
>
>날짜에 대해 여러 보고서가 존재하는 경우 최신 보고서만 반환됩니다. 제공된 날짜에 데이터 집합 보고서가 없으면 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

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
| `sampleCount` | 이 데이터 세트 ID를 사용하여 병합된 프로필의 샘플링된 총 수입니다. |
| `samplePercentage` | 샘플링된 병합된 프로필의 총 수(`numRowsToRead` 값([마지막 샘플 상태](#view-last-sample-status)에서 반환됨)의 백분율로 표시됨)`sampleCount` |
| `fullIDsCount` | 이 데이터 집합 ID를 사용한 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | 병합된 프로필의 총 수([마지막 샘플 상태](#view-last-sample-status)에서 반환되는 `totalRows` 값)의 백분율로 나타낸 `fullIDsCount`. |
| `name` | 데이터 집합을 만드는 동안 제공된 데이터 집합의 이름입니다. |
| `description` | 데이터 집합을 만드는 동안 제공된 데이터 세트에 대한 설명입니다. |
| `value` | 데이터 세트의 ID입니다. |
| `streamingIngestionEnabled` | 데이터 세트에 스트리밍 통합 사용 여부. |
| `createdUser` | 데이터 집합을 만든 사용자의 사용자 ID. |
| `reportTimestamp` | 보고서의 타임스탬프. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜에 대한 것입니다. `date` 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. |

## 네임스페이스별 프로필 배포 목록

프로필 저장소에 있는 병합된 모든 프로필에서 ID 네임스페이스별 분류를 보려면 `/previewsamplestatus/report/namespace` 끝점에 GET 요청을 수행할 수 있습니다.

ID 네임스페이스는 고객 데이터와 관련된 컨텍스트의 지표로 사용되는 Adobe Experience Platform Identity Service의 중요한 구성 요소입니다. 자세한 내용은 [identity 네임스페이스 개요](../../identity-service/namespaces.md)를 읽으십시오.

>[!NOTE]
>
>네임스페이스별 전체 프로필 수(각 네임스페이스에 대해 표시된 값을 함께 추가)는 하나의 프로필이 여러 네임스페이스와 연결될 수 있으므로 항상 프로필 수 지표보다 높습니다. 예를 들어 고객이 두 개 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

**API 형식**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 보고서 반환 날짜를 지정합니다. 날짜에 여러 보고서가 실행되면 해당 날짜에 대한 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 존재하지 않으면 404 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식:YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청은 `date` 매개 변수를 지정하지 않으므로 가장 최근 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 각 네임스페이스에 대한 세부 정보가 포함된 개별 객체가 포함된 `data` 배열이 포함됩니다. 표시된 응답이 4개의 네임스페이스를 표시하도록 잘렸습니다.

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
| `samplePercentage` | 샘플링된 병합된 프로필의 백분율([마지막 샘플 상태](#view-last-sample-status)에서 반환되는 `numRowsToRead` 값)로 표시되는 `sampleCount`입니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜에 대한 것입니다. `date` 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. |
| `fullIDsFragmentCount` | 네임스페이스에 있는 전체 프로필 조각 수입니다. |
| `fullIDsCount` | 네임스페이스에 있는 병합된 프로필의 총 수입니다. |
| `fullIDsPercentage` | 병합된 총 프로필([마지막 샘플 상태](#view-last-sample-status)에서 반환되는 `totalRows` 값)의 백분율로, 십진수 형식으로 표현됩니다.`fullIDsCount` |
| `code` | 네임스페이스의 `code`. 이것은 [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md)를 사용하여 네임스페이스를 사용하여 작업할 때 찾을 수 있으며 Experience Platform UI에서 [!UICONTROL ID 기호]라고도 합니다. 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/namespaces.md)를 참조하십시오. |
| `value` | 네임스페이스의 `id` 값입니다. 이것은 [Identity Service API](../../identity-service/api/list-namespaces.md)를 사용하여 네임스페이스를 사용하여 작업할 때 찾을 수 있습니다. |

## 데이터 세트 오버랩 보고서 생성

데이터 세트 오버랩 보고서는 주소 지정 가능한 대상(프로필)에 가장 많이 기여하는 데이터 세트를 노출하여 조직의 프로필 저장소 구성을 표시합니다. 이 보고서를 사용하면 데이터에 대한 통찰력을 제공할 뿐만 아니라 특정 데이터 세트에 대한 TTL(TTL)을 설정하는 등 라이선스 사용량을 최적화하는 작업을 수행할 수 있습니다.

`/previewsamplestatus/report/dataset/overlap` 끝점에 대한 GET 요청을 수행하여 데이터 집합 오버랩 보고서를 생성할 수 있습니다.

명령줄 또는 Postman UI를 사용하여 데이터 세트 오버랩 보고서를 생성하는 방법에 대한 단계별 지침을 보려면 [데이터 세트 오버랩 보고서 자습서](../tutorials/dataset-overlap-report.md)를 참조하십시오.

**API 형식**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 보고서 반환 날짜를 지정합니다. 동일한 날짜에 여러 보고서가 실행되면 해당 날짜에 대한 최근 보고서가 반환됩니다. 지정된 날짜에 보고서가 존재하지 않으면 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식:YYYY-MM-DD. 예: `date=2024-12-31` |

**요청**

다음 요청에서는 `date` 매개 변수를 사용하여 지정된 날짜에 대한 최신 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 데이터 세트 오버랩 보고서가 반환됩니다.

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
| `data` | `data` 개체에는 데이터 세트와 각 프로필 카운트의 쉼표로 구분된 목록이 포함되어 있습니다. |
| `reportTimestamp` | 보고서의 타임스탬프. 요청 중에 `date` 매개 변수가 제공된 경우 반환된 보고서는 제공된 날짜에 대한 것입니다. `date` 매개 변수를 제공하지 않으면 가장 최근 보고서가 반환됩니다. |

보고서 결과는 응답의 데이터 세트와 프로필 카운트에서 해석할 수 있습니다. 다음 예제 보고서 `data` 개체를 생각해 보십시오.

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

이 보고서는 다음 정보를 제공합니다.
* 다음 데이터 세트에서 나오는 데이터로 구성된 123개의 프로필이 있습니다.`5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 다음 두 데이터 세트에서 나오는 데이터로 구성된 454,412개의 프로필이 있습니다.`5d92921872831c163452edc8` 및 `5eb2cdc6fa3f9a18a7592a98`.
* 데이터 세트 `5eeda0032af7bb19162172a7`의 데이터만 구성하는 107개의 프로필이 있습니다.
* 조직에는 총 454,642개의 프로필이 있습니다.

## 다음 단계

프로필 스토어에서 샘플 데이터를 미리 보고 데이터 세트 오버랩 보고서를 실행하는 방법을 알고 있으므로 세그멘테이션 서비스 API의 예상 및 미리 보기 끝점을 사용하여 세그먼트 정의에 대한 요약 수준 정보를 볼 수도 있습니다. 이 정보는 세그먼트에서 예상 대상을 분리하는 데 도움이 됩니다. 세그멘테이션 API를 사용하여 세그먼트 미리 보기 및 견적을 사용하는 방법에 대한 자세한 내용은 [미리 보기 및 예상 끝점 안내서](../../segmentation/api/previews-and-estimates.md)를 참조하십시오.

