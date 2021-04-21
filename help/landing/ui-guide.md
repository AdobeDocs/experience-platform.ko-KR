---
keywords: Experience Platform;홈;인기 항목;Adobe Experience Platform;사용자 안내서;플랫폼 ui 안내서;플랫폼 소개;대시보드;Dashboard;Folio;home;popular topics;;user guide;ui guide;platform ui guide;introduction to platform;dashboard
solution: Experience Platform
title: Experience Platform UI 개요
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Adobe Experience Platform UI 가이드

이 안내서는 다양한 구성 요소가 사용되는 내용을 설명하고 추가 설명서에 대한 링크를 제공하는 Adobe Experience Platform 사용자 인터페이스(UI)를 사용하는 방법에 대한 소개로 사용됩니다.

Adobe Experience Platform에 대한 자세한 내용은 [Experience Platform 개요](home.md)를 참조하십시오.

## 홈 화면

Adobe Experience Platform에 로그인하면 [!UICONTROL Home] 페이지에 표시됩니다. 이 페이지는 [지표 대시보드](#metrics), [최근 데이터](#recent-data) 및 [권장 학습](#recommended-learning) 섹션으로 구성됩니다.

![](images/user-guide/homepage.png)

### 지표

지표 대시보드는 조직 내의 데이터 세트, 프로필, 세그먼트 및 대상에 대한 정보를 제공하는 카드를 제공합니다.

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL Datasets]** 섹션에는 IMS 조직 내의 데이터 세트 수가 표시됩니다. 이 숫자는 새 데이터 세트를 만들 때 업데이트됩니다. 데이터 집합에 대한 자세한 내용은 [데이터 집합 개요](../catalog/datasets/overview.md)에서 확인할 수 있습니다.

**[!UICONTROL Profiles]** 섹션에는 프로필 조각을 제외하고 IMS 조직 내에 프로필이 있는 총 사람 수가 표시됩니다. 이 총 사람 수는 총 주소 지정 가능 대상을 나타내며 24시간마다 한 번씩 업데이트됩니다. 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Segments]** 섹션에는 IMS 조직 내에서 만들어진 총 세그먼트 수가 표시됩니다. 이 번호는 새 세그먼트가 만들어질 때 업데이트됩니다. 세그먼트에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../segmentation/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Destinations]** 섹션에는 IMS 조직에 대해 만들어진 총 대상 수가 표시됩니다. 이 번호는 새 대상이 만들어질 때 업데이트됩니다. 대상에 대한 자세한 내용은 [대상 개요](../destinations/home.md)에서 확인할 수 있습니다.

### 최근 데이터

최근 데이터 대시보드에서는 최근에 만든 데이터 세트, 소스, 세그먼트 및 대상에 대한 정보를 제공합니다.

![](images/user-guide/homepage-recent.png)

**[!UICONTROL Recent datasets]** 섹션에는 IMS 조직 내에서 가장 최근에 만든 데이터 세트 5개가 나열됩니다. 이 목록은 새 데이터 세트를 만들 때마다 업데이트됩니다. 목록에서 데이터 세트를 선택하여 지정된 데이터 집합에 대한 자세한 정보를 보거나 **[!UICONTROL View all]**&#x200B;을 선택하여 만들어진 모든 데이터 집합 목록을 볼 수 있습니다. 데이터 집합에 대한 자세한 내용은 [데이터 집합 개요](../catalog/datasets/overview.md)에서 확인할 수 있습니다.

