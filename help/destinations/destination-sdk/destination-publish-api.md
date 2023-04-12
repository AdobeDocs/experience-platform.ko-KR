---
description: 이 페이지에서는 '/authoring/destinations/publish' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 게시 대상 API 끝점 작업
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# 게시 대상 끝점 API 작업 {#publish-destination}

>[!IMPORTANT]
>
>다른 Experience Platform 고객이 사용할 제품(공개) 대상을 제출하는 경우에만 이 API 엔드포인트를 사용해야 합니다. 직접 사용할 비공개 대상을 만드는 경우 게시 API를 사용하여 대상을 공식적으로 제출할 필요가 없습니다.

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/destinations/publish` API 엔드포인트.

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다. 읽기 [Destination SDK에서 작성된 대상을 검토하도록 제출](./submit-destination.md) 기타 모든 단계에 대해 대상 제출 프로세스의 일부로 수행해야 합니다.

다음과 같은 경우 게시 대상 API 엔드포인트를 사용하여 게시 요청을 제출합니다.

* Destination SDK 파트너인 경우 모든 Experience Platform 고객이 사용할 수 있도록 모든 Experience Platform 조직에서 생산화된 대상을 사용할 수 있도록 하려고 합니다.
* 다음을 수행합니다. *모든 업데이트* 참조하십시오. 구성 업데이트는 Experience Platform 팀이 승인한 새 게시 요청을 제출한 후에만 대상에 반영됩니다.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 게시할 대상 구성 제출 {#create}

에 POST 요청을 만들어 게시할 대상 구성을 제출할 수 있습니다 `/authoring/destinations/publish` 엔드포인트.

**API 형식**

```http
POST /authoring/destinations/publish
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 조직에서 게시할 대상을 제출합니다. 아래 페이로드에는 `/authoring/destinations/publish` 엔드포인트.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시를 위해 제출하는 대상 구성의 대상 ID입니다. 를 사용하여 대상 구성의 대상 ID를 가져옵니다 [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | 문자열 | 사용 `ALL` 대상이 모든 Experience Platform 고객을 위한 카탈로그에 표시되도록 합니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 대상 게시 요청의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

## 대상 게시 요청 나열 {#retrieve-list}

에 GET 요청을 작성하여 조직에 게시하기 위해 제출된 모든 대상 목록을 검색할 수 있습니다 `/authoring/destinations/publish` 엔드포인트.

**API 형식**

```http
GET /authoring/destinations/publish
```

**요청**

다음 요청은 조직 및 샌드박스 구성에 따라 액세스 권한이 있는 게시용으로 제출된 대상 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답에서는 사용한 조직 ID 및 샌드박스 이름을 기반으로 게시 권한이 있는 대상 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `configId` 는 한 대상에 대한 게시 요청에 해당합니다.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시용으로 제출한 대상 구성의 대상 ID입니다. |
| `publishDetailsList.configId` | 문자열 | 제출된 대상에 대한 대상 게시 요청의 고유 ID입니다. |
| `publishDetailsList.allowedOrgs` | 문자열 | 대상을 사용할 수 있는 Experience Platform 조직을 반환합니다. <br> <ul><li> 대상 `"destinationType": "PUBLIC"`, 이 매개 변수는 `"*"`: 모든 Experience Platform 조직에서 대상을 사용할 수 있음을 의미합니다.</li><li> 대상 `"destinationType": "DEV"`, 이 매개 변수는 대상을 작성 및 테스트하는 데 사용한 조직의 조직 ID를 반환합니다.</li></ul> |
| `publishDetailsList.status` | 문자열 | 대상 게시 요청의 상태입니다. 가능한 값은 다음과 같습니다 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 값이 있는 대상 `PUBLISHED` 는 라이브이며 Experience Platform 고객이 사용할 수 있습니다. |
| `publishDetailsList.destinationType` | 문자열 | 대상의 유형입니다. 값은 `DEV` 및 `PUBLIC`. `DEV` 는 Experience Platform 조직의 대상에 해당합니다. `PUBLIC` 은 게시를 위해 제출한 대상에 해당합니다. 이 두 옵션을 다음과 같은 Git 용어로 생각해 보십시오. `DEV` 버전은 로컬 작성 분기와 를 나타냅니다 `PUBLIC` version 은 원격 주 분기를 나타냅니다. |
| `publishDetailsList.publishedDate` | 문자열 | epoch 시간에 게시에 대해 대상이 제출된 날짜입니다. |

{style="table-layout:auto"}

## 특정 대상 게시 요청의 상태 가져오기 {#get}

에 GET 요청을 수행하여 특정 대상 게시 요청에 대한 세부 정보를 검색할 수 있습니다 `/authoring/destinations/publish` 게시 상태를 검색할 대상의 ID를 제공하고 끝점입니다.

**API 형식**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 게시 상태를 검색할 대상의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 대상 게시 요청에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## API 오류 처리

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상에 대한 게시 요청을 제출하는 방법을 알 수 있습니다. Adobe Experience Platform 팀이 게시 요청을 검토하고 영업일 기준으로 5일이 경과하면 다시 연락을 드립니다.
