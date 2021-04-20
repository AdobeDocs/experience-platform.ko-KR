---
keywords: Experience Platform;시작하기;고객 아이디;인기 항목;고객 아이에이 입력;고객 아이에이 출력
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 고객 AI의 입력 및 출력
topic: Getting started
description: 고객 AI에서 활용하는 필수 이벤트, 입력 및 결과물에 대한 자세한 내용을 살펴보십시오.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2867'
ht-degree: 1%

---

# 고객 AI에서 입력 및 출력

다음 문서는 고객 AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력 개요를 설명합니다.

## 시작하기

고객 AI는 다음 데이터 세트 중 하나를 분석하여 이탈률 또는 전환 성향 점수를 예측합니다.

- CEE(Consumer Experience Event) 데이터 세트
- [Analytics 소스 커넥터를 사용하는 Adobe Analytics 데이터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- [Audience Manager 소스 커넥터를 사용하는 Adobe Audience Manager 데이터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>소스 커넥터에서 데이터를 채우는 데 최대 4주가 소요됩니다. 최근에 커넥터를 설정하는 경우 데이터 세트에 고객 AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. [내역 데이터](#data-requirements) 섹션을 검토하여 예측 목표에 충분한 데이터가 있는지 확인하십시오.

이 문서는 CEE 스키마를 기본적으로 이해해야 합니다. 계속하기 전에 [Intelligent Services 데이터 준비](../data-preparation.md) 설명서를 검토하십시오.

다음 표에서는 이 문서에 사용되는 몇 가지 일반적인 용어에 대해 설명합니다.

| 용어 | 정의 |
| --- | --- |
| [경험 데이터 모델(XDM)](../../xdm/home.md) | XDM은 Adobe Experience Platform을 기반으로 하는 Adobe Experience Cloud이 올바른 고객에게 올바른 메시지를 적시에 적합한 채널에 전달할 수 있는 기본 프레임워크입니다. Experience Platform이 구축되는 방법론, XDM 시스템은 플랫폼 서비스에서 사용하기 위해 경험 데이터 모델 스키마를 운영합니다. |
| XDM 스키마 | Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. 데이터를 플랫폼에 인제스트하려면 데이터 구조를 설명하고 각 필드에 포함할 수 있는 데이터 유형에 제약 조건을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 XDM 클래스와 0개 이상의 혼합으로 구성됩니다. |
| XDM 클래스 | 모든 XDM 스키마는 레코드 또는 시간 시리즈로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 스키마의 클래스에 의해 정의됩니다. 이 클래스는 스키마를 처음 만들 때 스키마에 할당됩니다. XDM 클래스는 특정 데이터 비헤이비어를 나타내기 위해 스키마에서 포함해야 하는 속성의 최소 수를 설명합니다. |
| [혼합](../../xdm/schema/composition.md) | 스키마에서 하나 이상의 필드를 정의하는 구성 요소입니다. 혼합은 해당 필드가 스키마의 계층에서 표시되는 방식을 적용하므로 해당 필드가 포함된 모든 스키마에서 동일한 구조를 표시합니다. 믹스는 `meta:intendedToExtend` 특성으로 식별되는 특정 클래스와 호환됩니다. |
| [데이터 유형](../../xdm/schema/composition.md) | 스키마에 대해 하나 이상의 필드를 제공할 수도 있는 구성 요소입니다. 그러나 믹스와는 달리 데이터 유형은 특정 클래스로 제한되지 않습니다. 따라서 데이터 유형을 보다 유연하게 설명하여 서로 다른 클래스가 있는 여러 스키마에서 다시 사용할 수 있는 일반적인 데이터 구조를 설명합니다. 이 문서에 설명된 데이터 유형은 CEE와 Adobe Analytics 스키마 모두에서 지원됩니다. |
| 가입/해지 전환 | 구독을 취소하거나 갱신하지 않기로 선택한 계정의 백분율을 측정합니다. 가입자 이탈률이 높으면 MRR(Monthly Recognition Revenue)에 부정적인 영향을 줄 수 있으며 제품 또는 서비스에 대한 불만을 나타낼 수도 있습니다. |
| [실시간 고객 프로필](../../profile/home.md) | 실시간 고객 프로필은 타깃팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계된 데이터는 물론 Experience Platform과 함께 사용하는 시스템에서 발생한 개별 이벤트에 대해 실행 가능한 타임스탬프가 지정된 계정에 대한 데이터도 포함되어 있습니다. |

## 고객 AI 입력 데이터

>[!TIP]
>
> 고객 AI는 예측에 유용한 이벤트를 자동으로 결정하고 사용 가능한 데이터가 품질 예측을 생성하는 데 충분하지 않을 경우 경고를 표시합니다.

고객 AI는 CEE, Adobe Analytics 및 Adobe Audience Manager 데이터 세트를 지원합니다. CEE 스키마는 스키마 생성 프로세스 중에 혼합을 추가해야 합니다. Adobe Analytics 또는 Adobe Audience Manager 데이터 세트를 사용하는 경우 소스 커넥터는 연결 프로세스 동안 아래에 나열된 표준 이벤트(커머스, 웹 페이지 세부 사항, 응용 프로그램 및 검색)를 직접 매핑합니다.

Adobe Analytics 데이터 또는 Audience Manager 데이터 매핑에 대한 자세한 내용은 [분석 필드 매핑](../../sources/connectors/adobe-applications/analytics.md) 또는 [Audience Manager 필드 매핑](../../sources/connectors/adobe-applications/mapping/audience-manager.md) 안내서를 참조하십시오.

### 고객 AI {#standard-events}에서 사용하는 표준 이벤트

XDM 경험 이벤트는 다양한 고객 행동을 결정하는 데 사용됩니다. 데이터 구성 방식에 따라 아래 나열된 이벤트 유형에 고객의 모든 행동이 포함되지 않을 수 있습니다. 웹 사용자 활동을 명확하고 모호하게 식별하기 위해 필요한 데이터가 있는 필드를 파악하는 것은 전적으로 개인의 책임입니다. 예측 목표에 따라 필요한 필수 필드가 변경될 수 있습니다.

고객 AI는 모델 기능을 구축하기 위해 다양한 이벤트 유형을 사용합니다. 이러한 이벤트 유형은 여러 XDM 믹싱을 사용하여 스키마에 자동으로 추가됩니다.

>[!NOTE]
>
>Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 데이터 캡처에 필요한 표준 이벤트를 사용하여 스키마가 자동으로 생성됩니다. 데이터를 캡처하기 위해 고유한 사용자 정의 CEE 스키마를 만드는 경우 데이터를 캡처하는 데 필요한 혼합을 고려해야 합니다.

아래 나열된 각 표준 이벤트에 대한 데이터는 필요하지 않지만 특정 시나리오에 특정 이벤트는 필요합니다. 사용 가능한 표준 이벤트 데이터가 있으면 스키마에 포함하는 것이 좋습니다. 예를 들어 구매 이벤트 예측을 위해 고객 AI 응용 프로그램을 만들려면 `Commerce` 및 `Web page details` 데이터 유형의 데이터를 가져오는 것이 유용합니다.

플랫폼 UI에서 혼합을 보려면 왼쪽 레일의 **[!UICONTROL Schemas]** 탭을 선택하고 **[!UICONTROL Mixins]** 탭을 선택합니다.


| 믹신 | 이벤트 유형 | XDM 필드 경로 |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | 주문 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 체크아웃 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 구매 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemoval | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationClose | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsits | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | 검색 | search.keywords |

또한 고객 AI는 구독 데이터를 사용하여 보다 효과적인 이탈률 모델을 구축할 수 있습니다. 구독 데이터는 [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) 데이터 유형 형식을 사용하여 각 프로필에 필요합니다. 하지만 대부분의 필드는 선택 사항이지만, 최적 이탈 모델의 경우, `startDate`, `endDate` 및 기타 관련 세부 정보와 같이 가능한 한 많은 필드에 데이터를 제공하는 것이 좋습니다.

### 이전 데이터 {#data-requirements}

고객 AI를 사용하려면 모델 교육을 위한 내역 데이터가 필요하지만 필요한 데이터 양은 다음 두 가지 주요 요소를 기반으로 합니다.결과 창 및 적격한 모집단.

기본적으로, 고객 AI는 애플리케이션 구성 중에 적절한 인구 정의가 제공되지 않을 경우 지난 120일 동안 사용자가 활동을 수행했는지 확인합니다. 또한 고객 AI에는 예측된 목표 정의를 기반으로 한 기록 데이터의 최소 500개의 적격한 이벤트 및 500개의 유효 이벤트(총 1000개)가 필요합니다.

제공된 다음 예는 간단한 공식을 사용하여 필요한 최소 데이터 양을 결정하는 데 도움이 됩니다. 최소 요구 사항을 초과하는 경우 모델이 더 정확한 결과를 제공할 수 있습니다. 필요한 최소 금액보다 적은 경우 모델 교육을 위한 충분한 데이터가 없으므로 모델이 실패합니다.

**공식**:

필요한 최소 데이터 길이 = 적격한 모집단 + 결과 창

>[!NOTE]
>
> 30은 자격 조건을 갖춘 모집단에게 필요한 최소 일수입니다. 이 값이 제공되지 않으면 기본값은 120일입니다.

예

- 30일 후에 고객의 시계 구매 여부를 예측할 수 있습니다. 지난 60일 동안 일부 웹 활동이 있는 사용자의 점수를 매길 수도 있습니다. 이 경우 필요한 데이터의 최소 길이는 60일 + 30일입니다. 자격 조건을 갖춘 인구는 60일이며 결과 기간은 30일입니다.

- 사용자가 앞으로 7일 이내에 시계를 구매할 가능성이 있는지 여부를 예측해야 합니다. 이 경우 필요한 데이터의 최소 길이는 120일 + 7일입니다. 자격 조건을 갖춘 모집단 기본값은 120일이며, 결과 창은 총 127일이 7일입니다.

- 고객이 앞으로 7일 이내에 시계를 구입할 가능성이 있는지 여부를 예측할 수 있습니다. 지난 7일 동안 일부 웹 활동이 있는 사용자를 점수를 매길 수도 있습니다. 이 경우 필요한 데이터의 최소 길이는 30일 + 7일입니다. 자격 조건을 갖춘 인구는 최소 30일이 필요하며 결과 창은 총 37일이 7일입니다.

필요한 최소 데이터 외에도 고객 AI는 최신 데이터에서 가장 잘 작동합니다. 이 경우 고객 AI는 사용자의 최근 행동 데이터를 기반으로 미래에 대한 예측을 수행하고 있습니다. 즉, 보다 최근의 데이터가 보다 정확한 예측을 할 가능성이 높습니다.

### 예제 시나리오

이 섹션에서는 고객 AI 인스턴스에 대한 다양한 시나리오와 필수 및 권장 이벤트 유형에 대해 설명합니다. 혼합과 해당 필드 경로에 대한 자세한 내용은 위의 [표준 이벤트 테이블](#standard-events)을 참조하십시오.

>[!NOTE]
>
> 필수 이벤트 유형은 웹 사용자 활동을 명확하고 모호하게 식별하는 데 사용됩니다. 필요한 이벤트 유형 수는 스키마의 예측 목표 및 구조에 따라 변경됩니다. 특정 이벤트 유형이 필요하지 않은 경우 CEE 스키마를 작성하는 동안 해당 이벤트 유형을 포함하는 것이 좋습니다. Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 스트리밍 중인 데이터에 따라 필요한 표준 이벤트를 사용할 수 있습니다.

### 시나리오 1:전자 상거래 소매 웹 사이트에서 구매 전환

**예측 목표:** 웹 사이트에서 특정 의류 기사를 구매할 자격 조건을 갖춘 프로필의 전환 경향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 2:미디어 스트리밍 서비스 웹 사이트의 구독 전환

**예측 목표:** 표준 또는 프리미엄 플랜과 같은 특정 수준의 구독을 수행하기 위한 자격 조건을 갖춘 프로필의 구독 전환율을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

이 예에서 `order`, `checkouts` 및 `purchases`는 구독을 구매했음을 나타내는 데 사용됩니다.

또한 정확한 모델의 경우 [구독 데이터 유형](../../xdm/data-types/subscription.md)에서 사용 가능한 속성 중 일부를 사용하는 것이 좋습니다.

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 3:전자 상거래 소매 웹 사이트에서 가입

**예측 목표:** 구매 이벤트가 발생하지 않을 가능성을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 4:전자 상거래 소매 웹 사이트에서 업셀링 전환

**예측 목표:** 관련 새 제품을 구매하기 위해 특정 제품을 구매한 인구의 구매 경향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 5:온라인 뉴스 방송에서 구독 취소(가입 해지)

**예측 목표:** 다음 달 서비스 가입 해지를 위한 자격 조건을 갖춘 인구의 경향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- webVisit
- 검색

또한 정확한 모델의 경우 [구독 데이터 유형](../../xdm/data-types/subscription.md)에서 사용 가능한 속성 중 일부를 사용하는 것이 좋습니다.

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 6:모바일 애플리케이션 시작

**예측 목표:** 다음 X일 이내에 유료 모바일 애플리케이션을 실행할 자격 조건을 갖춘 프로필의 경향을 예측합니다. 이것은 &quot;월별 활성 사용자&quot;의 주요 성과 지표(KPI)를 예측하는 것과 유사합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력을 위해 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- applicationClose
- applicationCrashes
- applicationFeatureUsits
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

이 예제에서는 모바일 응용 프로그램을 구입해야 할 때 `order`, `checkouts` 및 `purchases`가 사용됩니다.

**추가적인 권장 표준 이벤트 유형:**

고객 AI 인스턴스를 구성하는 동안 목표 및 자격 조건을 갖춘 모집단의 복잡성을 감안하여 나머지 [이벤트 유형](#standard-events)이 필요할 수 있습니다. 특정 데이터 유형에 데이터를 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 7:트레이트 실현됨(Adobe Audience Manager)

**예측 목표:** 구현할 일부 트레이트의 경향을 예측합니다.

**필수 표준 이벤트 유형:**

Adobe Audience Manager의 트레이트를 사용하려면 [Audience Manager 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)를 사용하여 소스 연결을 만들어야 합니다. 소스 커넥터는 적절한 믹싱을 사용하여 스키마를 자동으로 만듭니다. 고객 AI에서 사용할 수 있도록 스키마에 대한 이벤트 유형을 수동으로 추가할 필요는 없습니다.

새 고객 AI 인스턴스를 구성할 때 목표를 정의하는 동안 점수를 매길 특정 트레이트를 선택하는 데 `audienceName` 및 `audienceID`을 사용할 수 있습니다.

## 고객 AI 출력 데이터

고객 AI는 적격한 개별 프로파일에 대해 몇 가지 속성을 생성합니다. 제공된 항목을 기반으로 점수(출력)를 사용하는 방법에는 두 가지가 있습니다. 실시간 고객 프로필 사용 데이터 세트가 있는 경우 [세그먼트 빌더](../../segmentation/ui/segment-builder.md)에서 실시간 고객 프로필의 통찰력을 사용할 수 있습니다. 프로필 사용 데이터 집합이 없는 경우 [데이터 레이크에서 사용 가능한 고객 AI 출력](./user-guide/download-scores.md) 데이터 집합을 다운로드할 수 있습니다.

>[!NOTE]
>
> 출력 값은 세그먼트를 만들고 정의하는 데 사용할 수 있는 실시간 고객 프로필에 사용됩니다.

아래 표에서는 고객 AI 출력에 있는 다양한 속성에 대해 설명합니다.

| 특성 | 설명 |
| ----- | ----------- |
| 점수 | 정의된 기간 내에 예측된 목표를 달성할 상대적인 가능성. 이 값은 확률 백분율로 간주되지 않고 전체 모집단에 비해 개인의 가능성이 높습니다. 이 점수는 0부터 100까지입니다. |
| 확률 | 이 속성은 정의된 기간 내에 예측된 목표를 달성하기 위한 프로파일의 실제 가능성입니다. 여러 목표 간 결과물을 비교할 때는 백분위수 또는 점수보다 확률을 고려하는 것이 좋습니다. 확성은 빈번하지 않은 이벤트에 대해 낮은 쪽에 있기 때문에 자격 있는 모집단에서 평균 확률을 결정할 때 항상 사용해야 합니다. 0과 1 사이의 가능성 범위 값입니다. |
| 백분위수 | 이 값은 유사한 점수가 지정된 다른 프로필과 상대적인 프로필의 성능에 대한 정보를 제공합니다. 예를 들어 이탈 시 백분위수 등급이 99인 프로필은 점수가 할당된 다른 모든 프로필의 99%와 비교하여 추사 위험이 높다는 것을 나타냅니다. 백분위수 범위는 1부터 100까지입니다. |
| 성향 유형 | 선택한 성향 유형. |
| 점수 날짜 | 점수가 발생한 날짜. |
| 영향력 있는 요인 | 프로필이 전환되거나 이탈할 가능성이 높은 이유를 예측했습니다. 요소는 다음 속성으로 구성됩니다.<ul><li>코드:프로필의 예측된 점수에 긍정적으로 영향을 주는 프로필 또는 행동 특성입니다. </li><li>값:프로필 또는 행동 속성의 값입니다.</li><li>중요도:예측된 점수(낮음, 보통, 높음)에 프로필 또는 행동 특성의 가중치를 나타냅니다.</li></ul> |

## 다음 단계 {#next-steps}

데이터를 준비하고 자격 증명과 스키마를 모두 준비했으면 [고객 AI 인스턴스 구성](./user-guide/configure.md) 가이드를 따라 시작합니다. 이 안내서에서는 고객 AI에 대한 인스턴스를 만드는 과정을 안내합니다.
