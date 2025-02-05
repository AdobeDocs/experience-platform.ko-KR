---
keywords: Experience Platform;홈;인기 항목;액세스 제어;adobe admin console
solution: Experience Platform
title: 액세스 제어 개요
description: Adobe Experience Platform에 대한 액세스 제어는 Adobe Admin Console을 통해 제공됩니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 5d5c57dfb9e4abda6b1bca96147a95d063bc17c6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# 액세스 제어 개요

Adobe Experience Platform에 대한 액세스 제어는 [Adobe Experience Cloud](https://experience.adobe.com/)의 **[!UICONTROL 권한]**&#x200B;을 통해 제공됩니다. 이 기능은 권한 및 샌드박스를 사용자와 연결하는 역할 및 정책을 활용합니다.

## 액세스 제어 계층 및 워크플로

Experience Platform에 대한 액세스 제어를 구성하려면 Experience Platform 제품이 있는 조직에 대한 시스템 또는 제품 관리자 권한이 있어야 합니다. 권한을 부여하거나 철회할 수 있는 최소 역할은 제품 관리자입니다. 권한을 관리할 수 있는 다른 관리자 역할은 시스템 관리자(제한 없음)입니다. 자세한 내용은 [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html)에 대한 Adobe Help Center 문서를 참조하십시오.

>[!NOTE]
>
>이 시점에서부터 이 문서에서 &quot;관리자&quot;에 대한 언급은 제품 관리자 이상(위에 설명된 대로)을 의미합니다.

액세스 권한을 얻고 할당하기 위한 높은 수준의 워크플로는 다음과 같이 요약할 수 있습니다.

- Adobe Experience Platform 또는 Experience Platform을 사용하는 애플리케이션/앱 서비스에 라이선스를 부여한 후 라이선스 부여 중에 지정된 관리자에게 이메일이 전송됩니다.
- 관리자가 [Adobe Admin Console](#adobe-admin-console)에 로그인하고 개요 페이지의 제품 목록에서 **Adobe Experience Platform**&#x200B;을(를) 선택합니다.
- Experience Platform 액세스 권한을 부여하려면 관리자가 기본 제품 프로필에 사용자를 추가하는 것이 좋습니다. `AEP-Default-All-Users`.
- Experience Platform 권한에서 관리자는 새 역할을 만들거나 기존 역할에 대한 권한 및 사용자를 편집할 수 있습니다.
- 역할을 만들거나 편집할 때 관리자는 **[!UICONTROL 사용자]** 탭을 사용하여 사용자를 역할에 추가하고, 역할의 권한을 편집하여 이러한 사용자에게 권한(예: &quot;[!UICONTROL 데이터 세트 읽기]&quot; 또는 &quot;[!UICONTROL 스키마 관리]&quot;)을 부여합니다. 마찬가지로 관리자는 동일한 편집 옵션을 사용하여 샌드박스에 대한 액세스 권한을 할당할 수 있습니다.
- 사용자가 Experience Platform 사용자 인터페이스에 로그인할 때 Experience Platform 기능에 대한 액세스는 이전 단계에서 부여한 권한에 의해 결정됩니다. 예를 들어 사용자에게 [!UICONTROL 데이터 세트 보기] 권한이 없는 경우 측면 메뉴의 **[!UICONTROL 데이터 세트]** 탭이 표시되지 않습니다.

Experience Platform에서 액세스 제어를 관리하는 방법에 대한 자세한 단계는 [액세스 제어 사용 안내서](./ui/overview.md)를 참조하십시오.

Experience Platform API에 대한 모든 호출은 권한에 대해 유효성이 검사되며 현재 사용자 컨텍스트에서 적절한 권한을 찾을 수 없는 경우 오류를 반환합니다. UI 내에서 요소는 현재 사용자에게 부여된 권한에 따라 숨겨지거나 변경됩니다.

## 권한 {#platform-permissions}

[!UICONTROL 권한]은(는) 조직의 Experience Platform 액세스를 관리하기 위한 중앙 위치를 제공합니다. [!UICONTROL 권한]을 통해 사용자 그룹에 [!UICONTROL 데이터 세트 관리], [!UICONTROL 데이터 세트 보기] 또는 [!UICONTROL 프로필 관리]와 같은 다양한 Experience Platform 기능에 대한 액세스 권한을 부여할 수 있습니다.

### 역할

[!UICONTROL 역할] 섹션에서 역할을 사용하여 사용자에게 권한이 할당됩니다. 역할을 사용하면 한 명 또는 여러 사용자에게 권한을 부여할 수 있으며, 역할을 통해 할당된 샌드박스 범위에 대한 액세스 권한도 포함할 수 있습니다. 사용자는 조직에 속한 하나 또는 여러 역할에 할당할 수 있습니다.

### 기본 역할

Experience Platform은 두 개의 사전 구성된 기본 역할과 함께 제공됩니다. 다음 표는 액세스 권한을 부여하는 샌드박스와 해당 샌드박스의 범위 내에서 부여하는 권한을 포함하여 각 기본 프로필에서 제공되는 내용을 간략하게 설명합니다.

| 역할 | 샌드박스 액세스 | 권한 |
| --- | --- | --- |
| 기본 프로덕션 모든 액세스 | 프로덕션 | 샌드박스 관리 권한을 제외하고 Experience Platform에 적용할 수 있는 모든 권한입니다. |
| 샌드박스 관리자 | N/A | 샌드박스 관리 권한에 대한 액세스 권한만 제공합니다. |

## 샌드박스 및 권한

비프로덕션 샌드박스는 다른 샌드박스와 데이터를 분리할 수 있는 데이터 가상화 의 한 형태이며 일반적으로 개발 실험, 테스트 또는 시도에 사용됩니다. 역할의 권한은 해당 역할의 사용자에게 액세스 권한이 부여된 샌드박스 환경 내의 Experience Platform 기능에 대한 액세스 권한을 부여합니다. 기본 Experience Platform 라이선스는 5개의 샌드박스(프로덕션 1개와 비프로덕션 4개)를 부여합니다. 비프로덕션 샌드박스 10개 팩 및 총 75개 샌드박스를 추가할 수 있습니다. 자세한 내용은 조직의 관리자 또는 Adobe 영업 담당자에게 문의하십시오.

Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하세요.

### 샌드박스에 대한 액세스

샌드박스에 대한 액세스는 역할을 통해 관리됩니다. 역할의 샌드박스에 대한 액세스를 활성화하는 방법에 대한 자세한 단계는 [특성 기반 액세스 제어 역할 안내서](./abac/ui/roles.md)를 참조하십시오.

사용자는 역할 내에서 하나 이상의 샌드박스에 대한 액세스 권한을 부여 받을 수 있습니다. 한 명의 사용자가 둘 이상의 역할에 포함된 경우 해당 사용자는 해당 역할에 포함된 모든 샌드박스에 액세스할 수 있습니다.

사용자는 &quot;샌드박스 관리&quot; 권한을 사용하여 샌드박스를 관리, 확인 또는 재설정할 수 있습니다.

### 리소스 권한 {#permissions}

역할 내의 리소스 [!UICONTROL 권한] 탭에는 해당 역할에 대해 활성 상태인 샌드박스 및 권한이 표시됩니다.

![권한-개요](./images/permissions.png)

리소스 권한을 통해 부여된 권한은 범주별로 정렬되며, 일부 권한은 여러 낮은 수준의 기능에 대한 액세스 권한을 부여합니다.

다음 표는 해당 역할에서 Experience Platform이 사용할 수 있는 권한을 간략하게 설명합니다(액세스 권한을 부여하는 특정 Experience Platform 기능 설명). 역할에 권한을 추가하는 방법에 대한 자세한 단계는 [특성 기반 액세스 제어 역할 안내서](./abac/ui/roles.md)를 참조하십시오.

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!DNL AI Assistant] | [!UICONTROL AI Assistant 사용] | [AI 길잡이](../ai-assistant/access.md)에게 질문할 수 있습니다. |
| [!DNL AI Assistant] | [!UICONTROL Operational Insights 보기] | [operational insights](../ai-assistant/home.md##operational-insights) 쿼리에 대한 응답을 얻을 수 있는 액세스 권한. |
| [!DNL Alerts] | [!UICONTROL 경고 내역 보기] | 경고 내역에 대한 읽기 전용 액세스 권한. |
| [!DNL Alerts] | [!UICONTROL 경고 해결] | 경고를 읽고, 편집하고, 삭제할 수 있는 액세스 권한 |
| [!DNL Alerts] | [!UICONTROL 경고 보기] | 경고에 대한 읽기 전용 액세스 권한. |
| [!DNL Alerts] | [!UICONTROL 경고 관리] | 경고 내역을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Computed Attributes] | [!UICONTROL 계산된 특성 보기] | 계산된 속성 탭, 인벤토리 및 세부 정보에 대한 읽기 전용 액세스 권한. |
| [!DNL Computed Attributes] | [!UICONTROL 계산된 특성 관리] | 계산된 속성을 읽고, 만들고, 삭제하고, 비활성화할 수 있는 액세스 권한. |
| [!DNL Dashboards] | [!UICONTROL 라이선스 사용 대시보드 보기] | 라이선스 사용 대시보드를 보려면 읽기 전용 권한입니다. |
| [!DNL Dashboards] | [!UICONTROL 표준 대시보드 관리] | Data Warehouse에 아직 없는 사용자 지정 특성을 추가합니다. |
| [!DNL Data Governance] | [!UICONTROL 사용 레이블 관리] | 사용 레이블을 읽고, 만들고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL 데이터 사용 정책 관리] | 데이터 사용 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL 데이터 사용 정책 보기] | 조직에 속한 데이터 사용 정책에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL 사용자 활동 로그 보기] | 플랫폼 활동의 기록된 [감사 로그](../landing/governance-privacy-security/audit-logs/overview.md)를 보기 위한 읽기 전용 액세스입니다. |
| [!DNL Data Ingestion] | [!UICONTROL 소스 관리] | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| [!DNL Data Ingestion] | [!UICONTROL 소스 보기] | **[!UICONTROL 카탈로그]** 탭의 사용 가능한 소스와 **[!UICONTROL 찾아보기]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 파트너 악수를 만들고, 수락하고, 거부하여 두 조직을 연결하고 [!DNL Segment Match] 흐름을 사용하도록 설정할 수 있습니다. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 활성 파트너와 함께 [!DNL Segment Match] 피드를 읽기, 만들기, 편집 및 게시할 수 있는 액세스 권한이 있습니다. |
| [!DNL Data Lifecycle] | [!UICONTROL 데이터 주기 보기] | 데이터 라이프사이클에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Lifecycle] | [!UICONTROL 데이터 수명 주기 관리] | 데이터 라이프사이클을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL 스키마 관리] | 스키마 및 관련 리소스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL 스키마 보기] | 스키마 및 관련 리소스에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL 관계 관리] | 스키마 관계 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL ID 메타데이터 관리] | 스키마에 대한 ID 메타데이터를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 관리] | 데이터 세트 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 보기] | 데이터 세트 및 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL 데이터 모니터링] | 모니터링 데이터 세트 및 스트림에 대한 읽기 전용 액세스. |
| [!DNL Data Science Workspace] | [!UICONTROL 데이터 과학 Workspace 관리] | [!DNL Data Science Workspace]에서 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Destinations] | [!UICONTROL 대상 보기] | **[!UICONTROL 카탈로그]** 탭에서 사용 가능한 대상 및 **[!UICONTROL 찾아보기]** 탭에서 인증된 대상을 보는 읽기 전용 액세스입니다. |
| [!DNL Destinations] | [!UICONTROL 대상 관리] | 대상 연결 및 대상 계정을 읽고 만들고 삭제할 수 있는 액세스 권한. |
| [!DNL Destinations] | [!UICONTROL 대상 활성화] | 사용자에게 기존 대상에 대한 세그먼트를 활성화할 수 있는 기능을 제공합니다. 활성화 워크플로에서 매핑 단계를 활성화합니다. 또한 이 권한을 사용하려면 대상에 데이터를 활성화하는 사용자에게 [!UICONTROL 대상 보기] 권한을 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL 매핑하지 않고 세그먼트 활성화] | 사용자에게 [매핑 단계](../destinations/ui/activate-batch-profile-destinations.md#mapping)를 표시하지 않고 기존 대상에 세그먼트를 활성화할 수 있는 기능을 제공합니다. 사용자는 활성화 워크플로에서 세그먼트를 추가하거나 제거할 수 있지만 매핑된 속성 또는 ID를 추가하거나 제거할 수 없습니다. 또한 이 권한을 사용하려면 대상에 데이터를 활성화하는 사용자에게 [!UICONTROL 대상 보기] 권한을 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL 데이터 집합 대상 관리 및 활성화] | 데이터 세트 내보내기 흐름을 읽고, 만들고, 편집하고, 비활성화하는 기능입니다. 생성된 활성 데이터 세트에 대한 데이터도 활성화할 수 있습니다. 또한 이 권한을 사용하려면 대상에 데이터를 활성화하는 사용자에게 [!UICONTROL 대상 보기] 권한을 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL 대상 작성] | [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)을(를) 사용하여 대상을 작성할 수 있습니다. |
| [!DNL Identity Management] | [!UICONTROL ID 네임스페이스 관리] | ID 네임스페이스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL ID 네임스페이스 보기] | ID 네임스페이스에 대한 읽기 전용 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL ID 그래프 보기] | ID 그래프에 대한 읽기 전용 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL Attribution AI 보기] | Attribution AI 설정 및 인사이트에 대한 읽기 전용 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL Attribution AI 관리] | Attribution AI 모델을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL 고객 AI 보기] | 고객 AI 모델을 읽거나 볼 수 있는 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL 고객 AI 관리] | 고객 AI 모델을 생성, 업데이트, 삭제, 활성화 또는 비활성화할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 프로필 관리] | 여러 소스에서 데이터를 수집하고 개별 고객을 위한 강력한 프로필을 빌드하며 데이터 레이크 및 실시간 고객 프로필 데이터 저장소에 프로필 활성화 데이터를 저장합니다. |
| [!DNL Profile Management] | [!UICONTROL 프로필 보기] | 사용 가능한 프로필에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 관리] | 세그먼트 읽기, 만들기, 편집 및 삭제 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 보기] | 사용 가능한 세그먼트에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 관리] | 병합 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 보기] | 사용 가능한 병합 정책에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 대상자 가져오기] | 가져온 대상자 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트에 대한 대상자 내보내기] | 평가된 대상 세그먼트를 데이터 세트로 내보내는 기능. |
| [!DNL Profile Management] | [!UICONTROL 대상자에 대한 세그먼트 평가] | 세그먼트 정의를 평가하여 대상자에 대한 프로필을 생성하는 기능. |
| [!DNL Profile Management] | [!UICONTROL B2B AI 보기] | 모든 B2B AI/ML 서비스에 대한 설정 및 구성에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL B2B AI 관리] | 모든 B2B AI/ML 서비스에 대한 설정 및 구성을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL B2B 프로필 보기] | B2B 엔티티 프로필(예: 계정, 영업 기회 등), 모든 B2B AI/ML 서비스에 대한 설정 및 구성, B2B 대시보드 위젯에 대한 읽기 전용 액세스입니다. |
| [!DNL Profile Management] | [!UICONTROL B2B 프로필 관리] | B2B 엔티티 프로필(예: 계정, 영업 기회 등)을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한입니다. 모든 B2B AI/ML 서비스 및 B2B 대시보드 위젯에 대한 설정 및 구성에 대한 읽기 전용 액세스입니다. |
| [!DNL Query Service] | [!UICONTROL 쿼리 관리] | Platform 데이터에 대한 구조화된 SQL 쿼리를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Query Service] | [!UICONTROL 쿼리 서비스 통합 관리] | 쿼리 서비스 액세스에 대한 만료되지 않는 자격 증명을 생성, 업데이트 및 삭제할 수 있는 액세스 권한입니다. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 관리] | 샌드박스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 보기] | 조직에 속한 샌드박스에 대한 읽기 전용 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 재설정] | 샌드박스를 재설정하는 기능. |

## 다음 단계

이 안내서를 읽고 Experience Platform의 액세스 제어에 대한 주요 원칙을 소개했습니다. 이제 [특성 기반 액세스 제어 사용 안내서](./abac/overview.md)를 계속 진행하여 Experience Cloud을 사용하여 Experience Platform을 만들고 역할에 대한 권한을 할당하는 방법에 대한 자세한 단계를 알아볼 수 있습니다.
