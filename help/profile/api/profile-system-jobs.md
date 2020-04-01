---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로파일 API 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# 프로필 시스템 작업(요청 삭제)

Adobe Experience Platform을 사용하면 다양한 소스의 데이터를 인제스트하고 개별 고객을 위한 강력한 프로파일을 구축할 수 있습니다. Data Lake 및 실시간 고객 프로필 데이터 저장소에 Platform으로 인제스트된 데이터가 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하려면 프로필 저장소에서 데이터 세트 또는 일괄 처리를 삭제해야 하는 경우가 있습니다. 이를 위해서는 실시간 고객 프로필 API를 사용하여 &quot;삭제 요청&quot;이라고도 하는 프로필 시스템 작업을 만들어야 하며, 이 작업은 필요에 따라 수정, 모니터링 또는 제거할 수도 있습니다.

>[!NOTE]
>Data Lake에서 데이터 집합 또는 배치를 삭제하려는 경우, 자세한 내용은 [카탈로그 서비스 개요를](../../catalog/home.md) 방문하십시오.

## 시작하기

이 안내서에서 사용되는 API 끝점은 실시간 고객 프로필 API의 일부입니다. 계속하기 전에 실시간 [고객 프로필 API 개발자 안내서를](getting-started.md)검토하십시오. 특히 프로필 개발자 안내서의 [시작 섹션은](getting-started.md#getting-started) 관련 항목에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 삭제 요청 보기

삭제 요청은 장기간 실행되는 비동기 프로세스입니다. 즉, 조직에서 한 번에 여러 개의 삭제 요청을 실행할 수 있습니다. 조직에서 현재 실행 중인 모든 삭제 요청을 보려면 종단점에 대한 GET 요청을 수행할 수 `/system/jobs` 있습니다.

선택적 쿼리 매개 변수를 사용하여 응답에서 반환되는 삭제 요청 목록을 필터링할 수도 있습니다. 여러 매개 변수를 사용하려면 앰퍼샌드(&amp;)를 사용하여 각 매개 변수를 분리합니다.

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
| `sort` | 결과를 오름차순(`asc`) 또는 내림차순(`desc`)으로 특정 필드별로 정렬합니다. 여러 결과 페이지를 반환할 때 정렬 매개 변수가 작동하지 않습니다. 예: `sort=batchId:asc` |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 해당 요청에 대한 세부 정보가 포함된 각 삭제 요청에 대한 객체가 포함된 &quot;하위&quot; 배열이 포함됩니다.

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
| _page.count | 총 요청 수입니다. 이 응답은 공간에 대해 잘렸습니다. |
| _page.next | 추가 결과 페이지가 있는 경우 [조회 요청의](#view-a-specific-delete-request) ID 값을 제공된 &quot;다음&quot; 값으로 대체하여 결과의 다음 페이지를 봅니다. |
| jobType | 만드는 작업 유형입니다. 이 경우 항상 &quot;DELETE&quot;를 반환합니다. |
| status | 삭제 요청의 상태입니다. 가능한 값은 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;입니다. |
| 지표 | 처리된 레코드 수(&quot;recordsProcessed&quot;) 및 요청이 처리된 시간(초) 또는 요청이 완료하는 데 걸린 시간을 포함하는 개체(&quot;timeTakenInSec&quot;). |

## 삭제 요청 만들기 {#create-a-delete-request}

새 삭제 요청을 시작하는 것은 `/systems/jobs` 끝점에 대한 POST 요청을 통해 수행됩니다. 이 경우 삭제할 데이터 세트 또는 일괄 처리의 ID가 요청의 본문에 제공됩니다.

### 데이터 집합 삭제

데이터 집합을 삭제하려면 데이터 집합 ID를 POST 요청 본문에 포함해야 합니다. 이 작업을 수행하면 지정된 데이터 세트에 대한 모든 데이터가 삭제됩니다. Experience Platform을 사용하면 기록 및 시간 시리즈 스키마를 기반으로 데이터 세트를 삭제할 수 있습니다.

>[!CAUTION]
> Experience Platform UI를 사용하여 프로필 사용 데이터 집합을 삭제하려고 하면 데이터 집합은 통합 기능이 비활성화되지만 API를 사용하여 삭제 요청이 생성될 때까지 삭제되지 않습니다. 자세한 내용은 이 문서의 [부록을](#appendix) 참조하십시오.

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
| dataSetId | **(필수)** 삭제할 데이터 집합의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 만든 삭제 요청의 세부 정보를 반환합니다. 요청을 조회하고 상태를 확인하는 데 사용할 수 있습니다. 생성 `status` 시 요청에 대한 값은 처리가 시작될 `"NEW"` 때까지 입니다. 응답의 `dataSetId` 값은 요청에서 전송된 `dataSetId` 응답과 일치해야 합니다.

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
| ID | 삭제 요청의 시스템에서 생성된 읽기 전용 ID입니다. |
| dataSetId | POST 요청에 지정된 데이터 집합의 ID입니다. |

### 일괄 처리 삭제

배치를 삭제하려면 배치 ID를 POST 요청 본문에 포함해야 합니다. 레코드 스키마를 기준으로 데이터 세트에 대한 일괄 처리를 삭제할 수 없다는 점을 참고하십시오. 시간 시리즈 스키마를 기반으로 한 데이터 세트에 대한 배치만 삭제할 수 있습니다.

>[!NOTE]
> 레코드 스키마를 기반으로 데이터 세트에 대한 배치를 삭제할 수 없는 이유는 레코드 형식 데이터 집합 배치가 이전 레코드를 덮어써기 때문에 &quot;실행 취소&quot; 또는 삭제할 수 없기 때문입니다. 레코드 스키마를 기반으로 데이터 세트에 대해 잘못된 일괄 처리가 미치는 영향을 제거하는 유일한 방법은 잘못된 레코드를 덮어쓸 수 있도록 올바른 데이터로 일괄 처리를 다시 가져오는 것입니다.

기록 및 시간 시리즈 동작에 대한 자세한 내용은 XDM 시스템 개요에서 XDM 데이터 비헤이비어에 [](../../xdm/home.md#data-behaviors) 대한 섹션을 참조하십시오.

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
| batchId | **(필수)** 삭제할 배치의 ID입니다. |

**응답**

성공적인 응답은 요청에 대한 고유한 시스템 생성 읽기 전용 ID를 포함하여 새로 만든 삭제 요청의 세부 정보를 반환합니다. 요청을 조회하고 상태를 확인하는 데 사용할 수 있습니다. 작성 시 요청에 대한 &quot;상태&quot;는 처리가 시작될 때까지 &quot;NEW&quot;입니다. 응답의 &quot;batchId&quot;는 요청에서 전송된 &quot;batchId&quot;와 일치해야 합니다.

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
| ID | 삭제 요청의 시스템에서 생성된 읽기 전용 ID입니다. |
| batchId | POST 요청에 지정된 일괄 처리의 ID입니다. |

레코드 데이터 집합 일괄 처리에 대한 삭제 요청을 시작하려고 하면 다음과 유사한 400 수준 오류가 발생합니다.

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

상태와 같은 세부 사항을 포함하여 특정 삭제 요청을 보려면 종단점에 대한 조회(GET) 요청을 수행하고 `/system/jobs` 경로에 삭제 요청의 ID를 포함할 수 있습니다.

**API 형식**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 매개 변수 | 설명 |
|---|---|
| {DELETE_REQUEST_ID} | **(필수)** 보려는 삭제 요청의 ID입니다. |

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

응답은 업데이트된 상태를 포함하여 삭제 요청의 세부 정보를 제공합니다. 응답에 있는 삭제 요청의 ID는 요청 경로에서 전송된 ID와 일치해야 합니다.

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
| jobType | 만들어지는 작업의 유형입니다. 이 경우 항상 &quot;DELETE&quot;를 반환합니다. |
| status | 삭제 요청의 상태입니다. 가능한 값:&quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| 지표 | 처리된 레코드 수(&quot;recordsProcessed&quot;) 및 요청이 처리된 시간(초) 또는 요청이 완료하는 데 걸린 시간을 포함하는 배열(&quot;timeTakenInSec&quot;). |

삭제 요청 상태가 &quot;완료&quot;되면 데이터 액세스 API를 사용하여 삭제된 데이터에 액세스하려고 시도하여 데이터가 삭제되었음을 확인할 수 있습니다. 데이터 액세스 API를 사용하여 데이터 집합 및 배치에 액세스하는 방법에 대한 지침은 데이터 액세스 [설명서를](../../data-access/home.md)검토하십시오.

## 삭제 요청 제거

Experience Platform을 사용하면 이전 요청을 삭제할 수 있습니다. 이 작업은 삭제 작업이 완료되지 않았거나 처리 단계에 갇혀 있는지 등 여러 가지 이유로 유용할 수 있습니다. 삭제 요청을 제거하려면 종단점에 대한 DELETE 요청을 수행하고 요청 경로에 제거할 삭제 요청의 ID를 포함할 수 `/system/jobs` 있습니다.

**API 형식**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 매개 변수 | 설명 |
|---|---|
| {DELETE_REQUEST_ID} | 제거할 삭제 요청의 ID입니다. |

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

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. ID로 삭제 요청을 보기 위한 GET 요청을 수행하여 요청이 삭제되었는지 확인할 수 있습니다. 삭제 요청이 제거되었음을 나타내는 HTTP 상태 404(찾을 수 없음)를 반환해야 합니다.

## 다음 단계

이제 경험 플랫폼 내의 프로필 스토어에서 데이터 집합 및 배치를 삭제하는 것과 관련된 단계를 알고 있으므로 잘못 추가되었거나 조직에서 더 이상 필요하지 않은 데이터를 안전하게 삭제할 수 있습니다. 삭제 요청은 취소할 수 없으므로 지금 필요하지 않으며 나중에 필요하지 않을 것으로 확신하는 데이터만 삭제해야 합니다.

## 부록 {#appendix}

다음 정보는 프로필 저장소에서 데이터 집합을 삭제하는 작업에 부수적입니다.

### Experience Platform UI를 사용하여 데이터 세트 삭제

Experience Platform 사용자 인터페이스를 사용하여 Profile에 대해 활성화된 데이터 세트를 삭제하면 &quot;Experience Data Lake에서 이 데이터 세트를 삭제하시겠습니까? &#39;프로필 시스템 작업&#39; API를 사용하여 프로필 서비스에서 이 데이터 집합을 삭제합니다.&quot;

UI **에서** 삭제를 클릭하면 데이터 세트에 대한 인제스트 기능이 비활성화되지만, DOES는 백엔드의 데이터 세트를 자동으로 삭제하지 않습니다. 데이터 집합을 영구적으로 삭제하려면 삭제 요청을 [만들기 위한 이 안내서의 단계를 사용하여 삭제 요청을](#create-a-delete-request)수동으로 만들어야 합니다.

다음 이미지는 UI를 사용하여 프로필 사용 데이터 세트를 삭제하려고 할 때의 경고를 보여줍니다.

![](../images/delete-profile-dataset.png)

데이터 집합 작업에 대한 자세한 내용은 [데이터 집합 개요를](../../catalog/datasets/overview.md)읽으십시오.