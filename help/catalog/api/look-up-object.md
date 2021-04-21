---
keywords: Experience Platform;홈;인기 항목;카탈로그;개체 조회;api
solution: Experience Platform
title: 카탈로그 개체 찾기
topic-legacy: developer guide
description: 특정 카탈로그 개체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 개체의 세부 정보를 볼 수 있습니다.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 카탈로그 개체 찾기

특정 [!DNL Catalog] 개체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 개체의 세부 정보를 볼 수 있습니다.

>[!NOTE]
>
>특정 개체를 볼 때는 여전히 [속성](filter-data.md)으로 필터링하고 관심 있는 속성만 반환하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 검색할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 해당 ID로 데이터 세트를 검색하여 `name`, `description`, `state`, `tags` 및 `files` 속성을 반환합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 본문에 요청된 `properties`만 있는 지정된 데이터 세트를 반환합니다.

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

>[!NOTE]
>
>값 앞에 `@`이(가) 있는 속성은 관련 개체를 나타냅니다. 이러한 개체의 세부 사항을 보는 방법에 대한 자세한 내용은 [상호 관련 개체 보기](appendix.md#view-interrelated-objects)의 부록 섹션을 참조하십시오.
