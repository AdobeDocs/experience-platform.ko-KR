---
title: 작업 순서 API 끝점
description: 데이터 위생 API의 /workorder 종단점을 사용하면 소비자 ID에 대한 삭제 작업을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 4%

---

# 작업 순서 끝점

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 Healthcare Shield를 구입한 조직에서만 사용할 수 있습니다.

다음 `/workorder` data 위생 API의 종단점을 사용하면 Adobe Experience Platform에서 소비자 ID에 대한 삭제 작업을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## ID 삭제 {#delete-identities}

에 POST 요청을 수행하여 단일 데이터 세트 또는 모든 데이터 세트에서 하나 이상의 소비자 ID를 삭제할 수 있습니다 `/workorder` 엔드포인트.

**API 형식**

```http
POST /workorder
```

**요청**

의 값에 따라 `datasetId` 요청 페이로드에 제공된 API 호출은 모든 데이터 세트 또는 지정한 단일 데이터 세트에서 소비자 ID를 삭제합니다. 다음 요청은 특정 데이터 세트에서 3개의 소비자 ID를 삭제합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `action` | 수행할 작업입니다. 값은 로 설정해야 합니다. `delete_identity` ID를 삭제할 때 사용됩니다. |
| `datasetId` | 단일 데이터 세트에서 삭제하는 경우 이 값은 해당 데이터 세트의 ID여야 합니다. 모든 데이터 세트에서 삭제하는 경우 값을 로 설정합니다. `ALL`.<br><br>단일 데이터 세트를 지정하는 경우 데이터 세트의 연결된 XDM(Experience Data Model) 스키마에 기본 ID가 정의되어 있어야 합니다. |
| `identities` | 삭제할 정보가 있는 하나 이상의 사용자의 ID가 포함된 배열입니다. 각 ID는 [id 네임스페이스](../../identity-service/namespaces.md) 및 값:<ul><li>`namespace`: 단일 문자열 속성을 포함합니다. `code`: id 네임스페이스를 나타냅니다. </li><li>`id`: ID 값입니다.</ul>If `datasetId` 단일 데이터 세트를 지정합니다. 각 엔티티는 아래에 있습니다 `identities` 스키마의 기본 id와 동일한 id 네임스페이스를 사용해야 합니다.<br><br>If `datasetId` 가 로 설정되어 있습니다. `ALL`, `identities` 각 데이터 세트가 다를 수 있으므로 배열은 단일 네임스페이스로 제한되지 않습니다. 그러나 요청에 의해 보고된 대로 조직에서 사용할 수 있는 네임스페이스가 여전히 제한됩니다 [ID 서비스](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces?lang=ko). |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 ID 삭제의 세부 사항을 반환합니다.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 순서의 ID입니다. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직의 ID입니다. |
| `batchId` | 이 삭제 순서가 연결된 일괄 처리의 ID로서, 디버깅 목적으로 사용됩니다. 여러 삭제 주문은 다운스트림 서비스에서 처리할 일괄 처리에 함께 번들로 제공됩니다. |
| `bundleOrdinal` | 다운스트림 처리를 위해 일괄 처리로 번들로 제공되었을 때 이 삭제 순서가 수신된 순서입니다. 디버깅 목적에 사용됩니다. |
| `payloadByteSize` | 이 삭제 순서를 만든 요청 페이로드에서 제공된 ID 목록의 크기(바이트)입니다. |
| `operationCount` | 이 삭제 순서가 적용되는 ID 수입니다. |
| `createdAt` | 삭제 순서가 생성된 시간의 타임스탬프입니다. |
| `responseMessage` | 시스템에서 반환된 최신 응답입니다. 처리 중에 오류가 발생하면 이 값은 잘못된 상황을 이해하는 데 도움이 되는 자세한 오류 정보가 포함된 JSON 문자열이 됩니다. |
| `status` | 삭제 순서의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 생성한 사용자입니다. |

{style=&quot;table-layout:auto&quot;}

## 모든 ID 삭제 상태를 나열합니다 {#list}

GET 요청을 수행하여 모든 ID 삭제 상태를 나열할 수 있습니다.

**API 형식**

```http
GET /workorder?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMS}` | 목록 호출에 대한 선택적 쿼리 매개 변수의 목록이며 여러 매개 변수들이 `&` 자. 허용되는 쿼리 매개 변수는 다음과 같습니다.<ul><li>`data` - 로 설정된 경우 부울 값 `true`에는 삭제 순서에 대해 수신된 모든 추가 요청 및 응답 데이터가 포함됩니다. 기본값은 `false`입니다.</li><li>`start` - 삭제 주문을 검색할 시간표의 시작에 대한 타임스탬프입니다.</li><li>`end` - 삭제 주문을 검색할 일정 종료의 타임스탬프입니다.</li><li>`page` - 반환할 특정 응답 페이지입니다.</li><li>`limit` - 페이지당 표시할 레코드 수입니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 현재 상태를 포함하여 모든 삭제 작업의 세부 정보를 반환합니다. 아래 예제 응답은 스페이스에 대해 잘렸습니다.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `results` | 삭제 주문 목록과 세부 정보를 포함합니다. 삭제 순서의 속성에 대한 자세한 내용은 [삭제 순서 조회](#lookup). |
| `total` | 현재 필터를 기반으로 하여 발견된 총 삭제 주문 수입니다. |
| `count` | 응답의 각 페이지에서 발견된 총 삭제 주문 수입니다. |
| `_links` | 나머지 응답을 탐색하는 데 도움이 되는 페이지 매김 정보를 포함합니다.<ul><li>`next`: 응답에 다음 페이지의 URL을 포함합니다.</li><li>`page`: 응답의 다른 페이지에 액세스하거나 각 페이지에서 반환되는 항목 수를 조정하는 URL 템플릿을 포함합니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## ID 삭제 상태 검색(#lookup)

요청을 보낸 후 [id 삭제](#delete-identities)를 입력하면 GET 요청을 사용하여 해당 상태를 확인할 수 있습니다.

**API 형식**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 다음 `workorderId` 조회 중인 id 삭제 |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 현재 상태를 포함하여 삭제 작업의 세부 정보를 반환합니다.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 순서의 ID입니다. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직의 ID입니다. |
| `batchId` | 이 삭제 순서가 연결된 일괄 처리의 ID로서, 디버깅 목적으로 사용됩니다. 여러 삭제 주문은 다운스트림 서비스에서 처리할 일괄 처리에 함께 번들로 제공됩니다. |
| `bundleOrdinal` | 다운스트림 처리를 위해 일괄 처리로 번들로 제공되었을 때 이 삭제 순서가 수신된 순서입니다. 디버깅 목적에 사용됩니다. |
| `payloadByteSize` | 이 삭제 순서를 만든 요청 페이로드에서 제공된 ID 목록의 크기(바이트)입니다. |
| `operationCount` | 이 삭제 순서가 적용되는 ID 수입니다. |
| `createdAt` | 삭제 순서가 생성된 시간의 타임스탬프입니다. |
| `responseMessage` | 시스템에서 반환된 최신 응답입니다. 처리 중에 오류가 발생하면 이 값은 잘못된 상황을 이해하는 데 도움이 되는 자세한 오류 정보가 포함된 JSON 문자열이 됩니다. |
| `status` | 삭제 순서의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 생성한 사용자입니다. |
