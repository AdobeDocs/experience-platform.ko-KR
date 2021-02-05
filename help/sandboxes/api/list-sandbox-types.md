---
keywords: Experience Platform;홈;인기 항목;목록 샌드박스
solution: Experience Platform
title: API에서 지원되는 샌드박스 유형 나열
topic: developer guide
description: /sandboxTypes 종단점에 GET 요청을 함으로써 조직에 대해 지원되는 샌드박스 유형 목록을 검색할 수 있습니다.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 2%

---


# API에서 지원되는 샌드박스 유형을 나열합니다.

`/sandboxTypes` 종단점에 GET 요청을 하여 조직에 대해 지원되는 샌드박스 유형 목록을 검색할 수 있습니다.

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

성공적인 응답은 조직에 대해 지원되는 샌드박스 유형 목록을 반환합니다.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
