---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개체 찾기
topic: developer guide
translation-type: tm+mt
source-git-commit: 4dcd174eda98fee1e8cf668819809bd061c6e8bb

---


# 개체 찾기

특정 카탈로그 개체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 개체의 세부 정보를 볼 수 있습니다.

>[!NOTE] 특정 개체를 볼 때는 여전히 속성으로 [필터링하고 관심 있는 속성만 반환하는 것이](filter-data.md) 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 검색할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 ID로 데이터 세트를 검색하고 `name`데이터 세트, `description``state`속성 `tags`및 `files` 속성을 반환합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 본문에 요청된 데이터만 있는 지정된 데이터 세트를 `properties` 반환합니다.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE] 값이 접두사로 추가된 속성은 관련 개체를 `@` 나타냅니다. 이러한 개체의 세부 사항을 보는 방법에 대한 단계는 관련 개체를 [](appendix.md#view-interrelated-objects) 보는 방법에 대한 부록 섹션을 참조하십시오.
