---
keywords: Experience Platform;홈;인기 항목;네임스페이스 목록;목록 네임스페이스
solution: Experience Platform
title: 사용 가능한 ID 네임스페이스 나열
description: 사용 가능한 모든 네임스페이스를 나열합니다.
role: Developer
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
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

응답에는 개체 배열이 포함되며 각 개체는 사용 가능한 네임스페이스를 나타냅니다. &quot;[!UICONTROL custom]&quot; 값이 &quot;[!UICONTROL false]&quot;인 네임스페이스는 표준 네임스페이스이지만 &quot;[!UICONTROL custom]&quot; 값이 &quot;[!UICONTROL true]&quot;인 네임스페이스는 조직에서 만든 네임스페이스입니다.

>[!NOTE]
>
>이 응답은 공백으로 잘렸습니다.

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

다음 자습서로 이동하여 [사용자 지정 네임스페이스를 만듭니다](./create-custom-namespace.md)
