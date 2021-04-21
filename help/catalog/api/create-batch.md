---
keywords: Experience Platform;홈;인기 항목;일괄 작성;카탈로그 서비스;api
solution: Experience Platform
title: API에서 일괄 처리 만들기
topic-legacy: developer guide
description: 카탈로그 API의 /batches 끝점에 POST 요청을 하여 배치를 만들 수 있습니다.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 일괄 처리 만들기

데이터 세트에 데이터를 인제스트하려면 데이터 세트에 묶음이 있어야 합니다. 기존 데이터 세트의 `id` 값을 사용하면 [!DNL Catalog] API의 `/batches` 끝점에 POST 요청을 하여 일괄 처리를 만들 수 있습니다.

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
| `datasetId` | 일괄 처리가 연결될 데이터 세트의 `id` |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 새로 만든 일괄 처리에 대한 세부 사항을 포함하는 응답 개체(예: `id`, 읽기 전용 시스템 생성 문자열)를 반환합니다.

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
