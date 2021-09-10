---
description: 이 페이지에서는 '/authoring/destinations/publish' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 게시 대상 API 끝점 작업
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 4%

---

# 게시 대상 끝점 API 작업 {#publish-destination}

>[!IMPORTANT]
>
>**API 엔드포인트**:  `platform.adobe.io/data/core/activation/authoring/destinations/publish`

이 페이지에서는 `/authoring/destinations/publish` API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다.

다음과 같은 경우 게시 대상 API 엔드포인트를 사용하여 게시 요청을 제출합니다.
* 대상 SDK 파트너는 모든 Experience Platform 고객이 사용할 수 있도록 모든 Experience Platform 조직에서 프로덕션 대상을 사용할 수 있도록 만들어야 합니다.
* 모든 샌드박스에서 고유한 Experience Platform 조직에서 사용자 지정 대상을 사용할 수 있도록 하려는 경우.

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 필요한 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 게시할 대상 구성 제출 {#create}

`/authoring/destinations/publish` 종단점에 POST 요청을 만들어 게시할 대상 구성을 제출할 수 있습니다.

**API 형식**


```http
POST /authoring/destinations/publish
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 조직에서 게시할 대상을 제출합니다. 아래 페이로드에는 `/authoring/destinations/publish` 종단점에서 허용하는 모든 매개 변수가 포함되어 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시를 위해 제출하는 대상 구성의 대상 ID입니다. [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list)를 사용하여 대상 구성의 대상 ID를 가져옵니다. |
| `destinationAccess` | 문자열 | `ALL` 또는 `LIMITED`. 모든 Experience Platform 고객 또는 특정 조직에 대한 카탈로그에 대상을 표시할지 여부를 지정합니다. <br> **참고**: 를 사용하는  `LIMITED`경우 대상은 Experience Platform 조직에 대해서만 게시됩니다. 고객 테스트를 위해 대상을 Experience Platform 조직의 하위 세트에 게시하려면 Adobe 지원에 문의하십시오. |
| `allowedOrgs` | 문자열 | `"destinationAccess":"LIMITED"`을 사용하는 경우 대상을 사용할 Experience Platform 조직을 지정합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 대상 게시 요청의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

## 대상 게시 요청 나열 {#retrieve-list}

`/authoring/destinations/publish` 종단점에 GET 요청을 하여 IMS 조직에 게시하기 위해 제출된 모든 대상 목록을 검색할 수 있습니다.

**API 형식**


```http
GET /authoring/destinations/publish
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 게시용으로 제출된 대상 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID 및 샌드박스 이름을 기반으로 게시 권한이 있는 대상 목록과 함께 HTTP 상태 200을 반환합니다. 하나의 `configId` 은 하나의 대상에 대한 게시 요청에 해당합니다.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시용으로 제출한 대상 구성의 대상 ID입니다. |
| `publishDetailsList.configId` | 문자열 | 제출된 대상에 대한 대상 게시 요청의 고유 ID입니다. |
| `publishDetailsList.allowedOrgs` | 문자열 | 대상을 사용할 수 있어야 하는 Experience Platform 조직을 반환합니다. |
| `publishDetailsList.status` | 문자열 | 대상 게시 요청의 상태입니다. 가능한 값은 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`입니다. |
| `publishDetailsList.publishedDate` | 문자열 | epoch 시간에 게시에 대해 대상이 제출된 날짜입니다. |

{style=&quot;table-layout:auto&quot;}

## 기존 대상 게시 요청 업데이트 {#update}

`/authoring/destinations/publish` 종단점에 PUT 요청을 만들고 허용된 조직을 업데이트할 대상의 ID를 제공하여 기존 대상 게시 요청의 허용된 조직을 업데이트할 수 있습니다. 호출 본문에서 업데이트된 허용된 조직을 제공합니다.

**API 형식**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 게시 요청을 업데이트할 대상의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 게시 요청을 업데이트합니다. 아래 예제 호출에서 허용되는 조직을 업데이트할 예정입니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## 특정 대상 게시 요청의 상태 가져오기 {#get}

`/authoring/destinations/publish` 종단점에 GET 요청을 만들고 게시 상태를 검색할 대상의 ID를 제공하여 특정 대상 게시 요청에 대한 자세한 정보를 검색할 수 있습니다.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## API 오류 처리

대상 SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상에 대한 게시 요청을 제출하는 방법을 알 수 있습니다. Adobe Experience Platform 팀이 게시 요청을 검토하고 영업일 기준으로 5일이 경과하면 다시 연락을 드립니다.
