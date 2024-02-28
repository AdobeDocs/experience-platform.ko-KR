---
keywords: Experience Platform;홈;인기 항목;api;속성 기반 액세스 제어;속성 기반 액세스 제어
solution: Experience Platform
title: 액세스 제어 정책 API 끝점
description: 속성 기반 액세스 제어 API의 /policies 끝점을 사용하면 Adobe Experience Platform에서 정책을 프로그래밍 방식으로 관리할 수 있습니다.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 2%

---

# 액세스 제어 정책 끝점

>[!NOTE]
>
>사용자 토큰이 전달되는 경우 토큰의 사용자는 요청된 조직에 대한 &quot;조직 관리자&quot; 역할이 있어야 합니다.

액세스 제어 정책은 속성을 함께 가져와서 허용 가능한 작업과 허용 불가능한 작업을 설정하는 명령문입니다. 이러한 정책은 로컬 또는 전역일 수 있으며 다른 정책을 무시할 수 있습니다. 다음 `/policies` 속성 기반 액세스 제어 API의 끝점을 사용하면 정책을 제어하는 규칙과 해당 제목 조건에 대한 정보를 포함하여 정책을 프로그래밍 방식으로 관리할 수 있습니다.

>[!IMPORTANT]
>
>이 끝점을 와 혼동하면 안 됩니다. `/policies` 의 엔드포인트 [정책 서비스 API](../../../data-governance/api/policies.md): 데이터 사용 정책을 관리하는 데 사용됩니다.

## 시작하기

