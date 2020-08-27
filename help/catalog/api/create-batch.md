---
keywords: Experience Platform;home;popular topics;create batch;catalog service;api
solution: Experience Platform
title: 데이터 세트 만들기
topic: developer guide
description: 데이터 세트에 데이터를 인제스트하려면 데이터 세트에 묶음이 있어야 합니다. 기존 데이터 세트의 id 값을 사용하여 카탈로그 API의 /batches 종단점에 POST 요청을 수행하여 배치를 만들 수 있습니다.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---


# 일괄 처리 만들기

데이터 세트에 데이터를 인제스트하려면 데이터 세트에 묶음이 있어야 합니다. 기존 데이터 집합의 `id` 값을 사용하여 API의 종단점에 POST 요청을 함으로써 일괄 처리를 만들 수 `/batches` [!DNL Catalog] 있습니다.

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
| `datasetId` | 일괄 `id` 이 연결될 데이터 세트 |

**응답**

성공적인 응답은 HTTP Status 201(Created)과 시스템에서 생성된 문자열, 읽기 전용 등 새로 만든 일괄 처리 `id`의 세부 사항이 포함된 응답 개체를 반환합니다.

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
