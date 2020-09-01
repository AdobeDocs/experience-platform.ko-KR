---
keywords: Experience Platform;home;popular topics;namespace list;list namespace
solution: Experience Platform
title: 사용 가능한 네임스페이스 목록
topic: API guide
description: 사용 가능한 모든 네임스페이스를 나열합니다.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 5%

---


# 사용 가능한 네임스페이스 목록

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 사용 가능한 네임스페이스를 나타내는 각 개체가 포함된 개체 배열이 포함됩니다. &quot;[!UICONTROL false]&quot; 값이 &quot;[!UICONTROL custom]&quot;인 네임스페이스는 표준 네임스페이스이며, &quot;trueValue&quot;의 &quot;custom[!UICONTROL &quot;이 있는 네임스페이스는]조직에서 만든 네임스페이스입니다.

>[!NOTE]
>
>공간이 잘렸습니다.

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

다음 자습서로 진행하여 사용자 정의 네임스페이스 [만들기](./create-custom-namespace.md)