**[!UICONTROL Recent sources]** 섹션에는 IMS 조직 내에서 가장 최근에 만든 소스 커넥터 5개가 나열됩니다. 이 목록은 새 소스 커넥터를 만들 때마다 업데이트됩니다. 목록에서 소스 연결을 선택하여 지정한 커넥터에 대한 자세한 정보를 보거나 **[!UICONTROL View all]**&#x200B;을 선택하여 만들어진 모든 소스 연결 목록을 볼 수 있습니다. 소스에 대한 자세한 내용은 [소스 개요](../sources/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Recent segments]** 섹션에는 IMS 조직 내에서 가장 최근에 만든 5개의 세그먼트 정의가 나열됩니다. 이 목록은 새 세그먼트 정의를 만들 때마다 업데이트됩니다. 목록에서 세그먼트 정의를 선택하여 지정된 세그먼트 정의에 대한 자세한 정보를 보거나 **[!UICONTROL View all]**&#x200B;을 선택하여 만들어진 모든 세그먼트 정의 목록을 볼 수 있습니다. 세그먼트에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../segmentation/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Recent destinations]** 섹션에는 IMS 조직 내에서 가장 최근에 만든 5개의 대상 목록이 표시됩니다. 이 목록은 새 대상을 만들 때마다 업데이트됩니다. 목록에서 대상을 선택하여 지정된 대상에 대한 자세한 정보를 보거나 **[!UICONTROL View all]**&#x200B;을 선택하여 만들어진 모든 대상 목록을 볼 수 있습니다. 대상에 대한 자세한 내용은 [대상 개요](../destinations/home.md)에서 확인할 수 있습니다.

### 권장 학습

**[!UICONTROL Recommended learning]** 섹션에서는 Adobe Experience Platform을 시작하기 위한 유용한 설명서에 대한 링크를 제공합니다.

![](images/user-guide/homepage-recommended.png)

## 위쪽 내비게이션 막대

플랫폼 UI의 위쪽 탐색 모음에는 현재 로그인된 IMS 조직이 표시되고 몇 가지 중요한 컨트롤이 제공됩니다.

내비게이션 바의 왼쪽에 Adobe Experience Platform 로고가 있습니다. 언제든지 이 옵션을 선택하면 플랫폼 UI 홈 화면으로 돌아갑니다.

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS 조직 전환기

위쪽 탐색 모음 오른쪽에 있는 첫 번째 항목은 **IMS 조직 전환기**&#x200B;입니다.

![](./images/user-guide/homepage-ims-org.png)

전환기를 선택하면 IMS의 드롭다운 메뉴가 열립니다. 액세스할 수 있는 조직이 있습니다(가능한 경우). 나열된 옵션을 선택하여 해당 IMS 조직으로 전환합니다.

![](./images/user-guide/homepage-ims-org-switcher.png)

### 애플리케이션 전환

위쪽 탐색의 오른쪽에 있는 다음 항목은 ![응용 프로그램 전환기](./images/user-guide/app-switcher-icon.png) 아이콘으로 표시되는 **응용 프로그램 전환기**&#x200B;입니다. 이 아이콘을 선택하면 Experience Platform, Analytics, Assets 및 Launch와 같이 IMS 조직에서 액세스할 수 있는 Adobe 애플리케이션 간을 전환할 수 있습니다.

### 도움말

응용 프로그램 전환기의 오른쪽에는 **도움말 및 지원 메뉴**&#x200B;이 있으며, 이 메뉴는 ![물음표/help](./images/user-guide/help-icon.png) 아이콘으로 표시됩니다. 이 아이콘을 선택하면 여러 도움말 및 지원 리소스가 포함된 팝업 메뉴가 나타납니다. **[!UICONTROL Help]** 탭에는 현재 사용 중인 페이지에 대한 관련 문서 목록이 표시됩니다. **[!UICONTROL Support]** 탭에서는 Adobe 지원 팀과 함께 지원 티켓을 만들 수 있습니다. **[!UICONTROL Feedback]** 탭에서는 플랫폼에 대한 피드백을 Adobe에 제출할 수 있습니다.

![](images/user-guide/homepage-help-clicked.png)

### 알림 및 공지

**알림 섹션**&#x200B;에서 ![벨/알림 및 공지](images/user-guide/notification-icon.png) 아이콘으로 표시됩니다. **[!UICONTROL Notifications]** 탭에는 제품 및 기타 관련 업데이트에 대한 중요한 정보가 표시되지만 **[!UICONTROL Announcements]** 탭에는 서비스 유지 관리에 대한 정보가 표시됩니다.

### 사용자 프로필

위쪽 내비게이션 막대의 최종 항목은 **사용자 설정**&#x200B;이며 ![사용자 설정/사용자 프로필](images/user-guide/profile-icon.png) 아이콘으로 표시됩니다. 환경 설정을 편집하거나 로그아웃하려면 이 아이콘을 선택합니다.

