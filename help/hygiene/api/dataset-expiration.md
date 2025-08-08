---
title: 데이터 세트 만료 API 끝점
description: 데이터 위생 API의 /ttl 끝점을 사용하면 Adobe Experience Platform에서 데이터 세트 만료를 프로그래밍 방식으로 예약할 수 있습니다.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# 데이터 세트 만료 끝점

Adobe Experience Platform의 데이터 세트를 삭제해야 하는 시기를 예약하려면 데이터 위생 API의 `/ttl` 끝점을 사용하십시오.

데이터 세트 만료는 지연된 삭제 작업입니다. 데이터 세트는 중간에 보호되지 않으며 예약된 만료 전에 다른 방법으로 삭제될 수 있습니다.

>[!NOTE]
>
>만료가 특정 순시로 적시되어 있지만 실제 삭제가 시작되기 전에 만료 후 최대 24시간의 지연이 있을 수 있습니다. 삭제가 시작되면 Experience Platform 시스템에서 데이터 세트의 모든 추적이 제거되기까지 최대 7일이 걸릴 수 있습니다.

삭제가 시작되기 전에 만료를 취소하거나 예약 시간을 변경할 수 있습니다. 취소된 만료를 다시 열려면 새 만료를 설정하십시오.

삭제가 시작되면 만료 작업이 `executing`(으)로 표시되어 더 이상 수정할 수 없습니다. 데이터 세트는 최대 7일 동안 복구할 수 있지만 수동 Adobe 서비스 요청을 통해서만 복구할 수 있습니다. 삭제하는 동안 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각각 데이터 세트 콘텐츠를 개별적으로 제거합니다. 삭제가 완료되면 만료는 `completed`(으)로 표시됩니다.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트로 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

Advanced Data Lifecycle Management는 데이터 집합 만료 끝점을 통해 데이터 집합 삭제를 지원하고 [작업 주문 끝점](./workorder.md)을 통해 기본 ID를 사용하여 ID 삭제(행 수준 데이터)를 지원합니다. Experience Platform UI를 통해 [데이터 세트 만료](../ui/dataset-expiration.md) 및 [레코드 삭제](../ui/record-delete.md)을 관리할 수도 있습니다. 자세한 내용은 연결된 설명서 를 참조하십시오.

>[!NOTE]
>
>데이터 수명 주기는 일괄 삭제를 지원하지 않습니다.

## 시작

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [API 안내서](./overview.md)에서 CRUD 작업에 필요한 헤더, 오류 메시지, Postman 컬렉션 및 샘플 API 호출 읽기 방법에 대한 정보를 검토하십시오.

>[!IMPORTANT]
>
>데이터 위생 API를 호출할 때는 -H `x-sandbox-name: {SANDBOX_NAME}` 헤더를 사용해야 합니다.

## 데이터 세트 만료 나열 {#list}

`/ttl` 끝점에 대한 GET 요청을 수행하여 조직에 대해 구성된 모든 데이터 세트 만료를 나열할 수 있습니다.

쿼리 매개 변수를 사용하여 결과를 필터링하여 기준에 맞는 만료만을 반환합니다. 각 결과에는 각 데이터 세트 만료에 대한 상태 및 구성 세부 정보가 포함됩니다.

**API 형식**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMETERS}` | `&`자로 구분된 여러 매개 변수가 있는 선택적 쿼리 매개 변수 목록입니다. 일반적인 매개 변수에는 페이지 매김을 위해 `limit` 및 `page`이(가) 포함됩니다. 지원되는 쿼리 매개 변수의 전체 목록을 보려면 [부록 섹션](#query-params)에서 지원되는 쿼리 매개 변수의 전체 목록을 참조하십시오. 가장 일반적으로 사용되는 모수는 아래 부록뿐만 아니라 다음과 같다. |
| `author` | 데이터 세트 만료를 가장 최근에 업데이트하거나 만든 사용자별로 필터링합니다. SQL 유사 패턴을 지원합니다(예: `LIKE %john%`). |
| `datasetId` | 특정 데이터 세트 ID별로 만료를 필터링합니다. |
| `datasetName` | 데이터 세트 이름에 대한 대/소문자를 구분하지 않는 필터가 일치합니다. |
| `status` | 쉼표로 구분된 상태 목록으로 필터링합니다. `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | 특정 만료 날짜가 있는 만료를 필터링합니다. |
| `limit` | 반환할 최대 결과 수(1-100, 기본값: 25)를 규정합니다. |
| `page` | 인덱스(기본값: 50, 최대: 100)를 기반으로 하여 페이지 매김된 결과. |

