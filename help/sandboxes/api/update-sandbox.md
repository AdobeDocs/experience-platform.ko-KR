---
keywords: Experience Platform;홈;인기 항목;업데이트 샌드박스
solution: Experience Platform
title: API에서 샌드박스 업데이트
topic: 개발자 가이드
description: 요청 경로에 샌드박스의 이름을 포함하는 PATCH 요청과 요청 페이로드에서 업데이트할 속성을 만들어 샌드박스에서 하나 이상의 필드를 업데이트할 수 있습니다.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# API의 샌드박스 업데이트

요청 경로에서 샌드박스의 `name`을 포함하는 PATCH 요청을 수행하고 요청 페이로드에서 업데이트할 속성을 설정하여 샌드박스에서 하나 이상의 필드를 업데이트할 수 있습니다.

>[!NOTE]
>
>현재 샌드박스의 `title` 속성만 업데이트할 수 있습니다.

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
