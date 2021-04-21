---
keywords: Experience Platform;홈;인기 항목;카탈로그;api;개체 바꾸기
solution: Experience Platform
title: 카탈로그 개체 바꾸기
topic-legacy: developer guide
description: 전체 리소스가 요청 페이로드로 대체되는 PUT 요청을 사용하여 카탈로그 개체의 내용을 덮어쓸 수 있습니다.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 카탈로그 개체 바꾸기

전체 리소스가 요청 페이로드로 대체되는 PUT 요청을 사용하여 [!DNL Catalog] 개체의 내용을 덮어쓸 수 있습니다.

>[!NOTE]
>
>[!DNL Catalog] 개체 내의 일부 특정 필드만 업데이트할 필요가 있는 경우 PATCH 요청을 사용하는 것이 더 효율적일 수 있습니다.

**API 형식**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 바꿀 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트를 페이로드에서 제공된 값으로 덮어씁니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공적으로 응답하면 덮어쓴 객체의 ID가 포함된 배열을 반환합니다. 이 ID는 PUT 요청에서 보낸 ID와 일치해야 합니다. 이제 이 개체에 대한 GET 요청을 수행하면 해당 세부 사항이 이전 PUT 요청의 페이로드에서 제공된 세부 항목으로 대체되었음을 알 수 있습니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
