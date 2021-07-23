---
title: Experience Platform Web SDK에 대한 데이터 스트림 구성
description: '데이터 스트림을 구성하는 방법을 알아봅니다. '
keywords: 구성;데이터 스트림;데이터 스트림 ID;에지;데이터 스트림 ID;환경 설정;edgeConfigId;id;ID 동기화 사용;ID 동기화 컨테이너 ID;샌드박스;스트리밍 입력;이벤트 데이터 세트;target;클라이언트 코드;속성 토큰;Target 환경 ID;쿠키 대상;URL 대상;Analytics 설정 차단 보고서 세트 ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# 데이터 스트림 구성

Adobe Experience Platform Web SDK에 대한 구성은 두 위치 간에 분할됩니다. SDK에서 [configure 명령](configuring-the-sdk.md)은 `edgeDomain`와 같이 클라이언트에서 처리해야 하는 항목을 제어합니다. 데이터 저장소는 SDK에 대한 다른 모든 구성을 처리합니다. Adobe Experience Platform Edge Network에 요청이 전송되면 `edgeConfigId` 을 사용하여 서버 측 구성을 참조합니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

이 기능에 대해 조직이 프로비저닝되어 있어야 합니다. 이를 사용하려면 고객 성공 관리자(CSM)에 허용 목록에 추가하다 문의하십시오.

## 데이터 스트림 구성 만들기

데이터 저장소는 데이터 스트림 구성 도구를 사용하여 Adobe [!DNL Experience Platform Launch]에 만들 수 있습니다.

![데이터 세트 도구 탐색](../images/datastreams/config.png)

>[!NOTE]
>
>허용 목록의 고객이 [!DNL Experience Platform Launch] 을 태그 관리자로 사용하는지 여부에 관계없이 데이터 스트림 구성 도구를 사용할 수 있습니다. 또한 사용자는 [!DNL Experience Platform Launch]에서 개발 권한이 필요합니다. 자세한 내용은 [!DNL Experience Platform Launch] 설명서의 [사용자 권한](../../tags/ui/administration/user-permissions.md) 문서를 참조하십시오.

화면의 오른쪽 상단 영역에서 **[!UICONTROL 새 데이터 스트림]**&#x200B;을 클릭하여 데이터 스트림을 만듭니다. 이름과 설명을 입력하면 각 환경에 대한 기본 설정을 묻는 메시지가 표시됩니다. 사용 가능한 설정은 아래에 자세히 설명되어 있습니다.

데이터 스트림을 만들 때 동일한 설정으로 세 개의 환경이 자동으로 만들어집니다. 이러한 세 환경은 *dev*, *stage* 및 *prod*&#x200B;입니다. 이 구성 요소는 [!DNL Experience Platform Launch]에 있는 세 가지 기본 환경과 일치합니다. 개발 환경에 [!DNL Experience Platform Launch] 라이브러리를 빌드하면 라이브러리는 구성의 개발 환경을 자동으로 사용합니다. 개별 환경에서 원하는 만큼 설정을 편집할 수 있습니다.

SDK에서 `edgeConfigId` 로 사용되는 ID는 구성과 환경을 지정하는 복합 ID입니다(예: `1c86778b-cdba-4684-9903-750e52912ad1:stage`). 복합 ID에 환경이 없는 경우(예: 이전 예제의 `stage`) 프로덕션 환경이 사용됩니다.

다음은 각 구성 환경에 사용할 수 있는 설정입니다. 대부분의 섹션은 활성화하거나 비활성화할 수 있습니다. 비활성화하면 설정이 저장되지만 활성 상태가 아닙니다.

## [!UICONTROL 타사 ID ] 설정

타사 ID 섹션은 항상 켜져 있는 유일한 섹션입니다. 사용 가능한 설정은 두 가지입니다. &quot;[!UICONTROL 타사 ID 동기화 Enabled]&quot; 및 &quot;[!UICONTROL 타사 ID 동기화 컨테이너 ID]&quot;.

![구성 UI의 ID 섹션](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL 타사 ID 동기화가 활성화됨]

SDK에서 타사 파트너와 ID 동기화를 수행하는지 여부를 제어합니다.

