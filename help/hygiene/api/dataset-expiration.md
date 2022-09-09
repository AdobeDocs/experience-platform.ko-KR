---
title: 데이터 집합 만료 API 끝점
description: 데이터 위생 API의 /ttl 종단점을 사용하면 Adobe Experience Platform에서 데이터 세트 만료를 프로그래밍 방식으로 예약할 수 있습니다.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 6%

---

# 데이터 집합 만료 끝점

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 Healthcare Shield를 구입한 조직에서만 사용할 수 있습니다.

다음 `/ttl` data 위생 API의 종단점을 사용하면 Adobe Experience Platform의 데이터 세트에 대한 만료 날짜를 예약할 수 있습니다.

데이터 집합 만료는 시간 지연된 삭제 작업일 뿐입니다. 데이터 집합은 중간에 보호되지 않으므로 만료에 도달하기 전에 다른 방법으로 삭제할 수 있습니다.

>[!NOTE]
>
>만료는 특정 시간으로 지정되지만 실제 삭제를 시작하기 전에 만료 후 최대 24시간이 지연될 수 있습니다. 삭제가 시작되면 Platform 시스템에서 데이터 세트의 모든 추적이 제거되려면 최대 7일이 걸릴 수 있습니다.

데이터 세트 삭제가 실제로 시작되기 전에 언제든지 만료를 취소하거나 트리거 시간을 수정할 수 있습니다. 데이터 세트 만료를 취소한 후 새 만료를 설정하여 다시 열 수 있습니다.

