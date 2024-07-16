---
keywords: Experience Platform;홈;인기 항목;개체 삭제;카탈로그 서비스;api
solution: Experience Platform
title: API에서 오브젝트 삭제
description: DELETE 요청 경로에 해당 ID를 제공하여 카탈로그 개체를 삭제할 수 있습니다.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 1%

---

# API에서 오브젝트 삭제

[!DNL Catalog] 개체의 ID를 DELETE 요청의 경로에 제공하여 개체를 삭제할 수 있습니다.

>[!WARNING]
>
>이 작업은 취소할 수 없으며 [!DNL Experience Platform]의 다른 곳에서 새로운 변경 사항이 발생할 수 있으므로 개체를 삭제할 때 각별히 주의하십시오.

**API 형식**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>`DELETE /batches/{ID}` 끝점은 더 이상 사용되지 않습니다. 일괄 처리를 삭제하려면 [일괄 처리 수집 API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)를 사용해야 합니다.

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 삭제할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 ID가 요청 경로에 지정된 데이터 세트를 삭제합니다.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 200(OK)과 삭제된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 DELETE 요청에서 전송된 ID와 일치해야 합니다. 삭제된 오브젝트에 대해 GET 요청을 수행하면 데이터 세트가 성공적으로 삭제되었는지 확인하는 HTTP 상태 404(찾을 수 없음)가 반환됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>요청에 입력한 ID와 일치하는 [!DNL Catalog] 개체가 없으면 HTTP 상태 코드 200을 계속 받을 수 있지만 응답 배열이 비어 있습니다.
