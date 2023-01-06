---
keywords: Experience Platform;홈;인기 항목;카탈로그;api;개체 바꾸기
solution: Experience Platform
title: 카탈로그 개체 바꾸기
description: PUT 요청을 사용하여 Catalog 개체의 컨텐츠를 덮어쓸 수 있으며, 이때 전체 리소스는 요청 페이로드로 대체됩니다.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 카탈로그 개체 바꾸기

의 컨텐츠를 덮어쓸 수 있습니다 [!DNL Catalog] 개체(PUT 요청을 사용하는 개체)를 포함하고, 전체 리소스는 요청 페이로드로 대체됩니다.

>[!NOTE]
>
>내 몇 개의 특정 필드만 업데이트해야 하는 경우 [!DNL Catalog] 개체를 만들 때 PATCH 요청을 사용하는 것이 더 효율적일 수 있습니다.

**API 형식**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 바꿀 객체입니다. 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트에 페이로드에 제공된 값으로 덮어씁니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**응답**

성공적으로 응답하면 덮어쓴 객체의 ID가 포함된 배열이 반환됩니다. 이 ID는 PUT 요청에 전송된 ID와 일치해야 합니다. 이제 이 개체에 대해 GET 요청을 수행하면 해당 세부 사항이 이전 PUT 요청의 페이로드에 제공된 세부 정보로 대체되었음을 알 수 있습니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
