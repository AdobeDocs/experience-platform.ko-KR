---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 프로필 시스템 작업 API 끝점
type: Documentation
description: Adobe Experience Platform을 사용하면 더 이상 필요하지 않거나 오류로 추가된 실시간 고객 프로필 데이터를 제거하기 위해 프로필 스토어에서 데이터 세트 또는 배치를 삭제할 수 있습니다. 이를 위해서는 프로필 API를 사용하여 프로필 시스템 작업을 생성하거나 요청을 삭제해야 합니다.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 2%

---

# 프로필 시스템 작업 끝점(요청 삭제)

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 수집하고 개별 고객을 위한 강력한 프로필을 구축할 수 있습니다. [!DNL Platform]에 수집된 데이터는 [!DNL Data Lake]에 저장되며, 프로필에 대해 데이터 세트를 사용하도록 설정한 경우 해당 데이터도 [!DNL Real-Time Customer Profile] 데이터 저장소에 저장됩니다. 더 이상 필요하지 않거나 오류로 추가된 데이터를 제거하기 위해 프로필 저장소에서 데이터 세트와 연결된 프로필 데이터를 삭제해야 하는 경우가 있습니다. 이를 위해서는 [!DNL Real-Time Customer Profile] API를 사용하여 필요한 경우 수정, 모니터링 또는 제거할 수 있는 [!DNL Profile] 시스템 작업 또는 `delete request`을(를) 만들어야 합니다.

>[!NOTE]
>
>[!DNL Data Lake]에서 데이터 세트 또는 배치를 삭제하려면 [카탈로그 서비스 개요](../../catalog/home.md)에서 자세한 내용을 확인하십시오.

## 시작하기

