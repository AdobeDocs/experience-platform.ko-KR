---
keywords: Experience Platform;홈;인기 항목;필터;필터;데이터 필터링;데이터 필터링
solution: Experience Platform
title: 카탈로그 객체 나열
description: 단일 API 호출을 통해 특정 유형의 사용 가능한 모든 개체 목록을 검색할 수 있습니다. 응답 크기를 제한하는 필터를 포함하는 것이 좋습니다.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 카탈로그 개체 나열

단일 API 호출을 통해 특정 유형의 사용 가능한 모든 개체 목록을 검색할 수 있습니다. 응답 크기를 제한하는 필터를 포함하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 나열할 객체입니다. 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 응답에서 반환된 결과를 필터링하는 데 사용되는 쿼리 매개 변수입니다. 여러 매개 변수는 앰퍼샌드(`&`). 다음 안내서를 참조하십시오. [카탈로그 데이터 필터링](filter-data.md) 추가 정보. |

**요청**

아래 샘플 요청은 데이터 세트 목록을 검색하고 `limit` 응답을 5개의 결과로 줄이고 `properties` 각 데이터 세트에 대해 표시되는 속성을 제한하는 필터.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 목록을 반환합니다. [!DNL Catalog] 요청에 제공된 쿼리 매개 변수로 필터링된 키-값 쌍 형태의 개체. 각 키-값 쌍에 대해 키는 [!DNL Catalog] 해당 개체의 다른 호출에서 사용할 수 있습니다. [특정 객체 보기](look-up-object.md) 자세한 내용

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
