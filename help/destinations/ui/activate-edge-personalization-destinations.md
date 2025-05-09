---
title: Edge 개인화 대상에 대한 대상자 활성화
description: 동일 페이지 및 다음 페이지 개인화 사용 사례를 위해 Adobe Experience Platform에서 Edge 개인화 대상으로 대상을 활성화하는 방법을 알아봅니다.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 25697d341b2970eeb20d9f2507ee701ade8046d3
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 2%

---


# Edge 개인화 대상에 대한 대상자 활성화

## 개요 {#overview}

Adobe Experience Platform은 [에지 대상](/help/destinations/destination-types.md#edge-personalization-destinations)과 함께 [에지 세분화](../../segmentation/methods/edge-segmentation.md)을(를) 사용하여 고객이 실시간으로 대규모로 대상을 만들고 타깃팅할 수 있도록 합니다. 이 기능은 동일한 페이지 및 다음 페이지 개인화 사용 사례를 구성하는 데 도움이 됩니다.

Edge 대상의 예로는 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결이 있습니다.

>[!NOTE]
>
>데이터 스트림 ID를 사용하여 [Adobe Target 연결을 구성](../catalog/personalization/adobe-target-connection.md) *없이*&#x200B;하는 경우 이 문서에 설명된 사용 사례는 지원되지 않습니다. 데이터스트림이 없을 때는 다음 세션 개인화 사용 사례만 지원됩니다.

>[!IMPORTANT]
> 
> * 데이터를 활성화하고 워크플로우의 [매핑 단계](#mapping)를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
> * 워크플로우의 [매핑 단계](#mapping)를 거치지 않고 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 매핑하지 않고 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]**, **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}
> 
> [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 문서에서는 Adobe Experience Platform Edge 대상에 대한 대상을 활성화하는 데 필요한 워크플로에 대해 설명합니다. [에지 세분화](../../segmentation/methods/edge-segmentation.md) 및 선택적 [프로필 특성 매핑](#mapping)과(와) 함께 사용하는 경우, 이러한 대상을 사용하면 웹 및 모바일 속성에서 동일한 페이지 및 다음 페이지 개인화 사용 사례를 사용할 수 있습니다.

Edge 개인화를 위해 Adobe Target 연결을 구성하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며, 이 비디오 녹화 이후 변경되었을 수 있습니다. 최신 정보는 아래 섹션에 설명된 구성 단계를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3449800/?quality=12&learn=on&captions=kor)

Adobe Target 및 사용자 지정 개인화 대상에 대상 및 프로필 속성을 공유하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3447362/?quality=12&learn=on&captions=kor)

## 사용 사례 {#use-cases}

Adobe Target과 같은 Adobe 개인화 솔루션 또는 자체 개인화 파트너 플랫폼(예: [!DNL Optimizely], [!DNL Pega])과 독점 시스템(예: 사내 CMS)을 사용하여 [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) 대상을 통해 더 심층적인 고객 개인화 경험을 제공합니다. 이 모든 과정은 Experience Platform Edge Network 데이터 수집 및 세그멘테이션 기능을 활용합니다.

아래 설명된 사용 사례에는 사이트 개인화 및 타깃팅된 온사이트 광고가 모두 포함됩니다.

이러한 사용 사례를 사용하려면 고객이 Experience Platform에서 대상과 프로필 특성 정보를 모두 검색하고 이 정보를 Experience Platform UI의 [Adobe Target](../catalog/personalization/adobe-target-connection.md) 또는 [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) 연결로 보내는 빠르고 간소화된 방법이 필요합니다.

### 동일 페이지 개인화 {#same-page}

사용자가 웹 사이트의 페이지를 방문합니다. 현재 페이지 방문 정보(예: 참조 URL, 브라우저 언어, 포함된 제품 정보)를 사용하여 Adobe이 아닌 플랫폼(예: [!DNL Pega], [!DNL Optimizely] 등)에 대한 [사용자 지정 개인화](../catalog/personalization/custom-personalization.md) 연결을 사용하여 다음 작업 또는 결정(예: 개인화)을 선택할 수 있습니다.

### 다음 페이지 개인화 {#next-page}

사용자가 웹 사이트에서 페이지 A를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 대상자 세트에 대한 자격이 있습니다. 그런 다음 페이지 A에서 페이지 B로 이동하는 링크를 클릭합니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께 페이지 A에서의 이전 상호 작용 동안 사용자가 자격을 얻은 대상은 다음 작업 또는 의사 결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 수행하는 데 사용됩니다.

### 다음 세션 개인화 {#next-session}

사용자가 웹 사이트의 여러 페이지를 방문합니다. 이러한 상호 작용을 기반으로 사용자는 대상자 세트에 대한 자격이 있습니다. 그런 다음 사용자는 현재 탐색 세션을 종료합니다.

다음 날 사용자는 동일한 고객 웹 사이트로 돌아갑니다. 현재 웹 사이트 방문에 의해 결정된 프로필 업데이트와 함께, 방문한 모든 웹 사이트 페이지와의 이전 상호 작용 동안 자격이 있었던 대상은 다음 작업/결정(예: 방문자에게 표시할 광고 배너 또는 A/B 테스트의 경우 표시할 페이지 버전)을 선택하는 데 사용됩니다.

### 홈페이지 배너 개인화 {#home-page-banner}

홈 임대 및 판매 회사는 Adobe Experience Platform의 대상 자격을 기반으로 배너를 통해 홈 페이지를 개인화하려고 합니다. 회사는 개인화된 경험을 얻어야 하는 대상을 선택하고, 이러한 대상을 Target 오퍼에 대한 타깃팅 기준으로 Adobe Target에 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

### 데이터 수집 UI에서 데이터 스트림 구성 {#configure-datastream}

개인화 대상을 설정하는 첫 번째 단계는 Experience Platform 웹 SDK에 대한 데이터 스트림을 구성하는 것입니다. 이 작업은 데이터 수집 UI에서 수행됩니다.

데이터스트림을 구성할 때 **[!UICONTROL Adobe Experience Platform]**&#x200B;에서 **[!UICONTROL Edge 세분화]**&#x200B;와 **[!UICONTROL Personalization 대상]**&#x200B;을 모두 선택해야 합니다.

>[!TIP]
>
>2024년 4월 릴리스부터 [Adobe Target에 대한 연결을 구성](/help/destinations/catalog/personalization/adobe-target-connection.md)할 때 Edge 세그멘테이션 확인란을 선택할 필요가 없습니다. 이 경우 [다음 세션 개인화](#next-session)가 사용 가능한 유일한 개인화 사용 사례입니다.

![Edge 세분화 및 Personalization 대상이 강조 표시된 데이터스트림 구성!](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

데이터 스트림을 설정하는 방법에 대한 자세한 내용은 [Experience Platform Web SDK 설명서](../../datastreams/configure.md#aep)에 설명된 지침을 따르십시오.

### [!DNL Active-On-Edge] 병합 정책 만들기 {#create-merge-policy}

대상 연결을 만든 후에는 [!DNL Active-On-Edge] 병합 정책을 만들어야 합니다. [!DNL Active-On-Edge] 병합 정책을 사용하면 대상이 [Edge](../../segmentation/methods/edge-segmentation.md)에서 지속적으로 평가되고 실시간 및 다음 페이지 개인화 사용 사례에 사용할 수 있습니다.

>[!IMPORTANT]
>
>현재 Edge 대상은 기본값으로 설정된 [Active-on-Edge 병합 정책](../../segmentation/ui/segment-builder.md#merge-policies)을 사용하는 대상의 활성화만 지원합니다. 다른 병합 정책을 사용하는 대상을 Edge 대상에 매핑하면 해당 대상이 평가되지 않습니다.

[병합 정책 만들기](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)에 대한 지침을 따르고 **[!UICONTROL Active-On-Edge 병합 정책]** 전환을 사용하도록 설정해야 합니다.

### Experience Platform에서 새 대상 만들기 {#create-audience}

[!DNL Active-On-Edge] 병합 정책을 만든 후에는 Experience Platform에서 새 대상을 만들어야 합니다.

[대상 빌더](../../segmentation/ui/segment-builder.md) 안내서에 따라 새 대상을 만들고 이전 단계에서 만든 [!DNL Active-On-Edge] 병합 정책을 [할당](../../segmentation/ui/segment-builder.md#merge-policies)하세요.

### 대상 연결 만들기 {#connect-destination}

데이터스트림을 구성한 후 개인화 대상 구성을 시작할 수 있습니다.

새 대상 연결을 만드는 방법에 대한 자세한 지침은 [대상 연결 만들기 자습서](../ui/connect-destination.md)를 따르십시오.

구성할 대상에 따라 다음 문서에서 대상별 사전 요구 사항 및 관련 정보를 참조하십시오.

* [Adobe Target 연결](../catalog/personalization/adobe-target-connection.md#parameters)
* [사용자 지정 개인화 연결](../catalog/personalization/custom-personalization.md#parameters)

## 대상 선택 {#select-destination}

전제 조건을 완료한 후 이제 동일한 페이지 및 다음 페이지 개인화에 사용할 Edge 개인화 대상을 선택할 수 있습니다.

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하여 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![Experience Platform UI에서 강조 표시된 대상 카탈로그 탭](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 아래 이미지에 표시된 대로 대상을 활성화할 개인화 대상에 해당하는 카드에서 **[!UICONTROL 대상 활성화]**&#x200B;를 선택합니다.

   ![카탈로그의 대상 카드에 강조 표시된 대상 컨트롤을 활성화합니다.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 대상을 활성화하는 데 사용할 대상 연결을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

   ![활성화 워크플로에서 대상 단계를 선택하십시오.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 다음 섹션으로 이동하여 [대상자를 선택](#select-audiences)하십시오.

## 대상자 선택 {#select-audiences}

대상 이름 왼쪽에 있는 확인란을 사용하여 대상에 대해 활성화할 대상을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

대상으로 활성화할 대상을 선택하려면 대상 이름 왼쪽에 있는 확인란을 사용한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

출처에 따라 여러 유형의 대상 중에서 선택할 수 있습니다.

* **[!UICONTROL 세그먼테이션 서비스]**: 세그먼테이션 서비스에 의해 Experience Platform 내에서 생성된 대상입니다. 자세한 내용은 [세그먼테이션 설명서](../../segmentation/ui/overview.md)를 참조하세요.
* **[!UICONTROL 사용자 지정 업로드]**: Experience Platform 외부에서 생성되어 Experience Platform에 CSV 파일로 업로드된 대상자입니다. 외부 대상자에 대한 자세한 내용은 [대상자 가져오기](../../segmentation/ui/audience-portal.md#import-audience)에 대한 설명서를 참조하십시오.
* 다른 Adobe 솔루션에서 가져온 다른 유형의 대상(예: [!DNL Audience Manager]).

![여러 대상이 강조 표시된 활성화 워크플로의 대상 선택 단계입니다.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## 속성 매핑 {#mapping}

>[!IMPORTANT]
>
>프로필 속성에 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 특성 기반 개인화를 위해 대상을 구성할 때 **[!UICONTROL 사용자 지정 Personalization]** 대상을 사용하려면 [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)를 사용해야 합니다. 모든 Edge Network API 호출은 [인증된 컨텍스트](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/)에서 수행되어야 합니다.
>
><br>통합에 Web SDK 또는 Mobile SDK을 이미 사용하고 있는 경우 서버측 통합을 추가하여 Edge Network API를 통해 특성을 검색할 수 있습니다.
>
><br>위의 요구 사항을 따르지 않는 경우 개인화는 대상자 멤버십만 기반으로 합니다.

사용자에 대한 개인화 사용 사례를 활성화할 속성을 선택합니다. 즉, 속성 값이 변경되거나 속성이 프로필에 추가되면 해당 프로필이 대상자의 멤버가 되어 개인화 대상에 활성화됩니다.

속성 추가는 선택 사항이며 다음 단계로 계속 진행하여 속성을 선택하지 않고 동일한 페이지 및 다음 페이지 개인화를 활성화할 수 있습니다. 이 단계에서 속성을 추가하지 않으면 프로필에 대한 대상자 멤버십 및 ID 맵 자격을 기반으로 개인화가 계속 수행됩니다.

![특성이 선택된 매핑 단계를 보여 주는 이미지입니다.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### 소스 속성 선택 {#select-source-attributes}

소스 특성을 추가하려면 **[!UICONTROL Source 필드]** 열에서 **[!UICONTROL 새 필드 추가]** 컨트롤을 선택하고 아래와 같이 원하는 XDM 특성 필드를 검색하거나 탐색합니다.

![매핑 단계에서 대상 특성을 선택하는 방법을 보여 주는 화면 기록입니다.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### 대상 속성 선택 {#select-target-attributes}

대상 특성을 추가하려면 **[!UICONTROL 대상 필드]** 열에서 **[!UICONTROL 새 필드 추가]** 컨트롤을 선택하고 원본 특성을 매핑할 사용자 지정 특성 이름을 입력하십시오.

>[!NOTE]
>
>대상 플랫폼에서 친숙한 이름 필드 매핑을 지원하기 위해 대상 특성 선택은 [사용자 지정 Personalization](../catalog/personalization/custom-personalization.md) 활성화 워크플로우에만 적용됩니다.

![매핑 단계에서 XDM 특성을 선택하는 방법을 보여 주는 화면 녹화](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## 대상자 내보내기 예약 {#scheduling}

기본적으로 [!UICONTROL 대상 일정] 페이지에는 현재 활성화 흐름에서 선택한 새로 선택한 대상만 표시됩니다.

대상에 대해 활성화된 모든 대상을 보려면 필터링 옵션을 사용하고 **[!UICONTROL 새 대상만 표시]** 필터를 비활성화하십시오.

![모든 대상 필터가 강조 표시되었습니다.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

**[!UICONTROL 대상 일정]** 페이지에서 각 대상을 선택한 다음 **[!UICONTROL 시작 날짜]** 및 **[!UICONTROL 종료 날짜]** 선택기를 사용하여 데이터를 대상으로 보내는 시간 간격을 구성하십시오.

시작 및 종료 날짜가 강조 표시된 활성화 워크플로의 ![대상 일정 단계입니다.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

**[!UICONTROL 다음]**&#x200B;을(를) 선택하여 [!UICONTROL 검토] 페이지로 이동합니다.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택한 항목에 대한 요약을 볼 수 있습니다. 흐름을 중단하려면 **[!UICONTROL 취소]**&#x200B;를 선택하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택을 확인하고 데이터를 대상으로 보내려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

![검토 단계의 선택 요약입니다.](../assets/ui/activate-edge-personalization-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;를 구매한 경우 **[!UICONTROL 해당 동의 정책 보기]**&#x200B;를 선택하여 적용된 동의 정책을 조회하고 그 결과로 활성화에 포함된 프로필 수를 확인합니다. 자세한 내용은 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)를 참조하세요.

### 데이터 사용 정책 확인 {#data-usage-policy-checks}

**[!UICONTROL 검토]** 단계에서 Experience Platform은 데이터 사용 정책 위반도 확인합니다. 다음은 정책이 위반되는 예입니다. 위반을 해결할 때까지 대상 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션에서 [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)을 읽어 보십시오.

![데이터 정책 위반의 예입니다.](../assets/common/data-policy-violation.png)

### 대상자 필터링 {#filter-audiences}

이 단계에서는 페이지에서 사용 가능한 필터를 사용하여 일정 또는 매핑이 이 워크플로우의 일부로 업데이트된 대상자만 표시할 수 있습니다. 보려는 테이블 열을 전환할 수도 있습니다.

![검토 단계에서 사용 가능한 대상 필터를 보여 주는 화면 기록입니다.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

선택에 만족하고 정책 위반이 발견되지 않은 경우 **[!UICONTROL 완료]**&#x200B;를 선택하여 선택을 확인하고 데이터를 대상으로 보내기 시작합니다.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