### 샌드 박스

위쪽 내비게이션 막대 바로 아래에 샌드박스 막대가 있습니다. 이 막대는 현재 플랫폼에 사용 중인 샌드박스를 표시합니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)에서 확인할 수 있습니다.

## 왼쪽 탐색 {#left-nav}

화면 왼쪽의 탐색은 플랫폼 UI에서 지원되는 모든 다른 서비스를 나열합니다.

>[!IMPORTANT]
>
>왼쪽 탐색 막대의 일부 섹션이 나타나지 않거나 회색으로 표시될 수 있습니다. 이러한 기능에 액세스할 수 없기 때문입니다. 이러한 섹션에 대한 액세스 권한이 있는 경우 시스템 관리자에게 문의하십시오.

![](images/user-guide/homepage-left.png)

**[!UICONTROL Home]** 섹션에서는 플랫폼 UI 홈 페이지로 돌아갈 수 있습니다.

**[!UICONTROL Workflows]** 섹션에는 플랫폼 내에서 작업을 수행하기 위한 여러 단계 작업 과정 목록이 표시됩니다. 워크플로우에 대한 자세한 내용은 [워크플로우 개요](./workflows.md)에서 확인할 수 있습니다.

### [!UICONTROL Connections]

**[!UICONTROL Sources]** 섹션에서 소스 연결을 생성, 업데이트 및 삭제할 수 있으므로 외부 소스의 데이터를 플랫폼에 인제스트할 수 있습니다. 소스에 대한 자세한 내용은 [소스 개요](../sources/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Destinations]** 섹션에서 대상을 만들고 업데이트 및 삭제할 수 있으므로 플랫폼에서 여러 외부 대상으로 데이터를 내보낼 수 있습니다. 대상에 대한 자세한 내용은 [대상 개요](../destinations/home.md)에서 확인할 수 있습니다.

### [!UICONTROL Customer]

**[!UICONTROL Profiles]** 섹션에서는 고객 프로파일을 검색하고, 프로필 지표를 보고, 병합 정책을 만들고 관리하고, 결합 스키마를 볼 수 있습니다. [!UICONTROL Profiles] 섹션 사용에 대한 자세한 내용은 [[!DNL Profile] 사용자 안내서](../profile/ui/user-guide.md)를 참조하십시오. 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Segments]** 섹션에서 세그먼트 정의를 만들고 관리할 수 있습니다. [!UICONTROL Segments] 섹션 사용에 대한 자세한 내용은 [세그멘테이션 사용자 안내서](../segmentation/ui/overview.md)를 참조하십시오. 세그멘테이션 서비스에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../segmentation/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Identities]** 섹션에서는 ID 네임스페이스를 만들고 관리할 수 있습니다. ID 네임스페이스에 대한 정보 및 플랫폼 UI에서 ID를 사용하는 방법에 대한 정보를 포함하여 [!UICONTROL Identities] 섹션에 대한 자세한 내용은 [ID 네임스페이스 개요](../identity-service/namespaces.md)를 참조하십시오.

### [!UICONTROL Privacy]

**[!UICONTROL Policies]** 섹션에서 데이터 사용 정책을 만들고 관리할 수 있습니다. 정책 섹션 사용에 대한 자세한 내용은 [데이터 사용 정책 사용자 안내서](../data-governance/policies/user-guide.md)를 참조하십시오. 데이터 사용 정책에 대한 자세한 내용은 [데이터 사용 정책 개요](../data-governance/policies/overview.md)에서 확인할 수 있습니다.

**[!UICONTROL Requests]** 섹션에서 개인 정보 요청을 만들고 관리할 수 있습니다. Privacy Service UI에 액세스하려면허용 목록에추가된 반드시 있어야 합니다. 요청 섹션 사용에 대한 자세한 내용은 [Privacy Service 사용 안내서](../privacy-service/ui/user-guide.md)를 참조하십시오. Privacy Service에 대한 자세한 내용은 [Privacy Service 개요](../privacy-service/home.md)에서 확인할 수 있습니다.

### [!UICONTROL Data Science]

