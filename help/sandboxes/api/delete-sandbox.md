---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 삭제
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# 샌드박스 삭제

요청 경로에 샌드박스를 포함하는 DELETE 요청을 만들어 샌드박스를 삭제할 `name` 수 있습니다.

>[!NOTE] 이 API 호출을 수행하면 샌드박스의 `status` 속성이 &quot;삭제됨&quot;으로 업데이트되고 비활성화됩니다. GET 요청은 삭제된 후에도 여전히 샌드박스의 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 삭제할 샌드박스의 `name` 이름입니다. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스를 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 샌드박스의 업데이트된 세부 정보를 반환하고 `state` &quot;삭제됨&quot;을 표시합니다.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
