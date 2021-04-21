---
keywords: Experience Platform;홈;인기 항목;카탈로그;다중 개체 조회;api
solution: Experience Platform
title: 여러 카탈로그 개체 찾기
topic-legacy: developer guide
description: 개체당 하나의 요청을 하는 대신 몇 개의 특정 개체를 보려는 경우 카탈로그는 동일한 유형의 여러 개체를 요청하는 간단한 단축키를 제공합니다. 단일 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 여러 카탈로그 개체 찾기

개체당 하나의 요청을 하는 대신 몇 개의 특정 개체를 보려는 경우 동일한 유형의 여러 개체를 요청하는 간단한 단축키를 제공합니다. [!DNL Catalog] 단일 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.

>[!NOTE]
>
>특정 [!DNL Catalog] 개체를 요청할 경우에도 필요한 속성만 반환하도록 `properties` 쿼리 매개 변수를 사용하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 검색할 특정 개체 중 하나에 대한 식별자입니다. |

**요청**

다음 요청에는 데이터 세트 ID의 쉼표로 구분된 목록과 각 데이터 세트에 대해 반환할 속성의 쉼표로 구분된 목록이 포함되어 있습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 각 데이터 세트에 대해 요청된 속성(`name`, `description` 및 `files`)만 포함하는 지정된 데이터 집합 목록을 반환합니다.

>[!NOTE]
>
>반환된 객체에 `properties` 쿼리에 지정된 요청된 속성이 하나 이상 포함되어 있지 않으면 응답은 ***`Sample Dataset 3`*** 및 ***`Sample Dataset 4`***&#x200B;에 표시된 대로 포함된 요청된 속성만 반환합니다.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
