---
title: 통합 태그 엔드포인트
description: Adobe Experience Platform API를 사용하여 태그 범주와 태그를 만들고, 업데이트하고, 관리하고, 삭제하는 방법에 대해 알아봅니다.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 3%

---

# 통합 태그 엔드포인트

>[!IMPORTANT]
>
>이 끝점 집합의 끝점 URL은 `https://experience.adobe.io`입니다.

태그는 메타데이터 분류를 관리하여 비즈니스 객체를 보다 쉽게 검색하고 분류할 수 있도록 해 주는 기능입니다. 그런 다음 이러한 태그를 태그 범주에 추가하여 추가 그룹으로 구성할 수 있습니다.

이 안내서에서는 태그와 태그 범주를 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출이 포함되어 있습니다.

## 시작하기

이 안내서에 사용되는 끝점은 Adobe Experience Platform API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 필요한 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 할 중요한 정보를 확인하십시오

### 용어집

다음 용어집에서는 **tag**&#x200B;과(와) **tag 범주** 간의 차이점을 강조 표시합니다.

- **태그**: 태그를 사용하면 비즈니스 개체의 메타데이터 분류법을 관리할 수 있으므로 더 쉽게 검색하고 분류할 수 있도록 이러한 개체를 분류할 수 있습니다.
   - **분류되지 않은 태그**: 분류되지 않은 태그는 태그 범주에 속하지 않는 태그입니다. 기본적으로 생성된 태그는 분류되지 않습니다.
- **태그 범주**: 태그 범주를 사용하면 태그를 의미 있는 집합으로 그룹화할 수 있으므로 태그의 목적에 더 많은 컨텍스트를 제공할 수 있습니다.

## 태그 범주 목록 검색 {#get-tag-categories}

`/tagCategory` 끝점에 대한 GET 요청을 통해 조직에 속한 태그 범주 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

태그 범주를 검색할 때 다음과 같은 선택적 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `start` | 결과 목록이 시작되는 위치입니다. 이를 사용하여 결과의 페이지 매김을 위한 시작 색인을 나타낼 수 있습니다. | `start=a` |
| `limit` | 페이지당 검색할 최대 태그 범주 수입니다. | `limit=20` |
| `property` | 태그 범주를 검색할 때 필터링할 속성입니다. 지원되는 값은 다음과 같습니다. &lt;ul≥<li>`name`: 태그 범주의 이름입니다.</li></ul> | `property=name==category` |
| `sortBy` | 태그 범주가 정렬되는 순서. 지원되는 값은 `name`, `createdAt` 및 `modifiedAt`입니다. | `sortBy=name` |
| `sortOrder` | 태그 범주가 정렬되는 방향입니다. 지원되는 값은 `asc` 및 `desc`입니다. | `sortOrder=asc` |

**요청**

+++조직의 모든 태그 범주를 나열하는 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공적인 응답은 조직의 모든 태그 범주 목록과 함께 HTTP 상태 200을 반환합니다.

+++조직의 모든 태그 범주 목록을 포함하는 샘플 응답입니다.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## 새 태그 범주 만들기 {#create-tag-category}

>[!IMPORTANT]
>
>시스템 관리자와 제품 관리자만 이 API 호출을 사용할 수 있습니다.

`/tagCategory` 끝점에 POST 요청을 하여 새 태그 범주를 만들 수 있습니다.

**API 형식**

```http
POST /tagCategory
```

**요청**

+++새 태그 카테고리를 만드는 샘플 요청입니다.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 만들려는 태그 범주의 이름입니다. |
| `description` | 만들려는 태그 범주에 대한 설명입니다. |

+++

**응답**

