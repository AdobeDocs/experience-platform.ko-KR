---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;api 안내서;쿼리;쿼리;쿼리 서비스;
solution: Experience Platform
title: 쿼리 API 끝점
description: 다음 섹션에서는 쿼리 서비스 API에서 /queries 끝점을 사용하여 수행할 수 있는 호출에 대해 설명합니다.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# 쿼리 끝점

## 샘플 API 호출

다음 섹션은 [!DNL Query Service] API에서 `/queries` 끝점을 사용하여 수행할 수 있는 호출을 안내합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

### 쿼리 목록 검색

`/queries` 끝점에 대한 GET 요청을 통해 조직에 대한 모든 쿼리 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*선택적*) 매개 변수가 응답에 반환된 결과를 구성하는 요청 경로에 추가되었습니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다. 사용 가능한 매개 변수는 아래에 나와 있습니다.

**쿼리 매개 변수**

다음은 쿼리를 나열하는 데 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 쿼리를 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 만들어진 항목별로 오름차순으로 결과를 정렬합니다. 만들기 전에 `-`을(를) 추가하면(`orderby=-created`) 내림차순으로 만들어진 항목별로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | ISO 형식 타임스탬프를 지정하여 결과 순서를 지정합니다. 시작 날짜가 지정되지 않은 경우 API 호출은 가장 오래 전에 생성된 쿼리를 먼저 반환한 다음 더 최근 결과를 계속 나열합니다.<br> ISO 타임스탬프를 사용하면 날짜 및 시간에 서로 다른 수준의 세부기간을 사용할 수 있습니다. 기본 ISO 타임스탬프는 `2020-09-07` 형식을 사용하여 2020년 9월 7일의 날짜를 나타냅니다. 보다 복잡한 예제는 `2022-11-05T08:15:30-05:00`(으)로 작성되며 2022년 11월 5일 오전 8:15:30(미국 동부 표준시)에 해당합니다. 시간대는 UTC 오프셋을 사용하여 제공될 수 있으며 접미사 &quot;Z&quot;(`2020-01-01T01:01:01Z`)로 표시됩니다. 시간대가 제공되지 않으면 기본값은 0입니다. |
| `property` | 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프해야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `updated`, `state` 및 `id`입니다. 지원되는 연산자 목록은 `>`(보다 큼), `<`(보다 작음), `>=`(보다 크거나 같음), `<=`(보다 작거나 같음), `==`(과 같음), `!=`(과 같지 않음) 및 `~`(포함)입니다. 예를 들어 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec`은(는) 지정된 ID를 가진 모든 쿼리를 반환합니다. |
| `excludeSoftDeleted` | 소프트 삭제된 쿼리를 포함해야 하는지 여부를 나타냅니다. 예를 들어 `excludeSoftDeleted=false`은(는) 일시 삭제된 쿼리를 **포함**&#x200B;합니다. (*부울, 기본값: true*) |
| `excludeHidden` | 비사용자 정의 쿼리를 표시할지 여부를 나타냅니다. 이 값을 false로 설정하면 CURSOR 정의, FETCH 또는 메타데이터 쿼리와 같은 비사용자 정의 쿼리가 **포함**&#x200B;됩니다. (*부울, 기본값: true*) |
| `isPrevLink` | `isPrevLink` 쿼리 매개 변수는 페이지 매김에 사용됩니다. API 호출 결과는 해당 `created` 타임스탬프 및 `orderby` 속성을 사용하여 정렬됩니다. 결과 페이지를 탐색할 때 뒤로 페이징할 때 `isPrevLink`이(가) true로 설정됩니다. 쿼리의 순서를 반대로 합니다. 예제로 &quot;다음&quot; 및 &quot;이전&quot; 링크를 참조하십시오. |

**요청**

다음 요청은 조직에 대해 생성된 최신 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 조직에 대한 쿼리 목록을 JSON으로 포함하는 HTTP 상태 200을 반환합니다. 다음 응답은 조직에 대해 생성된 최신 쿼리를 반환합니다.

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

`/queries` 끝점에 대한 POST 요청을 하여 새 쿼리를 만들 수 있습니다.

**API 형식**

```http
POST /queries
```

**요청**

다음 요청은 페이로드에 제공된 SQL 문으로 새 쿼리를 만듭니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

아래 요청 예제에서는 기존 쿼리 템플릿 ID를 사용하여 새 쿼리를 만듭니다.

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
| `dbName` | SQL 쿼리를 만드는 데이터베이스의 이름입니다. |
| `sql` | 만들려는 SQL 쿼리입니다. |
| `name` | SQL 쿼리의 이름입니다. |
| `description` | SQL 쿼리에 대한 설명입니다. |
| `queryParameters` | SQL 문의 매개 변수가 있는 값을 대체할 키 값 쌍입니다. 입력한 SQL 내에서 매개 변수 대체 요소를 사용하는 경우 **if**&#x200B;만 필요합니다. 이 키 값 쌍에 대해서는 값 유형 검사가 수행되지 않습니다. |
| `templateId` | 기존 쿼리의 고유 식별자입니다. SQL 문 대신 이를 제공할 수 있습니다. |
| `insertIntoParameters` | (선택 사항) 이 속성이 정의된 경우 이 쿼리는 INSERT INTO 쿼리로 변환됩니다. |
| `ctasParameters` | (선택 사항) 이 속성이 정의된 경우 이 쿼리는 CTAS 쿼리로 변환됩니다. |

**응답**

성공한 응답은 새로 만든 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 쿼리가 활성화되고 성공적으로 실행되면 `state`이(가) `SUBMITTED`에서 `SUCCESS`(으)로 변경됩니다.

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
>`_links.cancel`의 값을 사용하여 [만들어진 쿼리를 취소](#cancel-a-query)할 수 있습니다.

### ID로 쿼리 검색

`/queries` 끝점에 대한 GET 요청을 만들고 요청 경로에 쿼리의 `id` 값을 제공하여 특정 쿼리에 대한 자세한 정보를 검색할 수 있습니다.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 쿼리에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

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
>`_links.cancel`의 값을 사용하여 [만들어진 쿼리를 취소](#cancel-a-query)할 수 있습니다.

### 쿼리 취소 또는 일시 삭제

`/queries` 끝점에 PATCH 요청을 하고 요청 경로에 쿼리의 `id` 값을 제공하여 지정된 쿼리를 취소하거나 일시 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
PATCH /queries/{QUERY_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 작업을 수행할 쿼리의 `id` 값입니다. |


**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

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
| `op` | 리소스에 대해 수행할 작업의 유형입니다. 허용되는 값은 `cancel` 및 `soft_delete`입니다. 쿼리를 취소하려면 값이 `cancel `인 op 매개 변수를 설정해야 합니다. 소프트 삭제 작업은 GET 요청에서 쿼리가 반환되는 것을 중지하지만 시스템에서 쿼리가 삭제되지는 않습니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
