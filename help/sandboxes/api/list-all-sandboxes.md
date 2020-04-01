---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 모든 샌드박스 나열
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# 모든 샌드박스 나열

IMS 조직에 속한 모든 샌드박스를 나열하려면(활성 또는 기타) `/sandboxes` 끝점에 GET 요청을 하십시오.

**API 형식**

```http
GET /sandboxes
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `name`, `title``state`및 `type`같은 세부 사항을 포함하여 조직에 속하는 샌드박스 목록을 반환합니다.

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
        },
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
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 샌드박스의 이름입니다. API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <br/><ul><li>**만들기**:샌드박스가 생성되었지만 시스템에서 여전히 프로비전되고 있습니다.</li><li>**활성**:샌드박스가 만들어지고 활성화됩니다.</li><li>**실패**:오류로 인해 시스템에서 샌드박스를 프로비전하지 못해 비활성화되었습니다.</li><li>**삭제됨**:샌드박스가 수동으로 비활성화되었습니다.</li></ul> |
| `type` | 샌드박스 유형, &quot;개발&quot; 또는 &quot;프로덕션&quot;. |
| `isDefault` | 이 샌드박스가 조직의 기본 샌드박스인지 여부를 나타내는 부울 속성입니다. 일반적으로 프로덕션 샌드박스입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율성에 사용되는 이 값은 샌드박스를 변경할 때마다 업데이트됩니다. |
