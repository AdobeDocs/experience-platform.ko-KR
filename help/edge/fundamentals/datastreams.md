---
title: Experience Platform Web SDK에 대한 데이터 스트림 구성
description: '데이터 스트림을 구성하는 방법을 알아봅니다. '
keywords: 구성;데이터 스트림;데이터 스트림 ID;에지;데이터 스트림 ID;환경 설정;edgeConfigId;id;ID 동기화 사용;ID 동기화 컨테이너 ID;샌드박스;스트리밍 입력;이벤트 데이터 세트;target;클라이언트 코드;속성 토큰;Target 환경 ID;쿠키 대상;URL 대상;Analytics 설정 차단 보고서 세트 ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 74c19bb0498002b81f93954d4d8e40f0df36c97d
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 1%

---


# 데이터 스트림 구성

Adobe Experience Platform Web SDK에 대한 구성은 두 위치 간에 분할됩니다. 다음 [명령 구성](configuring-the-sdk.md) sdk에서 는 다음과 같이 클라이언트에서 처리해야 하는 작업을 제어합니다. `edgeDomain`. 데이터 저장소는 SDK에 대한 다른 모든 구성을 처리합니다. Adobe Experience Platform Edge Network에 요청이 전송되면 `edgeConfigId` 서버 측 구성을 참조하는 데 사용됩니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

이 기능에 대해 조직이 프로비저닝되어 있어야 합니다. 이를 사용하려면 고객 성공 관리자(CSM)에 허용 목록에 추가하다 문의하십시오.

## 데이터 스트림 구성 만들기

을(를) 선택하여 데이터 수집 UI에서 데이터 세트를 만들고 관리할 수 있습니다 **[!UICONTROL 데이터 스트림]** 을 클릭합니다.

![데이터 세트 도구 탐색](../images/datastreams/config.png)

>[!NOTE]
>
>에 액세스할 수 있는 동안 [!UICONTROL 데이터 스트림] Platform의 태그 관리 기능을 사용하는지에 관계없이 데이터 세트를 직접 관리하려면 개발자 권한이 있어야 합니다. 자세한 내용은 [사용자 권한](../../tags/ui/administration/user-permissions.md) 자세한 내용은 태그 설명서의 문서를 참조하십시오.

아이콘을 클릭하여 데이터 스트림 만들기 **[!UICONTROL 새 데이터 스트림]** 화면 오른쪽 상단 영역에 있습니다. 이름과 설명을 입력하면 각 환경에 대한 기본 설정을 묻는 메시지가 표시됩니다. 사용 가능한 설정은 아래에 자세히 설명되어 있습니다.

데이터 스트림을 만들 때 동일한 설정으로 세 개의 환경이 자동으로 만들어집니다. 이 세 가지 환경은 다음과 같습니다 *개발*, *단계*, 및 *prod*. 태그의 세 가지 기본 환경과 일치합니다. 개발 환경에 태그 라이브러리를 빌드하면 라이브러리는 구성의 개발 환경을 자동으로 사용합니다. 개별 환경에서 원하는 만큼 설정을 편집할 수 있습니다.

SDK에서 `edgeConfigId` 구성 및 환경을 지정하는 복합 ID입니다(예: `1c86778b-cdba-4684-9903-750e52912ad1:stage`). 복합 ID에 환경이 없는 경우(예: `stage` 앞의 예에서 ) 그런 다음 프로덕션 환경이 사용됩니다.

다음은 각 구성 환경에 사용할 수 있는 설정입니다. 대부분의 섹션은 활성화하거나 비활성화할 수 있습니다. 비활성화하면 설정이 저장되지만 활성 상태가 아닙니다.

## [!UICONTROL 타사 ID] 설정

타사 ID 섹션은 항상 켜져 있는 유일한 섹션입니다. 사용 가능한 설정은 두 가지입니다. &quot;[!UICONTROL 타사 ID 동기화가 활성화됨]&quot; 및 &quot;[!UICONTROL 타사 ID 동기화 컨테이너 ID]&quot;.

![구성 UI의 ID 섹션](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL 타사 ID 동기화가 활성화됨]

SDK에서 타사 파트너와 ID 동기화를 수행하는지 여부를 제어합니다.

### [!UICONTROL 타사 ID 동기화 컨테이너 ID]

ID 동기화를 컨테이너로 그룹화하여 다른 시간에 다른 ID 동기화를 실행할 수 있습니다. 지정된 구성 ID에 대해 실행되는 ID 동기화를 제어합니다.

## Adobe Experience Platform 설정

여기에 나열된 설정을 사용하면 Adobe Experience Platform에 데이터를 보낼 수 있습니다. Adobe Experience Platform을 구입한 경우에만 이 섹션을 활성화해야 합니다.

![Adobe Experience Platform 설정 블록](../images/datastreams/platform-config.png)

