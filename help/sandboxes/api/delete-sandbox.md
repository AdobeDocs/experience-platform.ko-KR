---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 삭제
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 4%

---


# 샌드박스 삭제

요청 경로에 샌드박스의 DELETE 요청을 수행하여 샌드박스를 삭제할 수 `name` 있습니다.

>[!NOTE]
>
>이 API 호출을 수행하면 샌드박스의 `status` 속성이 &quot;삭제됨&quot;으로 업데이트되고 비활성화됩니다. GET 요청은 삭제된 후에도 여전히 샌드박스의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 삭제할 샌드박스 `name` 의 이름입니다. |

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

성공적인 응답은 샌드박스의 업데이트된 세부 정보를 반환하며, 이 세부 사항은 &quot;삭제&quot; `state` 되었음을 나타냅니다.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
