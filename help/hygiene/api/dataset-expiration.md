---
title: 데이터 세트 만료 API 끝점
description: 데이터 위생 API의 /ttl 끝점을 사용하면 Adobe Experience Platform에서 데이터 세트 만료를 프로그래밍 방식으로 예약할 수 있습니다.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 2%

---

# 데이터 세트 만료 끝점

데이터 위생 API의 `/ttl` 끝점을 사용하면 Adobe Experience Platform의 데이터 세트에 대한 만료 날짜를 예약할 수 있습니다.

데이터 세트 만료는 시간이 지연된 삭제 작업일 뿐입니다. 데이터 세트는 중간에 보호되지 않으므로 만료에 도달하기 전에 다른 방법으로 삭제할 수 있습니다.

>[!NOTE]
>
>만료가 특정 순시로 적시되어 있지만 실제 삭제가 시작되기 전에 만료 후 최대 24시간의 지연이 있을 수 있습니다. 삭제가 시작되면 Experience Platform 시스템에서 데이터 세트의 모든 추적이 제거되기까지 최대 7일이 걸릴 수 있습니다.

데이터 세트 삭제가 실제로 시작되기 전에 언제든지 만료를 취소하거나 트리거 시간을 수정할 수 있습니다. 데이터 세트 만료를 취소한 후 새 만료를 설정하여 다시 열 수 있습니다.

데이터 세트 삭제가 시작되면 해당 만료 작업이 `executing`(으)로 표시되며 더 이상 변경되지 않을 수 있습니다. 데이터 세트 자체는 최대 7일 동안 복구할 수 있지만 Adobe 서비스 요청을 통해 시작된 수동 프로세스를 통해서만 가능합니다. 요청이 실행되면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각 서비스에서 데이터 세트의 콘텐츠를 제거하기 위한 별도의 프로세스를 시작합니다. 세 서비스 모두에서 데이터가 삭제되면 만료는 `completed`(으)로 표시됩니다.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트로 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

Advanced Data Lifecycle Management는 데이터 집합 만료 끝점을 통해 데이터 집합 삭제를 지원하고 [작업 주문 끝점](./workorder.md)을 통해 기본 ID를 사용하여 ID 삭제(행 수준 데이터)를 지원합니다. Experience Platform UI를 통해 [데이터 세트 만료](../ui/dataset-expiration.md) 및 [레코드 삭제](../ui/record-delete.md)을 관리할 수도 있습니다. 자세한 내용은 연결된 설명서 를 참조하십시오.

>[!NOTE]
>
>데이터 수명 주기는 일괄 삭제를 지원하지 않습니다.

## 시작하기

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [API 안내서](./overview.md)에서 CRUD 작업에 필요한 헤더, 오류 메시지, Postman 컬렉션 및 샘플 API 호출 읽기 방법에 대한 정보를 검토하십시오.

>[!IMPORTANT]
>
>데이터 위생 API를 호출할 때는 -H `x-sandbox-name: {SANDBOX_NAME}` 헤더를 사용해야 합니다.

## 데이터 세트 만료 나열 {#list}

GET 요청을 통해 조직의 모든 데이터 세트 만료를 나열할 수 있습니다. 쿼리 매개 변수를 사용하여 적절한 결과에 대한 응답을 필터링할 수 있습니다.