| 필드 | 설명 |
| --- | --- |
| [!UICONTROL 샌드박스] | **(필수)** 데이터를 보낼 Platform 샌드박스를 선택합니다. 샌드박스는 조직의 다른 샌드박스와 데이터 및 구현을 분리할 수 있는 Adobe Experience Platform의 가상 파티션입니다.<br><br>샌드박스를 선택하지 않고 데이터 스트림을 만드는 경우 나중에 샌드박스를 선택할 수 있습니다.<br><br>데이터 스트림을 만들고 샌드박스를 선택하면 샌드박스를 변경할 수 없습니다. 다음 [!UICONTROL 샌드박스] 따라서 선택한 샌드박스로 기존 데이터 스트림을 편집할 때는 선택 필드를 사용할 수 없습니다.<br><br> 다음 [!UICONTROL 샌드박스] 따라서 기존 데이터 스트림을 편집할 때는 선택 필드를 사용할 수 없습니다.<br><br>Experience Platform에서 샌드박스의 역할에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md). |
| [!UICONTROL 이벤트 데이터 세트] | **(필수)** 고객 이벤트 데이터를 스트리밍할 플랫폼 데이터 세트를 선택합니다. 이 스키마는 [XDM ExperienceEvent 클래스](../../xdm/classes/experienceevent.md). |
| [!UICONTROL 프로필 데이터 세트] | 고객 특성 데이터를 전송할 Platform 데이터 세트를 선택합니다. 이 스키마는 [XDM 개별 프로필 클래스](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Platform Web SDK 구현에 Offer decisioning을 활성화하려면 이 확인란을 선택하십시오. 다음 안내서를 참조하십시오. [platform Web SDK에서 Offer decisioning 사용](../personalization/offer-decisioning/offer-decisioning-overview.md) 를 참조하십시오. offer decisioning 기능에 대한 자세한 내용은 [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=ko-KR). |
| [!UICONTROL 에지 세그멘테이션] | 이 확인란을 선택하여 [에지 세분화](../../segmentation/ui/edge-segmentation.md) 이 데이터 스트림에 대해 설명합니다. Platform Web SDK가 Edge 세그먼테이션이 활성화된 데이터 스트림을 통해 데이터를 전송하면 해당 프로필에 대해 업데이트된 세그먼트 멤버십이 응답으로 다시 전송됩니다.<br><br>이 옵션은 [!UICONTROL 개인화 대상] 대상 [다음 페이지 개인화 사용 사례](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 개인화 대상] | 와 함께 사용하는 경우 [!UICONTROL 에지 세그멘테이션] 확인란을 선택하면 이 옵션을 사용하여 데이터 스트림이 Adobe Target과 같은 개인화 엔진에 연결할 수 있습니다. 의 특정 단계에 대해서는 대상 설명서 를 참조하십시오 [개인화 대상 구성](../../destinations/ui/configure-personalization-destinations.md). |

## Adobe Target 설정

Adobe Target을 구성하려면 클라이언트 코드를 제공해야 합니다. 다른 필드는 선택 사항입니다.

![Adobe Target 설정 블록](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>클라이언트 코드와 연관된 조직은 구성 ID가 생성된 조직과 일치해야 합니다.

### [!UICONTROL 클라이언트 코드]

Target 계정에 대한 고유 ID입니다. 이를 찾으려면 다음 위치로 이동할 수 있습니다 [!UICONTROL Adobe Target] > [!UICONTROL 설정]> [!UICONTROL 구현] > [!UICONTROL 설정 편집] 다음 [!UICONTROL 다운로드] 버튼 [!UICONTROL at.js] 또는 [!UICONTROL mbox.js]

### [!UICONTROL 속성 토큰]

[!DNL Target] 을 사용하면 고객이 속성을 사용하여 권한을 제어할 수 있습니다. 자세한 내용은 [Enterprise 권한](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 섹션 [!DNL Target] 설명서.

속성 토큰은 [!UICONTROL Adobe Target] > [!UICONTROL 설정] > [!UICONTROL 속성]

### [!UICONTROL Target 환경 ID]

[환경](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Adobe Target에서는 모든 개발 단계를 통해 구현을 관리하는 데 도움이 됩니다. 이 설정은 각 환경에서 사용할 환경을 지정합니다.

Adobe은 각 항목에 대해 이 설정을 다르게 설정할 것을 권장합니다 `dev`, `stage`, 및 `prod` 데이터 스트림 환경을 통해 작업을 단순화할 수 있습니다. 그러나 이미 Adobe Target 환경이 정의된 경우 해당 환경을 사용할 수 있습니다.

## Adobe Audience Manager 설정

Adobe Audience Manager으로 데이터를 전송하는 데 필요한 모든 것은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe 대상 관리 설정 블록](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL 쿠키 대상 활성화]

SDK가 를 통해 세그먼트 정보를 공유할 수 있도록 허용합니다 [쿠키 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 변환 전: [!DNL Audience Manager].

### [!UICONTROL URL 대상 사용]

SDK가 를 통해 세그먼트 정보를 공유할 수 있도록 허용합니다 [URL 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). 이러한 구성 요소는 [!DNL Audience Manager].

## Adobe Analytics 설정

데이터를 Adobe Analytics으로 전송할지 여부를 제어합니다. 자세한 내용은 [Analytics 개요](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics 설정 블록](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL 보고서 세트 ID]

보고서 세트는 아래의 Adobe Analytics 관리 섹션에 있습니다 [!UICONTROL 관리 > 보고서 세트]. 여러 보고서 세트를 지정하면 데이터가 각 보고서 세트에 복사됩니다.
