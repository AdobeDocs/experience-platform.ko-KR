---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 프로필 시스템 작업 API 끝점
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform을 사용하면 더 이상 필요하지 않거나 실수로 추가된 실시간 고객 프로필 데이터를 제거하기 위해 프로필 저장소에서 데이터 세트 또는 일괄 처리를 삭제할 수 있습니다. 이를 위해서는 프로필 API를 사용하여 프로필 시스템 작업을 만들거나 요청을 삭제해야 합니다.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 2%

---

# 프로필 시스템 작업 끝점(요청 삭제)

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 인제스트하고 개별 고객을 위한 강력한 프로파일을 구축할 수 있습니다. [!DNL Platform]으로 인제스트된 데이터는 [!DNL Data Lake]에 저장되며, 데이터 세트가 프로필에 대해 활성화된 경우 해당 데이터도 [!DNL Real-time Customer Profile] 데이터 저장소에도 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하기 위해 프로필 저장소에서 데이터 세트 또는 일괄 처리를 삭제할 수 있습니다. 이 작업을 수행하려면 [!DNL Real-time Customer Profile] API를 사용하여 [!DNL Profile] 시스템 작업 또는 `delete request`을 만들어야 합니다. 이 작업은 필요에 따라 수정, 모니터링 또는 제거할 수도 있습니다.

>[!NOTE]
>
>[!DNL Data Lake]에서 데이터 세트 또는 배치를 삭제하려는 경우 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 방문하십시오.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, Experience Platform API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 삭제 요청 보기

삭제 요청은 장기간 실행되는 비동기 프로세스입니다. 즉, 조직에서 한 번에 여러 개의 삭제 요청을 실행할 수 있습니다. 조직에서 현재 실행 중인 모든 삭제 요청을 보려면 `/system/jobs` 종단점에 대한 GET 요청을 수행할 수 있습니다.

선택적 쿼리 매개 변수를 사용하여 응답에서 반환된 삭제 요청 목록을 필터링할 수도 있습니다. 여러 매개 변수를 사용하려면 앰퍼샌드(`&`)를 사용하여 각 매개 변수를 구분합니다.

