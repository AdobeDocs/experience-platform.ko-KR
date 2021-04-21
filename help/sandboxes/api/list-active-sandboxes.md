---
keywords: Experience Platform;홈;인기 항목;목록 활성 샌드박스;목록 샌드박스
solution: Experience Platform
title: API의 현재 사용자에 대한 활성 샌드박스 목록
topic-legacy: developer guide
description: 루트 끝점에 GET 요청을 함으로써 현재 사용자에 대해 활성 상태인 샌드박스를 표시할 수 있습니다.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# API에서 현재 사용자에 대한 활성 샌드박스 나열

>[!NOTE]
>
>샌드박스 API에 제공된 다른 끝점과 달리 이 끝점은 샌드박스 관리 액세스 권한이 없는 사용자를 포함하여 모든 사용자에 대해 사용할 수 있습니다.

루트(`/`) 끝점에 GET 요청을 함으로써 현재 사용자에 대해 활성 상태인 샌드박스를 표시할 수 있습니다.

**API 형식**

```http
GET /{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 결과를 필터링하는 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](#query)의 섹션을 참조하십시오. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `name`, `title`, `state` 및 `type` 등의 세부 정보를 포함하여 현재 사용자에 대해 활성 상태인 샌드박스 목록을 반환합니다.

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
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>**만들기**:샌드박스가 생성되었지만 시스템에서 여전히 프로비저닝되고 있습니다.</li><li>**활성**:샌드박스가 만들어지고 활성화됩니다.</li><li>**실패**:오류로 인해 샌드박스를 시스템에 프로비저닝할 수 없으며 비활성화되었습니다.</li><li>**삭제됨**:샌드박스가 수동으로 비활성화되었습니다.</li></ul> |
| `type` | 샌드박스 유형(&quot;개발&quot; 또는 &quot;프로덕션&quot;). |
| `isDefault` | 이 샌드박스가 조직의 기본 샌드박스인지 여부를 나타내는 부울 속성입니다. 일반적으로 프로덕션 샌드박스입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율에 사용되므로 샌드박스를 변경할 때마다 이 값이 업데이트됩니다. |

## 쿼리 매개 변수 {#query} 사용

[[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API는 샌드박스를 나열할 때 쿼리 매개 변수를 페이지에 사용하고 결과를 필터링하는 기능을 지원합니다.

>[!NOTE]
>
>`limit` 및 `offset` 쿼리 매개 변수를 함께 지정해야 합니다. 하나만 지정하면 API에서 오류가 반환됩니다. 없음을 지정하면 기본 제한은 50이고 오프셋은 0입니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `limit` | 응답에서 반환될 최대 레코드 수입니다. |
| `offset` | 응답 목록을 시작(오프셋)할 첫 번째 레코드에서 시작된 엔티티의 수입니다. |
