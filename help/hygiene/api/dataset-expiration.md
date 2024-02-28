---
title: 데이터 세트 만료 API 끝점
description: 데이터 위생 API의 /ttl 끝점을 사용하면 Adobe Experience Platform에서 데이터 세트 만료를 프로그래밍 방식으로 예약할 수 있습니다.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 2%

---

# 데이터 세트 만료 끝점

다음 `/ttl` 데이터 위생 API의 끝점을 사용하면 Adobe Experience Platform의 데이터 세트에 대한 만료 날짜를 예약할 수 있습니다.

데이터 세트 만료는 시간이 지연된 삭제 작업일 뿐입니다. 데이터 세트는 중간에 보호되지 않으므로 만료에 도달하기 전에 다른 방법으로 삭제할 수 있습니다.

>[!NOTE]
>
>만료가 특정 순시로 적시되어 있지만 실제 삭제가 시작되기 전에 만료 후 최대 24시간의 지연이 있을 수 있습니다. 삭제가 시작되면 플랫폼 시스템에서 데이터 세트의 모든 추적이 제거되기까지 최대 7일이 걸릴 수 있습니다.

데이터 세트 삭제가 실제로 시작되기 전에 언제든지 만료를 취소하거나 트리거 시간을 수정할 수 있습니다. 데이터 세트 만료를 취소한 후 새 만료를 설정하여 다시 열 수 있습니다.

데이터 세트 삭제가 시작되면 해당 만료 작업이 다음과 같이 표시됩니다. `executing`및 더 이상 변경되지 않을 수 있습니다. 데이터 세트 자체는 최대 7일 동안 복구할 수 있지만 Adobe 서비스 요청을 통해 시작된 수동 프로세스를 통해서만 가능합니다. 요청이 실행되면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각 서비스에서 데이터 세트의 콘텐츠를 제거하기 위한 별도의 프로세스를 시작합니다. 세 서비스 모두에서 데이터가 삭제되면 만료는 다음과 같이 표시됩니다. `executed`.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트로 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

## 시작하기

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 다음을 검토하십시오. [API 안내서](./overview.md) crud 작업의 필수 헤더, 오류 메시지, Postman 컬렉션 및 샘플 API 호출 읽기 방법에 대한 정보입니다.

>[!IMPORTANT]
>
>데이터 위생 API를 호출할 때 -H를 사용해야 합니다 `x-sandbox-name: {SANDBOX_NAME}` 머리글입니다.

## 데이터 세트 만료 나열 {#list}

GET 요청을 통해 조직의 모든 데이터 세트 만료를 나열할 수 있습니다. 쿼리 매개 변수를 사용하여 적절한 결과에 대한 응답을 필터링할 수 있습니다.

