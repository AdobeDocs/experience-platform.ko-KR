---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그 API;부록
solution: Experience Platform
title: 카탈로그 서비스 API 안내서 부록
description: 이 문서에는 Adobe Experience Platform에서 카탈로그 API를 사용하는 데 도움이 되는 추가 정보가 포함되어 있습니다.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# [!DNL Catalog Service] API 안내서 부록

이 문서에는 [!DNL Catalog] API 작업에 도움이 되는 추가 정보가 포함되어 있습니다.

## 상호 관련된 개체 보기 {#view-interrelated-objects}

일부 [!DNL Catalog] 개체는 다른 [!DNL Catalog] 개체와 상호 관련될 수 있습니다. 응답 페이로드의 접두사 `@`이(가) 있는 모든 필드는 관련 개체를 나타냅니다. 이러한 필드의 값은 URI 형태로, 이를 별도의 GET 요청에서 사용하여 해당 필드가 나타내는 관련 개체를 검색할 수 있습니다.

[특정 데이터 집합을 찾는 중](look-up-object.md)에 문서에서 반환된 예제 데이터 집합에 다음 URI 값이 있는 `files` 필드가 포함되어 있습니다. `"@/datasetFiles?datasetId={DATASET_ID}"`. 이 URI를 새 GET 요청의 경로로 사용하여 `files` 필드의 내용을 볼 수 있습니다.

**API 형식**

```http
GET {OBJECT_URI}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_URI}` | 상호 관련된 개체 필드에서 제공한 URI입니다(`@` 기호 제외). |

**요청**

다음 요청은 예제 데이터 세트의 `files` 속성이 제공한 URI를 사용하여 데이터 세트의 연결된 파일 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 관련 개체 목록을 반환합니다. 이 예제에서는 데이터 세트 파일 목록이 반환됩니다.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 추가 요청 헤더

[!DNL Catalog]은(는) 업데이트하는 동안 데이터의 무결성을 유지하는 데 도움이 되는 몇 가지 헤더 규칙을 제공합니다.

### If-Match

객체 버전 관리를 사용하여 여러 사용자가 동시에 객체를 저장할 때 발생하는 데이터 손상 유형을 방지하는 것이 좋습니다.

객체를 업데이트할 때에는 먼저 업데이트할 객체를 보기 위해(GET) API를 호출하는 것이 좋습니다. 응답(및 응답이 단일 개체를 포함하는 모든 호출)에 포함된 헤더는 개체 버전을 포함하는 `E-Tag` 헤더입니다. 개체 버전을 업데이트(PUT 또는 PATCH) 호출에서 이름이 `If-Match`인 요청 헤더로 추가하면 버전이 동일한 경우에만 업데이트가 성공하여 데이터 충돌을 방지할 수 있습니다.

버전이 일치하지 않을 경우(객체를 검색한 이후 다른 프로세스에 의해 객체가 수정됨) 대상 리소스에 대한 액세스가 거부되었음을 나타내는 HTTP 상태 412(사전 조건 실패)를 받게 됩니다.

### Pragma

정보를 저장하지 않고 개체의 유효성을 검사할 수 있습니다. 값이 `validate-only`인 `Pragma` 헤더를 사용하면 유효성 검사 목적으로만 POST 또는 PUT 요청을 보낼 수 있으므로 데이터에 대한 변경 내용이 지속되지 않습니다.

## 데이터 압축

압축 기능은 데이터를 변경하지 않고 작은 파일의 데이터를 큰 파일로 병합하는 [!DNL Experience Platform] 서비스입니다. 성능상의 이유로, 쿼리할 때 데이터를 더 빨리 액세스할 수 있도록 작은 파일 세트를 더 큰 파일로 결합하는 것이 좋은 경우가 있습니다.

수집된 일괄 처리의 파일이 압축되면 모니터링 목적으로 연결된 [!DNL Catalog] 개체가 업데이트됩니다.
