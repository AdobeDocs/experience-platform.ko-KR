---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개체 삭제
topic: developer guide
translation-type: tm+mt
source-git-commit: 6c17351b04fedefd4b57b9530f1d957da8183a68

---


# 개체 삭제

DELETE 요청의 경로에 카탈로그 개체의 ID를 제공하여 삭제할 수 있습니다.

>[!WARNING] 실행 취소할 수 없으며 Experience Platform의 다른 곳에서 변경 사항이 발생할 수 있으므로 개체를 삭제할 때 각별히 주의하십시오.

**API 형식**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT] 끝점은 더 이상 사용되지 `DELETE /batches/{ID}` 않습니다. 배치를 삭제하려면 일괄 처리 통합 API를 사용해야 [합니다](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 삭제할 카탈로그 개체의 유형입니다. 유효한 개체는 다음과 같습니다. <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

성공적인 응답은 HTTP 상태 200(OK)과 삭제된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 DELETE 요청에서 전송된 ID와 일치해야 합니다. 삭제된 개체에 대한 GET 요청을 수행하면 HTTP 상태 404(찾을 수 없음)가 반환되어 데이터 집합이 성공적으로 삭제되었음을 확인합니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] 요청에 제공된 ID와 일치하는 카탈로그 개체가 없는 경우 여전히 HTTP 상태 코드 200을 받을 수 있지만 응답 배열은 비어 있게 됩니다.