샘플 응답은 새로 만든 태그 카테고리의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++새로 만든 태그 카테고리에 대한 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 특정 태그 범주 검색 {#get-tag-category}

`/tagCategory` 끝점에 GET 요청을 하고 태그 범주의 ID를 지정하여 조직에 속한 특정 태그 범주를 검색할 수 있습니다.

**API 형식**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 검색 중인 태그 범주의 ID입니다. |

**요청**

+++특정 태그 카테고리를 검색하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공한 응답은 지정된 태그 카테고리의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++지정된 태그 카테고리에 대한 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 요청한 태그 범주의 ID입니다. |
| `name` | 요청한 태그 범주의 이름입니다. |
| `description` | 요청된 태그 범주에 대한 설명입니다. |
| `createdBy` | 태그 카테고리를 만든 사용자의 ID입니다. |
| `createdAt` | 태그 카테고리가 생성된 시점의 타임스탬프입니다. |
| `modifiedBy` | 태그 카테고리를 마지막으로 업데이트한 사용자의 ID입니다. |
| `modifiedAt` | 태그 범주가 마지막으로 업데이트된 시간의 타임스탬프입니다. |
| `tagCount` | 태그 범주에 속하는 태그 수입니다. |

+++

## 특정 태그 범주 업데이트 {#update-tag-category}

>[!IMPORTANT]
>
>시스템 관리자와 제품 관리자만 이 API 호출을 사용할 수 있습니다.

`/tagCategory` 끝점에 PATCH 요청을 하고 태그 범주의 ID를 지정하여 조직에 속한 특정 태그 범주의 세부 정보를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 검색 중인 태그 범주의 ID입니다. |

**요청**

+++특정 태그 카테고리를 업데이트하기 위한 샘플 요청

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `op` | 완료된 작업입니다. 특정 태그 범주를 업데이트하려면 이 값을 `replace`(으)로 설정하십시오. |
| `path` | 업데이트할 필드의 경로입니다. 지원되는 값은 `name` 및 `description`입니다. |
| `value` | 업데이트할 필드의 업데이트된 값. |
| `from` | 업데이트할 필드의 원래 값입니다. |

+++

**응답**

새로 업데이트된 태그 카테고리에 대한 정보가 포함된 성공적인 응답 HTTP 상태 200입니다.

+++새로 업데이트된 태그 카테고리에 대한 세부 정보가 포함된 샘플 응답.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 특정 태그 범주 삭제 {#delete-tag-category}

>[!IMPORTANT]
>
>시스템 관리자와 제품 관리자만 이 API 호출을 사용할 수 있습니다.

`/tagCategory` 끝점에 DELETE 요청을 하고 태그 범주의 ID를 지정하여 조직에 속한 특정 태그 범주를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 검색 중인 태그 범주의 ID입니다. |

**요청**

+++특정 태그 카테고리 삭제를 위한 샘플 요청

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공적인 응답은 빈 응답과 함께 HTTP 상태 200을 반환합니다.

## 태그 목록 검색 {#get-tags}

`/tags` 끝점과 태그 범주의 ID에 대한 GET 요청을 통해 조직에 속한 태그 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

태그를 검색할 때 다음과 같은 선택적 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개 변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `start` | 결과 목록이 시작되는 위치입니다. 이를 사용하여 결과의 페이지 매김을 위한 시작 색인을 나타낼 수 있습니다. | `start=a` |
| `limit` | 페이지당 검색할 최대 태그 수입니다. | `limit=20` |
| `property` | 태그를 검색할 때 필터링할 속성입니다. 지원되는 값은 다음과 같습니다.<ul><li>`name`: 태그의 이름입니다.</li><li>`archived`: 태그가 보관되었는지 또는 보관 해제되었는지 여부입니다. 이 값은 `true` 또는 `false` 중 하나로 설정할 수 있습니다.</li><li>`tagCategoryId`: 태그가 속한 태그 범주의 ID입니다.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | 태그를 정렬하는 순서. 지원되는 값은 `name`, `createdAt` 및 `modifiedAt`입니다. | `sortBy=name` |
| `sortOrder` | 태그 범주가 정렬되는 방향입니다. 지원되는 값은 `asc` 및 `desc`입니다. | `sortOrder=asc` |


**요청**

+++특정 태그 범주에 속하는 모든 태그를 검색하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공적인 응답은 해당 태그 범주에 속하는 태그의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 태그에 대한 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## 새 태그 만들기 {#create-tag}

>[!IMPORTANT]
>
>시스템 관리자와 제품 관리자만 이 API 호출을 사용하여 지정된 태그 범주에 새 태그를 만들 수 있습니다.
>
>분류되지 않은 태그를 만드는 경우 **not**&#x200B;은(는) 관리자 권한이 필요합니다.

`/tags` 끝점에 대한 POST 요청을 수행하여 새 태그를 만들 수 있습니다.

**API 형식**

```http
POST /tags
```

**요청**

+++새 태그를 만드는 샘플 요청입니다.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | **필수**. 만들려는 태그의 이름입니다. |
| `tagCategoryId` | *선택 사항*. 태그가 속할 태그 범주의 ID입니다. 지정하지 않으면 분류되지 않은 카테고리의 일부로 태그가 만들어집니다. |

+++

**응답**

성공한 응답은 새로 만든 태그의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

+++새로 만든 태그의 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `name` | 새로 만든 태그의 이름입니다. |
| `id` | 새로 만든 태그의 ID. |
| `org` | 태그가 속한 조직의 ID입니다. |
| `createdAt` | 태그가 생성된 시점의 타임스탬프입니다. |
| `createdBy` | 태그를 만든 사용자의 ID입니다. |
| `modifiedAt` | 태그가 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `modifiedBy` | 태그를 마지막으로 업데이트한 사용자의 ID입니다. |
| `tagCategoryId` | 태그가 속한 태그 범주의 ID입니다. |
| `tagCategoryName` | 태그가 속한 태그 범주의 이름입니다. |

+++

## 특정 태그 검색 {#get-tag}

`/tags` 끝점에 대한 GET 요청을 만들고 검색할 태그의 ID를 지정하여 조직에 속한 특정 태그를 검색할 수 있습니다.

**API 형식**

```http
GET /tags/{TAG_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_ID}` | 검색 중인 태그의 ID. |

**요청**

+++특정 태그를 검색하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공한 응답은 지정된 태그의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++지정된 태그의 세부 정보를 포함하는 샘플 응답입니다.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `name` | 검색한 태그의 이름입니다. |
| `id` | 검색한 태그의 ID. |
| `org` | 태그가 속한 조직의 ID입니다. |
| `createdAt` | 태그가 생성된 시점의 타임스탬프입니다. |
| `createdBy` | 태그를 만든 사용자의 ID입니다. |
| `modifiedAt` | 태그가 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `modifiedBy` | 태그를 마지막으로 업데이트한 사용자의 ID입니다. |
| `tagCategoryId` | 태그가 속한 태그 범주의 ID입니다. |
| `tagCategoryName` | 태그가 속한 태그 범주의 이름입니다. |
| `archived` | 태그의 보관 상태입니다. `true`(으)로 설정하면 태그가 보관됩니다. |

+++

## 태그 유효성 검사 {#validate-tags}

`/tags/validate` 끝점에 대한 POST 요청을 통해 태그가 있는지 확인할 수 있습니다.

**API 형식**

```http
POST /tags/validate
```

**요청**

+++제공된 태그 ID의 유효성을 검사하기 위한 샘플 요청입니다.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `ids` | 유효성을 검사할 태그 ID 목록이 포함된 배열입니다. |
| `entity` | 유효성 검사를 요청하는 엔티티입니다. 이 매개 변수에 `{API_KEY}` 값을 사용할 수 있습니다. |

+++

**응답**

성공적인 응답은 유효한 태그와 유효하지 않은 태그에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

+++유효하고 잘못된 태그를 표시하는 샘플 응답입니다.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `invalidTags` | 잘못된 태그 ID 목록이 포함된 배열입니다. |
| `validTags` | 유효한 태그 ID 목록이 포함된 배열입니다. |

+++

## 특정 태그 업데이트 {#update-tag}

`/tags` 끝점에 PATCH 요청을 하고 업데이트할 태그의 ID를 제공하여 지정된 태그를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /tags/{TAG_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_ID}` | 업데이트 중인 태그의 ID입니다. |

**요청**

+++특정 태그를 업데이트하기 위한 샘플 요청

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 수행해야 하는 작업입니다. 이 사용 사례에서는 항상 `replace`(으)로 설정됩니다. |
| `path` | 업데이트할 필드의 경로입니다. 지원되는 값은 `name`, `archived` 및 `tagCategoryId`입니다. |
| `value` | 업데이트할 필드의 업데이트된 값. |
| `from` | 업데이트할 필드의 원래 값입니다. |

+++

**응답**

성공한 응답은 새로 업데이트된 태그의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++업데이트된 태그의 세부 정보가 포함된 샘플 응답입니다.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## 특정 태그 삭제 {#delete-tag}

>[!IMPORTANT]
>
>시스템 관리자와 제품 관리자만 이 API 호출을 사용할 수 있습니다.
>
>또한 태그를 삭제하려면 **태그를 비즈니스 개체에 연결할 수**&#x200B;없으며 **반드시**&#x200B;보관해야 합니다. [태그 끝점 업데이트](#update-tag)를 사용하여 태그를 보관할 수 있습니다.

`/tags` 끝점에 DELETE 태그를 만들고 삭제할 태그의 ID를 지정하여 특정 태그를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /tags/{TAG_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TAG_ID}` | 삭제 중인 태그의 ID. |

**요청**

+++특정 태그 삭제에 대한 샘플 요청

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**응답**

성공적인 응답은 빈 응답과 함께 HTTP 상태 200을 반환합니다.

## 다음 단계

이 안내서를 읽은 후에는 Adobe Experience Platform API를 사용하여 태그와 태그 범주를 만들고, 관리하고, 삭제하는 방법을 더 잘 이해할 수 있습니다. UI를 사용하여 태그를 관리하는 방법에 대한 자세한 내용은 [태그 관리 가이드](../ui/managing-tags.md)를 참조하십시오. UI를 사용하여 태그 범주를 관리하는 방법에 대한 자세한 내용은 [태그 범주 안내서](../ui/tags-categories.md)를 참조하십시오.