{style="table-layout:auto"}

**요청**

다음 요청은 2021년 8월 1일 이전에 업데이트되고, 이름이 &quot;Jane Doe&quot;와 일치하는 사용자가 마지막으로 업데이트한 모든 데이터 세트 만료를 검색합니다.

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 속성 | 설명 |
| --- | --- |
| `results` | 데이터 세트 만료 구성의 배열입니다. |
| `ttlId` | 데이터 세트 만료 구성에 대한 고유 식별자입니다. |
| `datasetId` | 해당 구성과 연계된 데이터 세트에 대한 고유 식별자. |
| `datasetName` | 데이터 세트의 이름입니다. |
| `sandboxName` | 이 데이터 세트 만료가 구성된 샌드박스 입니다. |
| `displayName` | 사람이 인식할 수 있는 만료 구성 이름. |
| `description` | 만료 구성에 대한 설명입니다. |
| `imsOrg` | 고유한 조직 식별자. |
| `status` | 현재 만료 상태입니다. `pending`, `executing`, `cancelled`, `completed` 중 하나. |
| `expiry` | 예약된 만료 날짜 및 시간(ISO 8601 형식). |
| `updatedAt` | 이 구성에 대한 마지막 업데이트의 타임스탬프입니다. |
| `updatedBy` | 구성을 마지막으로 업데이트한 사용자 또는 서비스의 식별자 및 이메일입니다. |
| `current_page` | 현재 결과 페이지의 색인(0부터 시작). |
| `total_pages` | 사용 가능한 총 결과 페이지 수입니다. |
| `total_count` | 반환된 총 데이터 세트 만료 구성 레코드 수입니다. |

{style="table-layout:auto"}

## 데이터 세트 만료 조회 {#lookup}

데이터 세트 만료 ID 또는 데이터 세트 ID를 경로 매개 변수로 사용하여 GET 요청을 수행함으로써 특정 데이터 세트 만료 구성에 대한 세부 정보를 검색합니다.

>[!IMPORTANT]
>
>데이터 세트 만료 ID(예: `SD-xxxxxx-xxxx`) 또는 경로에 데이터 세트 ID를 제공할 수 있습니다. 응답의 `ttlId`은(는) 데이터 집합 만료에 대한 고유 식별자입니다.

**API 형식**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| 매개변수 | 설명 |
| --- | --- |
| `{ID}` | 데이터 세트 만료 구성에 대한 고유 식별자입니다. 데이터 세트 만료 ID 또는 데이터 세트 ID를 제공할 수 있습니다. |
| `include` | (선택 사항) `history`(으)로 설정된 경우 응답에 구성에 대한 변경 이벤트가 있는 `history` 배열이 포함됩니다. |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 데이터 세트 만료 구성에 대한 고유 식별자입니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. |
| `datasetName` | 데이터 세트의 이름입니다. |
| `sandboxName` | 데이터 세트 만료가 구성된 샌드박스. |
| `displayName` | 사람이 인식할 수 있는 데이터 세트 만료 구성 이름. |
| `description` | 데이터 세트 만료 구성에 대한 설명입니다. |
| `imsOrg` | 이 구성과 연계된 고유 조직 식별자. |
| `status` | 데이터 세트 만료 구성의 현재 상태입니다.<br>하나: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | 데이터 세트에 대해 예약된 만료 타임스탬프(ISO 8601 형식)입니다. |
| `updatedAt` | 최신 업데이트에 대한 타임스탬프입니다. |
| `updatedBy` | 데이터 세트 만료를 마지막으로 업데이트한 사용자 또는 서비스의 식별자 및 이메일입니다. |

{style="table-layout:auto"}

### 카탈로그 만료 태그

[카탈로그 API](../../catalog/api/getting-started.md)를 사용하여 데이터 세트 세부 정보를 조회할 때 데이터 세트에 활성 만료가 있는 경우 `tags.adobe/hygiene/ttl` 아래에 나열됩니다.

