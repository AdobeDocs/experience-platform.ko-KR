---
keywords: Experience Platform;홈;인기 항목;필터;필터;필터 데이터;필터 데이터;;home;popular topics;filter;data;filter data
solution: Experience Platform
title: 카탈로그 개체 목록
topic-legacy: developer guide
description: 단일 API 호출을 통해 특정 유형의 사용 가능한 모든 개체 목록을 검색할 수 있으며, 응답 크기를 제한하는 필터를 포함하는 것이 좋습니다.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 카탈로그 개체 목록

단일 API 호출을 통해 특정 유형의 사용 가능한 모든 개체 목록을 검색할 수 있으며, 응답 크기를 제한하는 필터를 포함하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 나열할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 응답에서 반환된 결과를 필터링하는 데 사용되는 쿼리 매개 변수입니다. 여러 매개 변수는 앰퍼샌드(`&`)로 구분됩니다. 자세한 내용은 [카탈로그 데이터 필터링](filter-data.md)의 안내서를 참조하십시오. |

**요청**

아래 샘플 요청은 데이터 집합 목록을 검색합니다. 여기에는 `limit` 필터가 있으면 결과가 5개로 줄어들고 각 데이터 세트에 대해 표시된 속성을 제한하는 `properties` 필터가 있습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청에 제공된 쿼리 매개 변수를 기준으로 필터링된 키-값 쌍 형식의 [!DNL Catalog] 개체 목록을 반환합니다. 각 키-값 쌍에 대해 키는 해당 [!DNL Catalog] 개체에 대한 고유 식별자를 나타냅니다. 이러한 식별자는 자세한 내용을 보려면 [해당 특정 개체](look-up-object.md)을(를) 다른 호출에서 사용할 수 있습니다.

>[!NOTE]
>
>반환된 개체에 `properties` 쿼리에 지정된 요청된 속성 중 하나 이상이 포함되어 있지 않으면 응답에 포함된 요청된 속성만 반환됩니다(예: ***`Sample Dataset 3`*** 및 ***`Sample Dataset 4`*** 아래 참조).

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
