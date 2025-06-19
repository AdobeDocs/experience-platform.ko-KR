---
title: 삭제 요청 기록(작업 주문 끝점)
description: 데이터 위생 API의 /workorder 끝점을 사용하면 ID에 대한 삭제 작업을 프로그래밍 방식으로 관리할 수 있습니다.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# 삭제 요청 기록(Workorder 끝점) {#work-order-endpoint}

데이터 위생 API의 `/workorder` 끝점을 사용하면 Adobe Experience Platform에서 레코드 삭제 요청을 프로그래밍 방식으로 관리할 수 있습니다.

>[!IMPORTANT]
> 
>레코드 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정과 관련된 데이터 주체 권한 요청(준수)에 사용할 **not**&#x200B;입니다. 모든 규정 준수 사용 사례의 경우 대신 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)을(를) 사용하십시오.

## 시작

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md)에서 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 할당량 및 처리 타임라인 {#quotas}

레코드 삭제 요청은 조직의 라이선스 자격에 따라 결정되는 일별 및 월별 식별자 제출 제한을 따릅니다. 이러한 제한은 UI 및 API 기반 삭제 요청 모두에 적용됩니다.

>[!NOTE]
>
>하루에 최대 **1,000,000개의 식별자를 제출할 수 있습니다**. 단, 남은 월별 할당량이 허용하는 경우에만 제출합니다. 월별 상한이 100만 개 미만인 경우 일일 제출액은 해당 상한을 초과할 수 없습니다.

### 제품별 월별 제출 권한 {#quota-limits}

아래 표에는 제품 및 자격 수준별 식별자 제출 제한이 나와 있습니다. 각 제품에 대해 월간 상한은 고정 식별자 천장이나 사용 허가된 데이터 볼륨에 연결된 백분율 기반 임계값의 두 값 중 적은 값입니다.

| 제품 | 권한 설명 | 월별 상한(둘 중 더 작은 값) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 식별자 2,000,000개 또는 대응 가능 대상의 5% |
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 식별자 15,000,000개 또는 대응 가능 대상의 10% |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 2,000,000개의 식별자 또는 100개의 식별자/백만 CJA 권한 행당 |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 15,000,000개의 식별자 또는 100만 개의 CJA 권한 행당 200개의 식별자 |

>[!NOTE]
>
> 대부분의 조직에서는 실제 대응 가능 대상 또는 CJA 행 권한에 따라 월별 제한이 내려집니다.

할당량은 매월 1일에 재설정됩니다. 사용되지 않은 할당량은 **이월되지 않습니다**.

>[!NOTE]
>
>할당량은 **제출된 식별자**&#x200B;에 대한 조직의 라이선스가 부여된 월별 권한을 기반으로 합니다. 이러한 기능은 시스템 가드레일에 의해 적용되지 않지만 모니터링 및 검토 할 수 있습니다.
>
>레코드 삭제는 **공유 서비스**&#x200B;입니다. 월간 캡은 Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics 및 적용 가능한 모든 Shield 추가 기능에 걸쳐 가장 높은 권한을 반영합니다.

### 식별자 제출을 위한 처리 타임라인 {#sla-processing-timelines}

제출 후 레코드 삭제 요청은 자격 수준에 따라 큐에 추가되고 처리됩니다.

| 제품 및 자격 설명 | 대기열 기간 | 최대 처리 시간(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 최대 15일 | 30일 |
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 일반적으로 24시간 | 15일 |

조직에서 더 높은 제한을 필요로 하는 경우 Adobe 담당자에게 권한 검토를 문의하십시오.

>[!TIP]
>
>현재 할당량 사용 또는 권한 계층을 확인하려면 [할당량 참조 안내서](../api/quota.md)를 참조하세요.

## 레코드 삭제 요청 만들기 {#create}

`/workorder` 끝점에 대한 POST 요청을 만들어 단일 데이터 세트 또는 모든 데이터 세트에서 하나 이상의 ID를 삭제할 수 있습니다.

>[!TIP]
>
>API를 통해 제출된 각 레코드 삭제 요청에는 최대 **100,000개의 ID**&#x200B;가 포함될 수 있습니다. 효율성을 극대화하려면 요청당 가능한 한 많은 ID를 제출하고 단일 ID 작업 주문과 같은 대량 제출을 피하십시오.

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
