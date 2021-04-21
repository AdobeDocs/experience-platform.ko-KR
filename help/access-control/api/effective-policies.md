---
keywords: Experience Platform;홈;인기 항목;효과적인 정책;액세스 제어 api
solution: Experience Platform
title: 효과적인 정책 API 끝점
topic-legacy: developer guide
description: Adobe Experience Platform의 액세스 제어를 사용하면 Adobe Admin Console을 사용하여 다양한 플랫폼 기능에 대한 역할 및 권한을 관리할 수 있습니다. 이 문서는 Adobe Experience Platform용 액세스 제어 API를 사용하여 효과적인 정책을 보는 방법에 대한 지침으로 제공됩니다.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# 효과적인 정책 끝점

현재 사용자에 대한 유효한 정책을 보려면 [!DNL Access Control] API의 `/acl/effective-policies` 끝점에 POST 요청을 하십시오. 검색할 권한 및 리소스 유형은 배열 형태로 요청 페이로드에서 제공해야 합니다. 이것은 아래의 예제 API 호출에서 입증되었습니다.

**API 형식**

```http
POST /acl/effective-policies
```

**요청**

다음 요청은 현재 사용자의 &quot;[!UICONTROL Manage Datasets]&quot; 권한 및 &quot;[!UICONTROL schemas]&quot; 리소스 유형에 대한 액세스 정보를 검색합니다.

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
>페이로드 배열에서 제공할 수 있는 권한 및 리소스 유형의 전체 목록은 [허용된 권한 및 리소스 유형](#accepted-permissions-and-resource-types)의 부록 섹션을 참조하십시오.

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

이 문서에서는 리소스 유형에 대한 활성 권한 및 관련 정책에 대한 정보를 반환하기 위해 [!DNL Access Control] API를 호출하는 방법에 대해 다룹니다. [!DNL Experience Platform]에 대한 액세스 제어에 대한 자세한 내용은 [액세스 제어 개요](../home.md)를 참조하십시오.

## 부록

이 섹션에서는 [!DNL Access Control] API 사용에 대한 보충 정보를 제공합니다.

### 허용된 권한 및 리소스 유형

다음은 POST 요청의 페이로드에서 `/acl/active-permissions` 끝점에 포함할 수 있는 권한 및 리소스 유형 목록입니다.

**권한**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**리소스 유형**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
