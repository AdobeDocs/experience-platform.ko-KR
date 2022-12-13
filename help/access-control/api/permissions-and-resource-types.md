---
keywords: Experience Platform;홈;인기 항목;액세스 제어 권한;액세스 제어 리소스 유형;액세스 제어 api
solution: Experience Platform
title: 참조 API 끝점
topic-legacy: developer guide
description: 액세스 제어 API의 참조 끝점을 사용하면 사용 가능한 권한 및 리소스 유형의 이름을 볼 수 있습니다. 이 이름을 사용하여 현재 사용자에 대한 효과적인 액세스 제어 정책을 볼 수 있습니다.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 1%

---

# 참조 끝점

에 GET 요청을 수행하여 모든 권한 및 리소스 유형의 이름을 나열할 수 있습니다 `/acl/reference` 엔드포인트. 그런 다음 API 호출에서 이러한 이름을 사용할 수 있습니다 [효과적인 액세스 제어 정책 보기](./effective-policies.md) 현재 사용자의 경우

권한은 Adobe Admin Console을 통해 관리되는 정책이며 0개 이상의 리소스 유형 정책에 매핑됩니다. 리소스 유형은 특정 유형의 [!DNL Platform] 리소스(예: 데이터 세트 또는 스키마)

**API 형식**

```http
GET /acl/reference
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 `permissions` 개체 및 `resource-types` 각 객체에는 액세스 권한 또는 리소스 유형에 대한 전체 이름 목록이 들어 있습니다.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
