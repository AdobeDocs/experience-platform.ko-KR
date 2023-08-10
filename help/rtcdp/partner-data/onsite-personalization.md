---
title: 파트너 지원 방문자 인식을 사용하여 온사이트 경험 개인화
description: 파트너 지원 방문자 인식을 사용하여 방문자에게 개인화된 현장 경험을 제공하는 방법에 대해 알아보십시오.
hide: true
hidefromtoc: true
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 7%

---

# 파트너 지원 방문자 인식을 사용하여 온사이트 경험 개인화

파트너 지원 인식을 사용하여 웹 속성 방문자에게 개인화된 경험을 전달하는 방법을 알아봅니다. 이 자습서를 사용하여 Experience Platform 및 기타 Experience Cloud 솔루션의 다양한 요소에 대한 구현 시퀀스를 이해하여 인증된 방문자와 인증되지 않은 방문자에게 개인화된 경험을 표시할 수 있습니다.

![파트너가 제공한 속성을 사용하여 방문자에게 개인화된 경험을 전달하는 방법을 설명하는 인포그래픽입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## 업계 예 {#industry-example}

예를 들어, 인증률이 낮은 주택 개량 브랜드를 생각해 보자. 이 브랜드는 이전 내역 또는 인증 없이 서드파티 쿠키에 대한 의존도가 낮아지지 않고 처음 방문하는 사용자에게 개인화된 경험을 전달하려고 합니다.

이 브랜드는 파트너 인식 기술을 활용하여 방문자를 확률적으로 인식하고 보다 개인화된 경험을 제공합니다. 이렇게 하면 방문자가 마케팅 단계 아래로 이동할 때 사전 고려에 도움이 됩니다. 예를 들어, 브랜드는 최근에 이사한 사람들에게 어필하고 인기 있는 DIY 제품에 대해 할인을 제공하는 현장 콘텐츠에 대해 파트너가 제공한 인구 통계 신호를 사용할 수 있습니다.

## 전제 조건 및 계획 {#prerequisites-and-planning}

파트너가 제공한 속성을 사용하여 인증된 방문자와 인증되지 않은 방문자에게 개인화된 경험을 전달할 계획이라면 계획 프로세스에서 다음 전제 조건을 고려하십시오.

* 파트너의 인식 기술에 의해 예상되는 입력은 무엇이며, 이를 통해 추가 속성을 평가할 수 있습니까?
* 확률적으로 파생된 속성과 결정적으로 확인된 속성을 기반으로 다양한 채널 및 다양한 사용 사례에서 개인화를 제공하는 데 어느 정도까지 익숙합니까?
* 사전 인증되었지만 인식된 방문자가 인증될 때 해당 방문자의 경험은 어떻게 변경됩니까?

### 사용할 UI 기능, 플랫폼 구성 요소 및 Experience Cloud 제품 {#ui-functionality-and-elements}

이 사용 사례를 성공적으로 구현하려면 Real-time Customer Data Platform 및 기타 Experience Cloud 솔루션의 여러 영역을 사용해야 합니다. 필요한 사항을 가지고 있는지 확인하십시오 [속성 기반 액세스 제어 권한](/help/access-control/abac/overview.md) 이러한 모든 영역에 대해 시스템 관리자에게 필요한 권한을 부여해 달라고 요청하십시오.

* 데이터 수집
   * [Adobe Experience Platform 웹 SDK](/help/edge/home.md)
   * [태그](/help/tags/home.md)
   * [데이터스트림](/help/datastreams/overview.md)
* Real-Time CDP의 데이터 관리
   * [ID](/help/identity-service/namespaces.md)
   * [스키마](/help/xdm/home.md)
   * [데이터 사용 레이블](/help/data-governance/labels/overview.md)
   * [데이터 세트](/help/catalog/datasets/overview.md)
* 웹 속성 개인화
   * [에지 세분화](/help/segmentation/ui/edge-segmentation.md)
   * [Edge 개인화 대상](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (또는 선택한 개인화 플랫폼. 이 사용 사례 튜토리얼에서는 개인화 엔진으로서의 Adobe Target을 강조합니다.)

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

![파트너가 제공한 속성을 사용하여 방문자에게 개인화된 경험을 전달하는 방법을 설명하는 인포그래픽입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. 로서의 **고객**, 다음에서 라이선스를 부여했습니다. **데이터 파트너** 익명의 웹 사이트 방문자가 실시간으로 인사이트를 가져올 수 있습니다.
2. 로서의 **고객**&#x200B;를 호출하려면 속성에 클라이언트측 라이브러리를 배포합니다 **파트너** API를 사용하면 파트너가 제공한 신호를 Real-Time CDP으로 보내도록 Web SDK 또는 Mobile SDK를 구성할 수 있습니다.
3. 웹 사이트 또는 앱을 검색할 때 **방문자** 가 확률적으로 인식합니다. **파트너**: ID와 함께 속성을 반환합니다.
4. Real-Time CDP은 에지 세분화를 실행하여 수신 이벤트 히트를 평가하고 결과를 [ECID 식별자](https://experienceleague.adobe.com/docs/id-service/using/home.html).
5. Adobe Target은 에지 세분화 출력을 사용하여 경험을 로 다시 렌더링합니다. **방문자** 세션 내 개인화용.
6. 이벤트는 분석 및 재타겟팅과 같은 다운스트림 워크플로에 대해 전체적으로 유지됩니다.

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어보십시오.

### 데이터 관리 - ID 네임스페이스, 스키마 및 데이터 세트를 만들어 데이터 속성 관리 {#data-management}

인증되지 않은 방문자의 경험을 개인화하는 사용 사례를 달성할 준비를 하려면 먼저 수신되는 실시간 이벤트 및 대상 자격 데이터를 수신하도록 Real-Time CDP에서 데이터 관리 구조를 설정해야 합니다.

#### 파트너 ID ID 네임스페이스 만들기

먼저 파트너 ID ID 네임스페이스를 만들어야 합니다. 다음으로 이동 **[!UICONTROL 고객]** > **[!UICONTROL ID]** 왼쪽 레일에서 을 선택한 다음 **[!UICONTROL ID 네임스페이스 만들기]** 화면의 오른쪽 상단에 있습니다.

![파트너 ID가 강조 표시된 ID 네임스페이스 만들기 대화 상자입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

방법 자세히 알아보기 [파트너 ID ID 네임스페이스 만들기](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### 스키마 만들기

그런 다음 을(를) 만듭니다. [!UICONTROL 경험 이벤트] 나중에 웹 속성에서 수집할 시계열 데이터를 보관할 스키마입니다. [!UICONTROL XDM ExperienceEvent] 를 스키마의 기본 클래스로 사용합니다. 방법 알아보기 [Experience Platform UI를 사용하여 스키마 만들기](/help/xdm/ui/resources/schemas.md#create).

![스키마 만들기 및 XDM 경험 이벤트가 강조 표시된 스키마 작업 영역.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

스키마 및 [스키마에 필드 그룹 추가](/help/xdm/ui/resources/schemas.md#add-field-groups), 를 추가하는 것이 좋습니다. [웹 페이지 방문](/help/xdm/field-groups/event/web-details.md) 및 [ID 맵](/help/xdm/field-groups/profile/identitymap.md) 필드 그룹. 이는 디지털 속성 및 데이터 수집 관행에 적용할 수 있는 다른 필드 그룹에 추가됩니다.

또한 기존 필드 그룹을 만들거나 재사용하여 스키마에 추가하여 방문자에 대한 파트너가 제공한 인사이트를 캡처할 수 있습니다. 방법 읽기 [필드 그룹 만들기](/help/xdm/ui/resources/field-groups.md) 및 방법 [필드 추가](/help/xdm/ui/resources/field-groups.md) 필드 그룹으로 이동합니다. 예를 들어 연령 범위, 고용 상태, 월별 지출 금액 또는 구매 행동과 같은 파트너가 제공한 인사이트에 대해 개인화할 예정인 경우 필드 그룹에 적절한 필드가 포함되도록 합니다.

데이터 파트너가 방문자에게 안정적인 식별자를 제공하고 이를 Real-Time CDP으로 가져오려면 사용자 정의 필드 그룹의 식별자에 대해 적절하게 이름이 지정된 필드가 있어야 합니다. 또한 이전에 만든 ID 네임스페이스에서 필드를 ID로 표시해야 합니다. 다음 항목도 기억 [프로필에 포함할 스키마 활성화](/help/xdm/ui/resources/schemas.md#profile).

#### 데이터 세트 만들기

그런 다음 웹 속성 방문자로부터 수집하고 온사이트 개인화에 사용할 시계열 데이터를 보관할 데이터 세트를 만들어야 합니다.

다음에 대한 자습서 읽기: [데이터 세트를 만드는 방법](/help/catalog/datasets/user-guide.md#create) 스키마에서 데이터 세트를 만드는 옵션을 선택해야 합니다. 이전 단계에서 생성한 스키마를 기반으로 데이터 세트를 만듭니다.

스키마를 생성하는 단계와 유사하게, 데이터 세트를 [!UICONTROL 실시간 고객 프로필]. 에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 정보 [!UICONTROL 실시간 고객 프로필], 다음을 읽습니다 [스키마 튜토리얼 만들기.](/help/xdm/tutorials/create-schema-ui.md#profile)

### 웹 속성에서 이벤트 데이터 수집 구현 {#implement-data-collection}

데이터 관리 구성을 설정한 후에는 이제 실시간 이벤트를 구현해야 합니다 [데이터 수집](/help/collection/home.md) 웹 속성에서. Adobe 데이터 수집 라이브러리로 속성을 계측해야 합니다. [!UICONTROL 웹 SDK] - 실시간 이벤트 호출을 수집하여 Real-Time CDP으로 다시 보냅니다. 이 항목은 몇 가지 데이터 수집 구성 요소에 걸쳐 몇 가지 개별 작업으로 구성됩니다.

>[!IMPORTANT]
>
>파트너가 제공한 속성을 검색하려면 *웹 속성을 파트너 API 또는 기타 메서드와 통합하여 데이터 파트너의 특성을 실시간으로 호출하고 검색합니다*. 이 튜토리얼의 주제가 아니므로 선택한 파트너와 이 측면에 대해 논의하십시오.

먼저 화면 오른쪽 상단에 있는 애플리케이션 전환기를 사용하여 로 이동합니다. **[!UICONTROL 데이터 수집]** 섹션.

>[!TIP]
>
>볼 수 없는 경우 시스템 관리자에게 문의하여 액세스 권한을 요청하십시오. [!UICONTROL 데이터 수집] 애플리케이션 전환기에서.

![데이터 수집 섹션으로 이동하는 앱 전환기.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

다음 **[!UICONTROL 데이터 수집]** ui의 섹션은 아래 이미지와 유사합니다.

![플랫폼 UI의 데이터 수집 섹션.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 데이터 스트림 만들기

데이터 수집 섹션의 첫 번째 단계로, [새 데이터 스트림 만들기](/help/datastreams/configure.md). 데이터 스트림은 데이터를 수집하고 올바른 Adobe 앱(이 경우 Experience Platform)으로 올바르게 라우팅하는 방법의 기초입니다.

데이터 스트림을 만들 때 **[!UICONTROL 이벤트 스키마]** 필드에서 이전에 생성한 스키마를 선택합니다.

![새 데이터스트림을 구성할 때 강조 표시된 이벤트 스키마 선택기.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[이벤트 데이터 세트 선택](/help/datastreams/configure.md#aep) 드롭다운에서 이전에 만든 을(를) 보려면 옆에 있는 상자를 선택합니다. **[!UICONTROL Edge 세그멘테이션]** 및 **[!UICONTROL 개인화 대상]**, 및 선택 **[!UICONTROL 저장]**.

이벤트 기반 시계열 데이터를 가져오므로 이 시나리오에서는 프로필 데이터 세트를 선택할 필요가 없습니다.

#### 태그 속성 만들기

속성을 사이트에 태그를 배포할 때 확장, 규칙, 데이터 요소 및 라이브러리로 채우는 컨테이너로 간주합니다.

다음으로 이동 **[!UICONTROL 태그]** 및 선택 **[!UICONTROL 새 속성]**.

![새 태그 속성을 만듭니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

필수 필드를 입력하고 선택 **[!UICONTROL 저장]**.

![새 속성의 필수 필드를 채웁니다.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

방법에 대한 전체 정보 가져오기 [태그 속성 만들기](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

그런 다음 속성 내에 다양한 확장을 설치해야 합니다. 태그 속성을 선택하고 [!UICONTROL 확장] 섹션.

![새 태그 속성을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

다음 사항에 주목하십시오. [!UICONTROL 코어] 확장이 이미 설치되어 있습니다. 다음 섹션에 자세히 설명된 대로 확장을 두 개 더 설치해야 합니다.

![설치된 확장을 봅니다.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Web SDK 확장 설치

이 튜토리얼에서는 Web SDK를 사용하여 웹 사이트를 측정하는 방법을 설명합니다. 다음을 사용할 수도 있습니다. [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) 을 사용하여 앱 방문자에게 경험을 개인화할 수 있습니다.

![확장 카탈로그에서 Web SDK 확장 보기.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Web SDK를 구성하는 화면에서 아래로 이동하여 **[!UICONTROL 데이터스트림]** 섹션에 사용 중인 Experience Platform 샌드박스에 대한 정보를 제공합니다. 다음 드롭다운에서 적절한 샌드박스와 이전 단계에서 생성된 데이터스트림을 선택합니다. 다른 모든 환경에 대해 동일한 샌드박스 및 데이터스트림 값을 선택할 수 있습니다. 다른 설정은 그대로 두고 를 선택합니다. **[!UICONTROL 저장]**.

다음에 대한 전체 정보 가져오기 [웹 SDK 설치 방법](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### ID 서비스 확장 설치

사용 [Experience Cloud ID 서비스 확장](/help/tags/extensions/client/id-service/overview.md) 모든 Experience Cloud 솔루션에서 방문자에 대한 고유한 장치 기반 자사 ID를 만들 수 있습니다. 검색 대상 **[!UICONTROL ID 서비스]** 확장 카탈로그에서 를 설치하고 설치합니다. 확장을 설치할 때 모든 기본 설정을 유지합니다.

![확장 카탈로그에서 ID 서비스 확장 보기.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 환경 설정

그런 다음 로 이동합니다. **[!UICONTROL 환경]** 왼쪽 탐색 섹션에 있는 섹션을 참조하십시오. 이 단계에서는 웹 사이트를 Adobe Edge 네트워크에 연결하여 방문자 정보를 실시간으로 검색하고 전달해야 합니다.

개발 환경 오른쪽에 있는 상자 아이콘을 선택하고 모달 창에 표시되는 JavaScript 코드 조각의 표준 버전을 복사합니다.

![데이터 수집 UI의 환경 섹션에서 강조 표시된 상자 아이콘을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

이 코드 조각을 웹 사이트의 맨 위에 추가해야 합니다. 그 결과 웹 사이트는 Adobe Edge 네트워크를 호출하여 페이지에 로드되고 실행될 JavaScript 논리를 검색합니다. 이를 통해 방문자 ID 생성, 데이터 수집 및 실시간 경험 개인화와 같은 기능을 사용할 수 있습니다.

#### 데이터 요소 설정

데이터 요소는 데이터 사전(또는 데이터 맵)의 기본 구성단위입니다. 단일 데이터 요소는 쿼리 문자열, URL, 쿠키 값, JavaScript 변수 등에 값을 매핑할 수 있는 변수입니다. 자세한 내용 [데이터 요소](/help/tags/ui/managing-resources/data-elements.md).

이 사용 사례에서는 두 개의 데이터 요소를 설정해야 합니다.

먼저 다음을 설정합니다. `partnerData` 요소를 생성하지 않습니다. 다음 위치로 이동 **[!UICONTROL 데이터 요소]** 섹션 및 선택 **[!UICONTROL 새 데이터 요소 만들기]**.

![새 데이터 요소를 만듭니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

데이터 요소에 이름을 지정합니다 `partnerData`을(를) 상태로 둡니다. [!UICONTROL 확장] 값: [!UICONTROL 코어], 및 설정 **[!UICONTROL 데이터 요소 유형]** 다음으로: **[!UICONTROL JavaScript 변수]**. 입력 `partnerData` (제목이 있는 필드에서) **[!UICONTROL JavaScript 변수 이름]** 및 선택 **[!UICONTROL 저장]**.

![partnerData 데이터 요소를 올바르게 구성하기 위해 강조 표시된 선택 사항입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

두 번째 데이터 요소를 설정하려면 새 변수의 이름을 지정합니다 `pageVisit`, 를 설정합니다. **[!UICONTROL 확장]** 끝 **[!UICONTROL Adobe Experience Platform]** 및 선택 **[!UICONTROL XDM 개체]** 를 데이터 유형으로 사용하십시오.

![pageVisit 데이터 요소를 올바르게 구성하기 위해 강조 표시된 선택 항목입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

스키마에서 데이터 파트너에게 기대하는 값에 해당하는 타사 속성을 선택합니다. 그런 다음 제목이 있는 라디오 단추를 선택합니다 **[!UICONTROL 전체 개체 제공]**. 데이터베이스처럼 보이는 아이콘을 선택하고 `partnerData` 이전에 만든 데이터 요소입니다.

#### 규칙 설정

다음에서 **[!UICONTROL 규칙]** 섹션에서는 방금 만든 데이터 요소에 로드된 속성으로 Adobe에 개인화 요청을 보내도록 웹 사이트를 구성할 수 있습니다. 자세한 내용 [규칙 만들기](/help/tags/ui/managing-resources/rules.md).

선택 **[!UICONTROL 새 규칙 만들기]**. 이 규칙 이름 지정 **[!UICONTROL 개인화]** 옆에 있는 + 기호를 선택합니다. **[!UICONTROL 이벤트]**. 선택 **[!UICONTROL 페이지 하단]** 를 이벤트로 사용하고 저장합니다.

![규칙의 이벤트 유형 부분에 대한 선택 사항입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

옆에 있는 + 기호를 선택합니다. **[!UICONTROL 작업]**. 확장을 다음으로 업데이트 **[!UICONTROL Adobe Experience Platform 웹 SDK]** 및 설정 **[!UICONTROL 작업 유형]** 끝 **[!UICONTROL 이벤트 보내기]**.

![규칙의 작업 유형 부분에 대한 선택 사항입니다.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

다음에서 **[!UICONTROL 유형]** 오른쪽의 드롭다운 선택기에서 `web.webpagedetails.pageViews` 를 이벤트 유형으로 사용하십시오.

![이벤트 유형을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

XDM 데이터 옆에 있는 데이터베이스 아이콘을 선택하고 `pageVisit` 데이터 요소입니다.

작업 구성 목록을 아래로 스크롤하여 제목이 있는 상자를 선택해야 합니다. **[!UICONTROL 시각적 개인화 결정 렌더링]**. Adobe Target 또는 기타 유사한 제품을 통해 제공된 경험을 웹 페이지에서 시각적으로 렌더링할 수 있도록 하는 것이 중요합니다. 선택 **[!UICONTROL 변경 내용 유지]**, 및 **[!UICONTROL 저장]** 규칙입니다.

![시각적 개인화 결정 렌더링 확인란을 선택합니다.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 게시 워크플로우 설정

이 구성을 웹 페이지에 배포하기 위해 다음 단계는 방금 만든 리소스를 포함하는 라이브러리를 빌드하는 것입니다. 자세한 내용 [게시 플로우 설정](/help/tags/ui/publishing/publishing-flow.md).

선택 **[!UICONTROL 게시 플로우]** 그런 다음 **[!UICONTROL 라이브러리 추가]**.

선택 **[!UICONTROL 변경된 모든 리소스 추가]**, 라이브러리에 이름을 지정하고 환경을 로 설정합니다. **[!UICONTROL 개발]** 및 선택 **[!UICONTROL 개발에 저장 및 구축]**.

![라이브러리를 만들고 개발 환경에 배포](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 웹 사이트 테스트

이 시점에서 웹 사이트는 웹 SDK를 사용하여 완전히 계측되어야 합니다. 데이터 수집이 예상대로 작동하는지 테스트하려면 웹 사이트로 이동하고 브라우저의 개발자 도구를 사용하여 네트워크 트래픽을 검사할 수 있습니다.

입력 `interact` 검색 상자에서 페이지를 새로 고치면 웹 사이트의 네트워크 호출이 Adobe Edge 네트워크에 채워지는 것을 볼 수 있습니다.

![개발자 도구에서 채우는 네트워크 이벤트 보기.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 개인화 {#personalization}

이제 개인화를 위해 대상자를 만들고 활성화할 준비가 되었습니다.

#### 에지 세분화 설정

설정 [가장자리 세분화](/help/segmentation/ui/edge-segmentation.md) 따라서 방문자가 웹 자산을 방문할 때 방문자의 대상 멤버십이 실시간으로 평가됩니다.

또한 을(를) 설정해야 합니다 [active-on-edge 병합 정책](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) Edge Audiences용

#### Adobe Target 또는 기타 사용자 지정 개인화 대상과 통합

이제 개인화 엔진과 통합하여 웹 사이트 또는 앱 방문자에게 개인화된 콘텐츠를 표시할 준비가 되었습니다. Adobe은 [Adobe Target 대상](/help/destinations/catalog/personalization/adobe-target-connection.md) 이 목적을 위해.

>[!IMPORTANT]
>
>다음에 대한 자습서 읽기: [edge 개인화 대상으로 대상자 활성화](/help/destinations/ui/activate-edge-personalization-destinations.md) 대상자를 활성화하는 데 필요한 단계에 대한 전체 보기입니다.

## 제한 사항 및 문제 해결 {#limitations-and-troubleshooting}

이 페이지에 설명된 사용 사례를 탐색할 때 다음 제한 사항에 유의하십시오.

* 파트너 ID를 사용하는 경우, [id 그래프](/help/identity-service/ui/identity-graph-viewer.md).

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* [신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완](/help/rtcdp/partner-data/supplement-first-party-profiles.md)하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.
* Real-Time CDP에서 서드파티 데이터 지원을 사용하여 [데이터 파트너의 잠재 고객으로 프로필 기반을 확장하고 이들과 협력하여 새로운 고객을 확보하거나 연락하십시오](/help/rtcdp/partner-data/prospecting.md).
* (**준비 중**) [!BADGE Beta]{type=Informative}파트너 ID를 사용하여 PII 또는 해시된 PII를 허용하지 않는 게시 에코시스템으로 **활성화 범위를 확장**&#x200B;했습니다.