**API 형식**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 여러 매개 변수가 로 구분된 선택적 쿼리 매개 변수 목록 `&` 자. 일반적인 매개 변수는 다음과 같습니다. `limit` 및 `page` 페이지 매김 목적으로 지원되는 쿼리 매개 변수의 전체 목록은 다음을 참조하십시오. [부록 섹션](#query-params). |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 데이터 세트의 만료 결과가 표시됩니다. 다음 예제는 공백에 대해 잘렸습니다.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 속성 | 설명 |
| --- | --- |
| `totalRecords` | 목록 호출의 매개 변수와 일치하는 데이터 세트 만료 수입니다. |
| `ttlDetails` | 반환된 데이터 세트 만료에 대한 세부 정보를 포함합니다. 데이터 세트 만료의 속성에 대한 자세한 내용은 만들기 응답 섹션을 참조하십시오. [조회 호출](#lookup). |

{style="table-layout:auto"}

## 데이터 세트 만료 조회 {#lookup}

데이터 세트 만료를 조회하려면 다음 중 하나를 사용하여 GET 요청을 수행합니다. `datasetId` 또는 `ttlId`.

**API 형식**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 조회할 만료에 해당하는 데이터 세트의 ID입니다. |
| `{TTL_ID}` | 데이터 세트 만료 ID입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 데이터 세트에 대한 만료 세부 정보를 조회합니다 `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트 만료의 세부 정보를 반환합니다.

<!-- Is there a different response from making a GET request to either '/ttl/{DATASET_ID}?include=history' or '/ttl/{TTL_ID}'? If so please can you provide the response for both (or just the ttl endpoint itf it differs from teh example) -->

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `datasetName` | 이 만료가 적용되는 데이터 세트의 표시 이름입니다. |
| `sandboxName` | 대상 데이터 세트가 있는 샌드박스의 이름입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료를 마지막으로 업데이트한 시점의 타임스탬프입니다. |
| `updatedBy` | 만료를 마지막으로 업데이트한 사용자입니다. |
| `displayName` | 만료 요청의 표시 이름입니다. |
| `description` | 만료 요청에 대한 설명. |

{style="table-layout:auto"}

### 카탈로그 만료 태그

사용 시 [카탈로그 API](../../catalog/api/getting-started.md) 데이터 세트 세부 사항을 조회하려면 데이터 세트에 활성 만료가 있는 경우 아래에 나열됩니다. `tags.adobe/hygiene/ttl`.

다음 JSON은 카탈로그에서 데이터 세트 세부 정보에 대한 잘린 응답을 나타내며 만료 값은 입니다. `32503680000000`. 태그의 값은 Unix Epoch가 시작된 이후의 정수(밀리초)로 만료를 인코딩합니다.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## 데이터 세트 만료 만들기 또는 업데이트 {#create-or-update}

PUT 요청을 통해 데이터 세트에 대한 만료 날짜를 만들거나 업데이트합니다. PUT 요청은 다음 중 하나를 사용합니다. `datasetId` 또는 `ttlId`.

**API 형식**

```http
PUT /ttl/{DATASET_ID}
PUT /ttl/{TTL_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 만료를 예약하려는 데이터 세트의 ID입니다. |
| `{TTL_ID}` | 데이터 세트 만료 ID입니다. |

**요청**

다음 요청은 데이터 세트를 예약합니다 `5b020a27e7040801dedbf46e` 2022년 말(그리니치 표준시) 삭제. 데이터 세트에 대한 기존 만료가 없으면 새 만료가 만들어집니다. 데이터 세트에 이미 보류 중인 만료가 있는 경우 해당 만료는 새 만료로 업데이트됩니다 `expiry` 값.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `expiry` | ISO 8601 형식의 날짜 및 시간입니다. 문자열에 명시적 시간대 오프셋이 없으면 시간대는 UTC로 간주됩니다. 시스템 내의 데이터 수명은 제공된 만료 값에 따라 설정된다. 동일한 데이터 세트의 이전 만료 타임스탬프는 사용자가 제공한 새 만료 값으로 대체됩니다. |
| `displayName` | 만료 요청의 표시 이름입니다. |
| `description` | 만료 요청에 대한 선택적 설명. |

{style="table-layout:auto"}

**응답**

성공한 응답은 데이터 세트 만료의 세부 정보를 반환하며, 기존 만료가 업데이트된 경우에는 HTTP 상태 200(OK)으로, 기존 만료가 없는 경우에는 201(Created)로 반환합니다.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `imsOrg` | 조직의 ID입니다. |
| `status` | 데이터 세트 만료의 현재 상태입니다. |
| `expiry` | 데이터 세트를 삭제할 예약된 날짜 및 시간입니다. |
| `updatedAt` | 만료를 마지막으로 업데이트한 시점의 타임스탬프입니다. |
| `updatedBy` | 만료를 마지막으로 업데이트한 사용자입니다. |

{style="table-layout:auto"}

## 데이터 세트 만료 취소 {#delete}

DELETE 요청을 통해 데이터 세트 만료를 취소할 수 있습니다.

>[!NOTE]
>
>상태가 인 데이터 세트 만료만 `pending` 취소할 수 있습니다. 실행되었거나 이미 취소된 만료를 취소하려고 하면 HTTP 404 오류가 반환됩니다.

**API 형식**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{EXPIRATION_ID}` | 다음 `ttlId` / 취소하려는 데이터 세트 만료. |

{style="table-layout:auto"}

**요청**

다음 요청은 ID가 있는 데이터 세트 만료를 취소합니다 `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 만료를 반환합니다. `status` 속성이 로 설정되어 있습니다. `cancelled`.

## 데이터 세트의 만료 상태 내역 검색 {#retrieve-expiration-history}

쿼리 매개 변수를 사용하여 특정 데이터 세트의 만료 상태 기록을 조회할 수 있습니다 `include=history` 조회 요청에서. 결과에는 데이터 세트 만료, 적용된 모든 업데이트 및 해당 취소 또는 실행(해당되는 경우)에 대한 정보가 포함됩니다. 다음을 사용할 수도 있습니다 `ttlId` 데이터 세트 만료 기간.

**API 형식**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 만료 내역을 조회할 데이터 세트의 ID입니다. |
| `{TTL_ID}` | 데이터 세트 만료 ID입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트 만료의 세부 정보를 반환하며 `history` 세부 정보를 제공하는 배열 `status`, `expiry`, `updatedAt`, 및 `updatedBy` 기록된 각 업데이트에 대한 속성입니다.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
| `datasetName` | 이 만료가 적용되는 데이터 세트의 표시 이름입니다. |
| `sandboxName` | 대상 데이터 세트가 있는 샌드박스의 이름입니다. |
| `displayName` | 만료 요청의 표시 이름입니다. |
| `description` | 만료 요청에 대한 설명. |
| `imsOrg` | 조직의 ID입니다. |
| `history` | 만료 업데이트 기록을 개체 배열로 나열하며 각 개체에는 `status`, `expiry`, `updatedAt`, 및 `updatedBy` 업데이트 시 만료에 대한 속성입니다. |

{style="table-layout:auto"}

## 부록

### 수락된 쿼리 매개 변수 {#query-params}

다음 표에서는 사용 가능한 쿼리 매개 변수가 다음과 같은 경우 간략하게 설명합니다. [데이터 세트 만료 나열](#list):

>[!NOTE]
>
>다음 `description`, `displayName`, 및 `datasetName` 매개 변수에는 모두 LIKE 값으로 검색하는 기능이 포함되어 있습니다. 즉, 문자열 &quot;Name1&quot;을 검색하여 &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot;라는 예약된 데이터 세트 만료를 찾을 수 있습니다.

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `author` | 만료 대상 `created_by` 는 검색 문자열과 일치합니다. 검색 문자열이 다음으로 시작되는 경우 `LIKE` 또는 `NOT LIKE`나머지 부분은 SQL 검색 패턴으로 처리됩니다. 그렇지 않으면 전체 검색 문자열은 의 전체 컨텐츠와 정확히 일치해야 하는 리터럴 문자열로 처리됩니다. `created_by` 필드. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 표시된 간격에서 언제든지 취소된 만료와 일치합니다. 이 설정은 만료가 나중에 다시 열린 경우에도 적용됩니다(동일한 데이터 세트에 대해 새 만료로 설정). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 지정된 간격 동안 완료된 만료와 일치합니다. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | 지정된 시간에 시작하여 24시간 기간에 생성된 만료와 일치합니다.<br><br>시간 없이 날짜 (예: `2021-12-07`)는 해당 날짜의 시작 날짜/시간을 나타냅니다. 따라서 `createdDate=2021-12-07` 은(는) 의 2021년 12월 7일에 생성된 모든 만료를 나타냅니다. `00:00:00` 에서 `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | 표시된 시간 또는 그 이후에 생성된 만료와 일치합니다. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 표시된 시간 또는 그 전에 생성된 만료와 일치합니다. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | 특정 데이터 세트에 적용되는 만료와 일치합니다. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | 데이터 세트 이름에 제공된 검색 문자열이 포함된 만료와 일치합니다. 일치는 대/소문자를 구분하지 않습니다. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | 표시 이름에 제공된 검색 문자열이 포함된 만료와 일치합니다. 일치는 대/소문자를 구분하지 않습니다. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | 정확한 실행 날짜, 실행 종료 날짜 또는 실행 시작 날짜를 기준으로 결과를 필터링합니다. 특정 날짜, 특정 날짜 이전 또는 특정 날짜 이후에 작업 실행과 관련된 데이터 또는 레코드를 검색하는 데 사용됩니다. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 지정된 간격 동안 실행될 만료일 또는 이미 실행된 만료일과 일치합니다. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | 반환할 최대 만료 수를 나타내는 1에서 100 사이의 정수입니다. 기본값은 25입니다. | `limit=50` |
| `orderBy` | 다음 `orderBy` query 매개 변수는 API에서 반환되는 결과의 정렬 순서를 지정합니다. 하나 이상의 필드를 기준으로 데이터를 오름차순(ASC) 또는 내림차순(DESC) 순서로 정렬하는 데 사용합니다. ASC, DESC를 각각 지정하려면 + 또는 - 접두사를 사용하십시오. 다음 값이 허용됩니다. `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | 조직 ID가 매개 변수의 ID와 일치하는 데이터 세트 만료와 일치합니다. 이 값의 기본값은 `x-gw-ims-org-id` 헤더와 는 요청이 서비스 토큰을 제공하지 않는 한 무시됩니다. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | 반환할 만료 페이지를 나타내는 정수입니다. | `page=3` |
| `sandboxName` | 샌드박스 이름이 인수와 정확히 일치하는 데이터 세트 만료와 일치 기본값은 요청의 샌드박스 이름으로 설정됩니다. `x-sandbox-name` 머리글입니다. 사용 `sandboxName=*` 모든 샌드박스에서 데이터 세트 만료를 포함합니다. | `sandboxName=dev1` |
| `search` | 지정된 문자열이 만료 ID와 정확히 일치하는 만료 일치 또는 **포함됨** 다음 필드 중 하나에서:<br><ul><li>작성자</li><li>표시 이름</li><li>설명</li><li>표시 이름</li><li>데이터 세트 이름</li></ul> | `search=TESTING` |
| `status` | 쉼표로 구분된 상태 목록입니다. 포함된 경우 응답은 현재 상태가 나열된 데이터 세트 만료와 일치합니다. | `status=pending,cancelled` |
| `ttlId` | 만료 요청을 해당 ID와 일치시킵니다. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 좋아요 `createdDate` / `createdFromDate` / `createdToDate`를 조정할 때 반드시 필요합니다. 하지만 은 생성 시간 대신 데이터 세트 만료의 업데이트 시간과 일치합니다.<br><br>만료는 작성, 취소 또는 실행 시기를 포함하여 모든 편집 시 업데이트된 것으로 간주됩니다. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}
