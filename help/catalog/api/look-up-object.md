---
keywords: Experience Platform;홈;인기 항목;카탈로그;개체 조회;api
solution: Experience Platform
title: 카탈로그 개체 조회
description: 특정 카탈로그 객체의 고유 식별자를 알고 있는 경우 GET 요청을 수행하여 해당 객체의 세부 정보를 볼 수 있습니다.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 카탈로그 개체 조회

특정 [!DNL Catalog] 객체를 사용하여 해당 객체의 세부 사항을 볼 수 있도록 GET 요청을 수행할 수 있습니다.

>[!NOTE]
>
>특정 개체를 볼 때는 여전히 가장 좋은 방법입니다 [속성별 필터링](filter-data.md) 원하는 속성만 반환합니다.

**API 형식**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 검색할 개체 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 검색할 특정 객체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트를 ID로 검색하여 반환합니다 `name`, `description`, `state`, `tags`, 및 `files` 속성을 사용합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청한 데이터 세트만 있는 지정된 데이터 집합을 반환합니다 `properties` 몸 안에서

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
>값 접두사가 있는 속성 `@` 상호 관련 객체를 나타냅니다. 의 부록 섹션을 참조하십시오. [상호 관련 객체 보기](appendix.md#view-interrelated-objects) 이러한 객체의 세부 정보를 보는 방법에 대한 단계입니다.