데이터 집합 삭제가 시작되면 해당 만료 작업이 `executing`, 더 이상 변경되지 않을 수 있습니다. 데이터 세트 자체는 최대 7일 동안 복구할 수 있지만 Adobe 서비스 요청을 통해 시작된 수동 프로세스를 통해서만 복구할 수 있습니다. 요청이 실행되면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 개별 프로세스를 시작하여 해당 서비스에서 데이터 세트의 컨텐츠를 제거합니다. 세 서비스 모두에서 데이터가 삭제되면 만료는 로 표시됩니다 `executed`.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트에 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 데이터 집합 만료 목록 {#list}

GET 요청을 만들어 조직에 대한 모든 데이터 세트 만료를 나열할 수 있습니다.

**API 형식**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 여러 매개 변수를 로 구분하여 선택적 쿼리 매개 변수 목록입니다 `&` 자. 일반적인 매개 변수에는 다음이 포함됩니다 `size` 및 `page` 페이지를 매길 때 사용합니다. 지원되는 쿼리 매개 변수의 전체 목록은 [부록 섹션](#query-params). |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 결과 데이터 세트 만료가 나열됩니다. 다음 예제는 스페이스에 대해 잘렸습니다.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| 속성 | 설명 |
| --- | --- |
| `results` | 반환된 데이터 세트 만료에 대한 세부 정보를 포함합니다. 데이터 세트 만료 속성에 대한 자세한 내용은 응답 섹션을 참조하십시오 [조회 호출](#lookup). |
| `current_page` | 나열된 결과의 현재 페이지입니다. |
| `total_pages` | 응답의 총 페이지 수입니다. |
| `total_count` | 응답의 총 데이터 세트 만료 수입니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 만료 조회 {#lookup}

GET 요청을 통해 데이터 세트 만료를 조회할 수 있습니다.

**API 형식**

```http
GET /ttl/{TTL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TTL_ID}` | 조회할 데이터 세트 만료 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트 만료 세부 사항을 반환합니다.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료의 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `updatedBy` | 만료 기간을 마지막으로 업데이트한 사용자입니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 만료 만들기 {#create}

POST 요청을 통해 데이터 세트에 대한 만료 날짜를 만들 수 있습니다.

**API 형식**

```http
POST /ttl
```

**요청**

다음 요청은 데이터 집합을 예약합니다 `5b020a27e7040801dedbf46e` 2022년 말(그리니치 평균 시간) 삭제에 대한

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `datasetId` | 만료 날짜를 예약하려는 데이터 세트의 ID입니다. |
| `expiry` | 데이터 세트가 삭제될 시기에 대한 ISO 8601 타임스탬프. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 데이터 집합 만료의 세부 정보가 반환되고, 기존 만료가 업데이트된 경우 HTTP 상태 200(OK), 기존 만료가 없는 경우 201(생성됨)이 반환됩니다.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료의 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `updatedBy` | 만료 기간을 마지막으로 업데이트한 사용자입니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 만료 업데이트 {#update}

PUT 요청을 통해 데이터 세트 만료를 업데이트할 수 있습니다.

**API 형식**

```http
PUT /ttl/{TTL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TTL_ID}` | 수정할 데이터 세트 만료의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 데이터 세트에 대한 만료를 업데이트합니다 `5b020a27e7040801dedbf46e` 따라서 2023년 말(그리니치 표준시)에 만료됩니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `expiry` | 데이터 세트가 삭제될 시기에 대한 ISO 8601 타임스탬프. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 업데이트된 만료에 대한 세부 정보를 반환합니다.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료의 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `updatedBy` | 만료 기간을 마지막으로 업데이트한 사용자입니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 만료 취소 {#delete}

DELETE 요청을 만들어 데이터 세트 만료를 취소할 수 있습니다.

**API 형식**

```http
DELETE /ttl/{TTL_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TTL_ID}` | 취소할 데이터 세트 만료 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 데이터 세트에 대한 만료를 업데이트합니다 `5b020a27e7040801dedbf46e` 따라서 2023년 말(그리니치 표준시)에 만료됩니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트 만료 세부 사항을 반환하고 `status` 이제 속성이 `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료의 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `updatedBy` | 만료 기간을 마지막으로 업데이트한 사용자입니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 세트 만료 기록 검색

쿼리 매개 변수를 사용하여 특정 데이터 세트 만료 내역을 조회할 수 있습니다 `include=history` 조회 요청에서. 그 결과에는 데이터 세트 만료 작성, 적용된 모든 업데이트 및 취소 또는 실행(해당되는 경우)에 대한 정보가 포함됩니다.

**API 형식**

```http
GET /ttl/{TTL_ID}?include=history
```

| 매개 변수 | 설명 |
| --- | --- |
| `{TTL_ID}` | 조회하려는 기록 데이터 세트 만료의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트 만료 세부 사항을 반환하고 `history` 세부 정보를 제공하는 스토리지 `status`, `expiry`, `updatedAt`, 및 `updatedBy` 각 기록된 업데이트에 대한 속성입니다.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료의 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `history` | 만료에 대한 업데이트 기록을 객체 배열로서 나열하고 각 객체에는 `status`, `expiry`, `updatedAt`, 및 `updatedBy` 업데이트 시 만료에 대한 속성입니다. |

{style=&quot;table-layout:auto&quot;}

## 부록

### 허용된 쿼리 매개 변수 {#query-params}

다음 표에서는 사용 가능한 쿼리 매개 변수에 대해 설명합니다. [데이터 집합 만료 목록](#list):

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| `size` | 반환할 최대 만료 수를 나타내는 1과 100 사이의 정수입니다. 기본값은 25입니다. | `size=50` |
| `page` | 반환할 만료 페이지를 나타내는 정수입니다. | `page=3` |
| `status` | 쉼표로 구분된 상태 목록입니다. 포함된 경우 응답은 현재 상태가 나열된 데이터 세트 만료와 일치합니다. | `status=pending,cancelled` |
| `author` | 만료와 일치하는 값 `created_by` 은 검색 문자열과 일치합니다. 검색 문자열이 `LIKE` 또는 `NOT LIKE`을 지정하면 나머지 항목은 SQL 검색 패턴으로 처리됩니다. 그렇지 않으면 전체 검색 문자열이 페이지의 전체 콘텐츠와 정확히 일치해야 하는 리터럴 문자열로 처리됩니다 `created_by` 필드. | `author=LIKE %john%` |
| `createdDate` | 지정된 시간에 시작하여 24시간 창에 생성된 만료와 일치합니다.<br><br>시간이 없는 날짜(예: `2021-12-07`)은 해당 날짜의 시작 부분에 있는 날짜/시간을 나타냅니다. 따라서, `createdDate=2021-12-07` 은(는) 2021년 12월 7일에 만료로 설정됩니다. `00:00:00` through `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | 표시된 시간에 또는 이후에 생성된 만료와 일치합니다. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 표시된 시간에 또는 그 전에 생성된 만료와 일치합니다. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 좋아요 `createdDate` / `createdFromDate` / `createdToDate`하지만 은(는) 데이터 세트 만료 시간이 생성 시간이 아닌 업데이트 시간과 일치합니다.<br><br>만료 은 작성, 취소 또는 실행 시기를 포함하여 모든 편집 시 업데이트되는 것으로 간주됩니다. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 지정된 간격에서 언제든지 취소된 만료와 일치합니다. 만료가 나중에 다시 열렸더라도 적용됩니다(동일한 데이터 세트에 대한 새 만료 설정). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 지정된 간격 동안 완료된 만료와 일치합니다. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 지정된 간격 동안 실행해야 하거나 이미 실행된 만료와 일치합니다. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
