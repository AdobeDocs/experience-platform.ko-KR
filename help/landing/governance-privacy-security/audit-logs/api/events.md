---
title: 감사 이벤트 API 끝점
description: 감사 쿼리 API를 사용하여 Experience Platform에서 감사 이벤트를 검색하는 방법에 대해 알아봅니다.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# 감사 이벤트 엔드포인트

감사 로그는 다양한 서비스 및 기능에 대한 사용자 활동의 세부 정보를 제공하는 데 사용됩니다. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다. [!DNL Audit Query] API의 `/audit/events` 끝점을 사용하면 [!DNL Platform]에서 조직의 활동에 대한 이벤트 데이터를 프로그래밍 방식으로 검색할 수 있습니다.

## 시작하기

이 가이드에 사용된 API 끝점은 [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 [!DNL Experience Platform] API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 감사 이벤트 나열

페이로드에서 검색할 이벤트를 지정하여 `/audit/events` 끝점에 대한 GET 요청을 수행하면 이벤트 데이터를 검색할 수 있습니다.

**API 형식**

```http
GET /audit/events
```

[!DNL Audit Query] API는 이벤트를 나열할 때 페이지 및 필터 결과를 쿼리 매개 변수로 사용할 수 있도록 지원합니다.

| 매개변수 | 설명 |
| --- | --- |
| `limit` | 응답에서 반환할 최대 레코드 수입니다. 기본 `limit`은(는) 50입니다. |
| `start` | 반환된 검색 결과의 첫 번째 항목에 대한 포인터입니다. 다음 결과 페이지에 액세스하려면 이 매개 변수는 제한으로 표시된 것과 동일한 양만큼 증가해야 합니다. 예: limit=50인 요청에 대한 다음 결과 페이지에 액세스하려면 매개 변수 start=50을 사용한 다음 그 다음 페이지에 대해 start=100을 사용하는 등의 작업을 수행합니다. |
| `queryId` | /audit/events 끝점에 쿼리할 때 응답에는 queryId 문자열 속성이 포함됩니다. 별도의 호출에서 동일한 쿼리를 만들려면 검색 매개 변수를 다시 수동으로 구성하는 대신 ID 값을 단일 쿼리 매개 변수로 포함할 수 있습니다. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**응답**

성공적인 응답은 요청에 지정된 지표 및 필터에 대한 결과 데이터 포인트를 반환합니다.

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| 속성 | 설명 |
| --- | --- |
| `customerAuditLogList` | 개체가 요청에 지정된 각 이벤트를 나타내는 배열입니다. 각 개체에는 필터 구성 및 반환된 이벤트 데이터에 대한 정보가 들어 있습니다. |
| `userEmail` | 이벤트를 수행한 사용자의 이메일입니다. |
| `eventType` | 이벤트 유형. 이벤트 유형에는 `Core` 및 `Enhanced`이(가) 포함됩니다. |
| `imsOrgId` | 이벤트가 발생한 조직의 ID입니다. |
| `permissionResource` | 권한을 제공한 제품 또는 기능이 작업을 수행합니다. 리소스는 다음 중 하나일 수 있습니다. <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | 작업과 관련된 권한 유형입니다. |
| `assetType` | 작업이 수행된 플랫폼 리소스의 유형입니다. |
| `assetId` | 작업이 수행된 Platform 리소스에 대한 고유 식별자입니다. |
| `assetName` | 작업이 수행된 Platform 리소스의 이름입니다. |
| `action` | 이벤트에 대해 기록된 작업 유형입니다. 작업은 다음 중 하나일 수 있습니다. <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | 작업의 상태입니다. 상태는 다음 중 하나일 수 있습니다. </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
