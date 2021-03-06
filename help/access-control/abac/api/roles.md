---
keywords: Experience Platform;홈;인기 항목;api;속성 기반 액세스 제어;속성 기반 액세스 제어
solution: Experience Platform
title: 역할 API 끝점
description: 속성 기반 액세스 제어 API의 /roles 엔드포인트를 사용하면 Adobe Experience Platform에서 역할을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 3%

---

# 역할 끝점

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 미국 기반 의료 고객 제한된 릴리스에서 사용할 수 있습니다. 이 기능은 완전히 릴리스되면 모든 Real-time Customer Data Platform 고객이 사용할 수 있습니다.

역할은 관리자, 전문가 또는 최종 사용자가 조직의 리소스에 대한 액세스를 정의합니다. 역할 기반 액세스 제어 환경에서 사용자 액세스 프로비저닝은 일반적인 책임 및 요구 사항을 통해 그룹화됩니다. 역할에는 주어진 권한 세트가 있으며 필요한 보기 또는 쓰기 액세스 범위에 따라 조직의 구성원을 하나 이상의 역할에 할당할 수 있습니다.

다음 `/roles` 특성 기반 액세스 제어 API의 종단점을 사용하면 조직의 역할을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 속성 기반 액세스 제어 API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 역할 목록 검색 {#list}

에 GET 요청을 작성하여 조직에 속한 모든 기존 역할을 나열할 수 있습니다 `/roles` 엔드포인트.

**API 형식**

```http
GET /roles/
```

**요청**

다음 요청은 조직에 속하는 역할 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 해당 역할 유형, 권한 세트 및 제목 속성에 대한 정보를 포함하여 조직의 역할 목록을 반환합니다.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 역할에 해당하는 ID입니다. 이 ID는 자동으로 생성됩니다. |
| `name` | 역할의 이름입니다. |
| `description` | 설명 속성은 역할에 대한 추가 정보를 제공합니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |
| `permissionSets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `sandboxes` | 이 속성은 특정 역할에 대해 제공된 조직 내의 샌드박스를 표시합니다. |
| `subjectAttributes` | 주체가 액세스할 수 있는 플랫폼 리소스와 주체 간의 상관관계를 나타내는 특성입니다. |
| `subjectAttributes.labels` | 쿼리된 역할에 적용된 데이터 사용 레이블을 표시합니다. |

## 역할 조회 {#lookup}

해당 역할이 포함된 GET 요청을 작성하여 개별 역할을 조회할 수 있습니다 `roleId` 를 입력합니다.

**API 형식**

```http
GET /roles/{ROLE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| {ROLE_ID} | 조회할 역할의 ID입니다. |

**요청**

다음 요청은 다음에 대한 정보를 검색합니다. `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 해당 역할 유형, 권한 집합 및 제목 속성에 대한 정보를 포함하여 쿼리된 역할 ID에 대한 세부 정보를 반환합니다.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 역할에 해당하는 ID입니다. 이 ID는 자동으로 생성됩니다. |
| `name` | 역할의 이름입니다. |
| `description` | 설명 속성은 역할에 대한 추가 정보를 제공합니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |
| `permissionSets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `sandboxes` | 이 속성은 특정 역할에 대해 제공된 조직 내의 샌드박스를 표시합니다. |
| `subjectAttributes` | 주체가 액세스할 수 있는 플랫폼 리소스와 주체 간의 상관관계를 나타내는 특성입니다. |
| `subjectAttributes.labels` | 쿼리된 역할에 적용된 데이터 사용 레이블을 표시합니다. |

## 역할 ID별로 주제 조회

에 GET 요청을 수행하여 피사체를 검색할 수도 있습니다 `/roles` {ROLE_ID}을(를) 제공하는 동안 끝점입니다.

**API 형식**

```http
GET /roles/{ROLE_ID}/subjects
```

| 매개 변수 | 설명 |
| --- | --- |
| {ROLE_ID} | 조회하려는 주체와 연관된 역할의 ID입니다. |

**요청**

다음 요청은 와 연관된 주제를 검색합니다. `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 해당 제목 ID 및 제목 유형을 포함하여 쿼리된 역할 ID와 연결된 주제를 반환합니다.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `roleId` | 쿼리된 주체와 연관된 역할 ID입니다. |
| `subjectType` | 쿼리된 주체의 유형입니다. |
| `subjectId` | 쿼리된 주제에 해당하는 ID입니다. |

## 역할 만들기 {#create}

새 역할을 만들려면, `/roles` 역할 이름, 설명 및 역할 유형에 대한 값을 제공하는 중 끝점입니다.

**API 형식**

```http
POST /roles/
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 역할의 이름입니다. 역할에 대한 정보를 조회하는 데 사용할 수 있으므로 역할 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 역할에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 수사적 값입니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |

**응답**

성공적인 응답은 해당 역할 ID와 역할 유형, 권한 세트 및 제목 속성에 대한 정보를 사용하여 새로 만든 역할을 반환합니다.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 역할에 해당하는 ID입니다. 이 ID는 자동으로 생성됩니다. |
| `name` | 역할의 이름입니다. |
| `description` | 설명 속성은 역할에 대한 추가 정보를 제공합니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |
| `permissionSets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `sandboxes` | 이 속성은 특정 역할에 대해 제공된 조직 내의 샌드박스를 표시합니다. |
| `subjectAttributes` | 주체가 액세스할 수 있는 플랫폼 리소스와 주체 간의 상관관계를 나타내는 특성입니다. |
| `subjectAttributes.labels` | 쿼리된 역할에 적용된 데이터 사용 레이블을 표시합니다. |

## 역할 업데이트 {#patch}

에 PATCH 요청을 작성하여 역할의 속성을 업데이트할 수 있습니다 `/roles` 적용할 작업에 해당 역할 ID 및 값을 제공하는 끝점입니다.

**API 형식**

```http
PATCH /roles/{ROLE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| {ROLE_ID} | 업데이트할 역할의 ID입니다. |

**요청**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| 작업 | 설명 |
| --- | --- |
| `op` | 역할을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적으로 응답하면 업데이트하도록 선택한 속성에 대한 새 값을 포함하여 업데이트된 역할이 반환됩니다.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 역할에 해당하는 ID입니다. 이 ID는 자동으로 생성됩니다. |
| `name` | 역할의 이름입니다. |
| `description` | 설명 속성은 역할에 대한 추가 정보를 제공합니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |
| `permissionSets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `sandboxes` | 이 속성은 특정 역할에 대해 제공된 조직 내의 샌드박스를 표시합니다. |
| `subjectAttributes` | 주체가 액세스할 수 있는 플랫폼 리소스와 주체 간의 상관관계를 나타내는 특성입니다. |
| `subjectAttributes.labels` | 쿼리된 역할에 적용된 데이터 사용 레이블을 표시합니다. |

## 역할 ID별 역할 업데이트 {#put}

에 PUT 요청을 작성하여 역할을 업데이트할 수 있습니다 `/roles` 업데이트하려는 역할에 해당하는 역할 ID를 지정하는 끝점입니다.

**API 형식**

```http
PUT /roles/{ROLE_ID}
```

**요청**

다음 요청은 역할 ID의 이름, 설명 및 역할 유형을 업데이트합니다. `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `name` | 역할의 업데이트된 이름입니다. |
| `description` | 역할에 대한 업데이트된 설명입니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |

**응답**

성공적으로 수행하면 이름, 설명 및 역할 유형에 대한 새 값을 포함하여 업데이트된 역할이 반환됩니다.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 역할에 해당하는 ID입니다. 이 ID는 자동으로 생성됩니다. |
| `name` | 역할의 이름입니다. |
| `description` | 설명 속성은 역할에 대한 추가 정보를 제공합니다. |
| `roleType` | 지정된 역할 유형입니다. 역할 유형에 사용할 수 있는 값은 다음과 같습니다. `user-defined` 및 `system-defined`. |
| `permissionSets` | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 지정 역할을 만들 수 있도록 해줍니다. |
| `sandboxes` | 이 속성은 특정 역할에 대해 제공된 조직 내의 샌드박스를 표시합니다. |
| `subjectAttributes` | 주체가 액세스할 수 있는 플랫폼 리소스와 주체 간의 상관관계를 나타내는 특성입니다. |
| `subjectAttributes.labels` | 쿼리된 역할에 적용된 데이터 사용 레이블을 표시합니다. |

## 역할 ID별로 주체 업데이트

역할과 연관된 주제를 업데이트하려면 PATCH 요청에서 `/roles` 업데이트하려는 대상의 역할 ID를 제공하는 중 끝점입니다.

**API 형식**

```http
PATCH /roles/{ROLE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| {ROLE_ID} | 업데이트할 주체와 연관된 역할 ID입니다. |

**요청**

다음 요청은 관련 주제를 업데이트합니다 `{ROLE_ID}`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| 작업 | 설명 |
| --- | --- |
| `op` | 역할을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 쿼리된 역할 ID와 연결된 업데이트된 주제를 반환합니다.

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `subjectId` | 주체의 ID입니다. |
| `subjectType` | 제목 유형입니다. |

## 역할 삭제 {#delete}

역할을 삭제하려면 다음과 같이 DELETE 요청을 하십시오 `/roles` 삭제할 역할의 ID를 지정하는 동안 끝점입니다.

**API 형식**

```http
DELETE /roles/{ROLE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| {ROLE_ID} | 삭제할 역할의 ID입니다. |

**요청**

다음 요청은 ID가 인 역할을 삭제합니다 `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

역할에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 역할이 관리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받게 됩니다.