이 안내서에 사용된 API 끝점은 특성 기반 액세스 제어 API의 일부입니다. 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 정책 목록 검색 {#list}

에 GET 요청 `/policies` 조직의 기존 정책을 모두 나열하는 끝점입니다.

**API 형식**

```http
GET /policies
```

**요청**

다음 요청은 기존 정책 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공한 응답은 기존 정책 목록을 반환합니다.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 정책에 해당하는 ID입니다. 이 식별자는 자동으로 생성되며, 정책을 조회, 업데이트 및 삭제하는 데 사용할 수 있습니다. |
| `imsOrgId` | 쿼리된 정책에 액세스할 수 있는 조직입니다. |
| `createdBy` | 정책을 만든 사용자의 ID입니다. |
| `createdAt` | 정책이 생성된 시간입니다. 다음 `createdAt` 속성은 unix epoch 타임스탬프에 표시됩니다. |
| `modifiedBy` | 정책을 마지막으로 업데이트한 사용자의 ID입니다. |
| `modifiedAt` | 정책이 마지막으로 업데이트된 시간입니다. 다음 `modifiedAt` 속성은 unix epoch 타임스탬프에 표시됩니다. |
| `name` | 정책의 이름입니다. |
| `description` | (선택 사항) 특정 정책에 대한 추가 정보를 제공하기 위해 추가할 수 있는 속성입니다. |
| `status` | 정책의 현재 상태. 이 속성은 정책이 현재 있는지 여부를 정의합니다. `active` 또는 `inactive`. |
| `subjectCondition` | 주제에 적용되는 조건. 주제는 작업을 수행하기 위해 리소스에 대한 액세스를 요청하는 특정 속성을 가진 사용자입니다. 이 경우, `subjectCondition` 제목 속성에 적용되는 쿼리와 유사한 조건입니다. |
| `rules` | 정책을 정의하는 규칙 세트입니다. 규칙은 주체가 리소스에 대한 작업을 성공적으로 수행하기 위해 인증되는 속성 조합을 정의합니다. |
| `rules.effect` | 다음에 대한 값을 고려한 후 발생하는 효과 `action`, `condition` 및 `resource`. 가능한 값은 다음과 같습니다. `permit`, `deny`, 또는 `indeterminate`. |
| `rules.resource` | 주체가 액세스할 수 있거나 액세스할 수 없는 에셋 또는 개체입니다.  리소스는 파일, 애플리케이션, 서버 또는 API일 수 있습니다. |
| `rules.condition` | 리소스에 적용된 조건. 예를 들어 리소스가 스키마인 경우, 스키마에 해당 스키마에 대한 작업이 허용되는지 또는 허용되지 않는지 여부에 기여하는 특정 레이블이 스키마에 적용될 수 있습니다. |
| `rules.action` | 조회한 리소스에 대해 주체가 수행할 수 있는 작업입니다. 가능한 값은 다음과 같습니다. `read`, `create`, `edit`, 및 `delete`. |

## ID별로 정책 세부 정보 조회 {#lookup}

에 GET 요청 `/policies` 개별 정책에 대한 정보를 검색하기 위해 요청 경로에 정책 ID를 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
GET /policies/{POLICY_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {POLICY_ID} | 검색할 정책의 ID입니다. |

**요청**

다음 요청은 개별 정책에 대한 정보를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

요청이 성공하면 쿼리된 정책 ID에 대한 정보가 반환됩니다.

```json
{
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 정책에 해당하는 ID입니다. 이 식별자는 자동으로 생성되며, 정책을 조회, 업데이트 및 삭제하는 데 사용할 수 있습니다. |
| `imsOrgId` | 쿼리된 정책에 액세스할 수 있는 조직입니다. |
| `createdBy` | 정책을 만든 사용자의 ID입니다. |
| `createdAt` | 정책이 생성된 시간입니다. 다음 `createdAt` 속성은 unix epoch 타임스탬프에 표시됩니다. |
| `modifiedBy` | 정책을 마지막으로 업데이트한 사용자의 ID입니다. |
| `modifiedAt` | 정책이 마지막으로 업데이트된 시간입니다. 다음 `modifiedAt` 속성은 unix epoch 타임스탬프에 표시됩니다. |
| `name` | 정책의 이름입니다. |
| `description` | (선택 사항) 특정 정책에 대한 추가 정보를 제공하기 위해 추가할 수 있는 속성입니다. |
| `status` | 정책의 현재 상태. 이 속성은 정책이 현재 있는지 여부를 정의합니다. `active` 또는 `inactive`. |
| `subjectCondition` | 주제에 적용되는 조건. 주제는 작업을 수행하기 위해 리소스에 대한 액세스를 요청하는 특정 속성을 가진 사용자입니다. 이 경우, `subjectCondition` 제목 속성에 적용되는 쿼리와 유사한 조건입니다. |
| `rules` | 정책을 정의하는 규칙 세트입니다. 규칙은 주체가 리소스에 대한 작업을 성공적으로 수행하기 위해 인증되는 속성 조합을 정의합니다. |
| `rules.effect` | 다음에 대한 값을 고려한 후 발생하는 효과 `action`, `condition` 및 `resource`. 가능한 값은 다음과 같습니다. `permit`, `deny`, 또는 `indeterminate`. |
| `rules.resource` | 주체가 액세스할 수 있거나 액세스할 수 없는 에셋 또는 개체입니다.  리소스는 파일, 애플리케이션, 서버 또는 API일 수 있습니다. |
| `rules.condition` | 리소스에 적용된 조건. 예를 들어 리소스가 스키마인 경우, 스키마에 해당 스키마에 대한 작업이 허용되는지 또는 허용되지 않는지 여부에 기여하는 특정 레이블이 스키마에 적용될 수 있습니다. |
| `rules.action` | 조회한 리소스에 대해 주체가 수행할 수 있는 작업입니다. 가능한 값은 다음과 같습니다. `read`, `create`, `edit`, 및 `delete`. |


## 정책 만들기 {#create}

POST 새 정책을 만들려면 `/policies` 엔드포인트.

**API 형식**

```http
POST /policies
```

**요청**

다음 요청은 이라는 새 정책을 만듭니다. `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| 매개변수 | 설명 |
| --- | --- |
| `name` | 정책의 이름입니다. |
| `description` | (선택 사항) 특정 정책에 대한 추가 정보를 제공하기 위해 추가할 수 있는 속성입니다. |
| `imsOrgId` | 정책이 포함된 조직입니다. |
| `rules` | 정책을 정의하는 규칙 세트입니다. 규칙은 주체가 리소스에 대한 작업을 성공적으로 수행하기 위해 인증되는 속성 조합을 정의합니다. |
| `rules.effect` | 다음에 대한 값을 고려한 후 발생하는 효과 `action`, `condition` 및 `resource`. 가능한 값은 다음과 같습니다. `permit`, `deny`, 또는 `indeterminate`. |
| `rules.resource` | 주체가 액세스할 수 있거나 액세스할 수 없는 에셋 또는 개체입니다.  리소스는 파일, 애플리케이션, 서버 또는 API일 수 있습니다. |
| `rules.condition` | 리소스에 적용된 조건. 예를 들어 리소스가 스키마인 경우, 스키마에 해당 스키마에 대한 작업이 허용되는지 또는 허용되지 않는지 여부에 기여하는 특정 레이블이 스키마에 적용될 수 있습니다. |
| `rules.action` | 조회한 리소스에 대해 주체가 수행할 수 있는 작업입니다. 가능한 값은 다음과 같습니다. `read`, `create`, `edit`, 및 `delete`. |

**응답**

요청이 성공하면 고유한 정책 ID와 관련 규칙을 포함하여 새로 만든 정책이 반환됩니다.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 정책에 해당하는 ID입니다. 이 식별자는 자동으로 생성되며, 정책을 조회, 업데이트 및 삭제하는 데 사용할 수 있습니다. |
| `name` | 정책의 이름입니다. |
| `rules` | 정책을 정의하는 규칙 세트입니다. 규칙은 주체가 리소스에 대한 작업을 성공적으로 수행하기 위해 인증되는 속성 조합을 정의합니다. |
| `rules.effect` | 다음에 대한 값을 고려한 후 발생하는 효과 `action`, `condition` 및 `resource`. 가능한 값은 다음과 같습니다. `permit`, `deny`, 또는 `indeterminate`. |
| `rules.resource` | 주체가 액세스할 수 있거나 액세스할 수 없는 에셋 또는 개체입니다.  리소스는 파일, 애플리케이션, 서버 또는 API일 수 있습니다. |
| `rules.condition` | 리소스에 적용된 조건. 예를 들어 리소스가 스키마인 경우, 스키마에 해당 스키마에 대한 작업이 허용되는지 또는 허용되지 않는지 여부에 기여하는 특정 레이블이 스키마에 적용될 수 있습니다. |
| `rules.action` | 조회한 리소스에 대해 주체가 수행할 수 있는 작업입니다. 가능한 값은 다음과 같습니다. `read`, `create`, `edit`, 및 `delete`. |


## 정책 ID로 정책 업데이트 {#put}

개별 정책의 규칙을 업데이트하려면에 PUT 요청을 수행합니다 `/policies` 요청 경로에 업데이트할 정책의 ID를 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
PUT /policies/{POLICY_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {POLICY_ID} | 업데이트할 정책의 ID입니다. |

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "com.adobe.action.read"
        ]
      }
    ]
  }'
```

**응답**

성공한 응답은 업데이트된 정책을 반환합니다.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## 정책 속성 업데이트 {#patch}

개별 정책의 속성을 업데이트하려면에 PATCH 요청을 `/policies` 요청 경로에 업데이트할 정책의 ID를 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
PATCH /policies/{POLICY_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {POLICY_ID} | 업데이트할 정책의 ID입니다. |

**요청**

다음 요청은 의 값을 대체합니다. `/description` 정책 ID에서 `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
      }
    ]
  }'
```

| 작업 | 설명 |
| --- | --- |
| `op` | 역할을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공한 응답은 업데이트된 설명과 함께 쿼리된 정책 ID를 반환합니다.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## 정책 삭제 {#delete}

정책을 삭제하려면 다음에 대한 DELETE 요청을 `/policies` 삭제할 정책의 ID를 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
DELETE /policies/{POLICY_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {POLICY_ID} | 삭제할 정책의 ID입니다. |

**요청**

다음 요청은 ID가 인 정책을 삭제합니다. `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

정책에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 정책이 관리에서 제거되었으므로 HTTP 상태 404(찾을 수 없음)를 받게 됩니다.
