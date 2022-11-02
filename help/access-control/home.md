---
keywords: Experience Platform;홈;인기 항목;액세스 제어;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: 액세스 제어 개요
description: Adobe Experience Platform에 대한 액세스 제어는 Adobe Admin Console을 통해 제공됩니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: e2d3267715f693a321b2f4ce1bae0650f38c21d7
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 3%

---

# 액세스 제어 개요

액세스 제어 대상 [!DNL Experience Platform] 는 [Adobe Admin Console](https://adminconsole.adobe.com). 이 기능은 의 제품 프로필을 활용합니다 [!DNL Admin Console]- 권한 및 샌드박스를 사용자와 연결합니다.

## 액세스 제어 계층 및 워크플로우

액세스 제어를 구성하려면 [!DNL Experience Platform]인 경우, 조직에 대한 관리자 권한이 있어야 합니다 [!DNL Experience Platform] 제품 통합. 권한을 부여하거나 해지하는 최소 역할은 제품 프로필 관리자입니다. 권한을 관리할 수 있는 다른 관리자 역할은 제품 관리자(제품 내의 모든 프로필을 관리할 수 있음)와 시스템 관리자(제한 없음)입니다. 의 Adobe Help Center 문서를 참조하십시오. [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html) 추가 정보.

>[!NOTE]
>
>이 시점부터 이 문서의 &quot;관리자&quot;에 대한 모든 언급은 제품 프로필 관리자 이상(위에 요약된 설명)을 참조합니다.

액세스 권한을 획득하고 할당하는 상위 수준의 워크플로우는 다음과 같이 요약할 수 있습니다.

- Adobe Experience Platform 또는 Experience Platform을 사용하는 응용 프로그램/앱 서비스에 라이선스를 부여하면 라이선스 중에 지정된 관리자에게 이메일이 전송됩니다.
- 관리자가 로그인하는 [Adobe Admin Console](#adobe-admin-console) 및 선택 **Adobe Experience Platform** 개요 페이지의 제품 목록에서 을 선택합니다.
- 관리자는 기본값을 볼 수 있습니다 [제품 프로필](#product-profiles) 필요에 따라 새 고객 제품 프로필을 만듭니다.
- 관리자는 기존 제품 프로필에 대한 권한 및 사용자를 편집할 수 있습니다.
- 제품 프로필을 만들거나 편집할 때 관리자는 **[!UICONTROL 사용자]** 탭하고 이러한 사용자에게 권한을 부여합니다(예: &quot;[!UICONTROL 데이터 세트 읽기]&quot; 또는 &quot;[!UICONTROL 스키마 관리]&quot;) **[!UICONTROL 권한]** 탭. 마찬가지로 관리자는 동일한 권한 탭을 사용하여 샌드박스에 대한 액세스 권한을 할당할 수 있습니다.
- 사용자가 [!DNL Experience Platform] 사용자 인터페이스, 액세스 권한 [!DNL Platform] 기능은 2단계에서 부여된 권한에 의해 파생됩니다. 예를 들어, 사용자에게 &quot;[!UICONTROL 데이터 세트 보기]&quot; 권한, **[!UICONTROL 데이터 세트]** 해당 사용자는 사이드 메뉴의 탭을 볼 수 없습니다.

액세스 제어 관리 방법에 대한 자세한 단계 [!DNL Experience Platform]를 참조하고 [액세스 제어 사용 안내서](./ui/overview.md).

모든 호출 [!DNL Experience Platform] API는 권한에 대해 유효성이 확인되며, 현재 사용자 컨텍스트에서 적절한 권한이 없으면 오류를 반환합니다. UI 내에서 요소는 현재 사용자에게 부여된 권한에 따라 숨기거나 변경됩니다.

## Adobe Admin Console

Adobe Admin Console은 조직에 대한 Adobe 제품 권한 및 액세스를 관리하기 위한 중앙 위치를 제공합니다. 콘솔을 통해 다양한 사용자에 대한 액세스 권한을 사용자 그룹에 부여할 수 있습니다 [!DNL Platform] 기능(예: &quot;)[!UICONTROL 데이터 세트 관리]&quot;, &quot;[!UICONTROL 데이터 세트 보기]&quot; 또는 &quot;[!UICONTROL 프로필 관리]&quot;.

### 제품 프로필

에서 [!DNL Admin Console], 권한은 제품 프로필을 사용하여 사용자에게 할당됩니다. 제품 프로필을 사용하면 한 명 이상의 사용자에게 권한을 부여하고 제품 프로필을 통해 샌드박스의 범위에 대한 액세스 권한을 포함할 수 있습니다. 사용자는 조직에 속한 하나 이상의 제품 프로필에 할당할 수 있습니다.

### 기본 제품 프로필

[!DNL Experience Platform] 에는 두 개의 사전 구성된 기본 제품 프로필이 포함되어 있습니다. 다음 표에서는 액세스 권한을 부여하는 샌드박스 및 해당 샌드박스의 범위 내에서 부여하는 권한을 포함하여 각 기본 프로필에 제공되는 사항을 설명합니다.

| 제품 프로필 | 샌드박스 액세스 | 권한 |
| --- | --- | --- |
| 기본 프로덕션 모든 액세스 권한 | 프로덕션 | 적용 가능한 모든 권한 [!DNL Experience Platform]( 샌드박스 관리 권한 제외). |
| 샌드박스 관리자 | 해당 없음 | 샌드박스 관리 권한에 대한 액세스 권한만 제공합니다. |

## 샌드박스 및 권한

비프로덕션 샌드박스는 다른 샌드박스에서 데이터를 분리할 수 있도록 해주는 데이터 가상화 형태이며 일반적으로 개발 실험, 테스트 또는 평가에 사용됩니다. 제품 프로필의 권한을 통해 프로필의 사용자에게 [!DNL Platform] 액세스 권한이 부여된 샌드박스 환경 내의 기능입니다. 기본 Experience Platform 라이센스는 5개의 샌드박스(프로덕션 1개와 비프로덕션 4개)를 부여합니다. 비프로덕션 샌드박스 10개의 팩을 총 75개의 샌드박스에 추가할 수 있습니다. 자세한 내용은 IMS 조직 관리자 또는 Adobe 영업 담당자에게 문의하십시오.

샌드박스에 대한 자세한 내용은 [!DNL Experience Platform]을(를) 참조하십시오. [샌드박스 개요](../sandboxes/home.md).

### 샌드박스 액세스

샌드박스에 대한 액세스는 제품 프로필을 통해 관리됩니다. 제품 프로필용 샌드박스에 대한 액세스를 활성화하는 방법에 대한 자세한 단계는 [액세스 제어 사용 안내서](./ui/overview.md).

사용자는 제품 프로필 내에서 하나 이상의 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 한 사용자가 둘 이상의 제품 프로필에 포함된 경우 해당 사용자는 해당 프로필에 포함된 모든 샌드박스에 액세스할 수 있습니다.

샌드박스 관리 권한을 사용하면 샌드박스를 관리, 보기 또는 재설정할 수 있습니다.

### 권한 {#permissions}

제품 프로필 내의 권한 탭에는 해당 프로필에 대해 활성 상태인 샌드박스 및 권한이 표시됩니다.

![권한 개요](./images/permissions.png)

를 통해 부여된 권한 [!DNL Admin Console] 몇 가지 낮은 수준 기능에 대한 액세스를 부여하는 몇 가지 권한을 사용하여 카테고리별로 정렬됩니다.

다음 표에서는 사용 가능한 사용 권한에 대해 설명합니다 [!DNL Experience Platform] 에서 [!DNL Admin Console]- 특정 [!DNL Platform] 액세스 권한을 부여하는 기능입니다. 제품 프로필에 권한을 추가하는 방법에 대한 자세한 단계는 다음을 참조하십시오. [액세스 제어 사용 안내서](./ui/overview.md).

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 스키마 관리] | 스키마 및 관련 리소스를 읽기, 생성, 편집 및 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL 스키마 보기] | 스키마 및 관련 리소스에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL 관계 관리] | 스키마 관계를 읽기, 생성, 편집 및 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL ID 메타데이터 관리] | 스키마에 대한 ID 메타데이터를 읽기, 생성, 편집 및 삭제할 수 있는 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 관리] | 데이터 세트를 읽기, 만들기, 편집 및 삭제할 수 있는 액세스 권한. 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 보기] | 데이터 세트 및 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 모니터링] | 데이터 세트 및 스트림 모니터링에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Profile Management] | [!UICONTROL 프로필 관리] | 고객 프로필에 사용되는 데이터 세트를 읽기, 만들기, 편집 및 삭제할 수 있는 액세스 권한. 사용 가능한 프로필에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 프로필 보기] | 사용 가능한 프로필에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 관리] | 세그먼트 읽기, 만들기, 편집 및 삭제에 액세스할 수 있습니다. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 보기] | 사용 가능한 세그먼트에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 관리] | 병합 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 보기] | 사용 가능한 병합 정책에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트용 대상 내보내기] | 평가된 대상 세그먼트를 데이터 세트로 내보내기 기능. |
| [!DNL Profile Management] | [!UICONTROL 대상에 세그먼트 평가] | 세그먼트 정의를 평가하여 대상의 프로필을 생성하는 기능. |
| [!DNL Identities] | [!UICONTROL ID 네임스페이스 관리] | ID 네임스페이스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Identities] | [!UICONTROL ID 네임스페이스 보기] | ID 네임스페이스에 대한 읽기 전용 액세스 권한. |
| [!DNL Identities] | [!UICONTROL ID 그래프 보기] | ID 그래프에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 관리] | 샌드박스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 보기] | 조직에 속하는 샌드박스에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 재설정] | 샌드박스를 재설정하는 기능. |
| [!DNL Destinations] | [!UICONTROL 대상 관리] | 대상을 읽기, 만들기, 편집 및 비활성화하기 위한 액세스 권한. |
| [!DNL Destinations] | [!UICONTROL 대상 보기] | 에서 사용 가능한 대상에 대한 읽기 전용 액세스 **[!UICONTROL 카탈로그]** 의 탭 및 인증된 대상 **[!UICONTROL 찾아보기]** 탭. |
| [!DNL Destinations] | [!UICONTROL 대상 활성화] | 생성된 활성 대상에 데이터를 활성화하는 기능. 이 권한을 사용하려면 다음 중 하나가 필요합니다 [!UICONTROL 대상 보기] 또는 [!UICONTROL 대상 관리] 대상을 활성화할 사용자에게 부여됩니다. |
| [!DNL Destinations] | [!UICONTROL 데이터 집합 대상 관리 및 활성화] | 데이터 집합 내보내기 흐름을 읽기, 만들기, 편집 및 비활성화할 수 있습니다. 또한 생성된 활성 데이터 세트에 데이터를 활성화하는 기능입니다. |
| [!DNL Destinations] | [!UICONTROL 대상 작성] | 을 사용하여 대상을 작성할 수 있는 기능 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL 소스 관리] | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| [!DNL Data Ingestion] | [!UICONTROL 소스 보기] | 에서 사용 가능한 소스에 대한 읽기 전용 액세스 권한 **[!UICONTROL 카탈로그]** 의 탭 및 인증된 소스 **[!UICONTROL 찾아보기]** 탭. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 두 IMS 조직을 연결하고 활성화하기 위해 파트너 핸드셰이크를 생성, 수락 및 거부할 수 있는 액세스 권한 [!DNL Segment Match] 흐름. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 읽기, 만들기, 편집 및 게시에 대한 액세스 권한 [!DNL Segment Match] 활성 파트너가 피드를 제공합니다. |
| [!DNL Data Science Workspace] | [!UICONTROL 데이터 과학 작업 공간 관리] | 에서 읽기, 만들기, 편집 및 삭제할 수 있는 액세스 권한 [!DNL Data Science Workspace]. |
| 데이터 거버넌스 | [!UICONTROL 데이터 사용 레이블 적용] | 사용 레이블을 읽고, 만들고, 삭제할 수 있는 액세스 권한. |
| 데이터 거버넌스 | [!UICONTROL 데이터 사용 정책 관리] | 데이터 사용 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| 데이터 거버넌스 | [!UICONTROL 데이터 사용 정책 보기] | 조직에 속하는 데이터 사용 정책에 대한 읽기 전용 액세스 권한입니다. |
| 데이터 거버넌스 | [!UICONTROL 사용자 활동 로그 보기] | 기록된 보기에 대한 읽기 전용 액세스 [감사 로그](../landing/governance-privacy-security/audit-logs/overview.md) 플랫폼 활동. |
| [!DNL Dashboards] | [!UICONTROL 라이선스 사용 대시보드 보기] | 라이센스 사용 대시보드를 보려면 읽기 전용 액세스 권한이 있어야 합니다. |
| [!DNL Dashboards] | [!UICONTROL 표준 대시보드 관리] | 데이터 웨어하우스에 아직 있지 않은 사용자 지정 특성을 추가합니다. |
| [!DNL Query Service] | [!UICONTROL 쿼리 관리] | 플랫폼 데이터에 대한 구조화된 SQL 쿼리를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Query Service] | [!UICONTROL Query Service 통합 관리] | Query Service 액세스를 위해 만료되지 않은 자격 증명을 만들고, 업데이트하고, 삭제할 수 있는 액세스 권한입니다. |

## 다음 단계

이 안내서를 읽으면에서 액세스 제어의 주요 원리를 소개합니다 [!DNL Experience Platform]. 이제 다음을 계속 수행할 수 있습니다. [액세스 제어 사용 안내서](./ui/overview.md) 를 사용하는 방법에 대한 자세한 단계 [!DNL Admin Console] 제품 프로필을 만들고 권한을 할당합니다. [!DNL Platform].