이 가이드에 사용된 API 끝점은 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)의 일부입니다. 계속하기 전에 [시작 안내서](getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 삭제 요청 보기

삭제 요청은 오래 실행되는 비동기 프로세스입니다. 즉, 조직에서 한 번에 여러 삭제 요청을 실행할 수 있습니다. 조직에서 현재 실행 중인 모든 삭제 요청을 보려면 `/system/jobs` 끝점에 대한 GET 요청을 수행할 수 있습니다.

선택적 쿼리 매개 변수를 사용하여 응답에서 반환되는 삭제 요청 목록을 필터링할 수도 있습니다. 여러 매개 변수를 사용하려면 앰퍼샌드(`&`)를 사용하여 각 매개 변수를 구분하십시오.

**API 형식**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
|---|---|
| `start` | 요청의 생성 시간에 따라 반환된 결과 페이지를 오프셋합니다. 예: `start=4` |
| `limit` | 반환되는 결과 수를 제한합니다. 예: `limit=10` |
| `page` | 요청 생성 시간에 따라 결과의 특정 페이지를 반환합니다. 예: `page=2` |
| `sort` | 결과를 오름차순(`asc`) 또는 내림차순(`desc`)으로 특정 필드별로 정렬합니다. 여러 결과 페이지를 반환할 때 정렬 매개 변수가 작동하지 않습니다. 예: `sort=batchId:asc` |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 해당 요청의 세부 사항이 포함된 각 삭제 요청에 대한 오브젝트가 있는 &quot;하위&quot; 배열이 포함됩니다.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
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
| `_page.count` | 총 요청 수입니다. 이 응답은 공백으로 잘렸습니다. |
| `_page.next` | 추가 결과 페이지가 있는 경우 [조회 요청](#view-a-specific-delete-request)의 ID 값을 제공된 `"next"` 값으로 바꾸어 다음 결과 페이지를 보십시오. |
| `jobType` | 생성 중인 작업 유형입니다. 이 경우 항상 `"DELETE"`을(를) 반환합니다. |
| `status` | 삭제 요청의 상태입니다. 가능한 값은 `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`입니다. |
| `metrics` | 처리된 레코드 수(`"recordsProcessed"`)와 요청이 처리된 시간(초) 또는 요청이 완료되는 데 걸린 시간(`"timeTakenInSec"`)을 포함하는 개체입니다. |

## 삭제 요청 만들기 {#create-a-delete-request}

새 삭제 요청을 시작하는 작업은 `/systems/jobs` 끝점에 대한 POST 요청을 통해 수행됩니다. 여기서 삭제할 데이터 세트 또는 배치의 ID는 요청 본문에 제공됩니다.

### 데이터 세트 및 관련 프로필 데이터 삭제

POST 저장소에서 데이터 세트 및 데이터 세트와 연결된 모든 프로필 데이터를 삭제하려면 데이터 세트 ID를 프로필 요청의 본문에 포함해야 합니다. 이 작업은 주어진 데이터 세트에 대한 모든 데이터를 삭제합니다. [!DNL Experience Platform]을(를) 사용하면 레코드와 시계열 스키마를 기준으로 데이터 세트를 삭제할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 속성 | 설명 |
|---|---|
| `dataSetId` | **(필수)** 삭제하려는 데이터 세트의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 생성된 삭제 요청의 세부 정보를 반환합니다. 요청을 검색하고 상태를 확인하는 데 사용할 수 있습니다. 생성 시 요청의 `status`은(는) 처리를 시작할 때까지 `"NEW"`입니다. 응답의 `dataSetId`은(는) 요청에서 보낸 `dataSetId`과(와) 일치해야 합니다.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 속성 | 설명 |
|---|---|
| `id` | 시스템에서 생성한 삭제 요청에 대한 읽기 전용 ID입니다. |
| `dataSetId` | POST 요청에 지정된 데이터 세트의 ID입니다. |

### 일괄 처리 삭제

배치를 삭제하려면 배치 ID가 POST 요청 본문에 포함되어야 합니다. 레코드 스키마를 기반으로 데이터 세트에 대한 배치를 삭제할 수 없습니다. 시계열 스키마를 기반으로 하는 데이터 세트의 배치만 삭제할 수 있습니다.

>[!NOTE]
>
> 레코드 스키마를 기반으로 데이터 세트 배치를 삭제할 수 없는 이유는 레코드 유형 데이터 세트 배치가 이전 레코드를 덮어쓰므로 &quot;실행 취소&quot; 또는 삭제할 수 없기 때문입니다. 레코드 스키마를 기반으로 데이터 세트에 대한 잘못된 배치의 영향을 제거하는 유일한 방법은 잘못된 레코드를 덮어쓰기 위해 배치를 올바른 데이터로 다시 수집하는 것입니다.

레코드 및 시계열 동작에 대한 자세한 내용은 [!DNL XDM System] 개요에서 [XDM 데이터 동작에 대한 섹션](../../xdm/home.md#data-behaviors)을 검토하십시오.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 속성 | 설명 |
|---|---|
| `batchId` | **(필수)** 삭제하려는 일괄 처리의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 생성된 삭제 요청의 세부 정보를 반환합니다. 요청을 검색하고 상태를 확인하는 데 사용할 수 있습니다. 생성 시 요청의 `"status"`은(는) 처리를 시작할 때까지 `"NEW"`입니다. 응답의 `"batchId"` 값은 요청에서 보낸 `"batchId"` 값과 일치해야 합니다.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 속성 | 설명 |
|---|---|
| `id` | 시스템에서 생성한 삭제 요청에 대한 읽기 전용 ID입니다. |
| `batchId` | POST 요청에 지정된 일괄 처리의 ID입니다. |

레코드 데이터 세트 배치에 대한 삭제 요청을 시작하려고 하면 다음과 유사한 400 수준 오류가 발생합니다.

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

상태와 같은 세부 정보를 포함하여 특정 삭제 요청을 보려면 `/system/jobs` 끝점에 대한 조회(GET) 요청을 수행하고 삭제 요청의 ID를 경로에 포함할 수 있습니다.

**API 형식**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{DELETE_REQUEST_ID}` | **(필수)** 보려는 삭제 요청의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답은 업데이트된 상태를 포함하여 삭제 요청의 세부 정보를 제공합니다. 응답의 삭제 요청 ID(`"id"` 값)는 요청 경로에서 보낸 ID와 일치해야 합니다.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
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
| `jobType` | 만들어지는 작업 유형입니다. 이 경우 항상 `"DELETE"`을(를) 반환합니다. |
| `status` | 삭제 요청의 상태입니다. 가능한 값: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | 처리된 레코드 수(`"recordsProcessed"`)와 요청이 처리된 시간(초) 또는 요청이 완료되는 데 걸린 시간(`"timeTakenInSec"`)을 포함하는 배열입니다. |

삭제 요청 상태가 `"COMPLETED"`이면 데이터 액세스 API를 사용하여 삭제된 데이터에 액세스함으로써 데이터가 삭제되었음을 확인할 수 있습니다. 데이터 액세스 API를 사용하여 데이터 세트 및 배치에 액세스하는 방법에 대한 지침은 [데이터 액세스 설명서](../../data-access/home.md)를 참조하십시오.

## 삭제 요청 제거

[!DNL Experience Platform]을(를) 사용하면 이전 요청을 삭제할 수 있습니다. 삭제 작업이 완료되지 않았거나 처리 단계에서 중단되었는지 여부 등 여러 가지 이유로 유용할 수 있습니다. 삭제 요청을 제거하기 위해 `/system/jobs` 끝점에 대한 DELETE 요청을 수행하고 제거할 삭제 요청의 ID를 요청 경로에 포함할 수 있습니다.

**API 형식**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 매개변수 | 설명 |
|---|---|
| {DELETE_REQUEST_ID} | 제거할 삭제 요청의 ID입니다. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 삭제 요청은 HTTP 상태 200(OK)과 빈 응답 본문을 반환합니다. ID로 삭제 요청을 보려면 GET 요청을 수행하여 요청이 삭제되었는지 확인할 수 있습니다. 삭제 요청이 제거되었음을 나타내는 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

## 다음 단계

[!DNL Experience Platform] 내의 [!DNL Profile store]에서 데이터 세트 및 배치를 삭제하는 단계를 알았으므로 잘못 추가되었거나 조직에 더 이상 필요하지 않은 데이터를 안전하게 삭제할 수 있습니다. 삭제 요청은 실행 취소할 수 없으므로 지금은 필요하지 않고 미래에는 필요하지 않다고 확신하는 데이터만 삭제해야 합니다.
