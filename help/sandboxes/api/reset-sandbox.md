---
keywords: Experience Platform;홈;인기 항목;샌드박스 재설정
solution: Experience Platform
title: API의 샌드박스 재설정
topic: 개발자 가이드
description: 개발 샌드박스에는 샌드박스에서 기본이 아닌 모든 리소스를 삭제하는 "공장 재설정" 기능이 있습니다. 요청 경로에 샌드박스의 이름을 포함하는 PUT 요청을 만들어 샌드박스를 재설정할 수 있습니다.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 3%

---


# API의 샌드박스 재설정

개발 샌드박스에는 샌드박스에서 기본이 아닌 모든 리소스를 삭제하는 &quot;공장 재설정&quot; 기능이 있습니다. 요청 경로에서 샌드박스의 `name`을 포함하는 PUT 요청을 수행하여 샌드박스를 재설정할 수 있습니다.

**API 형식**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 재설정할 샌드박스의 `name` 속성입니다. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스를 재설정합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `action` | 샌드박스를 재설정하려면 이 매개 변수를 &quot;reset&quot; 값으로 요청 페이로드에서 제공해야 합니다. |

**응답**

성공적인 응답은 업데이트된 샌드박스의 세부 정보를 반환하며, 이 응답의 `state`이(가) &quot;재설정&quot;임을 표시합니다.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>샌드박스가 재설정되면 시스템에서 프로비저닝하는 데 약 15분이 소요됩니다. 프로비저닝되면 샌드박스의 `state`이 &quot;active&quot; 또는 &quot;failed&quot;가 됩니다.