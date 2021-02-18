---
title: Experience Platform 웹 SDK용 Edge 구성 만들기
description: 'Experience Platform 에지 네트워크를 구성하는 방법을 알아봅니다. '
keywords: 구성;edge;edge 구성 id;환경 설정;edgeConfigId;id 동기화 사용;ID 동기화 컨테이너 ID;샌드박스;스트리밍 가져오기;이벤트 데이터 세트;대상;클라이언트 코드;Target 환경 ID;쿠키 대상;URL 대상;Analytics 설정 블록 보고서 세트 id;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---


# 에지 구성 만들기

Adobe Experience Platform Web SDK에 대한 구성은 두 곳으로 분할됩니다. SDK의 [구성 명령](configuring-the-sdk.md)은 `edgeDomain`와 같이 클라이언트에서 처리해야 하는 작업을 제어합니다. Edge 구성은 SDK에 대한 다른 모든 구성을 처리합니다. Adobe Experience Platform Edge Network에 요청이 전송되면 `edgeConfigId`은(는) 서버측 구성을 참조하는 데 사용됩니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

이 기능에 대해 조직이 프로비저닝되어야 합니다. CSM(Customer Success Manager)에 문의하여를 허용 목록에 추가하다 사용해 보십시오.

## 에지 구성 만들기

가장자리 구성 도구를 사용하여 [!DNL Experience Platform Launch] Adobe에서 가장자리 구성을 만들 수 있습니다.

![edge 구성 툴 탐색](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Edge 구성 도구는 허용 목록 고객이 [!DNL Experience Platform Launch]을(를) 태그 관리자로 사용하는지에 관계없이 사용할 수 있습니다. 또한 사용자는 [!DNL Experience Platform Launch]에 현상 권한이 필요합니다. 자세한 내용은 [!DNL Experience Platform Launch] 설명서의 [사용자 권한](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/admin/user-permissions.html) 문서를 참조하십시오.

화면의 오른쪽 위 영역에서 **[!UICONTROL 새 가장자리 구성]**&#x200B;을 클릭하여 가장자리 구성을 만듭니다. 이름과 설명을 입력하면 각 환경에 대한 기본 설정을 묻는 메시지가 표시됩니다. 사용 가능한 설정은 아래에 자세히 설명되어 있습니다.

Edge 구성을 만들 때 동일한 설정으로 3개의 환경이 자동으로 만들어집니다. 이러한 세 가지 환경은 *dev*, *stage* 및 *prod*&#x200B;입니다. 이 세 환경은 [!DNL Experience Platform Launch]의 세 가지 기본 환경과 일치합니다. 개발 환경에 [!DNL Experience Platform Launch] 라이브러리를 빌드하면 라이브러리는 구성에서 개발 환경을 자동으로 사용합니다. 개별 환경에서 원하는 만큼 설정을 편집할 수 있습니다.

`edgeConfigId`으로 SDK에 사용되는 ID는 구성과 환경을 지정하는 합성 ID입니다(예: `1c86778b-cdba-4684-9903-750e52912ad1:stage`). 합성 ID에 환경이 없으면(예: 이전 예제의 `stage`) 프로덕션 환경이 사용됩니다.

아래에서는 각 구성 환경에 사용할 수 있는 설정을 찾을 수 있습니다. 대부분의 섹션은 활성화하거나 비활성화할 수 있습니다. 비활성화하면 설정이 저장되지만 활성화되지 않습니다.

## [!UICONTROL IdentitySettings ] 설정

ID 섹션은 항상 켜져 있는 유일한 섹션입니다. 사용 가능한 설정은 두 가지입니다.&quot;[!UICONTROL ID 동기화 활성화됨]&quot; 및 &quot;[!UICONTROL ID 동기화 컨테이너 ID]&quot;.

![구성 UI의 ID 섹션](../../assets/edge_configuration_identity.png)

### [!UICONTROL ID 동기화 사용]

SDK가 타사 파트너와의 ID 동기화를 수행하는지 여부를 제어합니다.

### [!UICONTROL ID 동기화 컨테이너 ID]

ID 동기화를 컨테이너로 그룹화하여 서로 다른 ID 동기화를 다른 시간에 실행할 수 있도록 할 수 있습니다. 지정된 구성 ID에 대해 실행되는 ID 동기화 컨테이너를 제어합니다.

## Adobe Experience Platform 설정

여기에 나열된 설정을 통해 데이터를 Adobe Experience Platform으로 보낼 수 있습니다. Adobe Experience Platform을 구입한 경우에만 이 섹션을 활성화해야 합니다.

![Adobe Experience Platform 설정 블록](../../assets/edge_configuration_aep.png)

### [!UICONTROL 샌드박스]

샌드박스는 Adobe Experience Platform에서 고객이 데이터와 구현을 서로 분리할 수 있도록 하는 위치입니다. 작동 방법에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md)를 참조하십시오.

