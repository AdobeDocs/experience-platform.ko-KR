---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: 지원되는 샌드박스 유형 목록
topic: developer guide
description: /sandboxTypes 종단점에 GET 요청을 수행하여 조직에 대해 지원되는 샌드박스 유형 목록을 검색할 수 있습니다.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 2%

---


# 지원되는 샌드박스 유형 목록

종단점에 GET 요청을 하여 조직에 대해 지원되는 샌드박스 유형 목록을 검색할 수 `/sandboxTypes` 있습니다.

**API 형식**

```http
GET /sandboxTypes
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 조직에서 지원되는 샌드박스 유형 목록을 반환합니다.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
