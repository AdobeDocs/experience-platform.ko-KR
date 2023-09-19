---
keywords: Experience Platform;홈;인기 항목;사용 가능한 샌드박스 나열;샌드박스 나열
solution: Experience Platform
title: 사용 가능한 샌드박스 API 엔드포인트
description: 사용 가능한 샌드박스 끝점에 GET 요청을 하여 현재 사용자가 사용할 수 있는 샌드박스를 나열할 수 있습니다.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 130f3a9b65befc1cc8cf400b8ca8ca4d6e7f71e4
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 사용 가능한 샌드박스 끝점

>[!NOTE]
>
>Sandbox API에 제공되는 다른 엔드포인트와 달리 이 엔드포인트는 Sandbox 관리 액세스 권한이 없는 엔드포인트를 포함하여 모든 사용자가 사용할 수 있습니다.

사용 가능한 샌드박스 끝점에 GET 요청을 하여 현재 사용자가 사용할 수 있는 샌드박스를 나열할 수 있습니다.

**API 형식**

```http
GET /{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 다음을 참조하십시오. [부록 문서](./appendix.md#query) 사용 가능한 매개 변수 목록입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 다음과 같은 세부 정보를 포함하여 현재 사용자가 사용할 수 있는 샌드박스 목록을 반환합니다. `name`, `title`, `state`, 및 `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 샌드박스의 이름. API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>`creating`: 샌드박스가 생성되었지만 시스템에 의해 아직 프로비저닝되고 있습니다.</li><li>`active`: 샌드박스가 생성되고 활성화됩니다.</li><li>`failed`: 오류로 인해 시스템에서 샌드박스를 프로비저닝할 수 없어 샌드박스가 비활성화되었습니다.</li><li>`deleted`: 샌드박스가 수동으로 비활성화되었습니다.</li></ul> |
| `type` | 샌드박스 유형, &quot;개발&quot; 또는 &quot;프로덕션&quot;. |
| `isDefault` | 이 샌드박스가 조직의 기본 프로덕션 샌드박스인지 여부를 나타내는 부울 속성. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자. 버전 제어 및 캐싱 효율성에 사용되며 이 값은 샌드박스가 변경될 때마다 업데이트됩니다. |