### [!UICONTROL 스트리밍 입구]

스트리밍 입구는 Adobe Experience Platform의 HTTP 소스입니다. 이러한 템플릿은 Adobe Experience Platform의 &quot;[!UICONTROL 소스]&quot; 탭 아래에 HTTP API로 만들어집니다.

### [!UICONTROL 이벤트 데이터 세트]

에지 구성은 [!UICONTROL 경험 이벤트] 클래스의 스키마가 있는 데이터 집합에 데이터 전송을 지원합니다.

## Adobe Target 설정

Adobe Target을 구성하려면 클라이언트 코드를 제공해야 합니다. 다른 필드는 선택 사항입니다.

![Adobe Target 설정 블록](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>클라이언트 코드와 연관된 조직은 구성 ID가 생성된 조직과 일치해야 합니다.

### [!UICONTROL 클라이언트 코드]

타겟 계정의 고유 ID. 이를 찾으려면 [!UICONTROL Adobe Target] > [!UICONTROL 설정] [!UICONTROL 구현] > [!UICONTROL 설정 편집][!UICONTROL [!UICONTROL 다운로드] 단추([!UICONTROL at.js] 또는 )로 이동할 수 있습니다. 2/>mbox.js]

### [!UICONTROL 속성 토큰]

[!DNL Target] 속성을 사용하여 권한을 제어할 수 있습니다. 자세한 내용은 [!DNL Target] 설명서의 [엔터프라이즈 권한](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) 섹션에서 찾을 수 있습니다.

속성 토큰은 [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL 속성]에서 찾을 수 있습니다.

### [!UICONTROL Target 환경 ID]

[Adobe Target](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) 의 환경을 사용하면 모든 개발 단계를 통해 구현을 관리할 수 있습니다. 이 설정은 각 환경에서 사용할 환경을 지정합니다.

Adobe에서는 작업을 단순화하기 위해 `dev`, `stage` 및 `prod` 에지 구성 환경에 대해 이 설정을 다르게 설정하는 것이 좋습니다. 그러나 이미 Adobe Target 환경이 정의된 경우 이러한 환경을 사용할 수 있습니다.

## Adobe Audience Manager 설정

Adobe Audience Manager으로 데이터를 전송하는 데 필요한 모든 것은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe 대상 관리 설정 블록](../../assets/edge_configuration_aam.png)

### [!UICONTROL 쿠키 대상 활성화]

SDK가 [!DNL Audience Manager]의 [쿠키 대상](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)을 통해 세그먼트 정보를 공유할 수 있도록 허용합니다.

### [!UICONTROL URL 대상이 활성화됨]

SDK가 [URL 대상](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)을 통해 세그먼트 정보를 공유할 수 있도록 허용합니다. 이러한 구성 요소는 [!DNL Audience Manager]에서 구성됩니다.

## Adobe Analytics 설정

데이터를 Adobe Analytics으로 전송할지 여부를 제어합니다. 자세한 내용은 [분석 개요](../data-collection/adobe-analytics/analytics-overview.md)에 있습니다.

![Adobe Analytics 설정 블록](../../assets/edge_configuration_aa.png)

### [!UICONTROL 보고서 세트 ID]

보고서 세트는 [!UICONTROL 관리 > 보고서 세트] 아래의 Adobe Analytics 관리 섹션에서 찾을 수 있습니다. 여러 보고서 세트가 지정된 경우 데이터는 각 보고서 세트에 복사됩니다.