다음 JSON은 만료 값이 `32503680000000`인 데이터 집합에 대한 잘린 카탈로그 API 응답을 표시합니다. 태그는 Unix Epoch 이후 만료 시간을 밀리초 단위로 인코딩합니다.

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

데이터 세트가 만료되어 삭제할 수 있는 시기를 정의할 새 데이터 세트 만료 구성을 만듭니다.\
데이터 세트 ID, 만료 날짜 또는 날짜-시간(ISO 8601 형식), 표시 이름 및 설명(선택 사항)을 입력합니다.

>[!NOTE]
>
>만료 값은 날짜(YYYY-MM-DD) 또는 날짜 및 시간(YYYY-MM-DDTHH:MM:SSZ)일 수 있습니다. 날짜만 지정하면 시스템에서는 해당 날짜의 자정(UTC, 00:00:00Z)을 사용합니다. 만료는 24시간 이상이어야 합니다.

데이터 세트 만료를 만들려면 아래와 같이 POST 요청을 보냅니다.

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `datasetId` | **필수.** 만료를 적용할 데이터 세트의 고유 식별자입니다. |
| `expiry` | **필수.** ISO 8601 형식의 만료 날짜 및 시간입니다. 시스템 내 데이터의 수명을 정의합니다. 날짜만 제공되는 경우 기본값은 자정(UTC, 00:00:00Z)입니다. 만료 **은(는) 적어도 24시간 이후여야 합니다**. <br>**참고**:<ul><li>데이터 세트에 대한 데이터 세트 만료가 이미 존재하는 경우 요청이 실패합니다.</li></ul> |
| `displayName` | **필수.** 사람이 인식할 수 있는 데이터 집합 만료 구성 이름입니다. |
| `description` | 데이터 세트 만료 구성에 대한 선택적 설명입니다. |

**응답**

성공적인 응답은 HTTP 201(생성됨) 상태와 새 데이터 세트 만료 구성을 반환합니다.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 생성된 데이터 세트 만료 구성에 대한 고유 식별자입니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. |
| `datasetName` | 데이터 세트의 이름입니다. |
| `sandboxName` | 이 데이터 세트 만료가 구성된 샌드박스 입니다. |
| `displayName` | 데이터 세트 만료 구성의 표시 이름입니다. |
| `description` | 데이터 세트 만료 구성에 대한 설명입니다. |
| `imsOrg` | 이 구성과 연계된 고유 조직 식별자. |
| `status` | 데이터 세트 만료 구성의 현재 상태입니다.<br>하나: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | 데이터 세트에 대해 예약된 만료 타임스탬프입니다. |
| `updatedAt` | 가장 최근 업데이트에 대한 타임스탬프입니다. |
| `updatedBy` | 데이터 세트 만료 구성을 마지막으로 업데이트한 사용자 또는 서비스의 식별자 및 이메일입니다. |

데이터 세트에 대한 데이터 세트 만료가 이미 존재하는 경우 400(잘못된 요청) HTTP 상태가 발생합니다. 이러한 데이터 세트가 없거나 데이터 세트에 대한 액세스 권한이 없는 경우 404(찾을 수 없음) HTTP 상태가 발생합니다.

## 데이터 세트 만료 구성 업데이트 {#update}

기존 데이터 집합 만료 구성을 업데이트하려면 `/ttl/DATASET_EXPIRATION_ID`에 PUT 요청을 하십시오. 구성의 `displayName`, `description` 및 `expiry` 필드만 업데이트할 수 있습니다. 만료 상태가 `pending`인 경우에만 업데이트가 허용됩니다.

>[!NOTE]
>
>`expiry` 필드는 날짜(YYYY-MM-DD) 또는 날짜 및 시간(YYYY-MM-DDTHH:MM:SSZ)을 허용합니다. 날짜만 제공된 경우 시스템에서는 해당 날짜의 자정(UTC, 00:00:00Z)을 사용합니다. 만료 **은(는) 적어도 24시간 이후여야 합니다**.

**API 형식**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 데이터 세트 만료 구성에 대한 고유 식별자입니다. **참고**: 응답에서 이 항목을 `ttlId`(으)로 참조합니다. |

**요청**

