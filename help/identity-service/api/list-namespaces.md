---
keywords: Experience Platform;홈;인기 항목;네임스페이스 목록;목록 네임스페이스
solution: Experience Platform
title: 사용 가능한 ID 네임스페이스 나열
description: 사용 가능한 모든 네임스페이스를 나열합니다.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# 사용 가능한 ID 네임스페이스 나열

**API 형식**

```http
GET /idnamespace/identities
```

**요청**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

이 응답에는 사용 가능한 네임스페이스를 나타내는 각 개체가 있는 개체 배열이 포함됩니다. &quot;[!UICONTROL 사용자 지정]&quot; 값[!UICONTROL false]&quot;는 표준 네임스페이스이며,[!UICONTROL 사용자 지정]&quot; 값[!UICONTROL true]&quot; 네임스페이스는 조직이 만든 네임스페이스입니다.

>[!NOTE]
>
>이 응답은 스페이스에 대해 잘렸습니다.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## 다음 단계

다음 자습서로 진행하여 [사용자 지정 네임스페이스 만들기](./create-custom-namespace.md)
