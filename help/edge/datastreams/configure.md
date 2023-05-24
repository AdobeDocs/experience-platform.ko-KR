---
title: 데이터스트림 구성
description: 클라이언트측 웹 SDK 통합을 다른 Adobe 제품 및 서드파티 대상과 연결하는 방법에 대해 알아봅니다.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 209aa63717e05fabc8742ac591102b8fdb243ee4
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 2%

---


# 데이터스트림 구성

이 문서에서는 를 구성하는 단계를 설명합니다. [데이터스트림](./overview.md) UI에서

## 액세스 [!UICONTROL 데이터스트림] 작업 영역

을 선택하여 데이터 수집 UI 또는 Experience Platform UI에서 데이터스트림을 만들고 관리할 수 있습니다. **[!UICONTROL 데이터스트림]** 왼쪽 탐색.

![데이터 수집 UI의 데이터 스트림 탭](../assets/datastreams/configure/datastreams-tab.png)

다음 **[!UICONTROL 데이터스트림]** 탭에는 친숙한 이름, ID 및 마지막 수정 날짜를 포함하여 기존 데이터 스트림 목록이 표시됩니다. 데이터 스트림의 이름을 선택하십시오. [세부 정보 보기 및 서비스 구성](#view-details).

&quot;기타&quot; 아이콘(**...**)을 클릭하여 특정 데이터 스트림에 사용할 수 있습니다. 선택 **[!UICONTROL 편집]** 을(를) 업데이트하려면 [기본 구성](#configure) 데이터 스트림에 대해 또는 을 선택합니다. **[!UICONTROL 삭제]** 데이터 스트림을 제거합니다.

![기존 데이터 스트림을 편집하거나 삭제하는 옵션](../assets/datastreams/configure/edit-datastream.png)

## 새 데이터 스트림 만들기 {#create}

데이터 스트림을 생성하려면 다음을 선택하여 시작합니다. **[!UICONTROL 새 데이터스트림]**.

![새 데이터스트림](../assets/datastreams/configure/new-datastream-button.png)을 선택합니다

구성 단계에서 시작하는 데이터 스트림 만들기 워크플로우가 나타납니다. 여기에서 데이터 스트림의 이름과 선택적 설명을 제공해야 합니다.

Experience Platform에서 사용하도록 이 데이터 스트림을 구성하고 Platform Web SDK를 사용하는 경우 [이벤트 기반 XDM(경험 데이터 모델) 스키마](../../xdm/classes/experienceevent.md) 수집 예정인 데이터를 나타냅니다.

![데이터 스트림에 대한 기본 구성](../assets/datastreams/configure/configure.png)

선택 **[!UICONTROL 고급 옵션]** 데이터 스트림을 구성할 추가 컨트롤을 표시합니다.

![고급 구성 옵션](../assets/datastreams/configure/advanced-options.png) {#advanced-options}

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 지리적 위치] | 사용자의 IP 주소를 기반으로 지리적 위치 조회가 발생하는지 여부를 결정합니다. 기본 설정 **[!UICONTROL 없음]** 지리적 위치 조회를 비활성화하는 반면 **[!UICONTROL 도시]** 를 설정하면 소수점 두 자리로 GPS 좌표가 제공됩니다. 지리적 위치는 다음 이전 [!UICONTROL IP 난독화] 의 영향을 받지 않습니다.  [!UICONTROL IP 난독화] 설정. |
| [!UICONTROL IP 난독화] | 데이터 스트림에 적용할 IP 난독화의 유형을 나타냅니다. 고객 IP를 기반으로 하는 모든 처리는 IP 난독화 설정의 영향을 받습니다. 데이터스트림에서 데이터를 받는 모든 Experience Cloud 서비스가 여기에 포함됩니다. <p>사용 가능한 옵션:</p> <ul><li>**[!UICONTROL 없음]**: IP 난독화를 비활성화합니다. 전체 사용자 IP 주소는 데이터 스트림을 통해 전송됩니다.</li><li>**[!UICONTROL 부분]**: IPv4 주소의 경우 사용자 IP 주소의 마지막 옥텟을 난독화합니다. IPv6 주소의 경우 주소의 마지막 80비트를 난독화합니다. <p>예:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL 전체]**: 전체 IP 주소를 난독화합니다. <p>예:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> IP 난독화가 다른 Adobe 제품에 미치는 영향: <ul><li>**Adobe Target**: 데이터 스트림 수준 [!UICONTROL IP 난독화] 설정은 Adobe Target에 설정된 IP 난독화 옵션보다 우선합니다. 예를 들어 데이터 스트림 수준이 [!UICONTROL IP 난독화] 옵션이 로 설정되어 있습니다. **[!UICONTROL 전체]** 그리고 Adobe Target IP 난독화 옵션이 로 설정되어 있습니다. **[!UICONTROL 마지막 옥텟 난독화]**, Adobe Target은 완전히 난독화된 IP를 수신하게 됩니다. 에서 Adobe Target 설명서 참조 [IP 난독화](https://developer.adobe.com/target/before-implement/privacy/privacy/) 및 [지리적 위치](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=en) 을 참조하십시오.</li><li>**Audience Manager**: 데이터스트림 수준의 IP 난독화 설정이 Audience Manager에 설정된 모든 IP 난독화 옵션보다 우선하며 모든 IP 주소에 적용됩니다. Audience Manager에 의해 수행된 모든 지리적 위치 조회는 데이터 스트림 수준의 영향을 받습니다 [!UICONTROL IP 난독화] 옵션을 선택합니다. 완전히 난독화된 IP를 기반으로 하는 Audience Manager에서 지리적 위치 조회를 수행하면 알 수 없는 영역이 발생하고 결과 지리적 위치 데이터를 기반으로 하는 모든 세그먼트는 실현되지 않습니다. 다음에서 Audience Manager 설명서 참조: [IP 난독화](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=en) 을 참조하십시오.</li><li>**Adobe Analytics**: 현재 없음 이외의 IP 난독화 옵션을 선택한 경우 Adobe Analytics에서 부분적으로 난독화된 IP 주소를 받습니다. Analytics가 완전히 난독화된 IP 주소를 수신하려면 Adobe Analytics에서 별도로 IP 난독화를 구성해야 합니다. 이 동작은 향후 릴리스에서 업데이트됩니다. Adobe Analytics 보기 [설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) analytics에서 IP 난독화를 활성화하는 방법에 대한 자세한 내용을 참조하십시오.</li></ul> |
| [!UICONTROL 자사 ID 쿠키] | 이 설정을 활성화하면 Edge Network가 를 조회할 때 지정된 쿠키를 참조하도록 지시합니다. [자사 디바이스 ID](../identity/first-party-device-ids.md): ID 맵에서 이 값을 조회하는 대신<br><br>이 설정을 활성화할 때 ID가 저장될 쿠키의 이름을 제공해야 합니다. |
| [!UICONTROL 타사 ID 동기화] | ID 동기화를 컨테이너로 그룹화하여 서로 다른 시간에 서로 다른 ID 동기화를 실행할 수 있습니다. 이 설정을 사용하면 이 데이터 스트림에 대해 실행할 ID 동기화 컨테이너를 지정할 수 있습니다. |
| [!UICONTROL 타사 ID 동기화 컨테이너 ID] | 서드파티 ID 동기화에 사용할 컨테이너의 숫자 ID입니다. |
| [!UICONTROL 컨테이너 ID 무시] | 이 섹션에서는 기본 ID를 재정의하는 데 사용할 수 있는 추가 타사 ID 동기화 컨테이너 ID를 정의할 수 있습니다. |
| [!UICONTROL 액세스 유형] | 데이터 스트림에 대해 Edge Network가 허용하는 인증 유형을 정의합니다. <ul><li>**[!UICONTROL 혼합 인증]**: 이 옵션을 선택하면 Edge Network가 인증된 요청과 인증되지 않은 요청을 모두 수락합니다. 웹 SDK를 사용하거나 [Mobile SDK](https://aep-sdks.gitbook.io/docs/)와 함께 [서버 API](../../server-api/overview.md). </li><li>**[!UICONTROL 인증만]**: 이 옵션을 선택하면 Edge Network가 인증된 요청만 수락합니다. 서버 API만 사용하고 인증되지 않은 요청이 Edge Network에 의해 처리되지 않도록 하려는 경우 이 옵션을 선택합니다.</li></ul> |

여기에서 Experience Platform을 위해 데이터스트림을 구성하는 경우 [데이터 수집을 위한 데이터 준비](./data-prep.md) 이 안내서로 돌아가기 전에 데이터를 Platform 이벤트 스키마에 매핑합니다. 그렇지 않으면 를 선택합니다. **[!UICONTROL 저장]** 다음 섹션으로 계속 진행하십시오.

## 데이터스트림 세부 정보 보기 {#view-details}

새 데이터 스트림을 구성하거나 기존 데이터 스트림을 선택하여 보려는 경우 해당 데이터 스트림에 대한 세부 정보 페이지가 나타납니다. 여기에서 ID를 포함하여 데이터 스트림에 대한 추가 정보를 찾을 수 있습니다.

![생성된 데이터 스트림에 대한 세부 정보 페이지](../assets/datastreams/configure/view-details.png)

데이터 스트림 세부 정보 화면에서 다음을 수행할 수 있습니다. [서비스 추가](#add-services) 을 사용하여 액세스 권한이 있는 Adobe Experience Cloud 제품의 기능을 활성화할 수 있습니다. 데이터 스트림의 [기본 구성](#create), 업데이트 [매핑 규칙](./data-prep.md), [데이터 스트림 복사](#copy)또는 완전히 삭제합니다.

## 데이터 스트림에 서비스 추가 {#add-services}

데이터스트림의 세부 정보 페이지에서 **[!UICONTROL 서비스 추가]** 를 입력하여 해당 데이터스트림에 사용 가능한 서비스를 추가할 수 있습니다.

![계속하려면 서비스 추가를 선택하십시오.](../assets/datastreams/configure/add-service.png)

다음 화면에서는 드롭다운 메뉴를 사용하여 이 데이터 스트림에 대해 구성할 서비스를 선택합니다. 액세스 권한이 있는 서비스만 이 목록에 표시됩니다.

![목록에서 서비스 선택](../assets/datastreams/configure/service-selection.png)

원하는 서비스를 선택하고 표시되는 구성 옵션을 입력한 다음 을 선택합니다 **[!UICONTROL 저장]** 를 입력하여 데이터스트림에 서비스를 추가할 수 있습니다. 추가된 모든 서비스는 데이터 스트림에 대한 세부 사항 보기에 표시됩니다.

![데이터스트림에 추가된 서비스](../assets/datastreams/configure/services-added.png)

아래 하위 섹션에서는 각 서비스의 구성 옵션에 대해 설명합니다.

>[!NOTE]
>
>각 서비스 구성에는 **[!UICONTROL 활성화됨]** 서비스를 선택하면 자동으로 활성화되는 전환입니다. 이 데이터스트림에 대해 선택한 서비스를 비활성화하려면 **[!UICONTROL 활성화됨]** 다시 전환합니다.

### Adobe Analytics 설정 {#analytics}

이 서비스는 데이터를 Adobe Analytics으로 전송할지 여부와 방법을 제어합니다. 추가 세부 정보는 의 안내서에서 확인할 수 있습니다. [analytics에 데이터 보내기](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics 설정 블록](../assets/datastreams/configure/analytics-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 보고서 세트 ID] | **(필수)** 전송한 데이터를 받을 Analytics 보고서 세트의 ID입니다. 이 ID는 Adobe Analytics UI의 [!UICONTROL 관리자] > [!UICONTROL 보고서 세트]. 여러 보고서 세트를 지정하면 데이터가 각 보고서 세트에 복사됩니다. |
| [!UICONTROL 보고서 세트 무시] | 이 섹션에서는 기본 ID를 재정의하는 데 사용할 수 있는 추가 보고서 세트 ID를 추가할 수 있습니다. |

### Adobe Audience Manager 설정 {#audience-manager}

이 서비스는 데이터를 Adobe Audience Manager으로 전송할지 여부와 방법을 제어합니다. Audience Manager에 데이터를 보내는 데 필요한 모든 사항은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe 대상자 관리 설정 블록](../assets/datastreams/configure/audience-manager-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 쿠키 대상 활성화됨] | SDK가 다음을 통해 세그먼트 정보를 공유할 수 있습니다. [쿠키 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 출처: [!DNL Audience Manager]. |
| [!UICONTROL URL 대상 활성화됨] | SDK가 다음을 통해 세그먼트 정보를 공유할 수 있습니다. [URL 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 출처: [!DNL Audience Manager]. |

### Adobe Experience Platform 설정 {#aep}

>[!IMPORTANT]
>
>Platform용 데이터 스트림을 활성화할 때 UI의 상단 리본에 표시된 대로 현재 사용 중인 Platform 샌드박스를 주목하십시오.
>
>![선택한 샌드박스](../assets/datastreams/configure/platform-sandbox.png)
>
>샌드박스는 조직의 다른 파티션과 데이터 및 구현을 격리할 수 있는 Adobe Experience Platform의 가상 파티션입니다. 데이터 스트림이 만들어지면 해당 샌드박스를 변경할 수 없습니다. Experience Platform에서 샌드박스의 역할에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md).

이 서비스는 데이터를 Adobe Experience Platform으로 전송할지 여부와 방법을 제어합니다.

![Adobe Experience Platform 설정 블록](../assets/datastreams/configure/platform-config.png)

| 설정 | 설명 |
|---| --- |
| [!UICONTROL 이벤트 데이터 세트] | **(필수)** 고객 이벤트 데이터를 스트리밍할 Platform 데이터 세트를 선택합니다. 이 스키마는 [XDM ExperienceEvent 클래스](../../xdm/classes/experienceevent.md). 데이터 세트를 추가하려면 다음을 선택합니다. **[!UICONTROL 이벤트 데이터 세트 추가]**. |
| [!UICONTROL 프로필 데이터 세트] | 고객 속성 데이터를 전송할 Platform 데이터 세트를 선택합니다. 이 스키마는 [XDM 개별 프로필 클래스](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Platform Web SDK 구현에 대한 Offer decisioning을 활성화하려면 이 확인란을 선택합니다. 다음 안내서를 참조하십시오 [platform Web SDK로 Offer decisioning 사용](../personalization/offer-decisioning/offer-decisioning-overview.md) 구현 세부 사항.<br><br>offer decisioning 기능에 대한 자세한 내용은 [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=ko-KR). |
| [!UICONTROL Edge 세그멘테이션] | 활성화하려면 이 확인란을 선택하십시오. [가장자리 세분화](../../segmentation/ui/edge-segmentation.md) 이 데이터스트림에 사용됩니다. SDK가 에지 세그멘테이션이 활성화된 데이터 스트림을 통해 데이터를 전송하면 해당 프로필의 업데이트된 세그먼트 멤버십이 응답으로 다시 전송됩니다.<br><br>이 옵션은 다음과 함께 사용할 수 있습니다. [!UICONTROL 개인화 대상] 대상 [다음 페이지 개인화 사용 사례](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 개인화 대상] | 을(를) 활성화한 후 을(를) 활성화할 때 [!UICONTROL Edge 세그멘테이션] 확인란을 선택하면 데이터 스트림을 다음과 같은 개인화 대상에 연결할 수 있습니다. [사용자 정의 개인화](../../destinations/catalog/personalization/custom-personalization.md).<br><br>의 특정 단계는 대상 설명서 를 참조하십시오. [개인화 대상 구성](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | 활성화하려면 이 확인란을 선택하십시오. [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 이 데이터스트림에 사용됩니다. <br><br> 이 옵션을 활성화하면 데이터 스트림에서 웹 및 앱 기반 인바운드 캠페인에서 개인화된 콘텐츠를 반환할 수 있습니다. [!DNL Adobe Journey Optimizer]. 이 옵션을 사용하려면 [!UICONTROL Edge 세그멘테이션] 활성화해야 합니다. If [!UICONTROL Edge 세그멘테이션] 이 선택되지 않으면 이 옵션이 회색으로 표시됩니다. |

### Adobe Target 설정 {#target}

이 서비스는 데이터를 Adobe Target으로 전송할지 여부와 방법을 제어합니다.

![Adobe Target 설정 블록](../assets/datastreams/configure/target-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 속성 토큰] | [!DNL Target] 에서는 고객이 속성을 사용하여 권한을 제어할 수 있습니다. 속성에 대한 자세한 내용은 [enterprise 권한 구성](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 다음에서 [!DNL Target] 설명서를 참조하십시오.<br><br>속성 토큰은 Adobe Target UI의 [!UICONTROL 설정] > [!UICONTROL 속성]. |
| [!UICONTROL Target 환경 ID] | [Adobe Target의 환경](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 을 사용하면 모든 개발 단계에서 구현을 관리할 수 있습니다. 이 설정은 이 데이터 스트림에 사용할 환경을 지정합니다.<br><br>가장 좋은 방법은 각 사용자에 대해 이를 다르게 설정하는 것입니다. `dev`, `stage`, 및 `prod` 데이터 스트림 환경으로 간단하게 유지할 수 있습니다. 그러나 이미 Adobe Target 환경이 정의된 경우 이러한 환경을 사용할 수 있습니다. |
| [!UICONTROL Target 타사 ID 네임스페이스] | 를 위한 ID 네임스페이스 `mbox3rdPartyId` 이 데이터 스트림에 을(를) 사용합니다. 다음 안내서를 참조하십시오 [구현 `mbox3rdPartyId` Web SDK를 사용하여](../personalization/adobe-target/using-mbox-3rdpartyid.md) 추가 정보. |
| [!UICONTROL 속성 토큰 재정의] | 이 섹션에서는 기본 속성 토큰을 재정의하는 데 사용할 수 있는 추가 속성 토큰을 정의할 수 있습니다. |

### [!UICONTROL 이벤트 전달] 설정

이 서비스는 데이터를 (으)로 전송할지 여부 및 방법을 제어합니다. [이벤트 전달](../../tags/ui/event-forwarding/overview.md).

![구성 UI의 이벤트 전달 섹션](../assets/datastreams/configure/event-forwarding-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 속성 실행] | **(필수)** 데이터를 보낼 이벤트 전달 속성입니다. |
| [!UICONTROL Launch 환경] | **(필수)** 선택한 속성 내에서 데이터를 보낼 환경입니다. |

>[!NOTE]
>
>다음을 선택할 수 있습니다. **[!UICONTROL ID 수동 입력]** 드롭다운 메뉴를 사용하는 대신 속성 및 환경 이름을 입력합니다.

## 데이터 스트림 복사 {#copy}

기존 데이터 스트림의 복사본을 만들고 필요에 따라 해당 세부 사항을 변경할 수 있습니다.

>[!NOTE]
>
>데이터 스트림은 동일한 내에서만 복사할 수 있습니다. [샌드박스](../../sandboxes/home.md). 즉, 한 샌드박스에서 다른 샌드박스로 데이터 스트림을 복사할 수 없습니다.

의 기본 페이지에서 [!UICONTROL 데이터스트림] 작업 영역에서 줄임표(**....**)을 선택합니다. **[!UICONTROL 복사]**.

![다음을 보여주는 이미지 [!UICONTROL 복사] 데이터 스트림 목록 보기에서 선택 중인 옵션](../assets/datastreams/configure/copy-datastream-list.png)

또는 다음을 선택할 수 있습니다 **[!UICONTROL 데이터 스트림 복사]** (특정 데이터스트림의 세부 사항 보기에서)

![다음을 보여주는 이미지 [!UICONTROL 복사] 데이터 스트림 세부 정보 보기에서 선택 중인 옵션](../assets/datastreams/configure/copy-datastream-details.png)

복사할 구성 옵션에 대한 세부 정보와 함께 생성할 새 데이터 스트림의 고유한 이름을 입력하라는 메시지가 표시되는 확인 대화 상자가 나타납니다. 준비가 되면 다음을 선택합니다. **[!UICONTROL 복사]**.

![데이터 스트림 복사를 위한 확인 대화 상자 이미지](../assets/datastreams/configure/copy-datastream-confirm.png)

의 메인 페이지 [!UICONTROL 데이터스트림] 작업 공간이 새 데이터 스트림이 나열된 상태로 다시 나타납니다.

## 다음 단계

이 안내서에서는 데이터 수집 UI에서 데이터스트림을 관리하는 방법을 다룹니다. 데이터 스트림을 설정한 후 Web SDK를 설치하고 구성하는 방법에 대한 자세한 내용은 [데이터 수집 E2E 안내서](../../collection/e2e.md#install).
