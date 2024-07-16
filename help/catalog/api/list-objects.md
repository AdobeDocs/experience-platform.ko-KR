---
keywords: Experience Platform;홈;자주 찾는 항목;필터;필터;데이터 필터링;데이터 필터링
solution: Experience Platform
title: 카탈로그 개체 나열
description: 단일 API 호출을 통해 특정 유형의 사용 가능한 모든 오브젝트 목록을 검색할 수 있습니다. 가장 좋은 방법은 응답 크기를 제한하는 필터를 포함하는 것입니다.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 카탈로그 개체 나열

단일 API 호출을 통해 특정 유형의 사용 가능한 모든 오브젝트 목록을 검색할 수 있습니다. 가장 좋은 방법은 응답 크기를 제한하는 필터를 포함하는 것입니다.

**API 형식**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 나열할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | 응답에서 반환된 결과를 필터링하는 데 사용되는 쿼리 매개 변수입니다. 여러 매개 변수는 앰퍼샌드(`&`)로 구분됩니다. 자세한 내용은 [카탈로그 데이터 필터링](filter-data.md)에 대한 안내서를 참조하세요. |

**요청**

아래 샘플 요청은 응답을 5개의 결과로 줄이는 `limit` 필터와 각 데이터 세트에 대해 표시되는 속성을 제한하는 `properties` 필터를 사용하여 데이터 세트 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청에 제공된 쿼리 매개 변수로 필터링된 [!DNL Catalog] 개체 목록을 키-값 쌍 형태로 반환합니다. 각 키-값 쌍의 키는 해당 [!DNL Catalog] 개체에 대한 고유 식별자를 나타냅니다. 그런 다음 [특정 개체 보기](look-up-object.md)에 대한 다른 호출에서 사용할 수 있습니다.

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
