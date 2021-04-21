---
keywords: Experience Platform;홈;인기 항목;개체 삭제;카탈로그 서비스;api
solution: Experience Platform
title: API에서 개체 삭제
topic-legacy: developer guide
description: DELETE 요청 경로에 카탈로그 ID를 제공하여 카탈로그 개체를 삭제할 수 있습니다.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# API에서 개체 삭제

DELETE 요청 경로에 해당 ID를 제공하여 [!DNL Catalog] 개체를 삭제할 수 있습니다.

>[!WARNING]
>
>이 작업은 실행 취소할 수 없으며 [!DNL Experience Platform]의 다른 곳에서 변경 내용이 발생할 수 있으므로 개체를 삭제할 때 주의하십시오.

**API 형식**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>`DELETE /batches/{ID}` 끝점은 더 이상 사용되지 않습니다. 배치를 삭제하려면 [일괄 처리 통합 API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)를 사용해야 합니다.

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 삭제할 [!DNL Catalog] 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 요청 경로에 ID가 지정된 데이터 세트를 삭제합니다.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 삭제된 데이터 세트의 ID를 포함하는 배열을 반환합니다. 이 ID는 DELETE 요청에서 보낸 ID와 일치해야 합니다. 삭제된 개체에 대해 GET 요청을 수행하면 HTTP 상태 404(찾을 수 없음)가 반환되어 데이터 세트가 성공적으로 삭제되었음을 확인합니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>요청에 제공된 ID와 일치하는 [!DNL Catalog] 개체가 없는 경우 여전히 HTTP 상태 코드 200을 받을 수 있지만 응답 배열은 비어 있게 됩니다.
