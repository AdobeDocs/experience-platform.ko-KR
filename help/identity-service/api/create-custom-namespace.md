---
keywords: Experience Platform;홈;자주 찾는 항목;네임스페이스;네임스페이스;네임스페이스;네임스페이스;ID 네임스페이스;ID 네임스페이스;ID;ID
solution: Experience Platform
title: ID 서비스 API에서 사용자 지정 네임스페이스 만들기
description: ID 네임스페이스 API를 사용하면 조직에서만 사용할 수 있는 사용자 지정 ID 네임스페이스를 만들 수 있습니다.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# ID 서비스 API에서 사용자 지정 네임스페이스 만들기

사용 [!DNL Identity Namespace] API를 사용하면 조직에서만 사용할 수 있는 사용자 지정 ID 네임스페이스를 만들 수 있습니다.

사용자 지정 네임스페이스 만들기에 대한 권장 사항은 을 참조하십시오. [id 서비스 FAQ 설명서](../troubleshooting-guide.md).

>[!NOTE]
>
>네임스페이스는 ID의 한정자입니다. 따라서 네임스페이스가 만들어지면 삭제할 수 없습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

다음 튜토리얼을 진행하십시오. [id의 기본 ID 나열](./list-native-id.md)
