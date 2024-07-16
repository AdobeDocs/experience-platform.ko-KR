---
keywords: Experience Platform;홈;인기 항목;카탈로그;개체 조회;api
solution: Experience Platform
title: 카탈로그 개체 조회
description: 특정 카탈로그 개체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 개체의 세부 정보를 볼 수 있습니다.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 카탈로그 개체 조회

특정 [!DNL Catalog] 개체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 개체의 세부 정보를 볼 수 있습니다.

>[!NOTE]
>
>특정 개체를 볼 때는 [속성별로 필터링](filter-data.md)하고 원하는 속성만 반환하는 것이 좋습니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 검색할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 검색할 특정 객체의 식별자입니다. |

**요청**

다음 요청은 ID로 데이터 세트를 검색하여 해당 `name`, `description`, `tags` 및 `files` 속성을 반환합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 본문에 요청된 `properties`만 있는 지정된 데이터 집합을 반환합니다.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>값 앞에 `@`이(가) 붙은 속성은 상호 관련된 개체를 나타냅니다. 이러한 개체의 세부 정보를 보는 방법에 대한 단계는 [상호 관련된 개체 보기](appendix.md#view-interrelated-objects)에 대한 부록 섹션을 참조하십시오.
