---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개체 바꾸기
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# 개체 바꾸기

PUT 요청을 사용하여 [!DNL Catalog] 개체의 내용을 덮어쓸 수 있습니다. PUT 요청에서는 전체 리소스가 요청 페이로드로 대체됩니다.

>[!NOTE]
>
>개체 내의 몇 개의 특정 필드만 업데이트해야 하는 경우 [!DNL Catalog] PATCH 요청을 사용하는 것이 더 효율적일 수 있습니다.

**API 형식**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 바꿀 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트에 페이로드에서 제공된 값을 덮어씁니다.

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

성공적인 응답은 덮어쓴 객체의 ID가 포함된 배열을 반환합니다. 이 ID는 PUT 요청에 전송된 ID와 일치해야 합니다. 이제 이 개체에 대한 GET 요청을 수행하면 해당 세부 사항이 이전 PUT 요청의 페이로드에서 제공된 세부 항목으로 대체되었다는 결과가 표시됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
