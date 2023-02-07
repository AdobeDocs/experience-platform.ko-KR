---
keywords: Experience Platform;홈;인기 항목;유효 정책;액세스 제어 api
solution: Experience Platform
title: 유효 정책 API 끝점
description: Adobe Experience Platform용 액세스 제어 API를 사용하여 효과적인 액세스 정책을 보는 방법을 알아봅니다.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 효과적인 정책 엔드포인트

>[!NOTE]
>
>사용자 토큰이 전달되면 토큰의 사용자는 요청된 조직에 대해 &quot;조직 관리자&quot; 역할이 있어야 합니다.

현재 사용자에 대한 유효한 액세스 제어 정책을 보려면 `/acl/effective-policies` 의 엔드포인트 [!DNL Access Control] API. 검색할 권한 및 리소스 유형은 요청 페이로드에서 배열 형태로 제공해야 합니다. 이것은 아래 예제 API 호출에서 확인됩니다.

**API 형식**

```http
POST /acl/effective-policies
```

**요청**

다음 요청은 &quot;[!UICONTROL 데이터 세트 관리]&quot; 권한 및 &quot;[!UICONTROL 스키마]현재 사용자의 리소스 유형입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>페이로드 배열에 제공할 수 있는 권한 및 리소스 유형의 전체 목록은 의 부록 섹션을 참조하십시오 [수락된 권한 및 리소스 유형](#accepted-permissions-and-resource-types).

**응답**

성공적인 응답은 요청에 제공된 권한 및 리소스 유형에 대한 정보를 반환합니다. 응답에는 요청에 지정된 리소스 유형에 대해 현재 사용자가 가지고 있는 활성 권한이 포함됩니다. 요청 페이로드에 포함된 권한이 현재 사용자에 대해 활성 상태인 경우 API는 별표( )가 있는 권한을 반환합니다`*`)을 클릭하여 권한이 활성 상태임을 나타냅니다. 사용자에 대해 활성화되지 않은 요청에서 제공된 모든 권한은 응답 페이로드에서 생략됩니다.

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

이 문서에서는 [!DNL Access Control] 리소스 유형에 대한 활성 권한 및 관련 액세스 정책에 대한 정보를 반환하기 위한 API입니다. 액세스 제어에 대한 자세한 정보 [!DNL Experience Platform]를 참조하고 [액세스 제어 개요](../home.md).

## 부록

이 섹션에서는 [!DNL Access Control] API.

### 허용된 권한 및 리소스 유형

다음은 POST 요청의 페이로드에 포함할 수 있는 권한 및 리소스 유형 목록입니다 `/acl/active-permissions` 엔드포인트.

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
