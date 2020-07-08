---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 효과적인 정책 보기
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# 효과적인 정책 보기

현재 사용자에 대한 유효한 정책을 보려면 액세스 제어 API에서 종단점에 대한 POST 요청을 `/acl/effective-policies` 수행하십시오. 검색할 권한 및 리소스 유형은 배열 형태로 요청 페이로드에서 제공해야 합니다. 이것은 아래의 예제 API 호출에서 입증되었습니다.

**API 형식**

```http
POST /acl/effective-policies
```

**요청**

다음 요청은 현재 사용자에 대한 &quot;데이터 집합 관리&quot; 권한에 대한 정보와 &quot;스키마&quot; 리소스 유형에 대한 액세스를 검색합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>페이로드 배열에서 제공할 수 있는 권한 및 리소스 유형의 전체 목록은 [허용된 권한 및 리소스 유형에 대한 부록 섹션을 참조하십시오](#accepted-permissions-and-resource-types).

**응답**

성공적인 응답은 요청에 제공된 권한 및 리소스 유형에 대한 정보를 반환합니다. 응답에는 현재 사용자가 요청에 지정된 리소스 유형에 대해 가지는 활성 권한이 포함됩니다. 요청 페이로드에 포함된 권한이 현재 사용자에 대해 활성 상태인 경우 API는 에스트스크(`*`)가 있는 권한을 반환하여 권한이 활성 상태임을 나타냅니다. 사용자에 대해 활성화되지 않은 요청에 제공된 모든 권한은 응답 페이로드에서 생략됩니다.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## 다음 단계

이 문서에서는 액세스 제어 API를 호출하여 리소스 유형에 대한 활성 권한 및 관련 정책에 대한 정보를 반환하는 방법을 다룹니다. Experience Platform의 액세스 제어에 대한 자세한 내용은 [액세스 제어 개요를 참조하십시오](../home.md).

## 부록

이 섹션에서는 액세스 제어 API 사용에 대한 보충 정보를 제공합니다.

### 허용된 권한 및 리소스 유형

다음은 종단점에 대한 POST 요청 페이로드에서 포함할 수 있는 권한 및 리소스 유형 `/acl/active-permissions` 목록입니다.

**권한**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**리소스 유형**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
