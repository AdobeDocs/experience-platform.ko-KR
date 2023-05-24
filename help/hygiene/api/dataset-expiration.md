---
title: 데이터 세트 만료 API 끝점
description: 데이터 위생 API의 /ttl 끝점을 사용하면 Adobe Experience Platform에서 데이터 세트 만료를 프로그래밍 방식으로 예약할 수 있습니다.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 2%

---

# 데이터 세트 만료 끝점

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 구입한 조직에서만 사용할 수 있습니다 **Adobe 헬스케어 실드** 또는 **Adobe 개인정보 보호 및 보안 실드**.

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

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 다음을 검토하십시오. [개요](./overview.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 데이터 세트 만료 나열 {#list}

GET 요청을 통해 조직의 모든 데이터 세트 만료를 나열할 수 있습니다.

**API 형식**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 여러 매개 변수가 로 구분된 선택적 쿼리 매개 변수 목록 `&` 자. 일반적인 매개 변수는 다음과 같습니다. `size` 및 `page` 페이지 매김 목적으로 지원되는 쿼리 매개 변수의 전체 목록은 다음을 참조하십시오. [부록 섹션](#query-params). |

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
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `totalRecords` | 목록 호출의 매개 변수와 일치하는 데이터 세트 만료 수입니다. |
| `ttlDetails` | 반환된 데이터 세트 만료에 대한 세부 정보를 포함합니다. 데이터 세트 만료의 속성에 대한 자세한 내용은 만들기 응답 섹션을 참조하십시오. [조회 호출](#lookup). |

{style="table-layout:auto"}

## 데이터 세트 만료 조회 {#lookup}

GET 요청을 통해 데이터 세트 만료를 조회할 수 있습니다.

**API 형식**

```http
GET /ttl/{DATASET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 조회할 만료에 해당하는 데이터 세트의 ID입니다. |

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

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 데이터 세트 만료 ID입니다. |
| `datasetId` | 이 만료가 적용되는 데이터 세트의 ID입니다. |
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

PUT 요청을 통해 데이터 세트의 만료 날짜를 만들거나 업데이트할 수 있습니다.

**API 형식**

```http
PUT /ttl/{DATASET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 만료를 예약하려는 데이터 세트의 ID입니다. |

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
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `expiry` | 데이터 세트가 삭제되는 시점을 위한 ISO 8601 타임스탬프. |
| `displayName` | 만료 요청의 표시 이름입니다. |
| `description` | 만료 요청에 대한 선택적 설명. |

{style="table-layout:auto"}

**응답**

성공한 응답은 데이터 세트 만료의 세부 정보를 반환하며, 기존 만료가 업데이트된 경우에는 HTTP 상태 200(OK)으로, 기존 만료가 없는 경우에는 201(Created)로 반환합니다.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 데이터 세트 만료 ID입니다. |
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
| `{EXPIRATION_ID}` | 다음 `workorderId` / 취소하려는 데이터 세트 만료. |

{style="table-layout:auto"}

**요청**

다음 요청은 ID가 있는 데이터 세트 만료를 취소합니다 `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 만료를 반환합니다. `status` 속성이 로 설정되어 있습니다. `cancelled`.

## 데이터 세트의 만료 상태 내역 검색

쿼리 매개 변수를 사용하여 특정 데이터 세트의 만료 상태 기록을 조회할 수 있습니다 `include=history` 조회 요청에서. 결과에는 데이터 세트 만료, 적용된 모든 업데이트 및 해당 취소 또는 실행(해당되는 경우)에 대한 정보가 포함됩니다.

**API 형식**

```http
GET /ttl/{DATASET_ID}?include=history
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 만료 내역을 조회할 데이터 세트의 ID입니다. |

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
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
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
| `workorderId` | 데이터 세트 만료 ID입니다. |
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

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `size` | 반환할 최대 만료 수를 나타내는 1에서 100 사이의 정수입니다. 기본값은 25입니다. | `size=50` |
| `page` | 반환할 만료 페이지를 나타내는 정수입니다. | `page=3` |
| `orgId` | 조직 ID가 매개 변수의 ID와 일치하는 데이터 세트 만료와 일치합니다. 이 값의 기본값은 `x-gw-ims-org-id` 헤더와 는 요청이 서비스 토큰을 제공하지 않는 한 무시됩니다. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | 쉼표로 구분된 상태 목록입니다. 포함된 경우 응답은 현재 상태가 나열된 데이터 세트 만료와 일치합니다. | `status=pending,cancelled` |
| `author` | 만료 대상 `created_by` 는 검색 문자열과 일치합니다. 검색 문자열이 다음으로 시작되는 경우 `LIKE` 또는 `NOT LIKE`나머지 부분은 SQL 검색 패턴으로 처리됩니다. 그렇지 않으면 전체 검색 문자열은 의 전체 컨텐츠와 정확히 일치해야 하는 리터럴 문자열로 처리됩니다. `created_by` 필드. | `author=LIKE %john%` |
| `sandboxName` | 샌드박스 이름이 인수와 정확히 일치하는 데이터 세트 만료와 일치 기본값은 요청의 샌드박스 이름으로 설정됩니다. `x-sandbox-name` 머리글입니다. 사용 `sandboxName=*` 모든 샌드박스에서 데이터 세트 만료를 포함합니다. | `sandboxName=dev1` |
| `datasetId` | 특정 데이터 세트에 적용되는 만료와 일치합니다. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | 지정된 시간에 시작하여 24시간 기간에 생성된 만료와 일치합니다.<br><br>시간 없이 날짜 (예: `2021-12-07`)는 해당 날짜의 시작 날짜/시간을 나타냅니다. 따라서 `createdDate=2021-12-07` 은(는) 의 2021년 12월 7일에 생성된 모든 만료를 나타냅니다. `00:00:00` 에서 `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | 표시된 시간 또는 그 이후에 생성된 만료와 일치합니다. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 표시된 시간 또는 그 전에 생성된 만료와 일치합니다. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 좋아요 `createdDate` / `createdFromDate` / `createdToDate`를 조정할 때 반드시 필요합니다. 하지만 은 생성 시간 대신 데이터 세트 만료의 업데이트 시간과 일치합니다.<br><br>만료는 작성, 취소 또는 실행 시기를 포함하여 모든 편집 시 업데이트된 것으로 간주됩니다. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 표시된 간격에서 언제든지 취소된 만료와 일치합니다. 이 설정은 만료가 나중에 다시 열린 경우에도 적용됩니다(동일한 데이터 세트에 대해 새 만료로 설정). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 지정된 간격 동안 완료된 만료와 일치합니다. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 지정된 간격 동안 실행될 만료일 또는 이미 실행된 만료일과 일치합니다. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
