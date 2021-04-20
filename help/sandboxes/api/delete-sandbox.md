---
keywords: Experience Platform;홈;인기 항목;샌드박스 삭제
solution: Experience Platform
title: API에서 샌드박스 삭제
topic: developer guide
description: 요청 경로에 샌드박스의 이름을 포함하는 DELETE 요청을 수행하여 샌드박스를 삭제할 수 있습니다.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---


# API에서 샌드박스 삭제

요청 경로에서 샌드박스의 `name`을 포함하는 DELETE 요청을 수행하여 샌드박스를 삭제할 수 있습니다.

>[!NOTE]
>
>이 API 호출을 수행하면 샌드박스의 `status` 속성이 &quot;삭제됨&quot;으로 업데이트되고 비활성화됩니다. GET 요청은 삭제된 후에도 샌드박스의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 삭제할 샌드박스의 `name`. |

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

성공적인 응답은 샌드박스의 업데이트된 세부 정보를 반환하고 해당 `state`이(가) &quot;삭제됨&quot;임을 표시합니다.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
