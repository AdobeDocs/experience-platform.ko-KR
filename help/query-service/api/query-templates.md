---
keywords: Experience Platform;home;popular topics;query service;query templates;api guide;templates;query service;
solution: Experience Platform
title: 쿼리 템플릿 API 끝점
topic-legacy: query templates
description: 다음 설명서는 쿼리 서비스 API에 대한 쿼리 템플릿을 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 쿼리 템플릿 끝점

## 샘플 API 호출

이제 사용할 헤더를 이해했으므로 [!DNL Query Service] API에 대한 호출을 시작할 준비가 되었습니다. 다음 섹션에서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다. 각 호출에는 일반 API 형식, 필수 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 쿼리 템플릿 목록 검색

`/query-templates` 종단점에 GET 요청을 함으로써 IMS 조직에 대한 모든 쿼리 템플릿 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택적*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다. |

**쿼리 매개 변수**

다음은 쿼리 템플릿 목록을 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에 사용할 수 있는 모든 쿼리 템플릿이 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 결과를 오름차순으로 정렬합니다. 만들기 전에 `-`(`orderby=-created`)을 추가하면 작성된 항목이 내림차순으로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. (*기본값:20*) |
| `start` | 0부터 시작하는 번호 매기기를 사용하여 응답 목록을 오프셋합니다. 예를 들어 `start=2`은 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값:0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **은(는) HTML을 escape해야 합니다.** 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `name` 및 `userId`입니다. 유일하게 지원되는 연산자는 `==`(과 같음)입니다. 예를 들어 `name==my_template`은 이름이 `my_template`인 모든 쿼리 템플릿을 반환합니다. |

**요청**

다음 요청은 IMS 조직에 대해 만든 최신 쿼리 템플릿을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 쿼리 템플릿 목록이 포함된 HTTP 상태 200을 반환합니다. 다음 응답은 IMS 조직에 대해 만든 최신 쿼리 템플릿을 반환합니다.

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
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
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
>`_links.delete` 값을 사용하여 쿼리 템플릿](#delete-a-specified-query-template)을(를) 삭제할 수 있습니다.[

### 쿼리 템플릿 만들기

`/query-templates` 끝점에 POST 요청을 하여 쿼리 템플릿을 만들 수 있습니다.

**API 형식**

```http
POST /query-templates
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sql` | 만들려는 SQL 쿼리입니다. |
| `name` | 쿼리 템플릿의 이름입니다. |

**응답**

성공적인 응답은 새로 만든 쿼리 템플릿에 대한 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "sql": "SELECT * FROM accounts;",
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>`_links.delete` 값을 사용하여 쿼리 템플릿](#delete-a-specified-query-template)을(를) 삭제할 수 있습니다.[

### 지정된 쿼리 템플릿 검색

`/query-templates/{TEMPLATE_ID}` 끝점에 GET 요청을 하고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 검색할 수 있습니다.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 쿼리 템플릿에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>`_links.delete` 값을 사용하여 쿼리 템플릿](#delete-a-specified-query-template)을(를) 삭제할 수 있습니다.[

### 지정된 쿼리 템플릿 업데이트

PUT 요청을 `/query-templates/{TEMPLATE_ID}` 끝점에 만들고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 업데이트할 수 있습니다.

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
>PUT 요청에는 sql 및 이름 필드를 모두 채워야 하며 **이 해당 쿼리 템플릿의 현재 내용을 덮어씁니다.**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sql` | 업데이트할 SQL 쿼리 |
| `name` | 예약된 쿼리의 이름입니다. |

**응답**

성공적인 응답은 지정된 쿼리 템플릿에 대한 업데이트된 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다.

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>`_links.delete` 값을 사용하여 쿼리 템플릿](#delete-a-specified-query-template)을(를) 삭제할 수 있습니다.[

### 지정된 쿼리 템플릿 삭제

DELETE 요청을 `/query-templates/{TEMPLATE_ID}`에 수행하고 요청 경로에 쿼리 템플릿의 ID를 제공하여 특정 쿼리 템플릿을 삭제할 수 있습니다.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
