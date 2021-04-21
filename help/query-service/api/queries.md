---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;api guide;queries;query;query;Query service;
solution: Experience Platform
title: 쿼리 API 끝점
topic-legacy: queries
description: 다음 섹션에서는 쿼리 서비스 API에서 /queries 끝점을 사용하여 수행할 수 있는 호출을 안내합니다.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---

# 쿼리 끝점

## 샘플 API 호출

다음 섹션에서는 [!DNL Query Service] API의 `/queries` 끝점을 사용하여 수행할 수 있는 호출을 안내합니다. 각 호출에는 일반 API 형식, 필수 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 쿼리 목록 검색

`/queries` 종단점에 GET 요청을 하여 IMS 조직에 대한 모든 쿼리 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택* 사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 쿼리 목록을 나열할 수 있는 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에 사용할 수 있는 모든 쿼리를 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 결과를 오름차순으로 정렬합니다. 만들기 전에 `-`(`orderby=-created`)을 추가하면 작성된 항목이 내림차순으로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. (*기본값:20*) |
| `start` | 0부터 시작하는 번호 매기기를 사용하여 응답 목록을 오프셋합니다. 예를 들어 `start=2`은 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값:0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **은(는) HTML을 escape해야 합니다.** 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `updated`, `state` 및 `id`입니다. 지원되는 연산자 목록은 `>`(보다 큼), `<`(보다 작음), `>=`(보다 크거나 같음), `<=`(작거나 같음), `==`(같음), `!=`(같지 않음) 및 `~`(포함)입니다. 예를 들어 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec`은 지정된 ID가 있는 모든 쿼리를 반환합니다. |
| `excludeSoftDeleted` | 소프트 삭제된 쿼리를 포함할지 여부를 나타냅니다. 예를 들어 `excludeSoftDeleted=false`은 **소프트 삭제된 쿼리를 포함합니다.** (*Boolean, 기본값:true*) |
| `excludeHidden` | 비 사용자 기반 쿼리를 표시할지를 나타냅니다. 이 값을 false로 설정하면 **CURSOR 정의, FETCH 또는 메타데이터 쿼리와 같은 사용자 중심의 쿼리를 포함하게 됩니다.** (*Boolean, 기본값:true*) |

**요청**

다음 요청은 IMS 조직에 대해 만든 최신 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 쿼리 목록이 포함된 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 IMS 조직에 대해 만든 최신 쿼리를 반환합니다.

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

`/queries` 끝점에 POST 요청을 하여 새 쿼리를 만들 수 있습니다.

**API 형식**

```http
POST /queries
```

**요청**

다음 요청은 페이로드에서 제공된 값으로 구성된 새 쿼리를 만듭니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| 속성 | 설명 |
| -------- | ----------- |
| `dbName` | SQL 쿼리를 만들 데이터베이스의 이름입니다. |
| `sql` | 만들려는 SQL 쿼리입니다. |
| `name` | SQL 쿼리의 이름입니다. |
| `description` | SQL 쿼리에 대한 설명입니다. |

**응답**

성공적인 응답은 새로 만든 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 쿼리가 활성화되고 성공적으로 실행되면 `state`이 `SUBMITTED`에서 `SUCCESS`로 변경됩니다.

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
>`_links.cancel` 값을 사용하여 [만든 쿼리](#cancel-a-query)를 취소할 수 있습니다.

### ID로 쿼리 검색

`/queries` 끝점에 GET 요청을 하고 요청 경로에 쿼리의 `id` 값을 제공하여 특정 쿼리에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /queries/{QUERY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 검색할 쿼리의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 쿼리에 대한 자세한 정보가 있는 HTTP 상태 200을 반환합니다.

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
>`_links.cancel` 값을 사용하여 [만든 쿼리](#cancel-a-query)를 취소할 수 있습니다.

### 쿼리 취소

`/queries` 끝점에 PATCH 요청을 하고 요청 경로에 쿼리의 `id` 값을 제공하여 지정된 쿼리를 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
PATCH /queries/{QUERY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 취소할 쿼리의 `id` 값입니다. |


**요청**

이 API 요청에서는 페이로드에 대한 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 쿼리를 취소하려면 `cancel ` 값으로 op 매개 변수를 설정해야 합니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
