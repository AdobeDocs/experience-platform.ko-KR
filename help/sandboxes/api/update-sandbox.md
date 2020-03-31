---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 업데이트
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# 샌드박스 업데이트

요청 경로에 샌드박스의 샌드박스를 포함하는 PATCH 요청과 요청 페이로드에서 업데이트할 속성을 만들어 샌드박스에서 하나 이상의 필드를 업데이트할 `name` 수 있습니다.

>[!NOTE] 현재 샌드박스의 `title` 속성만 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 업데이트할 샌드박스의 `name` 속성입니다. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스의 `title` 속성을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**응답**

성공적인 응답은 새로 업데이트된 샌드박스의 세부 정보와 함께 HTTP 상태 200(OK)을 반환합니다.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