**API 형식**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `start` | 요청의 만들기 시간에 따라 반환된 결과 페이지를 오프셋합니다. 예: `start=4` |
| `limit` | 반환된 결과 수를 제한합니다. 예: `limit=10` |
| `page` | 요청의 만들기 시간에 따라 특정 결과 페이지를 반환합니다. 예: `page=2` |
| `sort` | 결과를 오름차순(`asc`) 또는 내림차순(`desc`)으로 특정 필드별로 정렬합니다. 여러 결과 페이지를 반환할 때는 정렬 매개 변수가 작동하지 않습니다. 예: `sort=batchId:asc` |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 해당 요청의 세부 사항을 포함하는 각 삭제 요청에 대한 객체가 포함된 &quot;children&quot; 배열이 포함됩니다.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| 속성 | 설명 |
|---|---|
| `_page.count` | 총 요청 수입니다. 이 응답은 공간에 대해 잘렸습니다. |
| `_page.next` | 결과의 추가 페이지가 있는 경우 [조회 요청](#view-a-specific-delete-request)의 ID 값을 `"next"` 값이 제공된 값으로 대체하여 결과의 다음 페이지를 보십시오. |
| `jobType` | 만드는 작업 유형입니다. 이 경우 항상 `"DELETE"`을 반환합니다. |
| `status` | 삭제 요청의 상태입니다. 가능한 값은 `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`입니다. |
| `metrics` | 처리된 레코드 수(`"recordsProcessed"`) 및 요청을 처리한 시간(초) 또는 요청을 완료하는 데 걸린 시간을 포함하는 개체(`"timeTakenInSec"`). |

## 삭제 요청 {#create-a-delete-request} 만들기

새 삭제 요청을 시작하는 것은 삭제될 데이터 세트 또는 일괄 처리의 ID가 요청 본문에 제공되는 `/systems/jobs` 끝점에 대한 POST 요청을 통해 수행됩니다.

### 데이터 집합 삭제

프로필 저장소에서 데이터 세트를 삭제하려면 데이터 세트 ID를 POST 요청 본문에 포함해야 합니다. 이 작업을 수행하면 지정된 데이터 세트에 대한 모든 데이터가 삭제됩니다. [!DNL Experience Platform] 레코드 및 시간 시리즈 스키마 모두를 기반으로 데이터 세트를 삭제할 수 있습니다.

**API 형식**

```http
POST /system/jobs
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 속성 | 설명 |
|---|---|
| `dataSetId` | **(필수)** 삭제할 데이터 세트의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 만든 삭제 요청의 세부 사항을 반환합니다. 요청을 조회하고 상태를 확인하는 데 사용할 수 있습니다. 생성 시 요청에 대한 `status`은 처리를 시작할 때까지 `"NEW"`입니다. 응답의 `dataSetId`은 요청에서 보낸 `dataSetId`과 일치해야 합니다.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 속성 | 설명 |
|---|---|
| `id` | 삭제 요청의 고유한 시스템 생성 읽기 전용 ID. |
| `dataSetId` | POST 요청에 지정된 데이터 세트의 ID입니다. |

### 일괄 처리 삭제

배치를 삭제하려면 일괄 처리 ID를 POST 요청 본문에 포함해야 합니다. 기록 스키마를 기반으로 데이터 집합에 대한 배치를 삭제할 수 없다는 점을 참고하십시오. 시간 시리즈 스키마를 기반으로 데이터 세트에 대한 배치만 삭제할 수 있습니다.

>[!NOTE]
>
> 레코드 스키마를 기반으로 데이터 집합에 대한 배치를 삭제할 수 없는 이유는 레코드 유형 데이터 세트 배치가 이전 레코드를 덮어쓰기 때문에 &quot;실행 취소&quot; 또는 삭제할 수 없습니다. 기록 스키마를 기반으로 데이터 집합에 대한 잘못된 배치의 영향을 제거하는 유일한 방법은 잘못된 레코드를 덮어쓰도록 올바른 데이터로 일괄 처리를 다시 인제스트하는 것입니다.

기록 및 시간 시리즈 동작에 대한 자세한 내용은 [!DNL XDM System] 개요에서 XDM 데이터 비헤이비어](../../xdm/home.md#data-behaviors)에 대한 [섹션을 검토하십시오.

**API 형식**

```http
POST /system/jobs
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 속성 | 설명 |
|---|---|
| `batchId` | **(필수)** 삭제할 배치의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 만든 삭제 요청의 세부 사항을 반환합니다. 요청을 조회하고 상태를 확인하는 데 사용할 수 있습니다. 생성 시 요청에 대한 `"status"`은 처리를 시작할 때까지 `"NEW"`입니다. 응답의 `"batchId"` 값은 요청에서 전송된 `"batchId"` 값과 일치해야 합니다.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 속성 | 설명 |
|---|---|
| `id` | 삭제 요청의 고유한 시스템 생성 읽기 전용 ID. |
| `batchId` | POST 요청에 지정된 일괄 처리의 ID. |

레코드 데이터 세트 일괄 처리에 대한 삭제 요청을 시작하려고 하면 다음과 유사한 400개 수준 오류가 발생합니다.

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## 특정 삭제 요청 보기 {#view-a-specific-delete-request}

상태 등의 세부 사항을 포함하여 특정 삭제 요청을 보려면 `/system/jobs` 끝점에 대한 조회(GET) 요청을 수행하고 경로에 삭제 요청의 ID를 포함할 수 있습니다.

**API 형식**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DELETE_REQUEST_ID}` | **(필수)** 보려는 삭제 요청의 ID입니다. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에서는 업데이트된 상태를 포함하여 삭제 요청의 세부 정보를 제공합니다. 응답의 삭제 요청 ID(`"id"` 값)는 요청 경로에서 전송된 ID와 일치해야 합니다.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| 속성 | 설명 |
|---|---|
| `jobType` | 만드는 작업의 유형입니다. 이 경우 항상 `"DELETE"`을 반환합니다. |
| `status` | 삭제 요청의 상태입니다. 가능한 값:`"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | 처리된 레코드 수(`"recordsProcessed"`) 및 요청을 처리한 시간(초) 또는 요청을 완료하는 데 걸린 시간을 포함하는 배열(`"timeTakenInSec"`). |

삭제 요청 상태가 `"COMPLETED"`이면 데이터 액세스 API를 사용하여 삭제된 데이터에 액세스하려고 시도하여 데이터가 삭제되었음을 확인할 수 있습니다. 데이터 액세스 API를 사용하여 데이터 세트 및 배치에 액세스하는 방법에 대한 지침은 [데이터 액세스 설명서](../../data-access/home.md)를 검토하십시오.

## 삭제 요청 제거

[!DNL Experience Platform] 이전 요청을 삭제할 수 있습니다. 이 작업은 삭제 작업이 완료되지 않았거나 처리 단계에 갇혀 있는지 등 여러 가지 이유로 유용할 수 있습니다. 삭제 요청을 제거하기 위해 `/system/jobs` 끝점에 DELETE 요청을 수행하고 요청 경로로 제거할 삭제 요청의 ID를 포함할 수 있습니다.

**API 형식**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 매개 변수 | 설명 |
|---|---|
| {DELETE_REQUEST_ID} | 제거할 삭제 요청의 ID. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. ID로 삭제 요청을 보기 위한 GET 요청을 수행하여 요청이 삭제되었음을 확인할 수 있습니다. 삭제 요청이 제거되었음을 나타내는 HTTP 상태 404(찾을 수 없음)를 반환해야 합니다.

## 다음 단계

이제 [!DNL Experience Platform] 내의 [!DNL Profile Store]에서 데이터 집합 및 배치를 삭제하는 데 관련된 단계를 알고 있으므로 잘못 추가되었거나 조직에서 더 이상 필요하지 않은 데이터를 안전하게 삭제할 수 있습니다. 삭제 요청은 취소할 수 없으므로 지금 필요하지 않으며 나중에 필요하지 않을 데이터만 삭제해야 합니다.
