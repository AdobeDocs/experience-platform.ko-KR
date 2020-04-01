---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 세트 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: a25ca22fb8ec9eb95f74e4fd76a7f18e87343085

---


# 일괄 처리 만들기

데이터 세트에 데이터를 인제스트하려면 데이터 세트에 묶음이 연결되어 있어야 합니다. 기존 데이터 세트의 `id` 값을 사용하여 카탈로그 API의 `/batches` 끝점에 POST 요청을 만들어 일괄 처리를 만들 수 있습니다.

**API 형식**

```HTTP
POST /batches
```

**요청**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `datasetId` | 일괄 `id` 처리가 연결될 데이터 세트 |

**응답**

성공적인 응답은 HTTP 상태 201(작성됨)과 새로 만든 일괄 처리, 읽기 전용, 시스템 생성 문자열 등 세부 정보가 포함된 응답 개체를 반환합니다. `id`

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
