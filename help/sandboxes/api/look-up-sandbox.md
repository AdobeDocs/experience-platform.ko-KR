---
keywords: Experience Platform;홈;인기 있는 주제;샌드박스 찾기;샌드박스 찾기
solution: Experience Platform
title: API에서 샌드박스 찾기
topic-legacy: developer guide
description: 요청 경로에서 샌드박스의 이름 속성을 포함하는 GET 요청을 수행하여 개별 샌드박스를 찾을 수 있습니다.
exl-id: de8d965c-ca58-436e-b5b1-05a492de70f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# API에서 샌드박스 찾기

요청 경로에서 샌드박스의 `name` 속성을 포함하는 GET 요청을 수행하여 개별 샌드박스를 찾을 수 있습니다.

**API 형식**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 찾아볼 샌드박스의 `name` 속성입니다. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `name`, `title`, `state` 및 `type`을 비롯한 샌드박스의 세부 정보를 반환합니다.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 샌드박스의 이름입니다. API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>**만들기**:샌드박스가 생성되었지만 시스템에서 여전히 프로비저닝되고 있습니다.</li><li>**활성**:샌드박스가 만들어지고 활성화됩니다.</li><li>**실패**:오류로 인해 샌드박스를 시스템에 프로비저닝할 수 없으며 비활성화되었습니다.</li><li>**삭제됨**:샌드박스가 수동으로 비활성화되었습니다.</li></ul> |
| `type` | 샌드박스 유형(&quot;개발&quot; 또는 &quot;프로덕션&quot;). |
| `isDefault` | 이 샌드박스가 조직의 기본 샌드박스인지 여부를 나타내는 부울 속성입니다. 일반적으로 프로덕션 샌드박스입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율에 사용되므로 샌드박스를 변경할 때마다 이 값이 업데이트됩니다. |
