---
title: 콘텐츠 API 엔드포인트
description: Privacy Service API를 사용하여 액세스 데이터를 검색하는 방법에 대해 알아봅니다.
role: Developer
badgePrivateBeta: label="비공개 베타" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 8bd4bd293b68d01e072c1c0a776080379692c5ee
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# 컨텐츠 엔드포인트

>[!IMPORTANT]
>
>다음 `/content` 엔드포인트가 현재 beta 상태이고 조직에서 아직 액세스하지 못할 수 있습니다. 기능 및 설명서는 변경될 수 있습니다.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

&#39;액세스 정보&#39;(개인 정보 주체가 액세스 권한을 요청할 수 있는 정보)를 검색할 때 향상된 보안을 사용합니다. 에 대한 응답에 제공된 다운로드 URL `/jobs/{JOB_ID}` 이제 GET 요청이 Adobe 서비스 엔드포인트를 가리킵니다. 그런 다음 GET 요청을 할 수 있습니다. `/jobs/:JOB_ID/content` 고객 데이터를 JSON 형식으로 반환합니다. 이 액세스 방법은 보안을 강화하기 위해 인증 및 액세스 제어의 여러 계층을 구현합니다.

이 안내서를 사용하기 전에 다음을 참조하십시오. [시작 안내서](./getting-started.md) 아래 예제 API 호출에 제공된 필수 인증 헤더에 대한 정보입니다.

>[!TIP]
>
>필요한 액세스 정보에 대한 작업 ID를 현재 모르는 경우 `/jobs`을 엔드포인트로 설정하고 추가 쿼리 매개 변수를 사용하여 결과를 필터링합니다. 사용 가능한 쿼리 매개 변수의 전체 목록은 [개인 정보 작업 끝점 안내서](./privacy-jobs.md).

## 개인 정보 작업 정보 검색

현재 처리 상태와 같은 특정 작업에 대한 정보를 검색하려면 해당 작업의 `jobId` 에 대한 GET 요청 경로 `/jobs` 엔드포인트.

**API 형식**

```http
GET /jobs/{JOB_ID}
```

**요청**

다음 요청은 다음과 같은 작업의 세부 정보를 검색합니다. `jobId` 은 요청 경로에 제공됩니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 지정된 작업의 세부 정보를 반환합니다.

>[!NOTE]
>
>개인 정보 보호 작업에는 `complete` 포함할 상태 `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| 속성 | 설명 |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | 개인 정보 작업에 대한 고유 식별자. |
| `requestId` | Privacy Service에 수행된 특정 요청에 대한 고유 식별자. |
| `userKey` | `userKey` 은(는) `key` 개인 정보 보호 요청을 제출할 때 제공한 값입니다. 다음 `key` 값은 사용자에게 적절한 데이터 주체의 식별자를 제공할 수 있는 기회입니다. 일반적으로 시스템은 해당 데이터 주체를 추적하기 위해 만든 고유 식별자입니다. 팁: 모든 활성 개인 정보 작업을 나열하고 비교할 수 있습니다 `key` 각 작업에 대해 지속 기간을 한 번의 방문으로 설정해야 합니다. |
| `action` | 요청한 작업 유형입니다. 허용되는 값은 다음과 같습니다 `access` 및 `delete`. |
| `status` | 개인 정보 작업의 현재 상태입니다. |
| `submittedBy` | 개인 정보 보호 작업을 제출한 사람의 이메일 주소입니다. |
| `createdDate` | 개인 정보 작업을 만든 날짜 및 시간입니다. |
| `lastModifiedDate` | 개인 정보 작업을 마지막으로 수정한 날짜 및 시간입니다. |
| `userIds` | 사용자 식별자 및 관련 정보가 포함된 배열입니다. |
| `userIds.namespace` | 사용자 식별자에 사용되는 네임스페이스. |
| `userIds.value` | 사용자 식별자의 실제 값. |
| `userIds.type` | 식별자 유형(예: `standard` 또는 `custom`). |
| `userIds.namespaceId` | 사용자 ID를 분류하고 관리하는 데 사용되는 네임스페이스의 식별자입니다. |
| `userIds.isDeletedClientSide` | 클라이언트 측에서 식별자가 삭제되었는지 여부를 나타내는 부울입니다. |
| `productResponses` | 개인 정보 작업과 관련된 다양한 제품 또는 서비스의 응답이 포함된 배열입니다. |
| `productResponses.product` | 데이터 주체의 정보를 얻는 데 사용한 제품 또는 서비스의 이름입니다. |
| `productResponses.retryCount` | 요청을 다시 시도한 횟수입니다. |
| `productResponses.processedDate` | 제품 응답이 처리된 날짜 및 시간입니다. |
| `productResponses.productStatusResponse` | 제품 응답의 상태를 포함하는 개체. |
| `productResponses.productStatusResponse.status` | 제품 응답의 상태입니다. |
| `downloadURL` | 이 속성은 작업을 완료한 후 60일 동안 호출할 수 있는 끝점을 제공합니다. 작업 상태는 다음과 같아야 합니다. `complete` 및 `action` 은(는) 다음과 같아야 합니다. `access`. 그렇지 않으면 이 필드가 없습니다. |
| `regulation` | 다음과 같은 개인 정보 보호 요청이 처리되는 규정 프레임워크 `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`등. |

{style="table-layout:auto"}

## 고객 액세스 정보 가져오기 {#retrieve-access-data}

데이터 주체의 쿼리에 대한 응답으로 생성되는 &#39;액세스 정보&#39;를 얻으려면 다음에 대한 GET 요청을 수행하십시오. `/jobs/{JOB_ID}/content` 엔드포인트. 응답은 데이터 주체의 데이터를 저장하는 각 제품에 대한 하위 폴더가 있는 폴더가 포함된 zip 파일(*.zip)입니다.

>[!TIP]
>
>이 요청을 수행하려면 특정 작업 ID가 필요합니다. GET 특정 작업 ID를 검색해야 하는 경우 먼저 `/jobs` 을 엔드포인트로 설정하고 추가 쿼리 매개 변수를 사용하여 결과를 필터링합니다. 허용된 쿼리 매개 변수를 포함한 자세한 정보는 [개인 정보 작업 끝점 안내서](./privacy-jobs.md).

**API 형식**

```http
GET /jobs/{JOB_ID}/content
```

**요청**

다음 요청은 요청에 입력한 작업 ID에 대한 &#39;액세스 정보&#39;를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**응답**

응답은 zip 파일(*.zip)입니다. 정보는 보장될 수 없지만 일반적으로 JSON 형식으로 반환됩니다. 추출된 데이터는 모든 형식으로 반환될 수 있습니다.

