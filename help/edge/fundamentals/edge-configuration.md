---
title: 에지 구성
seo-title: Experience Platform 웹 SDK용 Edge 구성
description: '경험 플랫폼 에지 네트워크를 구성하는 방법을 알아봅니다. '
seo-description: '경험 플랫폼 에지 네트워크를 구성하는 방법을 알아봅니다. '
translation-type: tm+mt
source-git-commit: 2d58f7f95c6ad125e66856350aee2f29a0499061
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---


# 에지 구성

Adobe Experience Platform Web SDK에 대한 구성은 두 곳 간에 분할됩니다. SDK의 [구성 명령은](configuring-the-sdk.md) 클라이언트와 마찬가지로 클라이언트에서 처리해야 하는 작업을 제어합니다 `edgeDomain`. Edge Configuration handles all other configuration for the SDK. Adobe Experience Platform Edge Network로 요청이 전송되면 이 `edgeConfigId` 는 서버측 구성을 참조하는 데 사용됩니다. 따라서 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

## 에지 구성 ID 만들기

Edge 구성 ID는 Launch에서 Edge 구성 도구를 사용하여 만들 수 있습니다. 이 도구를 사용하면 이러한 구성 내의 환경뿐만 아니라 Edge 구성을 모두 만들 수 있습니다.

![edge 구성 툴 탐색](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>고객은 Launch를 태그 관리자로 사용하는지에 관계없이 Edge 구성 도구를 허용 목록에 사용할 수 있습니다. 또한 사용자는 Launch에서 현상 권한을 필요로 합니다. 자세한 내용은 [론치](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/admin/user-permissions.html) 설명서의 사용자 권한 문서를 참조하십시오.

화면의 오른쪽 상단 영역에서 UICONTROL **[새 에지 구성을]** 클릭하여 Edge 구성을 만들 수 있습니다. 이름과 설명을 입력하면 각 환경에 대한 기본 설정을 묻는 메시지가 표시됩니다.

### 기본 환경 설정

이러한 기본 설정은 동일한 설정으로 처음 세 개의 환경을 만드는 데 사용됩니다. 이러한 세 가지 환경은 개발, 준비 및 생산입니다. Launch의 세 가지 기본 환경과 일치합니다. 개발 환경에 론치 라이브러리를 빌드할 때 라이브러리는 사용자의 구성의 개발 환경을 자동으로 사용합니다. 개별 환경에서 원하는 만큼 설정을 편집할 수 있습니다.

SDK에서 구성 및 환경 `edgeConfigId` 을 지정하는 복합 ID로 사용되는 ID입니다. 환경이 없으면 프로덕션 환경이 사용됩니다.

### 환경 설정

다음은 환경에서 사용할 수 있는 각 설정입니다. 대부분의 섹션은 활성화하거나 비활성화할 수 있습니다. 비활성화하면 설정이 저장되지만 활성화되지 않습니다.

#### [!UICONTROL ID]

ID 섹션은 항상 켜져 있는 유일한 섹션입니다. 두 가지 사용 가능한 설정이 있습니다. ID 동기화 활성화 및 ID 동기화 컨테이너 ID.

![구성 UI의 ID 섹션](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID 동기화 사용]

SDK가 타사 파트너와 ID 동기화를 수행하는지 여부를 제어합니다.

##### [!UICONTROL ID 동기화 컨테이너 ID]

ID 동기화를 컨테이너로 그룹화하여 서로 다른 시간에 다른 ID 동기화를 실행할 수 있습니다. 지정된 구성 ID에 대해 실행되는 ID 동기화 컨테이너를 제어합니다.

#### Adobe Experience Platform

여기에 나열된 설정을 통해 데이터를 Adobe Experience Platform으로 보낼 수 있습니다. Adobe Experience Platform을 구입한 경우에만 이 섹션을 활성화해야 합니다.

![Adobe Experience Platform 설정 블록](../../assets/edge_configuration_aep.png)

##### [!UICONTROL 샌드박스]

샌드박스는 고객이 데이터 및 구현을 서로 분리할 수 있도록 Adobe Experience Platform의 위치입니다. 작동 방식에 대한 자세한 내용은 [샌드박스 설명서에 있습니다](../../sandboxes/home.md).

##### [!UICONTROL 스트리밍 입구]

스트리밍 유입은 Adobe Experience Platform의 HTTP 소스입니다. 이러한 템플릿은 Adobe Experience Platform의 [!UICONTROL 소스] 탭 아래에서 HTTP API로 만들어집니다.

##### [!UICONTROL 이벤트 데이터 집합]

Edge 구성은 클래스 [!UICONTROL 경험 이벤트의 스키마가 있는 데이터 세트에 데이터 전송을 지원합니다].

#### Adobe Target

Adobe Target을 구성하려면 클라이언트 코드를 제공해야 합니다. 다른 필드는 선택 사항입니다.

![Adobe Target 설정 블록](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>클라이언트 코드와 연관된 조직은 구성 ID가 생성된 조직과 일치해야 합니다.

##### [!UICONTROL 클라이언트 코드]

타겟 계정의 고유 ID. 이를 찾으려면 [!UICONTROL Adobe Target] > [!UICONTROL Setup][!UICONTROL >] 구현 [!UICONTROL >] 편집 설정 [!UICONTROL 을 다음]  [!UICONTROL 으로Adobe TargetJs 또는 mbox에 대한 DownloadButton을 다운로드할 수 있습니다.jjsAppJectorJectiveBox.로 이동합니다.]

##### [!UICONTROL 속성 토큰]

Target을 사용하면 속성을 통해 권한을 제어할 수 있습니다. 세부 사항은 Target 설명서의 [엔터프라이즈 권한](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) 섹션에서 찾을 수 있습니다.

속성 토큰은 [!UICONTROL Adobe Target] > [!UICONTROL 설정] > [UICONTROL 속성에서 찾을 수 있습니다.]

##### [!UICONTROL 타겟 환경 ID]

[Adobe Target의 환경을](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) 사용하면 모든 개발 단계를 통해 구현을 관리할 수 있습니다. 이 설정은 각 환경에서 사용할 환경을 지정합니다.

Adobe에서는 이러한 설정을 각 `dev`, `stage`및 `prod` Edge 구성 환경에 대해 다르게 설정하여 간소화할 것을 권장합니다. 하지만 이미 [!UICONTROL Adobe Target 환경을] 정의한 경우에는 이러한 환경을 사용할 수 있습니다.

#### Adobe Audience Manager

Adobe Audience Manager로 데이터를 전송하는 데 필요한 모든 것은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe Audience Manage 설정 블록](../../assets/edge_configuration_aam.png)

##### [!UICONTROL 쿠키 대상 사용]

SDK가 Audience Manager의 [쿠키 대상을 통해](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 세그먼트 정보를 공유할 수 있습니다.

##### [!UICONTROL URL 대상 사용]

SDK에서 [URL 대상을 통해 세그먼트 정보를 공유할 수 있습니다](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Audience Manager에서 구성됩니다.

#### Adobe Analytics

데이터를 Adobe Analytics로 전송할지 여부를 제어합니다. 자세한 내용은 [분석 개요에 나와 있습니다](../solution-specific/analytics/analytics-overview.md).

![Adobe Analytics 설정 블록](../../assets/edge_configuration_aa.png)

##### [!UICONTROL 보고서 세트 ID]

보고서 세트는 관리 > 보고서 세트 아래의 Adobe Analytics 관리 섹션에서 [!UICONTROL 찾을 수 있습니다]. 여러 보고서 세트가 지정된 경우 데이터는 각 보고서 세트에 복사됩니다.
