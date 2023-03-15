---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 템플릿;api 안내서;템플릿;쿼리 서비스;
solution: Experience Platform
title: 쿼리 템플릿 API 끝점
description: 이 안내서에서는 쿼리 서비스 API를 사용하여 수행할 수 있는 다양한 쿼리 템플릿 API 호출에 대해 자세히 설명합니다.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: ee6a54aeba4ddfeb98ee5e11283c299f00969a53
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 2%

---

# 쿼리 템플릿 끝점

## 샘플 API 호출

다음 섹션에서는 다음을 사용하여 수행할 수 있는 다양한 API 호출에 대해 설명합니다. [!DNL Query Service] API. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

다음을 참조하십시오. [UI 쿼리 템플릿 설명서](../ui/query-templates.md) Experience Platform UI를 통해 템플릿을 만드는 방법에 대한 자세한 내용

### 쿼리 템플릿 목록 검색

에 GET 요청을 하여 IMS 조직에 대한 모든 쿼리 템플릿 목록을 검색할 수 있습니다. `/query-templates` 엔드포인트.

**API 형식**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택 사항*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`). 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 쿼리 템플릿을 나열하기 위해 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 쿼리 템플릿을 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 다음과 같습니다. `created` 및 `updated`. 예를 들어, `orderby=created` 생성된 항목별로 오름차순으로 결과를 정렬합니다. 추가 `-` 만들기 전(`orderby=-created`)은 만들어진 항목별로 내림차순으로 정렬합니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | 0 기반 번호 매기기를 사용하여 응답 목록을 오프셋합니다. 예를 들어, `start=2` 세 번째로 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **필수** HTML 이스케이프 처리. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 다음과 같습니다. `name` 및 `userId`. 유일하게 지원되는 연산자는 입니다. `==` (와 같음). 예를 들어, `name==my_template` 은(는) 이라는 이름의 모든 쿼리 템플릿을 반환합니다. `my_template`. |

**요청**

다음 요청은 IMS 조직에 대해 생성된 최신 쿼리 템플릿을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 IMS 조직에 대한 쿼리 템플릿 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 IMS 조직에 대해 만든 최신 쿼리 템플릿을 반환합니다.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [쿼리 템플릿 삭제](#delete-a-specified-query-template).

### 쿼리 템플릿 만들기

에 POST 요청을 하여 쿼리 템플릿을 만들 수 있습니다. `/query-templates` 엔드포인트.

**API 형식**

```http
POST /query-templates
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sql` | 만들려는 SQL 쿼리입니다. 표준 SQL이나 매개변수 대체를 사용할 수 있습니다. SQL에서 매개 변수 대체를 사용하려면 매개 변수 키 앞에 를 추가해야 합니다. `$`. 예를 들어, `$key`및 SQL에 사용되는 매개 변수를 의 JSON 키 값 쌍으로 제공합니다. `queryParameters` 필드. 여기에 전달된 값은 템플릿에 사용되는 기본 매개 변수가 됩니다. 이러한 매개 변수를 재정의하려면 POST 요청에서 재정의해야 합니다. |
| `name` | 쿼리 템플릿의 이름입니다. |
| `queryParameters` | SQL 문의 매개 변수가 있는 값을 대체할 키 값 쌍입니다. 필요한 경우에만 **if** 제공한 SQL 내에서 매개 변수 대체 요소를 사용하고 있습니다. 이 키 값 쌍에 대해서는 값 유형 검사가 수행되지 않습니다. |

**응답**

성공적인 응답은 새로 생성된 쿼리 템플릿의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [쿼리 템플릿 삭제](#delete-a-specified-query-template).

### 지정된 쿼리 템플릿 검색

에 GET 요청을 하여 특정 쿼리 템플릿을 검색할 수 있습니다. `/query-templates/{TEMPLATE_ID}` 엔드포인트 및 요청 경로에 쿼리 템플릿의 ID 제공

**API 형식**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 다음 `id` 검색할 쿼리 템플릿의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 쿼리 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [쿼리 템플릿 삭제](#delete-a-specified-query-template).

### 지정된 쿼리 템플릿 업데이트

에 PUT 요청을 하여 특정 쿼리 템플릿을 업데이트할 수 있습니다. `/query-templates/{TEMPLATE_ID}` 엔드포인트 및 요청 경로에 쿼리 템플릿의 ID 제공

**API 형식**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 다음 `id` 검색할 쿼리 템플릿의 값입니다. |

**요청**

>[!NOTE]
>
>PUT 요청에는 sql 및 name 필드를 모두 채워야 하며 **덮어쓰기** 해당 쿼리 템플릿의 현재 콘텐츠입니다.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sql` | 만들려는 SQL 쿼리입니다. 표준 SQL이나 매개변수 대체를 사용할 수 있습니다. SQL에서 매개 변수 대체를 사용하려면 매개 변수 키 앞에 를 추가해야 합니다. `$`. 예를 들어, `$key`및 SQL에 사용되는 매개 변수를 의 JSON 키 값 쌍으로 제공합니다. `queryParameters` 필드. 여기에 전달된 값은 템플릿에 사용되는 기본 매개 변수가 됩니다. 이러한 매개 변수를 재정의하려면 POST 요청에서 재정의해야 합니다. |
| `name` | 쿼리 템플릿의 이름입니다. |
| `queryParameters` | SQL 문의 매개 변수가 있는 값을 대체할 키 값 쌍입니다. 필요한 경우에만 **if** 제공한 SQL 내에서 매개 변수 대체 요소를 사용하고 있습니다. 이 키 값 쌍에 대해서는 값 유형 검사가 수행되지 않습니다. |

**응답**

성공적인 응답은 지정된 쿼리 템플릿에 대해 업데이트된 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [쿼리 템플릿 삭제](#delete-a-specified-query-template).

### 지정된 쿼리 템플릿 삭제

에 DELETE 요청을 하여 특정 쿼리 템플릿을 삭제할 수 있습니다. `/query-templates/{TEMPLATE_ID}` 요청 경로에 쿼리 템플릿의 ID를 입력합니다.

**API 형식**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 다음 `id` 검색할 쿼리 템플릿의 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
