---
keywords: Experience Platform;홈;인기 항목;샌드박스;Sandbox;home;popular topics;sandbox
solution: Experience Platform
title: API에서 샌드박스 만들기
topic-legacy: developer guide
description: '''/sandbox'' 끝점에 POST 요청을 만들어 새 샌드박스를 만들 수 있습니다.'
exl-id: 676c5de8-2c3a-4612-9dd8-93e01cafe90e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# API에서 샌드박스 만들기

`/sandboxes` 끝점에 POST 요청을 하여 새 샌드박스를 만들 수 있습니다.

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
| `name` | 이후 요청의 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 이 값을 가능한 설명으로 만드는 것이 가장 좋습니다. 공백이나 대문자를 포함할 수 없습니다. |
| `title` | 플랫폼 사용자 인터페이스에서 표시 용도로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스의 유형입니다. 현재 조직은 &quot;개발&quot; 유형 샌드박스만 만들 수 있습니다. |

**응답**

성공적으로 응답하면 새로 만든 샌드박스의 세부 사항이 반환되고, 이 응답의 `state`이(가) &quot;생성&quot;임을 표시합니다.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>샌드박스는 시스템에서 프로비저닝하는 데 약 15분이 소요되며, 그 후 `state`은 &quot;활성&quot; 또는 &quot;실패&quot;가 됩니다.
