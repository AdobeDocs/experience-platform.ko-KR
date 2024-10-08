---
keywords: Experience Platform;홈;인기 항목;카탈로그;여러 개체 조회;api
solution: Experience Platform
title: 여러 카탈로그 개체 조회
description: 객체당 하나의 요청을 수행하는 대신 여러 개의 특정 객체를 보려는 경우 카탈로그는 동일한 유형의 여러 객체를 요청할 수 있는 간단한 단축키를 제공합니다. 단일 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 여러 카탈로그 개체 조회

개체당 하나의 요청을 하는 대신 여러 개의 특정 개체를 보려면 [!DNL Catalog]에서 같은 형식의 여러 개체를 요청하기 위한 간단한 바로 가기를 제공합니다. 단일 GET 요청을 사용하여 쉼표로 구분된 ID 목록을 포함하여 여러 특정 개체를 반환할 수 있습니다.

>[!NOTE]
>
>특정 [!DNL Catalog]개의 개체를 요청하는 경우에도 필요한 속성만 반환하려면 `properties` 쿼리 매개 변수를 사용하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | 검색할 특정 개체 중 하나에 대한 식별자입니다. |

**요청**

다음 요청에는 데이터 세트 ID의 쉼표로 구분된 목록과 각 데이터 세트에 대해 반환될 속성의 쉼표로 구분된 목록이 포함됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 각각에 대해 요청된 속성(`name`, `description` 및 `files`)만 포함하는 지정된 데이터 세트 목록을 반환합니다.

>[!NOTE]
>
>반환된 개체에 `properties` 쿼리로 표시된 요청된 속성이 하나 이상 포함되어 있지 않으면 아래 ***`Sample Dataset 3`*** 및 ***`Sample Dataset 4`***&#x200B;과(와) 같이 포함된 요청된 속성만 응답에서 반환합니다.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
