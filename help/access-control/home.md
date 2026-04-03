---
keywords: Experience Platform;홈;인기 항목;액세스 제어;adobe admin console
solution: Experience Platform
title: 액세스 제어 개요
description: Adobe Experience Platform에 대한 액세스 제어는 Adobe Admin Console을 통해 제공됩니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '3279'
ht-degree: 0%

---

# 액세스 제어 개요

Adobe Experience Platform에 대한 액세스 제어는 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 ](https://experience.adobe.com/)을(를) 통해 제공됩니다. 이 기능은 권한 및 샌드박스를 사용자와 연결하는 역할 및 정책을 활용합니다.

## 액세스 제어 계층 및 워크플로

Experience Platform에 대한 액세스 제어를 구성하려면 Experience Platform 제품이 있는 조직에 대한 시스템 또는 제품 관리자 권한이 있어야 합니다. 권한을 부여하거나 철회할 수 있는 최소 역할은 제품 관리자입니다. 권한을 관리할 수 있는 다른 관리자 역할은 시스템 관리자(제한 없음)입니다. 자세한 내용은 [관리 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html)에 대한 Adobe 도움말 센터 문서를 참조하십시오.

>[!NOTE]
>
>이 시점에서부터 이 문서에서 &quot;관리자&quot;에 대한 언급은 제품 관리자 이상(위에 설명된 대로)을 의미합니다.

액세스 권한을 얻고 할당하기 위한 높은 수준의 워크플로는 다음과 같이 요약할 수 있습니다.

- Adobe Experience Platform 또는 Experience Platform을 사용하는 애플리케이션/앱 서비스에 라이선스를 부여하면 라이선스 부여 중에 지정된 관리자에게 이메일이 전송됩니다.
- 관리자가 [Adobe Admin Console](#adobe-admin-console)에 로그인하고 개요 페이지의 제품 목록에서 **Adobe Experience Platform**&#x200B;을(를) 선택합니다.
- Experience Platform에 대한 액세스 권한을 부여하려면 관리자가 기본 제품 프로필에 사용자를 추가하는 것이 좋습니다. `AEP-Default-All-Users`.
- Experience Platform 권한에서 관리자는 새 역할을 만들거나 기존 역할에 대한 권한 및 사용자를 편집할 수 있습니다.
- 역할을 만들거나 편집할 때 관리자는 **[!UICONTROL users]** 탭을 사용하여 역할에 사용자를 추가하고, 역할 권한을 편집하여 이러한 사용자(예: &quot;[!UICONTROL Read Datasets]&quot; 또는 &quot;[!UICONTROL Manage Schemas]&quot;)에게 권한을 부여합니다. 마찬가지로 관리자는 동일한 편집 옵션을 사용하여 샌드박스에 대한 액세스 권한을 할당할 수 있습니다.
- 사용자가 Experience Platform 사용자 인터페이스에 로그인할 때 Experience Platform 기능에 대한 액세스는 이전 단계에서 부여된 권한에 의해 결정됩니다. 예를 들어 사용자에게 [!UICONTROL View Datasets] 권한이 없는 경우 측면 메뉴의 **[!UICONTROL Datasets]** 탭이 해당 사용자에게 표시되지 않습니다.

Experience Platform에서 액세스 제어를 관리하는 방법에 대한 자세한 단계는 [액세스 제어 사용 안내서](./ui/overview.md)를 참조하십시오.

Experience Platform API에 대한 모든 호출은 권한에 대해 유효성이 검사되며, 현재 사용자 컨텍스트에서 적절한 권한을 찾을 수 없는 경우 오류를 반환합니다. UI 내에서 요소는 현재 사용자에게 부여된 권한에 따라 숨겨지거나 변경됩니다.

## 권한 {#platform-permissions}

[!UICONTROL Permissions]은(는) 조직의 Experience Platform 액세스를 관리하기 위한 중앙 위치를 제공합니다. [!UICONTROL Permissions]을(를) 통해 사용자 그룹에 [!UICONTROL Manage Datasets], [!UICONTROL View Datasets] 또는 [!UICONTROL Manage Profiles]과(와) 같은 다양한 Experience Platform 기능에 대한 액세스 권한을 부여할 수 있습니다.

### 역할

[!UICONTROL Roles] 섹션에서 권한은 역할을 사용하여 사용자에게 할당됩니다. 역할을 사용하면 한 명 또는 여러 사용자에게 권한을 부여할 수 있으며, 역할을 통해 할당된 샌드박스 범위에 대한 액세스 권한도 포함할 수 있습니다. 사용자는 조직에 속한 하나 또는 여러 역할에 할당할 수 있습니다.

### 기본 역할

Experience Platform에는 두 개의 사전 구성된 기본 역할이 포함되어 있습니다. 다음 표는 액세스 권한을 부여하는 샌드박스와 해당 샌드박스의 범위 내에서 부여하는 권한을 포함하여 각 기본 프로필에서 제공되는 내용을 간략하게 설명합니다.

| 역할 | 샌드박스 액세스 | 권한 |
| --- | --- | --- |
| 기본 프로덕션 모든 액세스 | Prod | 샌드박스 관리 권한을 제외하고 Experience Platform에 적용할 수 있는 모든 권한입니다. |
| 샌드박스 관리자 | N/A | `Prod` 샌드박스 및 샌드박스 관리 권한에 대한 액세스를 제공합니다. |

## 샌드박스 및 권한

비프로덕션 샌드박스는 다른 샌드박스와 데이터를 분리할 수 있는 데이터 가상화 의 한 형태이며 일반적으로 개발 실험, 테스트 또는 시도에 사용됩니다. 역할 권한은 역할 사용자에게 액세스 권한이 부여된 샌드박스 환경 내의 Experience Platform 기능에 대한 액세스 권한을 부여합니다. 기본 Experience Platform 라이선스는 샌드박스 5개(프로덕션 1개 및 비프로덕션 4개)를 부여합니다. 비프로덕션 샌드박스 10개 팩 및 총 75개 샌드박스를 추가할 수 있습니다. 자세한 내용은 조직의 관리자 또는 Adobe 영업 담당자에게 문의하십시오.

Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.

### 샌드박스에 대한 액세스

샌드박스에 대한 액세스는 역할을 통해 관리됩니다. 역할의 샌드박스에 대한 액세스를 활성화하는 방법에 대한 자세한 단계는 [특성 기반 액세스 제어 역할 안내서](./abac/ui/roles.md)를 참조하십시오.

사용자는 역할 내에서 하나 이상의 샌드박스에 대한 액세스 권한을 부여 받을 수 있습니다. 한 명의 사용자가 둘 이상의 역할에 포함된 경우 해당 사용자는 해당 역할에 포함된 모든 샌드박스에 액세스할 수 있습니다.

사용자는 &quot;샌드박스 관리&quot; 권한을 사용하여 샌드박스를 관리, 확인 또는 재설정할 수 있습니다.

### 리소스 권한 {#permissions}

리소스 권한은 특정 Experience Platform 기능에 대한 액세스 권한을 부여합니다. 리소스는 역할에 개별적으로 할당할 수 있는 관련 권한 세트가 포함된 범주로 분류됩니다.

[!UICONTROL Permissions]에서 역할의 리소스 작업 영역은 해당 역할에 대해 활성 상태인 샌드박스 및 권한을 표시합니다.

![선택한 범주 및 사용 권한 목록이 있는 역할의 리소스 작업 영역입니다.](./images/permissions.png)

다음 표에서는 권한을 통해 관리되는 Experience Platform과 애플리케이션 모두에서 사용 가능한 리소스 범주를 설명합니다.

| 카테고리 | 설명 |
| --- | --- |
| [!DNL Adobe Mix Modeler] | [!DNL Adobe Mix Modeler]에 대한 권한을 구성, 관리 및 봅니다. |
| [!DNL AI Assistant] | [!DNL AI Assistant]에 대한 권한을 구성합니다. |
| [!DNL Alerts] | 경고 및 경고 내역에 대한 관리, 해결 및 보기 권한을 구성합니다. |
| [!DNL B2B Account Lists] | 계정 목록에서 계정 추가, 제거, 가져오기 및 삭제와 같은 작업을 포함하여 B2B 계정 목록에 대한 관리, 보기 및 게시 권한을 구성합니다. |
| [!DNL B2B Admin Configurations] | 디지털 자산 관리 연결, 자산 저장소 및 이벤트를 포함한 B2B 관리 구성에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL B2B Assets] | 이메일, SMS, 랜딩 페이지, 조각, 템플릿 및 이미지를 포함하여 B2B 자산에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL B2B Buying Groups] | 솔루션 관심사, 역할 템플릿 및 구매 그룹 상태와 같은 기능을 포함하여 B2B 구매 그룹에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL B2B Channel Configurations] | 통신 제한, API 자격 증명, 보안 설정 등의 설정을 포함하여 B2B 채널 구성에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL B2B Dashboards] | 계정 참여, 구매 그룹 단계, 급증하는 계정 및 연락처 범위와 같은 기능을 포함하여 B2B 대시보드에 대한 보기 권한을 구성합니다. |
| [!DNL B2B Journeys] | 계정 및 사용자 작업, 이벤트 리스너 및 분할 여정과 같은 기능을 포함하여 B2B 경로에 대한 관리, 보기 및 게시 권한을 구성합니다. |
| [!DNL Campaigns] | Journey Optimizer에서 캠페인에 대한 관리, 게시 및 보기 권한을 구성합니다. |
| [!DNL Channel Configurations] | 하위 도메인, IP 풀, 메시지 사전 설정, PTR 레코드, 제외 목록, 랜딩 페이지 설정, SMS 설정 및 파일 라우팅과 같은 채널 구성 기능을 관리, 보기 및 내보냅니다. |
| [!DNL Collaborations] | Real-Time Customer Data Profile Collaboration 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Computed Attributes] | 초안 또는 게시된 계산된 속성에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Customer Managed Keys] | 고객 관리 키에 대한 관리 권한을 구성합니다. |
| [!DNL Dashboards] | 표준, 사용자 지정 및 사용 허가된 대시보드에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Collection] | 데이터스트림에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Governance] | 레이블, 정책 및 활동 로그와 같은 데이터 유지 관리 기능에 대한 관리, 적용 및 보기 권한을 구성합니다. |
| [!DNL Data Ingestion] | 소스 및 대상 공유와 같은 데이터 수집 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Lifecycle] | 데이터 위생 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Management] | 데이터 세트 및 스트림 모니터링과 같은 데이터 관리 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Modeling] | 스키마, 관계 및 ID 메타데이터와 같은 데이터 모델링 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace]에 대한 관리 권한을 구성합니다. |
| [!DNL Decision Management] | 의사 결정 관리의 의사 결정, 오퍼 및 등급 전략 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Destinations] | 활성화 및 대상 SDK 작성과 같은 기능을 포함하여 대상에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Federated Data] | 페더레이션 데이터 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Identity Management] | ID 네임스페이스 및 ID 그래프와 같은 ID 서비스 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Intelligent Service] | 인텔리전트 서비스에서 기여도 AI 및 고객 AI에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL IP Warmup Configurations] | IP 준비 계획에 대한 관리 및 보기 권한을 구성하고 IP 준비 보고서를 보기 위한 권한을 봅니다. |
| [!DNL Journey Optimizer Library] | Adobe Journey Optimizer에서 라이브러리 항목에 대한 관리 권한을 구성합니다. |
| [!DNL Journey Optimizer Rules] | Adobe Journey Optimizer에서 빈도 규칙에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Journeys] | 여정 보고서, 이벤트, 데이터 소스 및 작업과 같은 기능을 포함하여 여정에 대한 관리, 게시 및 보기 권한을 구성합니다. |
| [!DNL Messages] | 메시지 미리 보기 및 테스트와 같은 기능을 포함하여 메시지에 대한 관리, 게시 및 보기 권한을 구성합니다. |
| [!DNL Privacy Service] | Privacy Service 기능에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Profile Management] | 대상자, 프로필 및 병합 정책과 같은 프로필 서비스 기능에 대한 관리, 보기, 내보내기 및 평가 권한을 구성합니다. |
| [!DNL Prospects] | 잠재 고객 스키마, 프로필, 대상자(예: 잠재 고객 아코디언 보기)에 대한 관리 및 보기 권한을 구성합니다. |
| [!DNL Query Service] | 만료되지 않는 자격 증명 및 구조화된 SQL 쿼리와 같은 서비스 기능을 쿼리하기 위한 권한 관리를 구성합니다. |
| [!DNL Reports] | 채널 보고서에 대한 보기 권한을 구성합니다. |
| [!DNL Run and Operate] | 상태 확인 및 작업 일정과 같은 실행 및 작업 기능에 대한 보기 권한을 구성합니다. |
| [!DNL Sandbox Administration] | 샌드박스를 관리할 때 관리, 보기 및 재설정 권한을 구성합니다. |
| [!DNL Traits Configuration] | 계산된 속성 UI를 통해 트레이트 관리 및 보기를 구성합니다. |
| [!DNL Translation Services] | 프로젝트, 작업, 검토, 내부, 설정 및 공급자에 대한 번역 서비스에 대한 관리 및 보기 권한을 구성합니다. |

