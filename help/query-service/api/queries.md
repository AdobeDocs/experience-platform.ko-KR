---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;api 안내서;쿼리;쿼리;쿼리 서비스;
solution: Experience Platform
title: 쿼리 API 끝점
description: 다음 섹션에서는 Query Service API에서 /queries 종단점을 사용하여 수행할 수 있는 호출을 살펴봅니다.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: e0287076cc9f1a843d6e3f107359263cd98651e6
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 2%

---

# 끝점 쿼리

## 샘플 API 호출

다음 섹션에서는 `/queries` 의 엔드포인트 [!DNL Query Service] API. 각 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

### 쿼리 목록 검색

IMS 조직에 대한 GET 요청을 수행하여 모든 쿼리 목록을 검색할 수 있습니다 `/queries` 엔드포인트.

**API 형식**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*선택 사항입니다*) 응답에서 반환된 결과를 구성하는 요청 경로에 매개 변수가 추가되었습니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`). 사용 가능한 매개 변수는 아래에 나와 있습니다.

**쿼리 매개 변수**

다음은 쿼리를 나열할 수 있는 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 종단점을 호출하면 조직에서 사용할 수 있는 모든 쿼리를 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 다음과 같습니다 `created` 및 `updated`. 예, `orderby=created` 은(는) 결과를 오름차순으로 정렬하게 됩니다. 추가 `-` 생성 전(`orderby=-created`)은 내림차순으로 만든 항목을 정렬합니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20년*) |
| `start` | 영(0) 기반 번호 지정을 사용하여 응답 목록을 오프셋합니다. 예, `start=2` 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **반드시** HTML 이스케이프 처리됨. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 다음과 같습니다 `created`, `updated`, `state`, 및 `id`. 지원되는 연산자 목록은 다음과 같습니다 `>` (보다 큼), `<` (보다 작음), `>=` (크거나 같음), `<=` (작거나 같음), `==` (같음), `!=` (같지 않음) 및 `~` (포함) 예, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 은 지정된 ID가 있는 모든 쿼리를 반환합니다. |
| `excludeSoftDeleted` | 소프트 삭제된 쿼리를 포함할지 여부를 나타냅니다. 예, `excludeSoftDeleted=false` will **포함** 소프트 삭제된 쿼리 (*부울, 기본값: true*) |
| `excludeHidden` | 사용자가 아닌 제어 쿼리를 표시할지를 나타냅니다. 이 값을 false로 설정하면 **포함** CURSOR 정의, FETCH 또는 메타데이터 쿼리와 같은 사용자 기반 쿼리가 아닙니다. (*부울, 기본값: true*) |
| `isPrevLink` | 다음 `isPrevLink` 페이지 매김에 쿼리 매개 변수가 사용됩니다. API 호출 결과는 해당 호출을 사용하여 정렬됩니다 `created` 타임스탬프 및 `orderby` 속성을 사용합니다. 결과 페이지를 탐색할 때 `isPrevLink` 는 뒤로 페이징 시 true로 설정됩니다. 쿼리의 순서를 취소합니다. 예로서 &quot;다음&quot; 및 &quot;이전&quot; 링크를 참조하십시오. |

**요청**

다음 요청은 IMS 조직에 대해 작성된 최신 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 쿼리 목록과 함께 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 IMS 조직에 대해 작성된 최신 쿼리를 반환합니다.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### 쿼리 만들기

에 POST 요청을 작성하여 새 쿼리를 만들 수 있습니다 `/queries` 엔드포인트.

**API 형식**

```http
POST /queries
```

**요청**

다음 요청은 페이로드에 제공된 SQL 문을 사용하여 새 쿼리를 만듭니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE $user_id;",
        "queryParameters": {
            $user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

아래 요청 예는 기존 쿼리 템플릿 ID를 사용하여 새 쿼리를 만듭니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| 속성 | 설명 |
| -------- | ----------- |
| `dbName` | SQL 쿼리를 만들 데이터베이스의 이름입니다. |
| `sql` | 만들 SQL 쿼리 |
| `name` | SQL 쿼리의 이름입니다. |
| `description` | SQL 쿼리에 대한 설명입니다. |
| `queryParameters` | SQL 문의 매개 변수화된 값을 대체하기 위한 키 값 쌍입니다. 필요한 경우에만 필요합니다 **if** 제공한 SQL 내에서 매개 변수 대체를 사용하고 있습니다. 이러한 키 값 쌍에는 값 유형 검사가 수행되지 않습니다. |
| `templateId` | 기존 쿼리의 고유 식별자입니다. SQL 문 대신 이를 제공할 수 있습니다. |
| `insertIntoParameters` | (선택 사항) 이 속성이 정의된 경우 이 쿼리는 INSERT INTO 쿼리로 변환됩니다. |
| `ctasParameters` | (선택 사항) 이 속성이 정의된 경우 이 쿼리는 CTAS 쿼리로 변환됩니다. |

**응답**

성공적인 응답은 새로 만든 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 쿼리가 활성화되고 성공적으로 실행되면 `state` 이(가) `SUBMITTED` to `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.cancel` to [만든 쿼리 취소](#cancel-a-query).

### ID로 쿼리 검색

에 GET 요청을 수행하여 특정 쿼리에 대한 세부 정보를 검색할 수 있습니다 `/queries` 끝점 및 쿼리 제공 `id` 값을 지정한 경우 이해할 수 있도록 해줍니다.

**API 형식**

```http
GET /queries/{QUERY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 다음 `id` 검색할 쿼리의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 쿼리에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.cancel` to [만든 쿼리 취소](#cancel-a-query).

### 쿼리 취소

에 PATCH 요청을 작성하여 지정된 질의 삭제를 요청할 수 있습니다 `/queries` 끝점 및 쿼리 제공 `id` 값을 지정한 경우 이해할 수 있도록 해줍니다.

**API 형식**

```http
PATCH /queries/{QUERY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 다음 `id` 취소할 쿼리의 값입니다. |


**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 쿼리를 취소하려면 값이 있는 op 매개 변수를 설정해야 합니다 `cancel `. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
