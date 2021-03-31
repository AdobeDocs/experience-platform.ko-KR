---
keywords: Experience Platform;홈;인기 항목;샌드박스;Sandbox;home;popular topics;sandbox
solution: Experience Platform
title: API에서 샌드박스 만들기
topic: 개발자 가이드
description: '''/sandbox'' 끝점에 POST 요청을 만들어 새 샌드박스를 만들 수 있습니다.'
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# API에서 샌드박스 만들기

`/sandboxes` 끝점에 POST 요청을 하여 개발 또는 프로덕션 샌드박스를 만들 수 있습니다.

## 개발 샌드박스 만들기

개발 샌드박스를 만들려면 `/sandboxes` 끝점에 POST 요청을 하고 `type` 속성에 대해 `development` 값을 제공합니다.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 이후 요청의 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 이 값을 가능한 설명으로 만드는 것이 가장 좋습니다. 이 값은 공백이나 특수 문자를 포함할 수 없습니다. |
| `title` | 플랫폼 사용자 인터페이스에서 표시 용도로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스의 유형입니다. `type` 속성 값은 개발 또는 제작일 수 있습니다. |

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

## 프로덕션 샌드박스 만들기

>[!NOTE]
>
>여러 제작 샌드박스 기능이 베타에 있습니다.

프로덕션 샌드박스를 만들려면 `/sandboxes` 끝점에 POST 요청을 하고 `type` 속성에 대해 `production` 값을 제공합니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;test-prod-sandbox&quot;라는 새 프로덕션 샌드박스를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 이후 요청의 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 이 값을 가능한 설명으로 만드는 것이 가장 좋습니다. 이 값은 공백이나 특수 문자를 포함할 수 없습니다. |
| `title` | 플랫폼 사용자 인터페이스에서 표시 용도로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스의 유형입니다. `type` 속성 값은 개발 또는 제작일 수 있습니다. |

**응답**

성공적으로 응답하면 새로 만든 샌드박스의 세부 사항이 반환되고, 이 응답의 `state`이(가) &quot;생성&quot;임을 표시합니다.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