**API 형식**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETERS}` | `&`자로 구분된 여러 매개 변수가 있는 선택적 쿼리 매개 변수 목록입니다. 일반적인 매개 변수에는 페이지 매김을 위해 `limit` 및 `page`이(가) 포함됩니다. 지원되는 쿼리 매개 변수의 전체 목록을 보려면 [부록 섹션](#query-params)을 참조하세요. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 데이터 세트의 만료 결과가 표시됩니다. 다음 예제는 공백에 대해 잘렸습니다.

>[!IMPORTANT]
>
>응답의 `ttlId`은(는) `{DATASET_EXPIRATION_ID}`이라고도 합니다. 둘 다 데이터 세트 만료에 대한 고유 식별자를 참조합니다.

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
| `total_count` | 목록 호출의 매개 변수와 일치하는 데이터 세트 만료 수입니다. |
| `results` | 반환된 데이터 세트 만료에 대한 세부 정보를 포함합니다. 데이터 집합 만료의 속성에 대한 자세한 내용은 [조회 호출](#lookup)을 만드는 응답 섹션을 참조하십시오. |

{style="table-layout:auto"}

## 데이터 세트 만료 조회 {#lookup}

데이터 세트 만료를 조회하려면 `{DATASET_ID}` 또는 `{DATASET_EXPIRATION_ID}`(으)로 GET 요청을 만듭니다.

>[!IMPORTANT]
>
>`{DATASET_EXPIRATION_ID}`은(는) 응답에서 `ttlId`(으)로 참조됩니다. 둘 다 데이터 세트 만료에 대한 고유 식별자를 참조합니다.

**API 형식**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 조회할 만료에 해당하는 데이터 세트의 ID입니다. |
| `{DATASET_EXPIRATION_ID}` | 데이터 세트 만료 ID입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 데이터 집합 `62759f2ede9e601b63a2ee14`에 대한 만료 세부 정보를 찾습니다.

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

[카탈로그 API](../../catalog/api/getting-started.md)를 사용하여 데이터 세트 세부 정보를 조회할 때 데이터 세트에 활성 만료가 있는 경우 `tags.adobe/hygiene/ttl` 아래에 나열됩니다.

다음 JSON은 카탈로그에서 데이터 세트 세부 정보에 대한 잘린 응답을 나타내며 만료 값은 `32503680000000`입니다. 태그의 값은 Unix Epoch가 시작된 이후의 정수(밀리초)로 만료를 인코딩합니다.

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

## 데이터 세트 만료 만들기 {#create}

지정된 기간 후에 시스템에서 데이터가 제거되도록 하려면 데이터 세트 ID와 만료 날짜 및 시간을 ISO 8601 형식으로 제공하여 특정 데이터 세트에 대한 만료를 예약하십시오.

데이터 세트 만료를 만들려면 아래 표시된 대로 POST 요청을 수행하고 페이로드 내에 아래 언급된 값을 제공합니다.

>[!NOTE]
>
>404 오류가 발생하면 요청에 슬래시가 추가로 없는지 확인합니다. 뒤쪽 슬래시로 인해 POST 요청이 실패할 수 있습니다.

**API 형식**

```http
POST /ttl
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| 속성 | 설명 |
| --- | --- |
| `datasetId` | **필수** 만료를 예약하려는 대상 데이터 세트의 ID입니다. |
| `expiry` | **필수** ISO 8601 형식의 날짜 및 시간입니다. 문자열에 명시적 시간대 오프셋이 없으면 시간대는 UTC로 간주됩니다. 시스템 내의 데이터 수명은 제공된 만료 값에 따라 설정된다.<br>참고:<ul><li>데이터 세트에 대한 데이터 세트 만료가 이미 존재하는 경우 요청이 실패합니다.</li><li>이 날짜 및 시간은 **24시간 이상이어야 합니다**.</li></ul> |
| `displayName` | 데이터 세트 만료 요청에 대한 선택적 표시 이름입니다. |
| `description` | 만료 요청에 대한 선택적 설명. |

**응답**

성공적인 응답은 HTTP 201(생성됨) 상태와 데이터 세트 만료의 새 상태를 반환합니다.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
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

데이터 세트에 대한 데이터 세트 만료가 이미 존재하는 경우 400(잘못된 요청) HTTP 상태가 발생합니다. 실패한 응답은 그러한 데이터 세트 만료가 존재하지 않거나 데이터 세트에 대한 액세스 권한이 없는 경우 404(찾을 수 없음) HTTP 상태를 반환합니다.

## 데이터 세트 만료 업데이트 {#update}

데이터 집합에 대한 만료 날짜를 업데이트하려면 PUT 요청 및 `ttlId`을(를) 사용하십시오. `displayName`, `description` 및/또는 `expiry` 정보를 업데이트할 수 있습니다.

>[!NOTE]
>
>만료 날짜 및 시간을 변경할 경우 향후 최소 24시간 이상이어야 합니다. 이렇게 강제 지연된 경우 만료를 취소하거나 다시 예약할 수 있으며 실수로 데이터가 손실되는 것을 방지할 수 있습니다.

**API 형식**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 변경하려는 데이터 세트 만료의 ID입니다. 참고: 응답에서 이 이름을 `ttlId`이라고 합니다. |

**요청**

다음 요청은 데이터 세트 만료 `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f`을(를) 2024년 말(그리니치 표준시)에 발생하도록 예약합니다. 기존 데이터 세트 만료가 발견되면 해당 만료가 새 `expiry` 값으로 업데이트됩니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
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
| `expiry` | **필수** ISO 8601 형식의 날짜 및 시간입니다. 문자열에 명시적 시간대 오프셋이 없으면 시간대는 UTC로 간주됩니다. 시스템 내의 데이터 수명은 제공된 만료 값에 따라 설정된다. 동일한 데이터 세트의 이전 만료 타임스탬프는 사용자가 제공한 새 만료 값으로 대체됩니다. 이 날짜 및 시간은 **24시간 이상이어야 합니다**. |
| `displayName` | 만료 요청의 표시 이름입니다. |
| `description` | 만료 요청에 대한 선택적 설명. |

{style="table-layout:auto"}

**응답**

기존 만료가 업데이트된 경우 성공한 응답은 데이터 세트 만료의 새 상태와 HTTP 상태 200(OK)을 반환합니다.

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

실패한 응답은 그러한 데이터 세트 만료가 존재하지 않는 경우 404(찾을 수 없음) HTTP 상태를 반환합니다.

## 데이터 세트 만료 취소 {#delete}

DELETE 요청을 하여 데이터 세트 만료를 취소할 수 있습니다.

