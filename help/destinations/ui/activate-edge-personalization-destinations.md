---
title: Edge 개인화 대상에 대한 대상자 활성화
description: 동일 페이지 및 다음 페이지 개인화 사용 사례를 위해 Adobe Experience Platform에서 Edge 개인화 대상으로 대상을 활성화하는 방법을 알아봅니다.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 2%

---


# Edge 개인화 대상에 대한 대상자 활성화

## 개요 {#overview}

Adobe Experience Platform 사용 [가장자리 세분화](../../segmentation/ui/edge-segmentation.md) 과 함께 [에지 대상](/help/destinations/destination-types.md#edge-personalization-destinations) 고객이 실시간으로 대규모로 대상자를 만들고 타깃팅할 수 있도록 지원. 이 기능은 동일한 페이지 및 다음 페이지 개인화 사용 사례를 구성하는 데 도움이 됩니다.

에지 대상의 예는 다음과 같습니다. [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 정의 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결.

>[!NOTE]
>
>날짜 [Adobe Target 연결 구성](../catalog/personalization/adobe-target-connection.md) *없이* 데이터 스트림 ID를 사용하는 경우 이 문서에 설명된 사용 사례는 지원되지 않습니다. 데이터스트림이 없을 때는 다음 세션 개인화 사용 사례만 지원됩니다.

>[!IMPORTANT]
> 
> * 데이터를 활성화하고 활성화하려면 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
> * 을(를) 거치지 않고 데이터를 활성화하려면 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 보기]**, **[!UICONTROL 매핑 없이 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}
> 
> 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 문서에서는 Adobe Experience Platform Edge 대상에 대한 대상을 활성화하는 데 필요한 워크플로에 대해 설명합니다. 함께 사용되는 경우 [가장자리 세분화](../../segmentation/ui/edge-segmentation.md) 및 선택 사항 [프로필 속성 매핑](#mapping), 이러한 대상을 사용하면 웹 및 모바일 속성에서 동일한 페이지 및 다음 페이지 개인화 사용 사례를 사용할 수 있습니다.

Edge 개인화를 위해 Adobe Target 연결을 구성하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후에 변경되었을 수 있습니다. 최신 정보는 아래 섹션에 설명된 구성 단계를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Adobe Target 및 사용자 지정 개인화 대상에 대상 및 프로필 속성을 공유하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## 사용 사례 {#use-cases}

Adobe Target과 같은 Adobe 개인화 솔루션 또는 고유한 개인화 파트너 플랫폼(예: [!DNL Optimizely], [!DNL Pega]를 통해 보다 심층적인 고객 개인화 경험을 제공할 수 있는 독점 시스템(예: 사내 CMS)은 물론 [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) 대상. 이 모든 것은 Experience Platform Edge Network 데이터 수집 및 세그멘테이션 기능을 활용합니다.

아래 설명된 사용 사례에는 사이트 개인화 및 타깃팅된 온사이트 광고가 모두 포함됩니다.

이러한 사용 사례를 활성화하려면 고객은 Experience Platform에서 대상과 프로필 속성 정보를 모두 검색하고 이 정보를 다음 중 하나로 전송하는 빠르고 간소화된 방법이 필요합니다. [Adobe Target](../catalog/personalization/adobe-target-connection.md) 또는 [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) Experience Platform UI의 연결.

### 동일 페이지 개인화 {#same-page}

사용자가 웹 사이트의 페이지를 방문합니다. 현재 페이지 방문 정보(예: 참조 URL, 브라우저 언어, 포함된 제품 정보)를 사용하여 다음을 사용하여 다음 작업 또는 결정(예: 개인화)을 선택할 수 있습니다. [사용자 정의 개인화](../catalog/personalization/custom-personalization.md) 비 Adobe 플랫폼에 대한 연결(예: [!DNL Pega], [!DNL Optimizely] 또는 기타.).

### 다음 페이지 개인화 {#next-page}

사용자가 웹 사이트에서 페이지 A를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 대상자 세트에 대한 자격이 있습니다. 그런 다음 페이지 A에서 페이지 B로 이동하는 링크를 클릭합니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께 페이지 A에서의 이전 상호 작용 동안 사용자가 자격을 얻은 대상은 다음 작업 또는 의사 결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 수행하는 데 사용됩니다.

### 다음 세션 개인화 {#next-session}

사용자가 웹 사이트의 여러 페이지를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 대상자 세트에 대한 자격이 있습니다. 그런 다음 사용자는 현재 탐색 세션을 종료합니다.

다음 날 사용자는 동일한 고객 웹 사이트로 돌아갑니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께, 방문한 모든 웹 사이트 페이지와의 이전 상호 작용 동안 자격이 있었던 대상은 다음 작업/결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 선택하는 데 사용됩니다.

### 홈페이지 배너 개인화 {#home-page-banner}

홈 임대 및 판매 회사는 Adobe Experience Platform의 대상 자격을 기반으로 배너를 통해 홈 페이지를 개인화하려고 합니다. 회사는 개인화된 경험을 얻어야 하는 대상을 선택하고, 이러한 대상을 Target 오퍼에 대한 타깃팅 기준으로 Adobe Target에 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

### 데이터 수집 UI에서 데이터 스트림 구성 {#configure-datastream}

개인화 대상을 설정하는 첫 번째 단계는 Experience Platform Web SDK에 대한 데이터 스트림을 구성하는 것입니다. 이 작업은 데이터 수집 UI에서 수행됩니다.

데이터 스트림을 구성할 때에서 **[!UICONTROL Adobe Experience Platform]** 둘 다 **[!UICONTROL Edge 세그멘테이션]** 및 **[!UICONTROL Personalization 대상]** 이(가) 선택되어 있습니다.

>[!TIP]
>
>2024년 4월 릴리스부터 다음과 같은 경우에는 Edge 세분화 확인란을 선택할 필요가 없습니다 [Adobe Target에 대한 연결 구성](/help/destinations/catalog/personalization/adobe-target-connection.md). 이 경우, [다음 세션 개인화](#next-session) 은 사용 가능한 유일한 개인화 사용 사례입니다.

![Edge 세그멘테이션 및 Personalization 대상이 강조 표시된 데이터스트림 구성](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

데이터 스트림을 설정하는 방법에 대한 자세한 내용은 [Platform Web SDK 설명서](../../datastreams/configure.md#aep).

### 만들기 [!DNL Active-On-Edge] 병합 정책 {#create-merge-policy}

대상 연결을 만든 후에는 [!DNL Active-On-Edge] 병합 정책. 다음 [!DNL Active-On-Edge] 병합 정책을 사용하면 대상이 지속적으로 평가됩니다 [가장자리에](../../segmentation/ui/edge-segmentation.md) 및 은 실시간 및 다음 페이지 개인화 사용 사례에 사용할 수 있습니다.

>[!IMPORTANT]
>
>현재 Edge 대상은 를 사용하는 대상의 활성화만 지원합니다. [Active-on-Edge 병합 정책](../../segmentation/ui/segment-builder.md#merge-policies) 을(를) 기본값으로 설정합니다. 다른 병합 정책을 사용하는 대상을 Edge 대상에 매핑하면 해당 대상이 평가되지 않습니다.

다음 지침을 따르십시오. [병합 정책 만들기](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), 및 을(를) 활성화해야 합니다. **[!UICONTROL Active-On-Edge 병합 정책]** 토글.

### Platform에서 새 대상 만들기 {#create-audience}

을(를) 만든 후 [!DNL Active-On-Edge] 병합 정책입니다. Platform에서 새 대상을 만들어야 합니다.

다음 [대상 빌더](../../segmentation/ui/segment-builder.md) 새 대상을 만드는 방법을 안내하고 [할당](../../segmentation/ui/segment-builder.md#merge-policies) 다음 [!DNL Active-On-Edge] 이전 단계에서 생성한 병합 정책입니다.

### 대상 연결 만들기 {#connect-destination}

데이터스트림을 구성한 후 개인화 대상 구성을 시작할 수 있습니다.

다음 [대상 연결 만들기 자습서](../ui/connect-destination.md) 새 대상 연결을 만드는 방법에 대한 자세한 지침은 을 참조하십시오.

구성할 대상에 따라 다음 문서에서 대상별 사전 요구 사항 및 관련 정보를 참조하십시오.

* [Adobe Target 연결](../catalog/personalization/adobe-target-connection.md#parameters)
* [사용자 지정 개인화 연결](../catalog/personalization/custom-personalization.md##parameters)

## 대상 선택 {#select-destination}

전제 조건을 완료한 후 이제 동일한 페이지 및 다음 페이지 개인화에 사용할 Edge 개인화 대상을 선택할 수 있습니다.

1. 다음으로 이동 **[!UICONTROL 연결 > 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭.

   ![Experience Platform UI에서 강조 표시된 대상 카탈로그 탭.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 선택 **[!UICONTROL 대상자 활성화]** 아래 이미지에 표시된 대로 대상자를 활성화하려는 개인화 대상에 해당하는 카드.

   ![카탈로그의 대상 카드에 강조 표시된 대상자 컨트롤을 활성화합니다.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 대상을 활성화하는 데 사용할 대상 연결을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

   ![활성화 워크플로에서 대상 단계를 선택합니다.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 다음 섹션으로 이동 [대상자 선택](#select-audiences).

## 대상자 선택 {#select-audiences}

대상 이름 왼쪽에 있는 확인란을 사용하여 대상에 활성화할 대상을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

대상에 대해 활성화할 대상을 선택하려면 대상 이름 왼쪽에 있는 확인란을 사용한 다음 을 선택합니다 **[!UICONTROL 다음]**.

출처에 따라 여러 유형의 대상 중에서 선택할 수 있습니다.

* **[!UICONTROL 세분화 서비스]**: 세분화 서비스에 의해 Experience Platform 내에서 생성된 대상자. 다음을 참조하십시오. [세그멘테이션 설명서](../../segmentation/ui/overview.md) 을 참조하십시오.
* **[!UICONTROL 사용자 정의 업로드]**: Experience Platform 외부에서 생성되어 CSV 파일로 플랫폼에 업로드된 대상자 외부 대상자에 대한 자세한 내용은 [대상자 가져오기](../../segmentation/ui/audience-portal.md#import-audience).
* 다른 Adobe 솔루션에서 가져온 다른 유형의 대상, 예: [!DNL Audience Manager].

![여러 대상이 강조 표시된 활성화 워크플로의 대상 선택 단계입니다.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## 속성 매핑 {#mapping}

>[!IMPORTANT]
>
>프로필 속성에 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 **[!UICONTROL 사용자 지정 Personalization]** 대상을 사용하려면 다음을 사용해야 합니다. [Edge Network 서버 API](../../server-api/overview.md) 속성 기반 개인화에 대한 대상을 구성할 때. 모든 서버 API 호출은 [인증된 컨텍스트](../../server-api/authentication.md).
>
><br>통합에 웹 SDK 또는 Mobile SDK를 이미 사용 중인 경우 서버측 통합을 추가하여 서버 API를 통해 속성을 검색할 수 있습니다.
>
><br>위의 요구 사항을 따르지 않는 경우 개인화는 대상 멤버십만 기반으로 합니다.

사용자에 대한 개인화 사용 사례를 활성화할 속성을 선택합니다. 즉, 속성 값이 변경되거나 속성이 프로필에 추가되면 해당 프로필이 대상자의 멤버가 되어 개인화 대상에 활성화됩니다.

속성 추가는 선택 사항이며 다음 단계로 계속 진행하여 속성을 선택하지 않고 동일한 페이지 및 다음 페이지 개인화를 활성화할 수 있습니다. 이 단계에서 속성을 추가하지 않으면 프로필에 대한 대상자 멤버십 및 ID 맵 자격을 기반으로 개인화가 계속 수행됩니다.

![속성이 선택된 매핑 단계를 보여 주는 이미지입니다.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### 소스 속성 선택 {#select-source-attributes}

소스 속성을 추가하려면 **[!UICONTROL 새 필드 추가]** 에 대한 제어 **[!UICONTROL Source 필드]** 아래와 같이 열을 검색하고 원하는 XDM 속성 필드로 이동합니다.

![매핑 단계에서 대상 속성을 선택하는 방법을 보여 주는 화면 기록입니다.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### 대상 속성 선택 {#select-target-attributes}

대상 속성을 추가하려면 **[!UICONTROL 새 필드 추가]** 에 대한 제어 **[!UICONTROL 대상 필드]** 소스 속성을 매핑할 사용자 지정 속성 이름을 입력하고 열을 선택합니다.

>[!NOTE]
>
>대상 속성 선택은 에만 적용됩니다. [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) 대상 플랫폼에서 친숙한 이름 필드 매핑을 지원하기 위한 활성화 워크플로.

![매핑 단계에서 XDM 속성을 선택하는 방법을 보여 주는 화면 레코딩](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## 대상자 내보내기 예약 {#scheduling}

기본적으로 [!UICONTROL 대상자 일정] 페이지에는 현재 활성화 플로우에서 선택한 새로 선택한 대상만 표시됩니다.

대상에 대해 활성화된 모든 대상을 보려면 필터링 옵션을 사용하고 을(를) 비활성화합니다. **[!UICONTROL 새 대상자만 표시]** 필터.

![모든 대상 필터가 강조 표시됩니다.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

다음에서 **[!UICONTROL 대상자 일정]** 페이지를 열고 각 대상을 선택한 다음 **[!UICONTROL 시작일]** 및 **[!UICONTROL 종료일]** 선택기를 사용하여 데이터를 대상으로 전송하는 시간 간격을 구성할 수 있습니다.

![시작 및 종료 날짜가 강조 표시된 활성화 워크플로의 대상자 예약 단계입니다.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

선택 **[!UICONTROL 다음]** 로 이동 [!UICONTROL 리뷰] 페이지를 가리키도록 업데이트하는 중입니다.

## 검토 {#review}

다음에서 **[!UICONTROL 리뷰]** 페이지에서 선택 사항의 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 끊으려면, **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토 단계의 선택 요약입니다.](../assets/ui/activate-edge-personalization-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;를 구매한 경우 **[!UICONTROL 해당 동의 정책 보기]**&#x200B;를 선택하여 적용된 동의 정책을 조회하고 그 결과로 활성화에 포함된 프로필 수를 확인합니다. 읽어보기 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 추가 정보.

### 데이터 사용 정책 확인 {#data-usage-policy-checks}

다음에서 **[!UICONTROL 리뷰]** 단계, Experience Platform은 데이터 사용 정책 위반도 확인합니다. 다음은 정책이 위반되는 예입니다. 위반을 해결할 때까지 대상 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) (데이터 거버넌스 설명서 섹션)

![데이터 정책 위반의 예입니다.](../assets/common/data-policy-violation.png)

### 대상자 필터링 {#filter-audiences}

이 단계에서는 페이지에서 사용 가능한 필터를 사용하여 일정 또는 매핑이 이 워크플로우의 일부로 업데이트된 대상자만 표시할 수 있습니다. 보려는 테이블 열을 전환할 수도 있습니다.

![검토 단계에서 사용 가능한 대상 필터를 보여 주는 화면 기록입니다.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

선택에 만족하고 정책 위반이 감지되지 않은 경우 다음을 선택합니다. **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
