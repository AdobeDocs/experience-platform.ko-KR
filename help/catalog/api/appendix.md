---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그 api;부록
solution: Experience Platform
title: 카탈로그 서비스 API 안내서 부록
topic-legacy: developer guide
description: 이 문서에는 Adobe Experience Platform의 카탈로그 API를 사용하여 작업하는 데 도움이 되는 추가 정보가 포함되어 있습니다.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API 안내서 부록

이 문서에는 [!DNL Catalog] API를 사용하여 작업하는 데 도움이 되는 추가 정보가 포함되어 있습니다.

## 관련 개체 보기 {#view-interrelated-objects}

일부 [!DNL Catalog] 개체는 다른 [!DNL Catalog] 개체와 상호 관련될 수 있습니다. 응답 페이로드에서 `@`이(가) 접두어로 설정한 모든 필드는 관련 개체를 나타냅니다. 이러한 필드에 대한 값은 URI 형식을 취합니다. URI는 별도의 GET 요청에서 해당 필드가 나타내는 관련 개체를 검색하는 데 사용할 수 있습니다.

특정 데이터 세트](look-up-object.md)를 조회하는 [의 문서에서 반환되는 예제 데이터 집합에는 다음 URI 값이 있는 `files` 필드가 포함되어 있습니다.`"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 이 URI를 새 GET 요청의 경로로 사용하여 `files` 필드의 내용을 볼 수 있습니다.

**API 형식**

```http
GET {OBJECT_URI}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{OBJECT_URI}` | 관련 개체 필드에서 제공하는 URI(`@` 기호 제외). |

**요청**

다음 요청은 데이터 집합의 `files` 속성을 예제에서 제공한 URI를 사용하여 데이터 집합에 연결된 파일의 목록을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 관련 개체 목록을 반환합니다. 이 예제에서는 데이터 세트 파일 목록이 반환됩니다.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 단일 호출에서 여러 요청 수행

[!DNL Catalog] API의 루트 끝점을 사용하면 한 번의 호출 내에서 여러 요청을 수행할 수 있습니다. 요청 페이로드에는 일반적으로 개별 요청일 때를 나타내는 개체 배열이 포함되며, 그런 다음 순서대로 실행됩니다.

이러한 요청이 [!DNL Catalog]에 대한 수정 또는 추가이고 변경 사항 중 하나가 실패할 경우 모든 변경 사항은 되돌려집니다.

**API 형식**

```http
POST /
```

**요청**

다음 요청은 새 데이터 세트를 만든 다음 해당 데이터 세트에 대한 관련 보기를 만듭니다. 이 예는 템플릿 언어를 사용하여 후속 호출에서 사용하기 위해 이전 호출에서 반환된 값에 액세스하는 방법을 보여줍니다.

예를 들어 이전 하위 요청에서 반환된 값을 참조하려는 경우 다음 형식으로 참조를 만들 수 있습니다.`<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>`(여기서 `{REQUEST_ID}`은 아래 설명된 대로 하위 요청에 대해 사용자가 제공한 ID입니다.) 이러한 템플릿을 사용하여 이전 하위 요청의 응답 개체 본문에 사용할 수 있는 모든 속성을 참조할 수 있습니다.

>[!NOTE]
>
>실행된 하위 요청이 개체에 대한 참조만 반환하면(카탈로그 API의 대부분의 POST 및 PUT 요청에 대한 기본값인 함) 이 참조는 `id` 값으로 앨리어스되며 `<<{OBJECT_ID}.id>>`로 사용할 수 있습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `id` | 응답에 대한 요청을 일치시킬 수 있도록 응답 개체에 첨부된 사용자 제공 ID. [!DNL Catalog] 은 이 값을 저장하지 않고 참조용으로 응답에 반환합니다. |
| `resource` | [!DNL Catalog] API의 루트에 상대적인 리소스 경로입니다. 프로토콜과 도메인은 이 값의 일부일 수 없으며 &quot;/&quot;로 접두사를 붙여야 합니다. <br/><br/> PATCH 또는 DELETE을 하위 요청의  `method`일부로 사용할 때는 리소스 경로에 개체 ID를 포함시킵니다. 사용자가 제공한 `id`과 혼동하지 않도록 리소스 경로는 [!DNL Catalog] 개체 자체의 ID를 사용합니다(예: `resource: "/dataSets/1234567890"`). |
| `method` | 요청에서 수행되는 작업과 관련된 메서드(GET, PUT, POST, PATCH 또는 DELETE)의 이름입니다. |
| `body` | POST, PUT 또는 PATCH 요청에서 일반적으로 페이로드로 전달되는 JSON 문서입니다. 이 속성은 GET 또는 DELETE 요청에 필요하지 않습니다. |

**응답**

성공적인 응답은 각 요청에 할당한 `id`, 개별 요청에 대한 HTTP 상태 코드 및 응답 `body`이(가) 포함된 개체 배열을 반환합니다. 3개의 샘플 요청이 모두 새 개체를 만들기 위한 것이었기 때문에 각 개체의 `body`은 새로 만든 개체의 ID만 포함된 배열이며, 이는 [!DNL Catalog]에서 가장 성공적인 POST 응답이 있는 표준입니다.

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

다중 요청에 대한 응답을 확인할 때는 반드시 상위 POST 요청에 대한 HTTP 상태 코드에만 의존하지 않고 각 개별 하위 요청의 코드를 확인해야 합니다.  전체 요청이 200을 반환하는 반면, 단일 하위 요청에서 404(잘못된 리소스의 GET 요청 등)를 반환할 수 있습니다.

## 추가 요청 헤더

[!DNL Catalog] 는 업데이트 중에 데이터의 무결성을 유지하는 데 도움이 되는 여러 헤더 규칙을 제공합니다.

### If-Match

객체를 여러 사용자가 동시에 저장할 때 발생하는 데이터 손상 유형을 방지하기 위해 객체 버전 관리를 사용하는 것이 좋습니다.

객체를 업데이트할 때 가장 좋은 방법은 업데이트할 객체를 보기(GET)위해 API 호출을 하는 것입니다. 응답 내에 포함된(및 응답에 단일 객체가 포함된 모든 호출)은 객체 버전을 포함하는 `E-Tag` 헤더입니다. 업데이트(PUT 또는 PATCH) 호출에서 개체 버전을 `If-Match`이라는 요청 헤더로 추가하면 버전이 여전히 동일한 경우에만 업데이트가 진행되어 데이터 충돌을 방지할 수 있습니다.

버전이 일치하지 않는 경우(객체를 검색한 후 다른 프로세스에서 수정한 경우) 대상 리소스에 대한 액세스가 거부되었음을 나타내는 HTTP 상태 412(사전 조건 없음)가 표시됩니다.

### Pragma

경우에 따라 정보를 저장하지 않고 객체의 유효성을 확인할 수 있습니다. 값이 `validate-only`인 `Pragma` 헤더를 사용하면 유효성 검사 목적으로만 POST 또는 PUT 요청을 보낼 수 있으므로 데이터 변경 내용이 지속되지 않습니다.

## 데이터 비교

압축은 데이터를 변경하지 않고 작은 파일의 데이터를 큰 파일로 병합하는 [!DNL Experience Platform] 서비스입니다. 성능상의 이유로 쿼리할 때 데이터에 빠르게 액세스할 수 있도록 작은 파일 집합을 큰 파일로 결합하는 것이 좋습니다.

인제스트된 일괄 처리 파일의 내용이 완료되면 관련 [!DNL Catalog] 객체가 모니터링용으로 업데이트됩니다.