>[!NOTE]
>
>상태가 `pending`인 데이터 세트 만료만 취소할 수 있습니다. 실행되었거나 이미 취소된 만료를 취소하려고 하면 HTTP 404 오류가 반환됩니다.

**API 형식**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{EXPIRATION_ID}` | 취소할 데이터 세트 만료의 `ttlId`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 ID가 `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`인 데이터 세트 만료를 취소합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답이 HTTP 상태 204(콘텐츠 없음)를 반환하고 만료의 `status` 특성이 `cancelled`(으)로 설정되어 있습니다.

## 부록

### 수락된 쿼리 매개 변수 {#query-params}

다음 표에서는 [데이터 세트 만료를 나열](#list)할 때 사용할 수 있는 쿼리 매개 변수에 대해 설명합니다.

>[!NOTE]
>
>`description`, `displayName` 및 `datasetName` 매개 변수에는 모두 LIKE 값으로 검색하는 기능이 포함되어 있습니다. 즉, 문자열 &quot;Name1&quot;을 검색하여 &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot;라는 예약된 데이터 세트 만료를 찾을 수 있습니다.

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `author` | `author` 쿼리 매개 변수를 사용하여 데이터 세트 만료를 가장 최근에 업데이트한 사람을 찾으십시오. 생성 후 업데이트가 없는 경우 만료의 원래 생성자와 일치합니다. 이 매개 변수는 `created_by` 필드가 검색 문자열에 해당하는 만료와 일치합니다.<br>검색 문자열이 `LIKE` 또는 `NOT LIKE`(으)로 시작하는 경우 나머지는 SQL 검색 패턴으로 처리됩니다. 그렇지 않으면 전체 검색 문자열은 `created_by` 필드의 전체 내용과 정확히 일치해야 하는 리터럴 문자열로 처리됩니다. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | 특정 데이터 세트에 적용되는 만료와 일치합니다. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | 데이터 세트 이름에 제공된 검색 문자열이 포함된 만료와 일치합니다. 일치는 대/소문자를 구분하지 않습니다. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | 표시 이름에 제공된 검색 문자열이 포함된 만료와 일치합니다. 일치는 대/소문자를 구분하지 않습니다. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | 정확한 실행 날짜, 실행 종료 날짜 또는 실행 시작 날짜를 기준으로 결과를 필터링합니다. 특정 날짜, 특정 날짜 이전 또는 특정 날짜 이후에 작업 실행과 관련된 데이터 또는 레코드를 검색하는 데 사용됩니다. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | 지정된 날짜의 24시간 동안 발생한 만료와 일치합니다. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | 지정된 간격 동안 실행될 만료일 또는 이미 실행된 만료일과 일치합니다. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | 반환할 최대 만료 수를 나타내는 1에서 100 사이의 정수입니다. 기본값은 25입니다. | `limit=50` |
| `orderBy` | `orderBy` 쿼리 매개 변수는 API에서 반환된 결과의 정렬 순서를 지정합니다. 하나 이상의 필드를 기준으로 데이터를 오름차순(ASC) 또는 내림차순(DESC) 순서로 정렬하는 데 사용합니다. ASC, DESC를 각각 지정하려면 + 또는 - 접두사를 사용하십시오. 허용되는 값은 `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`입니다. | `-datasetName` |
| `orgId` | 조직 ID가 매개 변수의 ID와 일치하는 데이터 세트 만료와 일치합니다. 이 값은 기본적으로 `x-gw-ims-org-id` 헤더의 값으로 설정되며, 요청에서 서비스 토큰을 제공하지 않는 한 무시됩니다. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | 반환할 만료 페이지를 나타내는 정수입니다. | `page=3` |
| `sandboxName` | 샌드박스 이름이 인수와 정확히 일치하는 데이터 세트 만료와 일치 요청의 `x-sandbox-name` 헤더에 있는 샌드박스 이름으로 기본 설정됩니다. `sandboxName=*`을(를) 사용하여 모든 샌드박스에서 데이터 집합 만료를 포함하세요. | `sandboxName=dev1` |
| `search` | 지정된 문자열이 만료 ID와 정확히 일치하거나 다음 필드 중 하나에서 **포함됨**&#x200B;인 만료와 일치합니다.<br><ul><li>작성자</li><li>표시 이름</li><li>설명</li><li>표시 이름</li><li>데이터 세트 이름</li></ul> | `search=TESTING` |
| `status` | 쉼표로 구분된 상태 목록입니다. 포함된 경우 응답은 현재 상태가 나열된 데이터 세트 만료와 일치합니다. | `status=pending,cancelled` |
| `ttlId` | 만료 요청을 해당 ID와 일치시킵니다. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | 지정된 날짜의 24시간 창에서 업데이트된 만료와 일치합니다. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | 지정된 시간에 시작하여 24시간 창에서 업데이트된 만료와 일치합니다.<br><br>만료를 만들거나 취소하거나 실행할 때를 포함하여 모든 편집 시 만료를 업데이트한 것으로 간주합니다. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

