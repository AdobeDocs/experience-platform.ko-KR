---
title: 작업 순서 API 끝점
description: 데이터 위생 API의 /workorder 종단점을 사용하면 소비자 ID에 대한 삭제 작업을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: fb9d226a4ea2d23ccbf61416e275a0de5025554f
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 4%

---

# 작업 순서 끝점

>[!IMPORTANT]
>
>소비자 삭제 요청은 현재 Adobe Healthcare Shield 또는 Privacy Shield를 구입한 조직에만 사용할 수 있습니다.

다음 `/workorder` data 위생 API의 종단점을 사용하면 Adobe Experience Platform에서 소비자 삭제 요청을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 소비자 삭제 요청 만들기 {#delete-consumers}

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
        "displayName": "Example Consumer Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | 수행할 작업입니다. 값은 로 설정해야 합니다. `delete_identity` 소비자 삭제 |
| `datasetId` | 단일 데이터 세트에서 삭제하는 경우 이 값은 해당 데이터 세트의 ID여야 합니다. 모든 데이터 세트에서 삭제하는 경우 값을 로 설정합니다. `ALL`.<br><br>단일 데이터 세트를 지정하는 경우 데이터 세트의 연결된 XDM(Experience Data Model) 스키마에 기본 ID가 정의되어 있어야 합니다. |
| `displayName` | 소비자 삭제 요청의 표시 이름입니다. |
| `description` | 소비자 삭제 요청에 대한 설명입니다. |
| `identities` | 삭제할 정보가 있는 하나 이상의 사용자의 ID가 포함된 배열입니다. 각 ID는 [id 네임스페이스](../../identity-service/namespaces.md) 및 값:<ul><li>`namespace`: 단일 문자열 속성을 포함합니다. `code`: id 네임스페이스를 나타냅니다. </li><li>`id`: ID 값입니다.</ul>If `datasetId` 단일 데이터 세트를 지정합니다. 각 엔티티는 아래에 있습니다 `identities` 스키마의 기본 id와 동일한 id 네임스페이스를 사용해야 합니다.<br><br>If `datasetId` 가 로 설정되어 있습니다. `ALL`, `identities` 각 데이터 세트가 다를 수 있으므로 배열은 단일 네임스페이스로 제한되지 않습니다. 그러나 요청에 의해 보고된 대로 조직에서 사용할 수 있는 네임스페이스가 여전히 제한됩니다 [ID 서비스](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces?lang=ko). |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 소비자 삭제의 세부 사항을 반환합니다.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 순서의 ID입니다. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID로, 디버깅 용도로 사용됩니다. 여러 삭제 주문은 다운스트림 서비스에서 처리하기 위해 함께 번들로 제공됩니다. |
| `action` | 작업 순서에 의해 수행되는 작업입니다. 소비자 삭제의 경우 값은 다음과 같습니다 `identity-delete`. |
| `createdAt` | 삭제 순서가 생성된 시간의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `status` | 삭제 순서의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 생성한 사용자입니다. |
| `datasetId` | 요청을 받는 데이터 세트의 ID입니다. 요청이 모든 데이터 세트에 대해 인 경우 이 값은 로 설정됩니다 `ALL`. |

{style=&quot;table-layout:auto&quot;}

## 소비자 삭제 상태 검색(#lookup)

후 [소비자 삭제 요청 만들기](#delete-consumers)를 입력하면 GET 요청을 사용하여 해당 상태를 확인할 수 있습니다.

**API 형식**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 다음 `workorderId` 소비자 삭제 정보를 조회하고 있습니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 현재 상태를 포함하여 삭제 작업의 세부 정보를 반환합니다.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 순서의 ID입니다. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID로, 디버깅 용도로 사용됩니다. 여러 삭제 주문은 다운스트림 서비스에서 처리하기 위해 함께 번들로 제공됩니다. |
| `action` | 작업 순서에 의해 수행되는 작업입니다. 소비자 삭제의 경우 값은 다음과 같습니다 `identity-delete`. |
| `createdAt` | 삭제 순서가 생성된 시간의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `status` | 삭제 순서의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 생성한 사용자입니다. |
| `datasetId` | 요청을 받는 데이터 세트의 ID입니다. 요청이 모든 데이터 세트에 대해 인 경우 이 값은 로 설정됩니다 `ALL`. |
| `productStatusDetails` | 요청과 관련된 다운스트림 프로세스의 현재 상태를 나열하는 배열입니다. 각 배열 객체에는 다음 속성이 포함됩니다.<ul><li>`productName`: 다운스트림 서비스의 이름입니다.</li><li>`productStatus`: 다운스트림 서비스의 요청의 현재 처리 상태입니다.</li><li>`createdAt`: 서비스에서 가장 최근 상태를 게시한 시간의 타임스탬프입니다.</li></ul> |

## 소비자 삭제 요청 업데이트

을(를) 업데이트할 수 있습니다 `displayName` 및 `description` PUT 요청을 통해 소비자 삭제를 요청합니다.

**API 형식**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 다음 `workorderId` 소비자 삭제 정보를 조회하고 있습니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `displayName` | 소비자 삭제 요청에 대해 업데이트된 표시 이름입니다. |
| `description` | 소비자 삭제 요청에 대한 업데이트된 설명입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 소비자 삭제의 세부 사항을 반환합니다.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 순서의 ID입니다. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID로, 디버깅 용도로 사용됩니다. 여러 삭제 주문은 다운스트림 서비스에서 처리하기 위해 함께 번들로 제공됩니다. |
| `action` | 작업 순서에 의해 수행되는 작업입니다. 소비자 삭제의 경우 값은 다음과 같습니다 `identity-delete`. |
| `createdAt` | 삭제 순서가 생성된 시간의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `status` | 삭제 순서의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 생성한 사용자입니다. |
| `datasetId` | 요청을 받는 데이터 세트의 ID입니다. 요청이 모든 데이터 세트에 대해 인 경우 이 값은 로 설정됩니다 `ALL`. |
| `productStatusDetails` | 요청과 관련된 다운스트림 프로세스의 현재 상태를 나열하는 배열입니다. 각 배열 객체에는 다음 속성이 포함됩니다.<ul><li>`productName`: 다운스트림 서비스의 이름입니다.</li><li>`productStatus`: 다운스트림 서비스의 요청의 현재 처리 상태입니다.</li><li>`createdAt`: 서비스에서 가장 최근 상태를 게시한 시간의 타임스탬프입니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}
