---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: 권한 및 리소스 유형의 목록 이름
topic: developer guide
description: Adobe Experience Platform의 액세스 제어를 통해 Adobe Admin Console을 사용하여 다양한 플랫폼 기능에 대한 역할 및 권한을 관리할 수 있습니다. /acl/reference 끝점에 GET 요청을 하여 모든 권한 및 리소스 유형의 이름을 나열할 수 있습니다. 그런 다음 API 호출에서 이러한 이름을 사용하여 현재 사용자에 대한 효과적인 정책을 볼 수 있습니다.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# 권한 및 리소스 유형의 목록 이름

종단점에 GET 요청을 하여 모든 권한 및 리소스 유형의 이름을 나열할 수 `/acl/reference` 있습니다. 그런 다음 API 호출에서 이러한 이름을 사용하여 현재 사용자에 대한 효과적인 정책 [을](./effective-policies.md) 볼 수 있습니다.

권한은 Adobe Admin Console을 통해 관리되고 0개 이상의 리소스 유형 정책에 매핑되는 정책입니다. 리소스 유형은 특정 유형의 리소스(예: 데이터 세트 또는 스키마)에 대한 읽기, 쓰기 및/또는 삭제 기능을 사용할 수 있는 [!DNL Platform] 정책입니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 각각 액세스 권한 또는 리소스 유형에 대한 전체 이름 목록이 포함된 `permissions` 개체와 `resource-types` 개체를 반환합니다.

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