다음 요청은 데이터 세트 만료 `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`에 대한 만료, 표시 이름 및 설명을 업데이트합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `displayName` | (선택 사항) 사람이 인식할 수 있는 데이터 세트 만료 구성의 새 이름입니다. |
| `description` | (선택 사항) 데이터 세트 만료 구성에 대한 새 설명입니다. |
| `expiry` | (선택 사항) ISO 8601 형식의 새 만료 날짜 또는 날짜 및 시간입니다. 날짜만 제공되는 경우 기본값은 자정(UTC)입니다. 만료 시간은 **적어도 24시간 이후여야 합니다**. |

>[!NOTE]
>
>이러한 필드 중 하나 이상을 요청에 제공해야 합니다.

**응답**

성공적인 응답은 HTTP 상태 200(OK)과 업데이트된 데이터 세트 만료 구성을 반환합니다.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 속성 | 설명 |
| --- | --- |
| `ttlId` | 업데이트된 데이터 세트 만료 구성에 대한 고유 식별자입니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. |
| `datasetName` | 데이터 세트의 이름입니다. |
| `sandboxName` | 이 데이터 세트 만료가 구성된 샌드박스 입니다. |
| `displayName` | 데이터 세트 만료 구성의 표시 이름입니다. |
| `description` | 데이터 세트 만료 구성에 대한 설명입니다. |
| `imsOrg` | 이 구성과 연결된 조직 ID입니다. |
| `status` | 데이터 세트 만료 구성의 현재 상태입니다.<br>하나: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | 데이터 세트에 대해 예약된 만료 타임스탬프입니다. |
| `updatedAt` | 가장 최근 업데이트에 대한 타임스탬프입니다. |
| `updatedBy` | 데이터 세트 만료 구성을 마지막으로 업데이트한 사용자 또는 서비스의 식별자 및 이메일입니다. |

{style="table-layout:auto"}

실패한 응답은 그러한 데이터 세트 만료가 존재하지 않는 경우 404(찾을 수 없음) HTTP 상태를 반환합니다.

## 데이터 세트 만료 취소 {#delete}

`/ttl/{ID}`에 DELETE을 요청하여 보류 중인 데이터 집합 만료 구성을 취소하십시오.

>[!NOTE]
>
>`pending` 상태의 데이터 세트 만료만 취소할 수 있습니다. 이미 `executing`, `completed` 또는 `cancelled`인 만료를 취소하려고 하면 HTTP 400(잘못된 요청)이 반환됩니다.

**API 형식**

```http
DELETE /ttl/{ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{ID}` | 데이터 세트 만료 구성에 대한 고유 식별자입니다. 데이터 세트 만료 ID 또는 데이터 세트 ID를 제공할 수 있습니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 ID가 `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`인 데이터 세트 만료를 취소합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 HTTP 상태 200(OK)과 취소된 데이터 세트 만료 구성을 반환합니다. 만료의 `status` 특성이 `cancelled`(으)로 설정되어 있지 않습니다.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| 속성 | 설명 |
|---|---|
| `ttlId` | 삭제된 데이터 세트 만료 구성에 대한 고유 식별자입니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. |
| `datasetName` | 데이터 세트의 이름입니다. |
| `sandboxName` | 이 데이터 세트 만료가 구성된 샌드박스 입니다. |
| `displayName` | 데이터 세트 만료 구성의 표시 이름입니다. |
| `description` | 데이터 세트 만료 구성에 대한 설명입니다. |
| `imsOrg` | 이 구성과 연계된 고유 조직 식별자. |
| `status` | 데이터 세트 만료 구성의 현재 상태입니다.<br>하나: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | 데이터 세트에 대해 예약된 만료 타임스탬프입니다. |
| `updatedAt` | 가장 최근 업데이트에 대한 타임스탬프입니다. |
| `updatedBy` | 데이터 세트 만료 구성을 마지막으로 업데이트한 사용자 또는 서비스의 식별자 및 이메일입니다. |

**예제 400(잘못된 요청) 응답**

`executing`, `completed` 또는 `cancelled` 만료 구성이 있는 데이터 집합을 취소하려고 하면 400 오류가 발생합니다.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>이미 `completed` 또는 `cancelled`인 데이터 집합 만료를 취소하려고 하면 404 오류가 발생합니다.

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

