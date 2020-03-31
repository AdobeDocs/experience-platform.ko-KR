---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b

---


# 샌드박스 만들기

종단점에 POST 요청을 만들어 새 샌드박스를 만들 수 `/sandboxes` 있습니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;dev-3&quot;이라는 새 개발 샌드박스를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 이후 요청에서 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 가능한 한 설명적으로 만드는 것이 좋습니다. 공백이나 대문자를 포함할 수 없습니다. |
| `title` | 플랫폼 사용자 인터페이스에서 표시 목적으로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스의 유형입니다. 현재 조직은 &quot;개발&quot; 유형의 샌드박스만 만들 수 있습니다. |

**응답**

성공적인 응답은 새로 만든 샌드박스의 세부 사항을 반환하고 &quot;생성&quot; `state` 임을 표시합니다.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE] 샌드박스는 시스템에서 프로비저닝하는 데 약 15분이 소요되며, 그 후 샌드박스는 &quot;활성&quot; 또는 &quot;실패&quot; `state` 가 됩니다.
