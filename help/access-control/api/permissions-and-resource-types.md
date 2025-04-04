---
keywords: Experience Platform;홈;인기 항목;액세스 제어 권한;액세스 제어 리소스 유형;액세스 제어 api
solution: Experience Platform
title: 참조 API 엔드포인트
description: 액세스 제어 API의 참조 끝점을 사용하면 사용 가능한 권한 및 리소스 유형의 이름을 볼 수 있으며, 현재 사용자에 대한 유효한 액세스 제어 정책을 보는 데 사용할 수 있습니다.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 참조 엔드포인트

>[!NOTE]
>
>사용자 토큰이 전달되는 경우 토큰의 사용자는 요청된 조직에 대한 &quot;조직 관리자&quot; 역할이 있어야 합니다.

`/acl/reference` 끝점에 대한 GET 요청을 수행하여 모든 권한 및 리소스 유형의 이름을 나열할 수 있습니다. 그런 다음 현재 사용자의 [유효 액세스 제어 정책 보기](./effective-policies.md)에 대한 API 호출에 이러한 이름을 사용할 수 있습니다.

권한은 Adobe Admin Console을 통해 관리되는 정책이며 0개 이상의 리소스 유형 정책에 매핑됩니다. 리소스 유형은 특정 유형의 [!DNL Experience Platform] 리소스(예: 데이터 세트 또는 스키마)에 대한 읽기, 쓰기 및/또는 삭제 기능을 활성화하는 정책입니다.

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

성공한 응답은 각각 액세스 권한 또는 리소스 유형에 대한 전체 이름 목록이 포함된 `permissions` 개체와 `resource-types` 개체를 반환합니다.

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
