---
title: 작업 주문 API 끝점
description: 데이터 위생 API의 /workorder 끝점을 사용하면 ID에 대한 삭제 작업을 프로그래밍 방식으로 관리할 수 있습니다.
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 1%

---

# 작업 주문 끝점 {#work-order-endpoint}

데이터 위생 API의 `/workorder` 끝점을 사용하면 Adobe Experience Platform에서 레코드 삭제 요청을 프로그래밍 방식으로 관리할 수 있습니다.

>[!IMPORTANT]
> 
>레코드 삭제 기능은 현재 Beta에 있으며 **제한된 릴리스**&#x200B;에서만 사용할 수 있습니다. 모든 고객이 이용할 수 있는 것은 아닙니다. 레코드 삭제 요청은 제한된 릴리스의 조직에만 사용할 수 있습니다.
>
>레코드 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정과 관련된 데이터 주체 권한 요청(준수)에 사용할 **not**&#x200B;입니다. 모든 규정 준수 사용 사례의 경우 대신 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)을(를) 사용하십시오.

## 시작하기

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md)에서 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 레코드 삭제 요청 만들기 {#create}

`/workorder` 끝점에 대한 POST 요청을 만들어 단일 데이터 세트 또는 모든 데이터 세트에서 하나 이상의 ID를 삭제할 수 있습니다.

>[!IMPORTANT]
> 
>매월 제출할 수 있는 총 고유 ID 레코드 삭제 횟수에는 제한이 있습니다. 이러한 제한은 라이선스 계약을 기반으로 합니다. Adobe Real-time Customer Data Platform 및 Adobe Journey Optimizer의 모든 에디션을 구입한 조직은 매월 최대 10만 건의 ID 레코드 삭제를 제출할 수 있습니다. **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;을(를) 구매한 조직은 매월 최대 60만 개의 ID 레코드 삭제를 제출할 수 있습니다.<br>UI를 통한 단일 [레코드 삭제 요청](../ui/record-delete.md)을 통해 한 번에 10,000개의 ID를 제출할 수 있습니다. 레코드를 삭제하는 API 메서드를 사용하면 100,000개의 ID를 한 번에 제출할 수 있습니다.<br>가능한 한 많은 ID를 요청당 ID 한도까지 제출하는 것이 좋습니다. 많은 양의 ID를 삭제하려는 경우 낮은 볼륨 또는 레코드당 하나의 ID 삭제 요청을 제출하지 않아야 합니다.

**API 형식**

```http
POST /workorder
```

>[!NOTE]
>
>데이터 라이프사이클 요청은 기본 ID 또는 ID 맵을 기준으로만 데이터 세트를 수정할 수 있습니다. 요청은 기본 ID를 지정하거나 ID 맵을 제공해야 합니다.

**요청**

요청 페이로드에 제공된 `datasetId`의 값에 따라 API 호출은 모든 데이터 세트 또는 지정한 단일 데이터 세트에서 ID를 삭제합니다. 다음 요청은 특정 데이터 세트에서 3개의 ID를 삭제합니다.

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
        "displayName": "Example Record Delete Request",
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
| `action` | 수행할 작업입니다. 레코드를 삭제하려면 값을 `delete_identity`(으)로 설정해야 합니다. |
| `datasetId` | 단일 데이터 세트에서 삭제하는 경우 이 값은 해당 데이터 세트의 ID여야 합니다. 모든 데이터 세트에서 삭제하는 경우 값을 `ALL`(으)로 설정하십시오.<br><br>단일 데이터 집합을 지정하는 경우 데이터 집합의 관련 XDM(Experience Data Model) 스키마에 기본 ID가 정의되어 있어야 합니다. 데이터 세트에 기본 ID가 없는 경우 데이터 라이프사이클 요청으로 수정하려면 데이터 세트에 ID 맵이 있어야 합니다.<br>ID 맵이 있으면 `identityMap`(이)라는 최상위 수준의 필드로 표시됩니다.<br>데이터 집합 행의 ID 맵에는 여러 ID가 있을 수 있지만, 한 ID만 기본으로 표시할 수 있습니다. `id`이(가) 기본 ID와 일치하도록 하려면 `"primary": true`을(를) 포함해야 합니다. |
| `displayName` | 레코드 삭제 요청에 대한 표시 이름입니다. |
| `description` | 레코드 삭제 요청에 대한 설명. |
| `identities` | 정보를 삭제하려는 하나 이상의 사용자 ID가 포함된 배열입니다. 각 ID는 [ID 네임스페이스](../../identity-service/features/namespaces.md) 및 값으로 구성됩니다.<ul><li>`namespace`: ID 네임스페이스를 나타내는 단일 문자열 속성 `code`을(를) 포함합니다. </li><li>`id`: ID 값입니다.</ul>`datasetId`에서 단일 데이터 집합을 지정하는 경우 `identities`의 각 엔터티는 스키마의 기본 ID와 동일한 ID 네임스페이스를 사용해야 합니다.<br><br>`datasetId`이(가) `ALL`(으)로 설정되어 있으면 각 데이터 세트가 다를 수 있으므로 `identities` 배열이 단일 네임스페이스로 제한되지 않습니다. 그러나 [ID 서비스](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)에서 보고한 대로 요청이 여전히 조직에서 사용할 수 있는 네임스페이스로 제한되어 있습니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 레코드 삭제에 대한 세부 정보를 반환합니다.

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
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 주문 ID. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID이며, 디버깅 목적으로 사용됩니다. 여러 삭제 주문이 함께 번들로 포함되어 다운스트림 서비스에서 처리됩니다. |
| `action` | 작업 주문에 의해 수행되는 작업입니다. 레코드 삭제의 경우 값은 `identity-delete`입니다. |
| `createdAt` | 삭제 순서가 생성된 시점의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `status` | 삭제 주문의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 만든 사용자입니다. |
| `datasetId` | 요청의 대상이 되는 데이터 세트의 ID입니다. 모든 데이터 세트에 대한 요청인 경우 값이 `ALL`(으)로 설정됩니다. |

{style="table-layout:auto"}

## 레코드 삭제 상태 검색 {#lookup}

[레코드 삭제 요청을 만들기](#create)한 후 GET 요청을 사용하여 레코드 상태를 확인할 수 있습니다.

**API 형식**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 조회 중인 레코드 삭제 `workorderId`입니다. |

{style="table-layout:auto"}

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
  "displayName": "Example Record Delete Request",
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
| `workorderId` | 삭제 주문 ID. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID이며, 디버깅 목적으로 사용됩니다. 여러 삭제 주문이 함께 번들로 포함되어 다운스트림 서비스에서 처리됩니다. |
| `action` | 작업 주문에 의해 수행되는 작업입니다. 레코드 삭제의 경우 값은 `identity-delete`입니다. |
| `createdAt` | 삭제 순서가 생성된 시점의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `status` | 삭제 주문의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 만든 사용자입니다. |
| `datasetId` | 요청의 대상이 되는 데이터 세트의 ID입니다. 모든 데이터 세트에 대한 요청인 경우 값이 `ALL`(으)로 설정됩니다. |
| `productStatusDetails` | 요청과 관련된 다운스트림 프로세스의 현재 상태를 나열하는 배열입니다. 각 배열 객체에는 다음 속성이 포함됩니다.<ul><li>`productName`: 다운스트림 서비스의 이름입니다.</li><li>`productStatus`: 다운스트림 서비스의 현재 요청 처리 상태입니다.</li><li>`createdAt`: 서비스에서 가장 최근 상태를 게시한 시점의 타임스탬프입니다.</li></ul> |

## 레코드 삭제 요청 업데이트

PUT 요청을 통해 레코드를 삭제할 `displayName` 및 `description`을(를) 업데이트할 수 있습니다.

**API 형식**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 조회 중인 레코드 삭제 `workorderId`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X PUT \
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
| `displayName` | 레코드 삭제 요청에 대해 업데이트된 표시 이름입니다. |
| `description` | 레코드 삭제 요청에 대한 업데이트된 설명. |

{style="table-layout:auto"}

**응답**

성공한 응답은 레코드 삭제에 대한 세부 정보를 반환합니다.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 삭제 주문 ID. 나중에 삭제 상태를 조회하는 데 사용할 수 있습니다. |
| `orgId` | 조직 ID입니다. |
| `bundleId` | 이 삭제 순서가 연결된 번들의 ID이며, 디버깅 목적으로 사용됩니다. 여러 삭제 주문이 함께 번들로 포함되어 다운스트림 서비스에서 처리됩니다. |
| `action` | 작업 주문에 의해 수행되는 작업입니다. 레코드 삭제의 경우 값은 `identity-delete`입니다. |
| `createdAt` | 삭제 순서가 생성된 시점의 타임스탬프입니다. |
| `updatedAt` | 삭제 순서가 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `status` | 삭제 주문의 현재 상태입니다. |
| `createdBy` | 삭제 순서를 만든 사용자입니다. |
| `datasetId` | 요청의 대상이 되는 데이터 세트의 ID입니다. 모든 데이터 세트에 대한 요청인 경우 값이 `ALL`(으)로 설정됩니다. |
| `productStatusDetails` | 요청과 관련된 다운스트림 프로세스의 현재 상태를 나열하는 배열입니다. 각 배열 객체에는 다음 속성이 포함됩니다.<ul><li>`productName`: 다운스트림 서비스의 이름입니다.</li><li>`productStatus`: 다운스트림 서비스의 현재 요청 처리 상태입니다.</li><li>`createdAt`: 서비스에서 가장 최근 상태를 게시한 시점의 타임스탬프입니다.</li></ul> |

{style="table-layout:auto"}
