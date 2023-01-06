---
keywords: Experience Platform;홈;인기 항목;개체 삭제;카탈로그 서비스;api
solution: Experience Platform
title: API에서 개체 삭제
description: DELETE 요청 경로에 해당 ID를 제공하여 카탈로그 개체를 삭제할 수 있습니다.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# API에서 개체 삭제

을(를) 삭제할 수 있습니다 [!DNL Catalog] DELETE 요청 경로에 해당 ID를 제공하여 개체의 ID를 설정합니다.

>[!WARNING]
>
>이 작업은 실행 취소할 수 없으며 의 다른 곳에서 변경 내용이 발생할 수 있으므로 개체를 삭제할 때 특별히 주의하십시오 [!DNL Experience Platform].

**API 형식**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>다음 `DELETE /batches/{ID}` 엔드포인트가 더 이상 사용되지 않습니다. 배치를 삭제하려면 [배치 수집 API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 유형 [!DNL Catalog] 삭제할 개체. 유효한 객체는 다음과 같습니다. <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 요청 경로에 ID가 지정된 데이터 세트를 삭제합니다.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 삭제된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 DELETE 요청에 전송된 ID와 일치해야 합니다. 삭제된 개체에 대해 GET 요청을 수행하면 HTTP 상태 404(찾을 수 없음)가 반환되고 데이터 세트가 성공적으로 삭제되었는지 확인합니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>없는 경우 [!DNL Catalog] 개체는 요청에 제공된 ID와 일치하며, 여전히 HTTP 상태 코드 200을 수신할 수 있지만 응답 배열은 비어 있습니다.
