---
keywords: Experience Platform;home;popular topics;catalog;api;update an object
solution: Experience Platform
title: 개체 업데이트
topic: developer guide
description: 'PATCH 요청 경로에 카탈로그 ID를 포함하여 카탈로그 개체의 일부를 업데이트할 수 있습니다. 이 문서에서는 필드 및 카탈로그 개체에서 PATCH 작업을 수행하기 위한 JSON 패치 표기법을 사용하는 방법에 대해 설명합니다. '
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 3%

---


# 개체 업데이트

PATCH 요청 경로에 개체 ID를 포함하여 개체의 일부를 업데이트할 수 있습니다. [!DNL Catalog] 이 문서에서는 카탈로그 개체에서 PATCH 작업을 수행하는 두 가지 방법에 대해 설명합니다.

* 필드 사용
* JSON 패치 표기법 사용

>[!NOTE]
>
>개체에 대한 PATCH 작업은 관련 개체를 나타내는 확장 가능한 필드를 수정할 수 없습니다. 관련 개체를 직접 수정해야 합니다.

## 필드를 사용한 업데이트

다음 예제 호출에서는 필드 및 값을 사용하여 개체를 업데이트하는 방법을 보여 줍니다.

**API 형식**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 업데이트할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트의 `name` 및 `description` 필드를 페이로드에서 제공하는 값으로 업데이트합니다. 업데이트되지 않을 개체 필드는 페이로드에서 제외할 수 있습니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**응답**

성공적인 응답은 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 이제 이 데이터 세트에 대한 GET 요청을 수행하면 해당 값 `name` 과 업데이트만 표시되고 다른 모든 값은 변경되지 `description` 않습니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## JSON 패치 표기법을 사용하여 업데이트

다음 예제 호출에서는 [RFC-6902에 설명된 대로 JSON 패치를 사용하여 개체를 업데이트하는 방법을 보여 줍니다](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API 형식**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 업데이트할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 세트의 `name` 및 `description` 필드를 각 JSON 패치 개체에 제공된 값으로 업데이트합니다. JSON 패치를 사용할 때는 컨텐츠 유형 헤더도 다음으로 설정해야 합니다 `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**응답**

성공적인 응답은 업데이트된 개체의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 이 개체에 대한 GET 요청을 수행하면 이제 다른 모든 값이 변경되지 않은 상태로 유지되 `name` 는 동안 `description` 및 업데이트만 표시됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