**[!UICONTROL Notebooks]** 섹션에서는 데이터를 탐색, 분석 및 모델링할 수 있는 대화형 개발 환경인 JupiterLab에 대한 액세스 권한을 제공합니다. 노트북 섹션 사용에 대한 자세한 내용은 [JupiterLab 사용자 안내서](../data-science-workspace/jupyterlab/overview.md)를 참조하십시오. 데이터 과학 작업 공간에 대한 자세한 내용은 [데이터 과학 작업 공간 개요](../data-science-workspace/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Models]** 섹션에서는 머신 러닝과 인공 지능을 활용하여 모델을 생성, 개발, 교육 및 조정하여 예측하도록 할 수 있습니다. 모델 섹션에 대한 자세한 내용은 [교육 튜토리얼에서 확인할 수 있으며 모델](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)을 평가합니다.

**[!UICONTROL Services]** 섹션에서는 예약된 트레이닝 및 점수에 대해 게시된 모델을 관리하거나, 개인화된 실시간 고객 경험을 제공하는 일련의 AI 서비스인 Adobe의 지능형 서비스를 활용할 수 있습니다. 서비스 섹션에 대한 자세한 내용은 [모델을 서비스 자습서](../data-science-workspace/models-recipes/publish-model-service-ui.md)로 게시를 참조하십시오.

### [!UICONTROL Data management]

**[!UICONTROL Schemas]** 섹션에서는 XDM(경험 데이터 모델) 스키마를 만들고 관리할 수 있습니다. 스키마에 대한 자세한 내용을 보려면 [스키마 만들기](../xdm/tutorials/create-schema-ui.md)의 자습서를 참조하십시오. XDM에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md)에서 확인할 수 있습니다.

**[!UICONTROL Datasets]** 섹션에서 데이터 집합을 만들고 관리할 수 있습니다. 데이터 집합에 대한 자세한 내용은 [데이터 집합 사용자 안내서](../catalog/datasets/user-guide.md)에서 확인할 수 있습니다.

**[!UICONTROL Queries]** 섹션에서는 쿼리를 만들고 관리하고 Adobe Experience Platform 쿼리 서비스에서 만든 SQL 쿼리를 기록하고 PostgreSQL 자격 증명을 볼 수 있습니다. 쿼리에 대한 자세한 내용은 [쿼리 서비스 사용 안내서](../query-service/ui/overview.md)에서 확인할 수 있습니다.

**[!UICONTROL Monitoring]** 섹션에서는 일괄 처리 및 스트리밍 통합 과정을 모니터링할 수 있습니다. 모니터링에 대한 자세한 내용은 [데이터 통합 사용자 안내서](../ingestion/quality/monitor-data-ingestion.md)에서 확인할 수 있습니다.

### [!UICONTROL Decisioning]

Offer Decisioning은 Adobe Experience Platform과 통합된 애플리케이션 서비스입니다.  Experience Platform을 활용하면 정확한 타이밍에 모든 접점에서 고객에게 최적의 오퍼와 경험을 제공할 수 있습니다. [!UICONTROL Offers] 및 [!UICONTROL Activities] 작업을 포함하여 Offer decisioning에 대한 자세한 내용을 보려면 [Offer decisioning 설명서](https://experienceleague.adobe.com/docs/offer-decisioning.html)를 방문하십시오.

### [!UICONTROL Administration]

플랫폼 UI(사용자 인터페이스)는 일일 스냅샷 중에 캡처되는 대로 조직의 라이센스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 탐색에서 **[!UICONTROL License usage]**&#x200B;을 선택하여 액세스할 수 있습니다. 라이센스 사용 대시보드에 대한 자세한 내용은 [라이센스 사용 대시보드 안내서](license-usage-dashboard.md)를 참조하십시오.

>[!IMPORTANT]
>
>라이센스 사용 대시보드 기능은 현재 알파 상태이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

## 다음 단계

이 안내서를 읽고 나면 이제 플랫폼 UI의 홈 페이지와 주요 탐색 요소에 대해 소개되었습니다. 사용자 인터페이스에서 작업하는 방법에 대한 자세한 내용은 각 개별 플랫폼 서비스에 대한 설명서를 참조하십시오. 이 문서에 대한 링크는 이 문서 앞에 있는 [왼쪽 탐색](#left-nav) 섹션에 제공됩니다.
