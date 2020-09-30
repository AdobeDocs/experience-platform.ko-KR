---
keywords: Experience Platform;home;popular topics;query service;api guide;queries;query;Query service;
solution: Experience Platform
title: 쿼리 서비스 개발자 가이드
topic: queries
description: 다음 섹션에서는 쿼리 서비스 API에서 /queries 끝점을 사용하여 수행할 수 있는 호출을 자세히 설명합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---


# 쿼리

## 샘플 API 호출

다음 섹션에서는 API의 끝점을 사용하여 수행할 수 있는 `/queries` 호출을 [!DNL Query Service] 안내합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 쿼리 목록 검색

종단점에 대한 GET 요청을 만들어 IMS 조직에 대한 모든 쿼리 목록을 검색할 수 `/queries` 있습니다.

**API 형식**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(앰퍼샌드)로 구분하여 포함할 수`&`있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 쿼리 목록을 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수가 없는 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 쿼리가 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 주문할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어, 결과를 오름차순으로 정렬합니다 `orderby=created` . 만들기 `-` 전(`orderby=-created`)을 추가하면 항목들이 내림차순으로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. (*Default value: 20*) |
| `start` | 제로 기반 번호 지정을 사용하여 응답 목록을 오프셋합니다. 예를 들어 세 번째 나열된 쿼리에서 시작하는 목록을 `start=2` 반환합니다. (*Default value: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터는 HTML을 **escape해야 합니다** . 쉼표는 여러 필터 집합을 결합하는 데 사용됩니다. 지원되는 필드는 `created``updated`, `state`및 `id`입니다. 지원되는 연산자 목록은 `>` (보다 큼), `<` (보다 작음), `>=` (보다 크거나 같음), `<=` (보다 작음), `==` (같음), `!=` (같지 않음) 및 `~` (포함)입니다. 예를 들어, 지정된 ID가 있는 모든 쿼리를 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 반환합니다. |
| `excludeSoftDeleted` | 소프트 삭제된 쿼리를 포함할지 여부를 나타냅니다. 예를 들어, `excludeSoftDeleted=false` 소프트 **삭제 쿼리는** 포함됩니다. (*부울, 기본값:true*) |
| `excludeHidden` | 비 사용자 제어 쿼리를 표시할지를 나타냅니다. 이 값을 false로 설정하면 CURSOR 정의, FETCH 또는 메타데이터 쿼리와 같은 사용자 중심의 쿼리가 **포함됩니다** . (*부울, 기본값:true*) |

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

성공적인 응답은 지정된 IMS 조직에 대한 쿼리 목록이 포함된 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 IMS 조직에 대해 생성된 최신 쿼리를 반환합니다.

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

종단점에 POST 요청을 만들어 새 쿼리를 만들 수 `/queries` 있습니다.

**API 형식**

```http
POST /queries
```

**요청**

다음 요청은 페이로드에서 제공하는 값으로 구성된 새 쿼리를 만듭니다.

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

성공적인 응답은 새로 만든 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 쿼리가 활성화되고 성공적으로 실행되면 쿼리 `state` 가 (으)로 `SUBMITTED` 변경됩니다 `SUCCESS`.

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
>의 값을 사용하여 만든 쿼리 `_links.cancel` 를 [취소할 수 있습니다](#cancel-a-query).

### ID로 쿼리 검색

종단점에 GET 요청을 만들고 요청 경로에 쿼리 `/queries` `id` 값을 제공하여 특정 쿼리에 대한 자세한 정보를 검색할 수 있습니다.

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

성공적인 응답은 지정된 쿼리에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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
>의 값을 사용하여 만든 쿼리 `_links.cancel` 를 [취소할 수 있습니다](#cancel-a-query).

### 쿼리 취소

종단점에 PATCH 요청을 만들고 요청 경로에 쿼리 `/queries` `id` 값을 제공하여 지정된 쿼리를 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
PATCH /queries/{QUERY_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 취소할 쿼리의 `id` 값입니다. |


**요청**

이 API 요청은 페이로드에 대한 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 문서를 참조하십시오.

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
| `op` | 쿼리를 취소하려면 값을 사용하여 op 매개 변수를 설정해야 합니다 `cancel `. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