다음 표는 해당 역할에서 Experience Platform이 사용할 수 있는 권한을 간략하게 설명합니다(액세스 권한을 부여하는 특정 Experience Platform 기능 설명). 역할에 권한을 추가하는 방법에 대한 자세한 단계는 [특성 기반 액세스 제어 역할 안내서](./abac/ui/roles.md)를 참조하십시오.

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | 조화로운 데이터를 보고 수정하는 기능입니다. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | 조화된 데이터에 대한 읽기 전용 액세스 |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | 모델 구성을 보고 수정하는 기능입니다. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | 모델 구성에 대한 읽기 전용 액세스 권한. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | 계획 구성을 보고 수정하는 기능입니다. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | 계획 구성에 대한 읽기 전용 액세스 권한. |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | [!DNL [AI assistant]](../ai-assistant/access.md)개의 질문을 할 수 있습니다. |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | [operational insights](../ai-assistant/home.md##operational-insights) 쿼리에 대한 응답을 얻을 수 있는 액세스 권한. |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | 사용자가 [!DNL AI Assistant]을(를) 사용하여 콘텐츠를 생성할 수 있도록 설정하십시오. |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | 사용자가 [!DNL AI Assistant]을(를) 사용하여 브랜드 지침을 만들 수 있도록 합니다. |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | 경고 내역에 대한 읽기 전용 액세스 권한. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | 경고를 읽고, 편집하고, 삭제할 수 있는 액세스 권한 |
| [!DNL Alerts] | [!UICONTROL View Alerts] | 경고에 대한 읽기 전용 액세스 권한. |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | 경고를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Account Lists]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Account Lists]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 계정 목록 CRUD 기능에 액세스할 수 있어야 합니다. `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | 왼쪽 탐색 메뉴에서 **[!UICONTROL B2B Admin Configurations]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL B2B Admin Configurations]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 SMS API 자격 증명 CRUD 기능에 액세스할 수 있어야 합니다. `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Assets]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Assets]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 Assets CRUD 기능에 액세스할 수 있어야 합니다. `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Templates]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Templates]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 템플릿 CRUD 함수 `/b2b-content-templates`에 액세스할 수 있어야 합니다. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Fragments]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Fragments]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 조각 CRUD 함수에 액세스할 수 있어야 합니다. `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Buying Groups]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Buying Groups]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 구매 그룹 CRUD 기능에 액세스할 수 있어야 합니다. `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Dashboard]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Dashboards]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 대시보드 CRUD 기능에 액세스할 수 있어야 합니다. `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Channels]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Channels]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 채널 CRUD 함수에 액세스할 수 있어야 합니다. `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | 왼쪽 탐색 메뉴에서 **[!UICONTROL Account Journeys]**&#x200B;을(를) 보고 액세스할 수 있습니다. **[!UICONTROL Account Journeys]**&#x200B;에 대한 액세스 권한이 있는 사용자는 모든 계정 여정 CRUD 함수에 액세스할 수 있어야 합니다. `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | 캠페인을 읽고, 만들고, 편집하고, 삭제할 수 있는 권한. |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | 캠페인을 승인하고 게시할 수 있습니다. |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | 캠페인을 게시할 수 있습니다. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | 캠페인에 대한 읽기 전용 액세스 권한 |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | 캠페인 보고서에 대한 읽기 전용 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | 메시지 일반 설정에 대한 읽기 전용 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | 하위 도메인 위임을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | IP 풀을 읽고 만들고 편집할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | 메시지 일반 설정을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | 메시지 사전 설정을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | 메시지 사전 설정에 대한 읽기 전용 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | PTR 기록 읽기 및 편집 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | PTR 레코드에 대한 읽기 전용 액세스 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | 비표시 규칙 읽기, 생성, 편집 및 삭제 액세스 |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | 비표시 목록에 대한 읽기 전용 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | 비표시 목록을 CSV 파일로 내보내기 위한 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | 랜딩 페이지 설정을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | SMS 설정을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | SMS 하위 도메인을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | 파일 공정순서를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | 파일 공정순서에 대한 읽기 전용 액세스 |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | 시드 목록을 만들고 편집하는 기능입니다. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | 언어 설정을 만들고 편집하는 기능. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | CJM 웹 하위 도메인을 만들고 편집하는 기능. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | 푸시 자격 증명을 작성, 편집 및 삭제하는 기능. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | 조직의 공동 작업 인스턴스를 보고, 만들고, 업데이트하고, 삭제합니다. 다른 조직의 공동 작업 인스턴스를 검색합니다. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | 조직의 공동 작업 인스턴스를 읽고 다른 조직의 공동 작업 인스턴스를 검색합니다. |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | 조직에서 시작한 연결 초대를 보고, 만들고, 삭제합니다. 다른 조직에서 시작한 연결 초대를 수락 및 거부합니다. |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | 연결 초대에 대한 읽기 전용 액세스 권한. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | 광고주는 설정을 보고 만들고 업데이트하며 연결을 제출하고 삭제할 수 있습니다. 게시자는 연결을 보거나, 수락하거나, 거부할 수 있습니다. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | 연결에 대한 읽기 전용 액세스 권한. |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | 온보딩하고 대상자를 검색합니다. 공개, 비공개 및 사용자 지정 대상을 업데이트하고 대상 인벤토리 메타데이터 설정을 관리합니다. |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | 대상자를 읽고 검색합니다. |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | 측정 데이터를 온보딩, 업데이트 및 삭제합니다. |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | 측정 데이터에 대한 읽기 전용 액세스 |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | 검색, 공유, 활성화 및 측정 활동에 대한 프로젝트를 보고, 만들고, 업데이트하고, 삭제합니다. |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | 검색, 공유, 활성화 및 측정 활동에 대한 프로젝트를 봅니다. |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | 사용자 활동에 대한 읽기 전용 액세스 권한. |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | 사용자 활동을 내보냅니다. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | 조직 및 인스턴스 레벨에서 신용 모니터링 |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | 계산된 속성 탭, 인벤토리 및 세부 정보에 대한 읽기 전용 액세스 권한. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | 계산된 속성을 읽고, 만들고, 삭제하고, 비활성화할 수 있는 액세스 권한. |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | 고객 관리 키를 보고 구성하는 데 액세스합니다. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | 라이선스 사용 대시보드를 보려면 읽기 전용 권한입니다. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Data Warehouse에 아직 없는 사용자 지정 특성을 추가합니다. |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | 프로필, 대상 및 세그먼트 대시보드에 대한 읽기 전용 액세스 권한입니다. 또한 왼쪽 탐색 및 대시보드 인벤토리 및 통합 탭에서 대시보드에 액세스할 수 있습니다. |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | 대시보드를 만들거나 편집할 수 있는 액세스 권한. |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | 사용자 정의 대시보드에 대한 읽기 전용 액세스 권한. |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | 일정을 만들 수 있습니다. |
| [!DNL Dashboards] | [!UICONTROL Export Dashboard Data] | Query pro 모드 대시보드에서 표 형식 데이터를 내보내는 사용자 기능을 제어합니다. |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | 데이터 스트림을 읽고, 만들고, 편집할 수 있는 액세스 권한. |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | 데이터스트림에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | 사용 레이블을 읽고, 만들고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | 데이터 사용 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | 조직에 속한 데이터 사용 정책에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | Experience Platform 활동의 기록된 [감사 로그](../landing/governance-privacy-security/audit-logs/overview.md)를 보기 위한 읽기 전용 액세스입니다. |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | 개인 정보 콘솔에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | **[!UICONTROL Catalog]** 탭의 사용 가능한 소스와 **[!UICONTROL Browse]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한입니다. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 파트너 공유를 만들고, 수락하고, 거부하여 두 조직에 연결하고, [!DNL Segment Match] 흐름을 사용하도록 설정할 수 있습니다. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 활성 파트너와 함께 [!DNL Segment Match] 피드를 읽기, 만들기, 편집 및 게시할 수 있는 액세스 권한이 있습니다. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | 데이터 라이프사이클에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | 데이터 라이프사이클을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | 스키마 및 관련 리소스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | 스키마 및 관련 리소스에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | 스키마 관계 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | 스키마에 대한 ID 메타데이터를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | 데이터 세트 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | 데이터 세트 및 스키마에 대한 읽기 전용 액세스 권한. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | 모니터링 데이터 세트 및 스트림에 대한 읽기 전용 액세스. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | [!DNL Data Science Workspace]에서 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | 경험 결정 엔티티를 관리하는 기능. |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | 경험 결정 엔티티에 대한 읽기 전용 액세스 권한. |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | 의사 결정 엔티티를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | 의사 결정 엔티티에 대한 읽기 전용 액세스 권한. |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | 모든 오퍼 및 구성 요소를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한입니다. 의사 결정 및 컬렉션에 대한 읽기 전용 액세스 권한. |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | 사용자 정의 보고서를 읽고, 만들고, 편집하고, 삭제하고, 작업 기능을 사용할 수 있는 액세스 권한. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | **[!UICONTROL Catalog]** 탭에서 사용 가능한 대상 및 **[!UICONTROL Browse]** 탭에서 인증된 대상을 보려면 읽기 전용 액세스하십시오. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | 대상 연결 및 대상 계정을 읽고 만들고 삭제할 수 있는 액세스 권한. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | 생성된 활성 대상에 데이터를 활성화하는 기능. 이 권한을 사용하려면 대상을 활성화할 사용자에게 [!UICONTROL View Destinations] 또는 [!UICONTROL Manage Destinations]을(를) 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | [매핑 단계](../destinations/ui/activate-batch-profile-destinations.md#mapping)를 표시하지 않고 기존 대상에 대상을 활성화하는 기능입니다. 사용자는 활성화 워크플로에서 대상을 추가하거나 제거할 수 있지만 매핑된 속성 또는 ID를 추가하거나 제거할 수 없습니다. 이 권한을 사용하려면 대상에 데이터를 활성화하는 사용자에게 [!UICONTROL View Destinations] 권한을 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | 데이터 세트 내보내기 흐름을 읽고, 만들고, 편집하고, 비활성화하는 기능입니다. 생성된 활성 데이터 세트에 대한 데이터도 활성화할 수 있습니다. 이 권한을 사용하려면 대상에 데이터를 활성화하는 사용자에게 [!UICONTROL View Destinations] 권한을 부여해야 합니다. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)을(를) 사용하여 대상을 작성할 수 있습니다. |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | 스키마, 모델 및 컴포지션 생성과 같은 모든 페더레이션 데이터 기능에 액세스하는 기능. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | ID 네임스페이스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | ID 네임스페이스에 대한 읽기 전용 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | ID 그래프에 대한 읽기 전용 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | ID 설정을 읽고, 만들고, 편집할 수 있는 액세스 권한. |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | ID 설정에 대한 읽기 전용 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | 기여도 AI 설정 및 인사이트에 대한 읽기 전용 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | 기여도 AI 모델을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한을 제공합니다. |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | 고객 AI 모델을 읽거나 볼 수 있는 액세스 권한. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | 고객 AI 모델을 생성, 업데이트, 삭제, 활성화 또는 비활성화할 수 있는 액세스 권한. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | IP 웜업 플랜에 대한 읽기 전용 액세스 권한. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | IP 웜업 계획을 관리하는 기능입니다. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | IP 준비 보고서에 대한 읽기 전용 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | 여정 읽기, 만들기, 편집 및 삭제 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL View Journeys] | 여정에 대한 읽기 전용 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | 여정 보고서에 대한 읽기 전용 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | 이벤트, 데이터 소스 또는 작업을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | 이벤트, 데이터 소스 또는 작업에 대한 읽기 전용 액세스 권한. |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | 정책이 적용될 때 여정을 승인하고 게시하는 기능. |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | 여정 게시 기능. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | 저장된 표현식을 추가 및 삭제하는 기능입니다. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | 콘텐츠 조각을 게시하는 기능입니다. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | 미리보기 및 교정을 위한 콘텐츠 시뮬레이트 옵션에 액세스 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | 빈도 규칙에 대한 읽기 전용 액세스 권한 |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | 빈도 규칙을 읽기, 만들기, 편집 또는 삭제할 수 있는 액세스 권한. |
| [!DNL Messages] | [!UICONTROL Manage Messages] | 메시지 읽기, 만들기, 편집 및 삭제에 대한 액세스 권한. |
| [!DNL Messages] | [!UICONTROL View Messages] | 메시지에 대한 읽기 전용 액세스 |
| [!DNL Messages] | [!UICONTROL View Messages Report] | 메시지 보고서를 읽고 편집할 수 있는 액세스 권한. |
| [!DNL Messages] | [!UICONTROL Publish Messages] | 메시지를 게시할 수 있습니다. |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | 정책이 적용될 때 메시지를 승인하고 게시하는 기능. |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | 개인 정보 보호 워크플로우를 읽고 쓸 수 있는 액세스 권한. |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | 개인 정보 보호 워크플로에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | 고객 프로필에 사용되는 데이터 세트를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. 사용 가능한 프로필에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | 사용 가능한 프로필에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | 대상자를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | 사용 가능한 대상자에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | 병합 정책을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | 사용 가능한 병합 정책에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | CSV 업로드 워크플로우를 사용하여 새 대상을 가져오는 기능. |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | 평가된 대상을 데이터 세트로 내보낼 수 있습니다. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | 세그먼트 정의를 평가하여 대상자에 대한 프로필을 생성하는 기능. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | 모든 B2B AI/ML 서비스에 대한 설정 및 구성에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | 모든 B2B AI/ML 서비스에 대한 설정 및 구성을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | B2B 엔티티 프로필(예: 계정, 영업 기회 등), 모든 B2B AI/ML 서비스에 대한 설정 및 구성, B2B 대시보드 위젯에 대한 읽기 전용 액세스입니다. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | B2B 엔티티 프로필(예: 계정, 영업 기회 등)을 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한입니다. 모든 B2B AI/ML 서비스 및 B2B 대시보드 위젯에 대한 설정 및 구성에 대한 읽기 전용 액세스입니다. |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | 유사 대상을 만들거나 삭제하는 기능입니다. |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | B2B 프로필 및 속성을 보는 기능. |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | 모든 프로필 설정에 대한 읽기 전용 액세스 권한. |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | 모든 프로필 설정을 읽고 편집할 수 있는 액세스 권한 |
| [!DNL Prospects] | [!UICONTROL View Prospects] | 잠재 고객 스키마, 프로필, 대상자 및 잠재 고객 아코디언에 대한 읽기 전용 액세스 권한. |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | 잠재 고객 스키마, 프로필 및 고객을 만들고 관리하는 기능. 잠재 고객 아코디언에 대한 읽기 전용 액세스 권한. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Experience Platform 데이터에 대한 구조화된 SQL 쿼리를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | 쿼리 서비스 액세스에 대한 만료되지 않는 자격 증명을 생성, 업데이트 및 삭제할 수 있는 액세스 권한입니다. |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | 기존 세션을 제거할 수 있습니다. |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | 조직의 IP 제한 사항을 관리하는 기능. |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | 채널 보고서를 보고 수정하는 기능입니다. |
| [!DNL Run and Operate] | [!UICONTROL View Health Checks] | 상태 검사에 대한 읽기 전용 액세스 권한. |
| [!DNL Run and Operate] | [!UICONTROL View Job Schedules] | 작업 일정에 대한 읽기 전용 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | 샌드박스를 읽고, 만들고, 편집하고, 삭제할 수 있는 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | 조직에 속한 샌드박스에 대한 읽기 전용 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | 샌드박스를 재설정하는 기능. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | 패키지를 생성, 가져오기 또는 내보내기 위한 액세스 권한. |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | 다른 조직에서 패키지를 공유할 수 있는 액세스 권한. |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | 트레이트에 대한 읽기 전용 액세스입니다. |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | 트레이트 관리에 대한 액세스 권한. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | 번역 프로젝트를 관리하는 기능입니다. |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | 번역 프로젝트에 대한 읽기 전용 액세스 권한. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | 번역 작업을 관리하는 기능. |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | 번역 작업에 대한 읽기 전용 액세스 권한. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | 번역 리뷰를 관리하는 기능. |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | 번역 검토에 대한 읽기 전용 액세스 권한. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | 사내 번역 관리 기능. |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | 사내에서 읽기 전용 번역 액세스 권한. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | 관리자가 번역 설정을 관리할 수 있는 기능입니다. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | 번역 공급업체를 관리하는 기능입니다. |

## 다음 단계

이 안내서를 읽고 Experience Platform의 액세스 제어의 주요 원칙을 소개했습니다. 이제 [특성 기반 액세스 제어 사용 안내서](./abac/overview.md)로 이동하여 Experience Cloud을 사용하여 Experience Platform에 대한 역할을 만들고 권한을 할당하는 방법에 대한 자세한 단계를 알아볼 수 있습니다.
