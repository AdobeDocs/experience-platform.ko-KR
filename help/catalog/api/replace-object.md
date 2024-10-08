---
keywords: Experience Platform;홈;인기 항목;카탈로그;api;개체 바꾸기
solution: Experience Platform
title: 카탈로그 개체 바꾸기
description: 전체 리소스가 요청 페이로드로 대체되는 PUT 요청을 사용하여 카탈로그 객체의 콘텐츠를 덮어쓸 수 있습니다.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 카탈로그 개체 바꾸기

전체 리소스가 요청 페이로드로 대체되는 PUT 요청을 사용하여 [!DNL Catalog] 개체의 콘텐츠를 덮어쓸 수 있습니다.

>[!NOTE]
>
>[!DNL Catalog] 개체 내의 일부 특정 필드만 업데이트해야 하는 경우 PATCH 요청을 사용하는 것이 더 효율적일 수 있습니다.

**API 형식**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 대체할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 페이로드에 제공된 값으로 데이터 세트를 덮어씁니다.

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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**응답**

성공한 응답은 덮어쓴 개체의 ID가 포함된 배열을 반환합니다. 이 ID는 PUT 요청에서 전송된 ID와 일치해야 합니다. 이제 이 개체에 대해 GET 요청을 수행하면 해당 세부 사항이 이전 PUT 요청의 페이로드에 제공된 세부 사항으로 대체됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
