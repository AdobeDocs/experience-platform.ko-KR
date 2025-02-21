---
title: 파트너 지원 방문자 인식을 사용하여 알 수 없는 방문자에 대한 온사이트 경험 개인화
description: 파트너 지원 방문자 인식을 사용하여 방문자에게 개인화된 온사이트 경험을 제공하는 방법을 알아보십시오.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: 02f2082e695d157415c9e0c59ca5d371c94bb991
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 89%

---

# 파트너 지원 방문자 인식을 사용하여 알 수 없는 방문자에 대한 온사이트 경험 개인화

>[!AVAILABILITY]
>
>이 기능은 Real-Time CDP(앱 서비스), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate 라이선스가 있는 고객이 사용할 수 있습니다. 이 패키지에 대한 자세한 내용은 [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)을 참조하고 Adobe 담당자에게 문의하십시오.

파트너 지원 인식을 사용하여 웹 속성 방문자에게 개인화된 경험을 제공하는 방법을 알아보십시오. 이 튜토리얼을 사용하여 인증된 방문자와 인증되지 않은 방문자에게 개인화된 경험을 표시하기 위해 Experience Platform 및 기타 Experience Cloud 솔루션의 다양한 요소 구현 시퀀스를 이해하십시오.

![파트너 제공 속성을 사용하여 방문자에게 개인화된 경험을 제공하는 방법을 설명하는 인포그래픽입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## 이 사용 사례를 고려하는 이유 {#why-this-use-case}

소비자가 무수한 방식으로 브랜드와 상호 작용할 때 디지털 경험의 단편화는 매우 현실적이며 해결하기 점점 더 어려워지고 있습니다. 응집력 있는 경험, 타깃팅된 추천 및 맞춤화된 상호 작용을 위한 최상의 고객 참여 전략은 모두 사용자 인식에 의해 제한됩니다.

이는 파트너 지원 실시간 인식이 의미 있는 변화를 가져올 수 있는 부분이다. Adobe을 통해 identity 파트너는 정교한 클라이언트측 데이터 수집 및 시장을 선도하는 경험 최적화 오퍼링에 연결할 수 있으므로 이전 기록이나 인증 없이 첫 번째 방문부터 경험 전달에 대한 기준을 효과적으로 높일 수 있습니다.

이는 소비자 패키지 상품, 온라인 소매 등과 같이 인증 비율이 낮은 버티컬에 특히 유용합니다.

## 업계 사례 {#industry-example}

예를 들어 인증률이 낮은 주택 개조 브랜드를 생각해 보십시오. 이 브랜드는 사전 기록이나 인증 없이, 서드파티 쿠키에 대한 의존도를 줄이지 않고 처음 방문자에게 개인화된 경험을 제공하고자 합니다.

이 브랜드는 파트너 인식 기술을 활용하여 방문자를 확률적으로 인식하고 보다 개인화된 경험을 제공합니다. 이를 통해 방문자는 마케팅 단계 아래로 이동할 때 미리 고려할 수 있습니다. 예를 들어 브랜드는 최근에 이동한 사람들에게 어필하는 온사이트 콘텐츠에 대해 파트너가 제공한 인구 통계 신호를 사용하고 인기 있는 DIY 제품에 대한 할인을 제공할 수 있습니다.

## 전제 조건 및 계획 {#prerequisites-and-planning}

인증된 방문자와 인증되지 않은 방문자에게 개인화된 경험을 제공하기 위해 파트너 제공 속성을 사용하려는 경우, 계획 프로세스에서 다음 전제 조건을 고려하십시오.

* 파트너의 인식 기술에서 추가 속성을 추가하려면 어떤 입력이 필요합니까?
* 확률적으로 파생된 데이터 세트와 결정적으로 확인된 속성을 기반으로 다양한 채널 및 다양한 사용 사례에서 개인화를 제공하는 데 어느 정도 익숙하십니까?
* 사전 인증되었지만 인식된 방문자의 경험은 인증 시 어떻게 변경되어야 합니까?

### 사용할 UI 기능, 플랫폼 구성 요소 및 Experience Cloud 제품 {#ui-functionality-and-elements}

이 사용 사례를 성공적으로 구현하려면 실시간 고객 데이터 플랫폼 및 기타 Experience Cloud 솔루션의 여러 영역을 사용해야 합니다. 이러한 모든 영역에 대해 필요한 [속성 기반의 액세스 제어 권한](/help/access-control/abac/overview.md)이 있는지 확인하거나, 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

* 데이터 수집
   * [Adobe Experience Platform 웹 SDK](/help/web-sdk/home.md)
   * [태그](/help/tags/home.md)
   * [데이터스트림](/help/datastreams/overview.md)
* Real-Time CDP의 데이터 관리
   * [ID](/help/identity-service/features/namespaces.md)
   * [스키마](/help/xdm/home.md)
   * [데이터 사용 레이블](/help/data-governance/labels/overview.md)
   * [데이터 세트](/help/catalog/datasets/overview.md)
* 웹 속성 개인화
   * [에지 세분화](/help/segmentation/methods/edge-segmentation.md)
   * [에지 개인화 대상](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)(또는 원하는 개인화 플랫폼을 선택합니다. 이 사용 사례 튜토리얼은 Adobe Target을 개인화 엔진으로 강조함)

## 비디오 워크스루 {#video-walkthrough}

알 수 없는 방문자를 위해 온사이트 경험을 개인화하는 방법에 대한 연습은 아래 비디오 튜토리얼을 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

![파트너 제공 속성을 사용하여 방문자에게 개인화된 경험을 제공하는 방법을 설명하는 인포그래픽입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. **고객**&#x200B;은 익명의 웹 사이트 방문자에게 실시간으로 인사이트를 가져올 수 있는 기능에 대한 라이선스를 **데이터 파트너**&#x200B;에게 부여합니다.
2. **고객**&#x200B;은 속성에 클라이언트측 라이브러리를 배포하여 **파트너** API를 호출하고 파트너 제공 신호를 Real-Time CDP로 보내도록 Web SDK 또는 Mobile SDK를 구성합니다.
3. 웹 사이트나 앱을 검색할 때, ID와 함께 속성을 반환하는 **파트너**&#x200B;가 **방문자**&#x200B;를 인식할 확률이 높습니다.
4. Real-Time CDP는 에지 세분화를 실행하여 들어오는 이벤트 히트를 평가하고 [ECID 식별자](https://experienceleague.adobe.com/docs/id-service/using/home.html)에 대한 결과를 유지합니다.
5. Adobe Target은 에지 세분화 출력을 사용하여 세션 내 개인화를 위해 **방문자**&#x200B;에게 경험을 다시 렌더링합니다.
6. 이벤트는 분석 및 대상 변경과 같은 다운스트림 워크플로를 위해 전체적으로 유지됩니다.

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어보십시오.

### 데이터 관리 - ID 네임스페이스, 스키마 및 데이터 세트를 만들어 데이터 속성 관리 {#data-management}

인증되지 않은 방문자의 경험을 개인화하는 사용 사례를 달성하기 위해 먼저 Real-Time CDP에서 데이터 관리 구조를 설정하여 들어오는 실시간 이벤트 및 대상자 선별 데이터를 수신해야 합니다.

#### 파트너 ID 네임스페이스 만들기

먼저 파트너 ID 네임스페이스를 생성해야 합니다. 왼쪽 레일의 **[!UICONTROL 고객]** > **[!UICONTROL ID]**&#x200B;로 이동한 다음 화면의 오른쪽 상단에서 **[!UICONTROL ID 네임스페이스 만들기]**&#x200B;를 선택합니다.

![파트너 ID가 있는 ID 네임스페이스 만들기 대화 상자가 강조 표시됩니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

[파트너 ID 네임스페이스 만들기](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace)에 대한 방법을 자세히 알아보십시오.

#### 스키마 만들기

다음으로 나중에 웹 속성에서 수집할 시계열 데이터를 보유하는 [!UICONTROL 경험 이벤트] 스키마를 만들고 [!UICONTROL XDM ExperienceEvent]를 스키마의 기본 클래스로 사용해야 합니다. [Experience Platform UI를 사용하여 스키마 만들기](/help/xdm/ui/resources/schemas.md#create)에 대해 자세히 알아보십시오.

![스키마 만들기 및 XDM Experience 이벤트가 있는 스키마 작업 영역이 강조 표시됩니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

스키마를 만들고 [스키마에 필드 그룹을 추가](/help/xdm/ui/resources/schemas.md#add-field-groups)할 때 [웹 페이지 방문](/help/xdm/field-groups/event/web-details.md) 및 [ID 맵](/help/xdm/field-groups/profile/identitymap.md) 필드 그룹을 추가하도록 하십시오. 이는 디지털 속성 및 데이터 수집 관행에 적용할 수 있는 다른 필드 그룹에 추가됩니다.

또한 기존 필드 그룹을 만들거나 재사용하고 스키마에 추가하여 방문자에 대한 파트너 제공 인사이트를 캡처할 수 있습니다. Read how to [필드 그룹 생성](/help/xdm/ui/resources/field-groups.md) 및 필드 그룹에 [필드 추가](/help/xdm/ui/resources/field-groups.md)를 하는 방법에 대해 자세히 알아보십시오. 예를 들어 연령대, 고용 상태, 월별 지출 능력 또는 구매 동작과 같은 파트너 제공 인사이트에 대해 개인화하려는 경우, 필드 그룹에 해당 필드를 포함시킵니다.

데이터 파트너가 방문자에게 안정적인 식별자를 제공하고 이를 Real-Time CDP로 가져오고자 한다고 가정하면 사용자 정의 필드 그룹의 식별자에 대해 적절하게 이름이 지정된 필드가 있어야 합니다. 또한 이전에 생성한 ID 네임스페이스에 필드를 ID로 표시해야 합니다. 또한 [스키마를 프로필에 포함하도록 활성화](/help/xdm/ui/resources/schemas.md#profile)해야 합니다.

#### 데이터 세트 만들기

다음으로, 웹 속성 방문자로부터 수집하고 온사이트 개인화에 사용할 시계열 데이터를 보관하는 데이터 세트를 생성해야 합니다.

[데이터 세트를 만드는 방법](/help/catalog/datasets/user-guide.md#create)에 대한 튜토리얼을 확인하고 스키마에서 데이터 세트를 생성하는 옵션을 선택하도록 합니다. 이전 단계에서 생성한 스키마를 기반으로 데이터 세트를 생성합니다.

스키마를 생성할 때의 단계와 유사하게 데이터 세트를 [!UICONTROL 실시간 고객 프로필]에 포함하도록 활성화해야 합니다. [!UICONTROL 실시간 고객 프로필]에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md#profile)를 참조하십시오.

### 웹 속성에서 이벤트 데이터 수집 구현 {#implement-data-collection}

데이터 관리 구성을 설정하면 이제 웹 속성에 실시간 이벤트 [데이터 수집](/help/collection/home.md)을 구현해야 합니다. 실시간 이벤트 호출을 수집하여 다시 Real-Time CDP로 보내려면 Adobe 데이터 수집 라이브러리인 [!UICONTROL Web SDK]를 사용하여 속성을 구성해야 합니다. 이 항목은 몇 가지 데이터 수집 구성 요소에 걸쳐 몇 가지 개별 작업으로 구성됩니다.

>[!IMPORTANT]
>
>파트너 제공 속성을 검색하려면 *웹 속성을 파트너 API 또는 다른 방법과 통합하여 데이터 파트너로부터 실시간으로 속성을 호출하고 검색*&#x200B;해야 합니다. 이 튜토리얼의 대상이 아니므로 선택한 파트너와 이에 대해 논의하십시오.

먼저 화면의 오른쪽 상단에 있는 애플리케이션 전환기를 사용하여 **[!UICONTROL 데이터 수집]** 섹션으로 이동합니다.

>[!TIP]
>
>애플리케이션 전환기에서 [!UICONTROL 데이터 수집]을 볼 수 없는 경우, 시스템 관리자에게 액세스 권한을 문의하십시오.

![데이터 수집 섹션으로 이동하는 앱 전환기.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

UI의 **[!UICONTROL 데이터 수집]** 섹션은 아래 이미지와 유사합니다.

![Platform UI의 데이터 수집 섹션.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 데이터스트림 만들기

데이터 수집 섹션의 첫 번째 단계로, [새 데이터스트림을 만듭니다](/help/datastreams/configure.md). 데이터스트림은 데이터를 수집하고 올바른 Adobe 앱(이 경우 Experience Platform)으로 올바르게 라우팅하는 방법의 기반입니다.

데이터스트림을 생성할 때 **[!UICONTROL 이벤트 스키마]** 필드에서 이전에 생성한 스키마를 선택합니다.

![새 데이터스트림을 구성할 때 이벤트 스키마 선택기가 강조 표시됩니다.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

드롭다운에서 이전에 생성한 [이벤트 데이터 세트를 선택](/help/datastreams/configure.md#aep)하고 **[!UICONTROL 에지 세분화]** 및 **[!UICONTROL 개인화 대상]** 옆에 있는 상자를 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

이벤트 기반의 시계열 데이터를 가져오고 있으므로 이 시나리오에서는 프로필 데이터 세트를 선택할 필요가 없습니다.

#### 태그 속성 만들기

사이트에 태그를 배포할 때 확장 기능, 규칙, 데이터 요소 및 라이브러리로 채워진 컨테이너를 속성이라고 생각해 보겠습니다.

**[!UICONTROL 태그]**&#x200B;로 이동하고 **[!UICONTROL 새 속성]**&#x200B;을 선택합니다.

![새 태그 속성을 만듭니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

필수 필드를 채우고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![새 속성에 대한 필수 필드를 채웁니다.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

[태그 속성 생성](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html) 방법에 대해 자세히 알아보십시오.

다음으로 속성 내에 다양한 확장 기능을 설치해야 합니다. 태그 속성을 선택하고 [!UICONTROL 확장] 섹션으로 이동합니다.

![새 태그 속성을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

[!UICONTROL 코어] 확장 기능이 이미 설치되어 있어야 합니다. 다음 섹션에 설명된 대로 두 개의 추가 확장 기능을 설치해야 합니다.

![설치된 확장 기능을 봅니다.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### 웹 SDK 확장 기능 설치

이 튜토리얼은 Web SDK를 사용하여 웹 사이트를 구성하는 방법을 설명합니다. 앱에서 [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)를 사용하여 앱 방문자에게 경험을 개인화할 수도 있습니다.

![확장 카탈로그의 Web SDK 확장 기능 보기.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Web SDK를 구성하는 화면에서 **[!UICONTROL 데이터스트림]** 섹션으로 이동하여 사용 중인 Experience Platform 샌드박스에 대한 정보를 제공합니다. 다음 드롭다운에서 이전 단계에 생성된 해당 샌드박스 및 데이터스트림을 선택합니다. 다른 모든 환경에 대해 동일한 샌드박스 및 데이터스트림 값을 선택할 수 있습니다. 다른 설정은 변경하지 않고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

[install Web SDK 설치 방법](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html)에 대해 자세히 알아보십시오.

#### ID 서비스 확장 기능 설치

[Experience Cloud ID 서비스 확장 기능](/help/tags/extensions/client/id-service/overview.md)을 사용하여 모든 Experience Cloud 솔루션에서 방문자를 위한 고유 장치 기반의 자사 ID를 만드십시오. 확장 카탈로그에서 **[!UICONTROL ID 서비스]**&#x200B;를 검색하여 설치합니다. 확장 기능을 설치할 때 모든 기본 설정을 유지하십시오.

![확장 기능 카탈로그의 ID 서비스 확장 기능을 확인하십시오.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 환경 설정

그 다음 왼쪽 탐색에서 **[!UICONTROL 환경]** 섹션으로 이동합니다. 이 단계에서는 웹 사이트를 Adobe Edge 네트워크에 연결하여 방문자 정보를 실시간으로 검색하고 전달해야 합니다.

개발 환경 오른쪽에 있는 상자 아이콘을 선택하고, 모달 창에 나타나는 JavaScript 코드 조각의 표준 버전을 복사합니다.

![데이터 수집 UI의 환경 섹션에서 강조 표시된 상자 아이콘을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

이 코드 조각을 웹 사이트 맨 위에 추가해야 합니다. 그 결과, 귀하의 웹 사이트는 Adobe Edge 네트워크를 호출하여 페이지에서 로드되고 실행될 JavaScript 논리를 검색합니다. 이를 통해 방문자 ID 생성, 데이터 수집 및 실시간 경험 개인화와 같은 기능이 작동할 수 있습니다.

#### 데이터 요소 설정

데이터 요소는 데이터 사전(또는 데이터 맵)의 기본 구성단위입니다. 단일 데이터 요소는 쿼리 문자열, URL, 쿠키 값, JavaScript 변수 등에 값을 매핑할 수 있는 변수입니다. [데이터 요소](/help/tags/ui/managing-resources/data-elements.md)에 대해 자세히 알아보십시오.

이 사용 사례의 경우 두 개의 데이터 요소를 설정해야 합니다.

먼저 `partnerData` 요소를 설정합니다. **[!UICONTROL 데이터 요소]** 섹션으로 이동한 다음 **[!UICONTROL 새 데이터 요소 만들기]**&#x200B;를 선택합니다.

![새 데이터 요소를 만듭니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

데이터 요소 `partnerData`의 이름을 지정하고 [!UICONTROL 확장 기능] 값을 [!UICONTROL 코어]로 유지한 후 **[!UICONTROL 데이터 요소 유형]**&#x200B;을 **[!UICONTROL JavaScript 변수]**&#x200B;로 설정합니다. **[!UICONTROL JavaScript 변수 이름]**&#x200B;이라는 필드에 `partnerData`를 입력하고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![partnerData 요소를 올바르게 구성하려면 선택 항목을 강조 표시합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

두 번째 데이터 요소를 설정하려면 새 변수 `pageVisit`의 이름을 지정하고, **[!UICONTROL 확장]**&#x200B;을 **[!UICONTROL Adobe Experience Platform]**&#x200B;으로 설정한 다음 **[!UICONTROL XDM 오브젝트]**&#x200B;를 데이터 유형으로 선택합니다.

![pageVisit 요소를 올바르게 구성하려면 선택 항목을 강조 표시합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

스키마에서 데이터 파트너에서 기대하는 값에 해당하는 서드파티 속성을 선택합니다. 그런 다음 **[!UICONTROL 전체 오브젝트 제공]**&#x200B;이라는 라디오 버튼을 선택합니다. 데이터베이스처럼 보이는 아이콘을 선택하고 이전에 생성한 `partnerData` 데이터 요소를 선택합니다.

#### 규칙 설정

**[!UICONTROL 규칙]** 섹션에서 방금 생성한 데이터 요소에 로드된 속성을 사용하여 Adobe에 개인화 요청을 보내도록 웹 사이트를 구성할 수 있습니다. [규칙 생성](/help/tags/ui/managing-resources/rules.md)에 대해 자세히 알아보십시오.

**[!UICONTROL 새 규칙 만들기]**&#x200B;를 선택합니다. 이 규칙 **[!UICONTROL 개인화]**&#x200B;의 이름을 지정하고 **[!UICONTROL 이벤트]** 옆에 있는 + 기호를 선택합니다. **[!UICONTROL 페이지 하단]**&#x200B;을 이벤트로 선택한 다음 저장합니다.

![규칙의 이벤트 유형 부분에 대한 선택 항목.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

**[!UICONTROL 작업]** 옆에 있는 + 기호를 선택합니다. 확장 기능을 **[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;로 업데이트하고 **[!UICONTROL 작업 유형]**&#x200B;을 **[!UICONTROL 이벤트 전송]**&#x200B;으로 설정합니다.

![규칙의 작업 유형 부분에 대한 선택 항목.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

오른쪽의 **[!UICONTROL 유형]** 드롭다운의 선택기에서 `web.webpagedetails.pageViews`를 이벤트 유형으로 선택합니다.

![이벤트 유형을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

XDM 데이터 옆에 있는 데이터베이스 아이콘을 선택하고 `pageVisit` 데이터 요소를 선택합니다.

작업 구성 목록을 아래로 스크롤하여 **[!UICONTROL 시각적 개인화 결정 렌더링]**&#x200B;이라는 상자를 확인하도록 합니다. 이는 Adobe Target 또는 기타 유사한 제품을 통해 제공되는 경험을 웹 페이지에서 시각적으로 렌더링할 수 있도록 하는 데 중요합니다. **[!UICONTROL 변경사항 유지]**&#x200B;를 선택한 다음 규칙 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![시각적 개인화 결정 렌더링 확인란을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 게시 워크플로 설정

이 구성을 웹 페이지에 배포하기 위한 다음 단계는 방금 만든 리소스를 포함하는 라이브러리를 구축하는 것입니다. [게시 흐름 설정](/help/tags/ui/publishing/publishing-flow.md)에 대해 자세히 알아보십시오.

**[!UICONTROL 게시 흐름]**&#x200B;을 선택한 다음 **[!UICONTROL 라이브러리 추가]**&#x200B;를 선택합니다.

**[!UICONTROL 변경된 모든 리소스 추가]**&#x200B;를 선택하고, 라이브러리 이름을 지정하고, 환경을 **[!UICONTROL 개발]**&#x200B;로 설정한 다음 **[!UICONTROL 개발에 저장 및 구축]**&#x200B;을 선택합니다.

![라이브러리 생성 및 개발 환경에 배포](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 웹 사이트 테스트

이 시점에서 웹 사이트는 Web SDK로 완전히 구성되어야 합니다. 데이터 수집이 예상대로 작동하는지 테스트하려면 웹 사이트로 이동하고 브라우저의 개발자 도구를 사용하여 네트워크 트래픽을 검사할 수 있습니다.

검색 상자에 `interact`를 입력하고 페이지를 새로 고치면 웹 사이트에서 Adobe Edge 네트워크로 채워지는 네트워크 호출이 표시됩니다.

![개발자 도구에 채워지는 네트워크 이벤트 보기.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 개인화 {#personalization}

이제 개인화를 위해 대상자를 만들고 활성화할 준비가 되었습니다.

#### 대상자 만들기 및 에지 세분화 설정

Platform UI에서 **[!UICONTROL 고객]** > **[!UICONTROL 대상]**(으)로 이동하여 웹 사이트 방문자를 캡처할 대상을 만듭니다.

![대상자로 이동하는 방법을 봅니다.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

방문자가 웹 속성을 방문할 때 방문자의 대상 멤버십이 실시간으로 평가되도록 대상을 [에지 세분화](/help/segmentation/methods/edge-segmentation.md)로 설정해야 합니다.

에지 대상자에 대한 [활성 온 에지 병합 정책](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy)도 설정하도록 합니다.

#### Adobe Target 또는 기타 고객 개인화 대상과 통합

이제 개인화 엔진과 통합하여 웹 사이트 또는 앱 방문자에게 개인화된 콘텐츠를 표시할 준비가 되었습니다. Adobe는 이를 위해 [Adobe Target 대상](/help/destinations/catalog/personalization/adobe-target-connection.md)을 사용하는 것을 추천합니다.

>[!IMPORTANT]
>
>대상자를 활성화하는 데 필요한 단계를 전반적으로 보려면 [에지 개인화 대상으로 대상 활성화](/help/destinations/ui/activate-edge-personalization-destinations.md)에 대한 튜토리얼을 참조하십시오.

## 제한 사항 및 문제 해결 {#limitations-and-troubleshooting}

이 페이지에 설명된 사용 사례를 탐색할 때 다음 제한 사항에 유의하십시오.

* 파트너 ID를 사용하는 경우, [ID 그래프](/help/identity-service/features/identity-graph-viewer.md)를 구축할 때 이 ID는 사용하지 않습니다.

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* [신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완](/help/rtcdp/partner-data/supplement-first-party-profiles.md)하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.
* Real-Time CDP에서 서드파티 데이터 지원을 사용하여 [데이터 파트너의 잠재 고객 프로필로 프로필 기반을 확장하고 데이터 파트너와 협력하여 신규 고객에게 도달하거나 확보할 수 있습니다](/help/rtcdp/partner-data/prospecting.md).
* 대상을 선택할 수 있도록 [잠재 고객 프로필 및 잠재 고객 활성화](/help/destinations/ui/activate-prospect-audiences.md)를 확장했습니다.
