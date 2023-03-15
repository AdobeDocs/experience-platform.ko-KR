---
description: 이 페이지에서는 "/authoring/destinations/publish" API 끝점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 게시 대상 API 엔드포인트 작업
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 1fb0fde2054528679235268ae96e3b7e78de80ef
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# 게시 대상 엔드포인트 API 작업 {#publish-destination}

>[!IMPORTANT]
>
>다른 Experience Platform 고객이 사용할 제품화된(공개) 대상을 제출하는 경우 이 API 끝점만 사용하면 됩니다. 직접 사용할 개인 대상을 만드는 경우 게시 API를 사용하여 대상을 공식적으로 제출할 필요가 없습니다.

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/destinations/publish` API 엔드포인트.

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다. 읽기 [Destination SDK에서 작성된 대상을 검토하기 위해 제출](./submit-destination.md) 다른 모든 단계는 대상 제출 프로세스의 일부로 수행해야 합니다.

다음과 같은 경우에 게시 요청을 제출하려면 게시 대상 API 엔드포인트를 사용합니다.

* Destination SDK 파트너로서 모든 Experience Platform 조직에서 모든 Experience Platform 고객이 사용할 수 있는 제품화된 대상을 만들고 싶을 수 있습니다.
* 다음을 수행합니다. *모든 업데이트* 을 참조하십시오. 구성 업데이트는 Experience Platform 팀이 승인하는 새 게시 요청을 제출한 후에만 대상에 반영됩니다.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 게시할 대상 구성 제출 {#create}

에 POST 요청을 하여 게시할 대상 구성을 제출할 수 있습니다. `/authoring/destinations/publish` 엔드포인트.

**API 형식**

```http
POST /authoring/destinations/publish
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 조직에 게시를 위한 대상을 제출합니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destinations/publish` 엔드포인트.

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
| `destinationId` | 문자열 | 게시를 위해 제출하는 대상 구성의 대상 ID입니다. 를 사용하여 대상 구성의 대상 ID 가져오기 [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | 문자열 | 사용 `ALL` 모든 Experience Platform 고객의 카탈로그에 대상이 표시됩니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 대상 게시 요청의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

## 대상 게시 요청 나열 {#retrieve-list}

에 GET 요청을 하여 IMS 조직에 게시하기 위해 제출된 모든 대상 목록을 검색할 수 있습니다. `/authoring/destinations/publish` 엔드포인트.

**API 형식**

```http
GET /authoring/destinations/publish
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 게시를 위해 제출된 대상 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID와 샌드박스 이름을 기반으로 액세스 권한이 있는 게시를 위해 제출된 대상 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `configId` 은 하나의 대상에 대한 게시 요청에 해당합니다.

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
| `destinationId` | 문자열 | 게시를 위해 제출한 대상 구성의 대상 ID. |
| `publishDetailsList.configId` | 문자열 | 제출된 대상에 대한 대상 게시 요청의 고유 ID. |
| `publishDetailsList.allowedOrgs` | 문자열 | 대상을 사용할 수 있는 Experience Platform 조직을 반환합니다. <br> <ul><li> 대상 `"destinationType": "PUBLIC"`, 이 매개 변수는 `"*"`즉, 모든 Experience Platform 조직에서 대상을 사용할 수 있습니다.</li><li> 대상 `"destinationType": "DEV"`, 이 매개 변수는 대상을 작성 및 테스트하는 데 사용한 조직의 조직 ID를 반환합니다.</li></ul> |
| `publishDetailsList.status` | 문자열 | 대상 게시 요청의 상태입니다. 가능한 값은 다음과 같습니다 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 값이 있는 대상 `PUBLISHED` 는 라이브이며 Experience Platform 고객이 사용할 수 있습니다. |
| `publishDetailsList.destinationType` | 문자열 | 대상의 유형입니다. 값은 다음과 같을 수 있습니다. `DEV` 및 `PUBLIC`. `DEV` 은 Experience Platform 조직의 대상에 해당합니다. `PUBLIC` 은 게시를 위해 제출한 대상에 해당합니다. Git 용어에서 다음 두 옵션을 생각해 보십시오. 여기서 `DEV` 버전은 로컬 작성 분기와 `PUBLIC` version 은 원격 주 분기를 나타냅니다. |
| `publishDetailsList.publishedDate` | 문자열 | 게시를 위해 대상이 제출된 날짜(시간 기준)입니다. |

{style="table-layout:auto"}

## 특정 대상 게시 요청의 상태 가져오기 {#get}

에 GET 요청을 하여 특정 대상 게시 요청에 대한 자세한 정보를 검색할 수 있습니다. `/authoring/destinations/publish` 끝점을 만들고 게시 상태를 검색할 대상의 ID를 제공합니다.

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

성공한 응답은 지정된 대상 게시 요청에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이제 이 문서를 읽고 대상에 대한 게시 요청을 제출하는 방법을 알 수 있습니다. Adobe Experience Platform 팀이 게시 요청을 검토하고 영업일 기준으로 5일 후에 다시 연락드리겠습니다.
