---
keywords: Experience Platform;홈;인기 항목;사용 가능한 샌드박스 목록;샌드박스 목록
solution: Experience Platform
title: 사용 가능한 샌드박스 API 끝점
description: 사용 가능한 샌드박스 종단점에 대한 GET 요청을 만들어 현재 사용자가 사용할 수 있는 샌드박스를 나열할 수 있습니다.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 사용 가능한 샌드박스 끝점

>[!NOTE]
>
>샌드박스 API에 제공된 다른 엔드포인트와 달리 이 엔드포인트는 샌드박스 관리 액세스 권한이 없는 사용자를 비롯하여 모든 사용자가 사용할 수 있습니다.

사용 가능한 샌드박스 종단점에 대한 GET 요청을 만들어 현재 사용자가 사용할 수 있는 샌드박스를 나열할 수 있습니다.

**API 형식**

```http
GET /{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [부록 문서](./appendix.md#query) 를 참조하십시오. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적으로 응답하면 다음과 같은 세부 사항을 포함하여 현재 사용자가 사용할 수 있는 샌드박스 목록이 반환됩니다 `name`, `title`, `state`, 및 `type`.

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
| `name` | 샌드박스의 이름입니다. API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>`creating`: 샌드박스가 생성되었지만 시스템에서 계속 프로비저닝되고 있습니다.</li><li>`active`: 샌드박스가 만들어지고 활성 상태가 됩니다.</li><li>`failed`: 오류로 인해 샌드박스를 시스템에서 프로비저닝할 수 없으며 비활성화되어 있습니다.</li><li>`deleted`: 샌드박스를 수동으로 비활성화했습니다.</li></ul> |
| `type` | 샌드박스 유형, &quot;개발&quot; 또는 &quot;프로덕션&quot;입니다. |
| `isDefault` | 이 샌드박스가 조직의 기본 프로덕션 샌드박스인지 여부를 나타내는 부울 속성입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율에 사용되는 경우 샌드박스를 변경할 때마다 이 값이 업데이트됩니다. |