### [!UICONTROL 타사 ID 동기화 컨테이너 ID]

ID 동기화를 컨테이너로 그룹화하여 다른 시간에 다른 ID 동기화를 실행할 수 있습니다. 지정된 구성 ID에 대해 실행되는 ID 동기화를 제어합니다.

## Adobe Experience Platform 설정

여기에 나열된 설정을 사용하면 Adobe Experience Platform에 데이터를 보낼 수 있습니다. Adobe Experience Platform을 구입한 경우에만 이 섹션을 활성화해야 합니다.

![Adobe Experience Platform 설정 블록](../images/datastreams/edge_configuration_aep.png)

### [!UICONTROL 샌드박스]

샌드박스는 고객이 서로 데이터와 구현을 분리할 수 있도록 해주는 Adobe Experience Platform의 위치입니다. 작동 방식에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md)를 참조하십시오.

### [!UICONTROL 스트리밍 인렛]

스트리밍 유입구는 Adobe Experience Platform의 HTTP 소스입니다. 이러한 파일은 HTTP API로서 Adobe Experience Platform의 &quot;[!UICONTROL 소스]&quot; 탭 아래에 만들어집니다.

### [!UICONTROL 이벤트 데이터 세트]

데이터 저장소는 [!UICONTROL Experience Event] 클래스의 스키마가 있는 데이터 세트에 데이터 전송을 지원합니다.

## Adobe Target 설정

Adobe Target을 구성하려면 클라이언트 코드를 제공해야 합니다. 다른 필드는 선택 사항입니다.

![Adobe Target 설정 블록](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>클라이언트 코드와 연관된 조직은 구성 ID가 생성된 조직과 일치해야 합니다.

### [!UICONTROL 클라이언트 코드]

Target 계정에 대한 고유 ID입니다. 이를 찾으려면 [!UICONTROL Adobe Target] > [!UICONTROL 설정] [!UICONTROL 구현] > [!UICONTROL 편집 설정] 옆에 있는 [!UICONTROL 다운로드] 또는 [!UICONTROL at.js] 또는 [!UICONTROL mbox.js]로 이동할 수 있습니다

### [!UICONTROL 속성 토큰]

[!DNL Target] 을 사용하면 고객이 속성을 사용하여 권한을 제어할 수 있습니다. 세부 사항은 [!DNL Target] 설명서의 [엔터프라이즈 권한](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 섹션에서 찾을 수 있습니다.

속성 토큰은 [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL 속성]에서 찾을 수 있습니다.

### [!UICONTROL Target 환경 ID]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Adobe Target의 환경은 모든 개발 단계를 통해 구현을 관리하는 데 도움이 됩니다. 이 설정은 각 환경에서 사용할 환경을 지정합니다.

Adobe은 이러한 설정을 각 `dev`, `stage` 및 `prod` 데이터 스트림 환경에 대해 다르게 설정하여 보다 간편하게 유지할 것을 권장합니다. 그러나 이미 Adobe Target 환경이 정의된 경우 해당 환경을 사용할 수 있습니다.

## Adobe Audience Manager 설정

Adobe Audience Manager으로 데이터를 전송하는 데 필요한 모든 것은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe 대상 관리 설정 블록](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL 쿠키 대상 활성화]

SDK가 [!DNL Audience Manager]의 [쿠키 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)을 통해 세그먼트 정보를 공유할 수 있도록 허용합니다.

### [!UICONTROL URL 대상 사용]

SDK가 [URL 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)을 통해 세그먼트 정보를 공유할 수 있도록 허용합니다. 이러한 구성 요소는 [!DNL Audience Manager]에서 구성됩니다.

## Adobe Analytics 설정

데이터를 Adobe Analytics으로 전송할지 여부를 제어합니다. 추가 세부 사항은 [Analytics 개요](../data-collection/adobe-analytics/analytics-overview.md)에 있습니다.

![Adobe Analytics 설정 블록](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL 보고서 세트 ID]

보고서 세트는 [!UICONTROL 관리 > ReportSuites]의 Adobe Analytics 관리 섹션에 있습니다. 여러 보고서 세트를 지정하면 데이터가 각 보고서 세트에 복사됩니다.
