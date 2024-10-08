---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 템플릿;api 안내서;템플릿;쿼리 서비스;
solution: Experience Platform
title: 쿼리 템플릿 API 끝점
description: 이 안내서에서는 쿼리 서비스 API를 사용하여 수행할 수 있는 다양한 쿼리 템플릿 API 호출에 대해 자세히 설명합니다.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 2%

---

# 쿼리 템플릿 끝점

## 샘플 API 호출

다음 섹션에서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출에 대해 설명합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

Experience Platform UI를 통해 템플릿을 만드는 방법에 대한 자세한 내용은 [UI 쿼리 템플릿 설명서](../ui/query-templates.md)를 참조하십시오.

### 쿼리 템플릿 목록 검색

`/query-templates` 끝점에 대한 GET 요청을 통해 조직에 대한 모든 쿼리 템플릿 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택 사항*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다. 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 쿼리 템플릿을 나열하기 위해 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 쿼리 템플릿을 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 만들어진 항목별로 오름차순으로 결과를 정렬합니다. 만들기 전에 `-`을(를) 추가하면(`orderby=-created`) 내림차순으로 만들어진 항목별로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | ISO 형식 타임스탬프를 지정하여 결과 순서를 지정합니다. 시작 날짜를 지정하지 않으면 API 호출이 가장 오래 전에 만든 템플릿을 먼저 반환한 다음 더 최근 결과를 계속 나열합니다.<br> ISO 타임스탬프를 사용하면 날짜 및 시간에 서로 다른 수준의 세부기간을 사용할 수 있습니다. 기본 ISO 타임스탬프는 `2020-09-07` 형식을 사용하여 2020년 9월 7일의 날짜를 나타냅니다. 보다 복잡한 예제는 `2022-11-05T08:15:30-05:00`(으)로 작성되며 2022년 11월 5일 오전 8:15:30(미국 동부 표준시)에 해당합니다. 시간대는 UTC 오프셋을 사용하여 제공될 수 있으며 접미사 &quot;Z&quot;(`2020-01-01T01:01:01Z`)로 표시됩니다. 시간대가 제공되지 않으면 기본값은 0입니다. |
| `property` | 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프해야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `name` 및 `userId`입니다. 지원되는 유일한 연산자는 `==`(과 같음)입니다. 예를 들어 `name==my_template`은(는) 이름이 `my_template`인 모든 쿼리 템플릿을 반환합니다. |

**요청**

다음 요청은 조직에 대해 생성된 최신 쿼리 템플릿을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 조직에 대한 쿼리 템플릿 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 조직에 대해 만든 최신 쿼리 템플릿을 반환합니다.

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
>`_links.delete`의 값을 사용하여 [쿼리 템플릿을 삭제](#delete-a-specified-query-template)할 수 있습니다.

### 쿼리 템플릿 만들기

`/query-templates` 끝점에 대한 POST 요청을 만들어 쿼리 템플릿을 만들 수 있습니다.

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
| `sql` | 만들려는 SQL 쿼리입니다. 표준 SQL이나 매개변수 대체를 사용할 수 있습니다. SQL에서 매개 변수 대체를 사용하려면 매개 변수 키 앞에 `$`을(를) 추가해야 합니다. 예를 들어 `$key`을(를) 사용하고 SQL에서 사용되는 매개 변수를 `queryParameters` 필드에 JSON 키 값 쌍으로 제공합니다. 여기에 전달된 값은 템플릿에 사용되는 기본 매개 변수가 됩니다. 이러한 매개 변수를 재정의하려면 POST 요청에서 재정의해야 합니다. |
| `name` | 쿼리 템플릿의 이름입니다. |
| `queryParameters` | SQL 문의 매개 변수가 있는 값을 대체할 키 값 쌍입니다. 입력한 SQL 내에서 매개 변수 대체 요소를 사용하는 경우 **if**&#x200B;만 필요합니다. 이 키 값 쌍에 대해서는 값 유형 검사가 수행되지 않습니다. |

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
>`_links.delete`의 값을 사용하여 [쿼리 템플릿을 삭제](#delete-a-specified-query-template)할 수 있습니다.

### 지정된 쿼리 템플릿 검색

`/query-templates/{TEMPLATE_ID}` 끝점에 대한 GET 요청을 만들고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 검색할 수 있습니다.

**API 형식**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 검색할 쿼리 템플릿의 `id` 값입니다. |

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
>`_links.delete`의 값을 사용하여 [쿼리 템플릿을 삭제](#delete-a-specified-query-template)할 수 있습니다.

### 지정된 쿼리 템플릿 업데이트

`/query-templates/{TEMPLATE_ID}` 끝점에 PUT 요청을 하고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 업데이트할 수 있습니다.

**API 형식**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 검색할 쿼리 템플릿의 `id` 값입니다. |

**요청**

>[!NOTE]
>
>PUT 요청을 사용하려면 sql 및 name 필드를 모두 채워야 하며, 해당 쿼리 템플릿의 현재 콘텐츠를 **덮어씁니다**.

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
| `sql` | 만들려는 SQL 쿼리입니다. 표준 SQL이나 매개변수 대체를 사용할 수 있습니다. SQL에서 매개 변수 대체를 사용하려면 매개 변수 키 앞에 `$`을(를) 추가해야 합니다. 예를 들어 `$key`을(를) 사용하고 SQL에서 사용되는 매개 변수를 `queryParameters` 필드에 JSON 키 값 쌍으로 제공합니다. 여기에 전달된 값은 템플릿에 사용되는 기본 매개 변수가 됩니다. 이러한 매개 변수를 재정의하려면 POST 요청에서 재정의해야 합니다. |
| `name` | 쿼리 템플릿의 이름입니다. |
| `queryParameters` | SQL 문의 매개 변수가 있는 값을 대체할 키 값 쌍입니다. 입력한 SQL 내에서 매개 변수 대체 요소를 사용하는 경우 **if**&#x200B;만 필요합니다. 이 키 값 쌍에 대해서는 값 유형 검사가 수행되지 않습니다. |

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
>`_links.delete`의 값을 사용하여 [쿼리 템플릿을 삭제](#delete-a-specified-query-template)할 수 있습니다.

### 지정된 쿼리 템플릿 삭제

`/query-templates/{TEMPLATE_ID}`에 DELETE 요청을 하고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 검색할 쿼리 템플릿의 `id` 값입니다. |

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
