---
keywords: Experience Platform;홈;인기 항목;카탈로그;여러 개체 조회;api
solution: Experience Platform
title: 여러 카탈로그 객체 조회
topic-legacy: developer guide
description: 개체당 한 개의 요청을 하는 대신 몇 개의 특정 개체를 보려는 경우 동일한 유형의 여러 개체를 요청하는 간단한 단축키를 제공합니다. 하나의 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 여러 카탈로그 개체 조회

객체당 하나의 요청을 수행하는 대신 여러 특정 객체를 보려면 [!DNL Catalog] 동일한 유형의 여러 개체를 요청하는 간단한 단축키를 제공합니다. 하나의 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.

>[!NOTE]
>
>특정 요청 시에도 [!DNL Catalog] 객체, 여전히 `properties` 필요한 속성만 반환하기 위한 쿼리 매개 변수입니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 검색할 특정 객체 중 하나에 대한 식별자입니다. |

**요청**

다음 요청에는 쉼표로 구분된 데이터 세트 ID 목록과 각 데이터 세트에 대해 반환할 속성의 쉼표로 구분된 목록이 포함되어 있습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 요청된 속성(`name`, `description`, 및 `files`) 내의 아무 곳에나 삽입할 수 있습니다.

>[!NOTE]
>
>반환된 개체에 `properties` 쿼리하면, 응답에 포함된 요청된 속성만 반환됩니다(예: ). ***`Sample Dataset 3`*** 및 ***`Sample Dataset 4`*** 아래의 제품에서 사용할 수 있습니다.

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
