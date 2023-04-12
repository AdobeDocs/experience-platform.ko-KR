---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;api 안내서;쿼리 서비스;쿼리 서비스 계정;계정
solution: Experience Platform
title: 계정 API 끝점
description: 영구적 을 위한 Query Service 계정을 만들 수 있습니다.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 4%

---

# 계정 끝점

Adobe Experience Platform 쿼리 서비스에서 계정은 외부 SQL 클라이언트와 함께 사용할 수 있는 만료되지 않은 자격 증명을 만드는 데 사용됩니다. 를 사용할 수 있습니다 `/accounts` query Service API의 끝점입니다. Query Service 통합 계정(기술 계정이라고도 함)을 프로그래밍 방식으로 생성, 검색, 편집 및 삭제할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 끝점은 Query Service API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 계정 만들기

에 POST 요청을 수행하여 Query Service 통합 계정을 만들 수 있습니다. `/accounts` 엔드포인트.

**API 형식**

```http
POST /accounts
```

**요청**

다음 요청은 조직에 대한 새 Query Service 통합 계정을 만듭니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `accountName` | **필수 여부** Query Service 통합 계정의 이름입니다. |
| `assignedToUser` | **필수 여부** Query Service 통합 계정이 만들어질 Adobe ID입니다. |
| `credential` | *(선택 사항)* Query Service 통합에 사용되는 자격 증명입니다. 지정하지 않으면 시스템에서 자동으로 자격 증명을 생성합니다. |
| `description` | *(선택 사항)* Query Service 통합 계정에 대한 설명입니다. |

**응답**

성공적인 응답은 새로 만든 Query Service 통합 계정의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 이러한 계정 세부 정보를 사용하여 Query Service를 외부 클라이언트와 연결할 수 있습니다.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `technicalAccountName` | Query Service 통합 계정의 이름입니다. |
| `technicalAccountId` | Query Service 통합 계정의 ID입니다. 이것은 `credential`을 입력하여 계정에 대한 암호를 작성합니다. |
| `credential` | Query Service 통합 계정의 자격 증명입니다. 이것은 `technicalAccountId`을 입력하여 계정에 대한 암호를 작성합니다. |

## 계정 업데이트

에 PUT 요청을 작성하여 Query Service 통합 계정을 업데이트할 수 있습니다. `/accounts` 엔드포인트.

**API 형식**

```http
POST /accounts/{ACCOUNT_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 업데이트할 Query Service 통합 계정의 ID입니다. |

**요청**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `accountName` | *(선택 사항)* Query Service 통합 계정의 업데이트된 이름입니다. |
| `assignedToUser` | *(선택 사항)* Query Service 통합 계정이 연결된 업데이트된 Adobe ID. |
| `credential` | *(선택 사항)* Query Service 계정에 대해 업데이트된 자격 증명입니다. |
| `description` | *(선택 사항)* Query Service 통합 계정에 대해 업데이트된 설명입니다. |

**응답**

성공적인 응답은 새로 업데이트된 Query Service 통합 계정에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## 모든 계정 나열

에 GET 요청을 수행하여 모든 Query Service 통합 계정 목록을 검색할 수 있습니다 `/accounts` 엔드포인트.

**API 형식**

```http
GET /accounts
```

**요청**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 모든 Query Service 통합 계정 목록과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## 계정 삭제

에 DELETE 요청을 작성하여 Query Service 통합 계정을 삭제할 수 있습니다. `/accounts` 엔드포인트.

**API 형식**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 삭제할 Query Service 통합 계정의 ID입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 계정이 성공적으로 삭제되었다는 메시지와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "result": "Success"
}
```
