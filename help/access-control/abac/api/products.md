---
keywords: Experience Platform;홈;인기 항목;api;속성 기반 액세스 제어;속성 기반 액세스 제어
solution: Experience Platform
title: 제품 API 엔드포인트
description: 속성 기반 액세스 제어 API의 /products 엔드포인트를 사용하면 Adobe Experience Platform에서 제품을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 3%

---

# 제품 끝점

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 미국 기반 의료 고객 제한된 릴리스에서 사용할 수 있습니다. 이 기능은 완전히 릴리스되면 모든 Real-time Customer Data Platform 고객이 사용할 수 있습니다.

다음 `/products` 특성 기반 액세스 제어 API의 종단점을 사용하면 조직의 제품과 연결된 권한 카테고리 및 권한 세트뿐만 아니라 제품을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 속성 기반 액세스 제어 API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 권한 있는 제품 목록 검색 {#list}

에 GET 요청을 수행하여 권한 있는 제품 목록을 검색할 수 있습니다 `/products` 엔드포인트.

**API 형식**

```http
GET /products/
```

**요청**

다음 요청은 조직에 속한 권한 있는 제품 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 조직에 속하는 권한 있는 제품 목록을 반환합니다.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 쿼리된 제품의 해당 ID입니다. |
| `name` | 쿼리된 제품의 이름입니다. |
| `serviceCode` | 쿼리된 제품의 해당 서비스 코드입니다. |

## 제품 ID별로 권한 카테고리 조회

에 GET 요청을 수행하여 주어진 제품에 대한 권한 카테고리를 찾을 수 있습니다 `/products/{PRODUCT_ID}/categories` 제품 ID를 지정하는 동안 끝점입니다.

**API 형식**

```http
GET /products/{PRODUCT_ID}/categories
```

| 매개 변수 | 설명 |
| --- | --- |
| {PRODUCT_ID} | 조회할 권한 카테고리와 연결된 제품의 ID입니다. |

**요청**

다음 요청은 와 관련된 권한 카테고리를 검색합니다 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 쿼리한 제품 ID와 연결된 권한 카테고리를 반환합니다.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `category` | 쿼리된 제품 ID 내에서 사용할 수 있는 권한 카테고리입니다. |
| `name` | 권한 카테고리의 이름입니다. |

## 제품 ID별로 권한 집합 조회

에 GET 요청을 수행하여 주어진 제품에 대한 권한 집합을 조회할 수 있습니다 `/products/{PRODUCT_ID}/permission-sets` 제품 ID를 지정하는 동안 끝점입니다.

**API 형식**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 매개 변수 | 설명 |
| --- | --- |
| {PRODUCT_ID} | 조회하려는 권한 세트와 연결된 제품의 ID입니다. |

**요청**

다음 요청은 와 연결된 권한 집합을 검색합니다 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 쿼리한 제품 ID와 연결된 권한 집합을 반환합니다.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `permission-sets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `id` | 쿼리된 권한 집합의 해당 ID입니다. |
| `name` | 쿼리된 권한 집합의 해당 이름입니다. |
| `category` | 사용 가능한 권한 카테고리입니다. |
| `permissions` | 사용 권한에는 샌드박스 만들기, 스키마 정의, 데이터 세트 관리 등 플랫폼 기능을 보거나 사용하는 기능이 포함됩니다. |
| `permissions.resource` | 주체가 액세스할 수 있거나 액세스할 수 없는 자산 또는 개체입니다. 리소스는 파일, 애플리케이션, 서버 또는 API일 수 있습니다. |
| `permissions.actions` | 질의한 리소스에 대해 주체가 수행할 수 있는 작업입니다. 가능한 값은 다음과 같습니다. `view`, `read`, `create`, `edit`, 및 `delete` |
