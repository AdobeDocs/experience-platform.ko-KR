---
keywords: Experience Platform;홈;인기 항목;네임스페이스;네임스페이스;네임스페이스;네임스페이스;네임스페이스;네임스페이스;ID 네임스페이스;ID 네임스페이스;ID 네임스페이스;ID;ID
solution: Experience Platform
title: ID 서비스 API에서 사용자 정의 네임스페이스 만들기
topic-legacy: API guide
description: ID 네임스페이스 API를 사용하여 조직에서만 사용할 수 있는 사용자 지정 ID 네임스페이스를 만들 수 있습니다.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# ID 서비스 API에서 사용자 정의 네임스페이스 만들기

[!DNL Identity Namespace] API를 사용하여 조직에서만 사용할 수 있는 사용자 지정 ID 네임스페이스를 만들 수 있습니다.

사용자 정의 네임스페이스 만들기에 대한 권장 사항은 [Identity Service FAQ 설명서](../troubleshooting-guide.md)를 참조하십시오.

>[!NOTE]
>
>네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스를 만들면 삭제할 수 없습니다.

**API 형식**

```http
POST /idnamespace/identities
```

**요청**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**응답**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## 다음 단계

다음 튜토리얼로 진행하여 [ID](./list-native-id.md)의 기본 ID를 나열합니다.
