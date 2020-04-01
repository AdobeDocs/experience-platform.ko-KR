---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 사용 가능한 네임스페이스 목록
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

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

응답에는 사용 가능한 네임스페이스를 나타내는 각 개체가 포함된 개체 배열이 포함됩니다. &quot;custom&quot; 값이 &quot;false&quot;인 네임스페이스는 표준 네임스페이스이며, &quot;true&quot;의 &quot;custom&quot; 값이 &quot;true&quot;인 네임스페이스는 조직에서 만든 네임스페이스입니다.

>[!NOTE] 이 응답은 공간에 대해 잘렸습니다.

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

다음 자습서로 진행하여 사용자 정의 네임스페이스를 [만듭니다.](./create-custom-namespace.md)