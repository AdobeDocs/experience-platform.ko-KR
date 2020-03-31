---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 재설정
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# 샌드박스 재설정

개발 샌드박스에는 샌드박스에서 기본이 아닌 모든 리소스를 삭제하는 &quot;공장 재설정&quot; 기능이 있습니다. 요청 경로에 샌드박스를 포함하는 PUT 요청을 만들어 샌드박스를 재설정할 `name` 수 있습니다.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `action` | 샌드박스를 재설정하려면 이 매개 변수를 &quot;reset&quot; 값과 함께 요청 페이로드에서 제공해야 합니다. |

**응답**

성공적인 응답은 업데이트된 샌드박스의 세부 사항을 반환하고 &quot;재설정&quot; `state` 임을 표시합니다.

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

>[!NOTE] 샌드박스가 재설정되면 시스템에서 프로비저닝하는 데 약 15분이 소요됩니다. 프로비저닝되면 샌드박스의 상태가 &quot;활성&quot; 또는 &quot;실패&quot; `state` 가 됩니다.