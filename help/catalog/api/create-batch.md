---
keywords: Experience Platform;홈;인기 항목;배치 만들기;카탈로그 서비스;api
solution: Experience Platform
title: API에서 일괄 처리 만들기
description: 카탈로그 API의 /batches 끝점에 POST 요청을 하여 배치를 만들 수 있습니다.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# 일괄 처리 만들기

데이터 세트가 데이터를 수집하려면 데이터 세트와 연결된 배치가 있어야 합니다. 기존 데이터 세트의 `id` 값을 사용하여 [!DNL Catalog] API의 `/batches` 끝점에 대한 POST 요청을 만들어 일괄 처리를 만들 수 있습니다.

**API 형식**

```HTTP
POST /batches
```

**요청**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| 속성 | 설명 |
| --- | --- |
| `datasetId` | 배치가 연결될 데이터 집합의 `id`입니다. |

**응답**

성공한 응답은 HTTP 상태 201(생성됨)과 새로 생성된 일괄 처리의 세부 사항을 포함하는 응답 개체를 반환합니다. 여기에는 `id`, 읽기 전용, 시스템 생성 문자열이 포함됩니다.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
