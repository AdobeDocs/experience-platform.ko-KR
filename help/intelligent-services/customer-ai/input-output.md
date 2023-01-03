---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;고객 ai 입력;고객 ai 출력
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 고객 AI의 입력 및 출력
topic-legacy: Getting started
description: Customer AI에서 활용하는 필수 이벤트, 입력 및 출력에 대해 자세히 알아보십시오.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 165e5ccae5ca78b3912fef1ba0b3fd4567e231fb
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 3%

---

# 고객 AI의 입출력

다음 문서에서는 Customer AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력에 대해 설명합니다.

## 시작하기

고객 AI는 다음 데이터 세트 중 하나를 분석하여 이탈이나 전환 성향 점수를 예측합니다.

- 를 사용하여 Adobe Analytics 데이터 [Analytics 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 를 사용하여 Adobe Audience Manager 데이터 [Audience Manager 원본 커넥터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- 경험 이벤트(EE) 데이터 세트
- 소비자 경험 이벤트(CEE) 데이터 세트

각 데이터 세트가 ECID와 같은 동일한 ID 유형(네임스페이스)을 공유하는 경우 다른 소스에서 여러 데이터 세트를 추가할 수 있습니다. 여러 데이터 세트 추가에 대한 자세한 내용은 [Customer AI 사용 안내서](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>소스 커넥터에서 데이터를 채우는 데 최대 4주가 소요됩니다. 최근에 커넥터를 설정하는 경우 데이터 세트에 고객 AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 다음 문서를 검토하십시오 [내역 데이터](#data-requirements) 예측 목표에 충분한 데이터가 있는지 확인하는 섹션을 참조하십시오.

이 문서는 CEE 스키마를 기본 이해해야 합니다. 다음 문서를 검토하십시오 [Intelligent Services 데이터 준비](../data-preparation.md) 설명서를 참조하십시오.

다음 표에서는 이 문서에서 사용되는 몇 가지 일반적인 용어에 대해 설명합니다.

| 용어 | 정의 |
| --- | --- |
| [XDM(경험 데이터 모델)](../../xdm/home.md) | XDM은 Adobe Experience Platform에서 제공하는 Adobe Experience Cloud이 올바른 사람에게 올바른 메시지를 적시에 적절한 채널에 전달할 수 있도록 하는 기본 프레임워크입니다. Experience Platform을 빌드하는 방법론인 XDM System은 Platform 서비스에서 사용하기 위해 Experience Data Model 스키마를 작동시킵니다. |
| XDM 스키마 | Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. 데이터를 Platform에 수집하려면 먼저 데이터 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제한을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 XDM 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. |
| XDM 클래스 | 모든 XDM 스키마에서는 레코드 또는 시계열로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 처음 만들 때 스키마에 할당된 스키마 클래스에 의해 정의됩니다. XDM 클래스는 특정 데이터 동작을 나타내려면 스키마에 포함해야 하는 가장 작은 수의 속성을 설명합니다. |
| [필드 그룹](../../xdm/schema/composition.md) | 스키마에 필드를 하나 이상 정의하는 구성 요소입니다. 필드 그룹은 해당 필드가 스키마 계층에 표시되는 방식을 적용하므로 포함된 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 해당 필드별로 식별되는 특정 클래스와 호환됩니다 `meta:intendedToExtend` 속성을 사용합니다. |
| [데이터 유형](../../xdm/schema/composition.md) | 스키마에 대해 하나 이상의 필드를 제공할 수 있는 구성 요소입니다. 그러나 필드 그룹과 달리 데이터 형식은 특정 클래스에 한정되지 않습니다. 따라서 데이터 형식을 보다 유연하게 사용하여 여러 스키마에서 다시 사용할 수 있는 공통 데이터 구조를 설명하거나 다른 클래스를 사용할 수 있습니다. 이 문서에 설명된 데이터 유형은 CEE 및 Adobe Analytics 스키마에서 모두 지원됩니다. |
| 이탈 | 구독을 취소하거나 갱신하지 않도록 선택하는 계정의 비율 측정입니다. 이탈률이 높으면 MRR(월별 반복 매출)에 부정적인 영향을 줄 수 있으며 제품 또는 서비스에 대한 불만을 나타낼 수도 있습니다. |
| [실시간 고객 프로필](../../profile/home.md) | 실시간 고객 프로필은 타겟팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계되는 데이터와, Experience Platform에 사용하는 시스템에서 발생한 개별 이벤트와 관련된 실행 가능한 타임스탬프 계정이 포함되어 있습니다. |

## 고객 AI 입력 데이터

>[!TIP]
>
> Customer AI는 예측에 유용한 이벤트를 자동으로 결정하고 사용 가능한 데이터가 품질 예측을 생성하기에 충분하지 않은 경우 경고를 표시합니다.

고객 AI는 Adobe Analytics, Adobe Audience Manager, EE(Experience Event) 및 CEE(Consumer Experience Event) 데이터 세트를 지원합니다. CEE 스키마를 사용하려면 스키마 생성 프로세스 중에 필드 그룹을 추가해야 합니다. Adobe Analytics 또는 Adobe Audience Manager 데이터 세트를 사용하는 경우 소스 커넥터는 연결 프로세스 중에 아래에 나열된 표준 이벤트(커머스, 웹 페이지 세부 사항, 애플리케이션 및 검색)를 직접 매핑합니다. 각 데이터 세트가 ECID와 같은 동일한 ID 유형(네임스페이스)을 공유하는 경우 다른 소스에서 여러 데이터 세트를 추가할 수 있습니다.

Adobe Analytics 데이터 또는 Audience Manager 데이터 매핑에 대한 자세한 내용은 [Analytics 필드 매핑](../../sources/connectors/adobe-applications/analytics.md) 또는 [Audience Manager 필드 매핑](../../sources/connectors/adobe-applications/mapping/audience-manager.md) 안내서.

### 고객 AI에서 사용하는 표준 이벤트 {#standard-events}

XDM 경험 이벤트는 다양한 고객 행동을 결정하는 데 사용됩니다. 데이터 구성 방식에 따라 아래 나열된 이벤트 유형은 고객의 모든 행동을 포괄하지 않을 수 있습니다. 웹 사용자 활동을 명확하고 분명하게 식별하는 데 필요한 데이터가 있는 필드를 결정하는 것은 귀하의 책임입니다. 예측 목표에 따라 필요한 필수 필드가 변경될 수 있습니다.

고객 AI는 모델 기능을 구축하기 위해 다양한 이벤트 유형을 사용합니다. 이러한 이벤트 유형은 여러 XDM 필드 그룹을 사용하여 스키마에 자동으로 추가됩니다.

>[!NOTE]
>
>Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 데이터를 캡처하는 데 필요한 표준 이벤트를 사용하여 스키마가 자동으로 생성됩니다. 데이터를 캡처하기 위해 고유한 사용자 지정 CEE 스키마를 생성하는 경우 데이터를 캡처하는 데 필요한 필드 그룹을 고려해야 합니다.

아래에 나열된 각 표준 이벤트에 대한 데이터가 필요하지 않지만 특정 이벤트는 특정 시나리오에 필요합니다. 사용 가능한 표준 이벤트 데이터가 있는 경우 스키마에 포함하는 것이 좋습니다. 예를 들어 구매 이벤트 예측을 위해 Customer AI 애플리케이션을 만들어야 하는 경우 의 데이터를 가져오는 것이 유용합니다 `Commerce` 및 `Web page details` 데이터 유형.

플랫폼 UI에서 필드 그룹을 보려면 **[!UICONTROL 스키마]** 왼쪽 레일의 탭을 선택하고 **[!UICONTROL 필드 그룹]** 탭.

| 필드 그룹 | 이벤트 유형 | XDM 필드 경로 |
| --- | --- | --- |
| [!UICONTROL 상거래 세부 사항] | 주문 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 체크아웃 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 구매 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemoval | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpen | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL 웹 세부 사항] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL 애플리케이션 세부 정보] | applicationClose | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsage | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL 검색 세부 사항] | 검색 | search.keywords |

또한 고객 AI는 구독 데이터를 사용하여 더 나은 이탈 모델을 구축할 수 있습니다. 구독 데이터는 [[!UICONTROL 구독]](../../xdm/data-types/subscription.md) 데이터 형식 형식입니다. 대부분의 필드는 선택 사항이지만 최적의 이탈 모델의 경우 다음과 같은 필드를 최대한 많은 필드에 데이터를 제공하는 것이 좋습니다. `startDate`, `endDate`, 및 기타 관련 세부 사항.

### 사용자 지정 이벤트 및 프로필 속성 추가

추가 정보 [표준 이벤트 필드](#standard-events) 고객 AI에서 사용하는 경우 사용자 지정 이벤트 및 사용자 지정 프로필 속성 옵션이 [인스턴스 구성](./user-guide/configure.md#custom-events).

선택한 데이터 세트에 스키마에 정의된 &quot;호텔 예약&quot; 또는 &quot;X 회사의 직원&quot;과 같은 사용자 지정 이벤트 또는 프로필 속성이 포함된 경우 해당 이벤트를 인스턴스에 추가할 수 있습니다. 이러한 추가적인 사용자 지정 이벤트 및 프로필 속성은 Customer AI에서 모델의 품질을 향상시키고 보다 정확한 결과를 제공하기 위해 사용합니다.

### 이전 데이터 {#data-requirements}

고객 AI에는 모델 교육을 위한 내역 데이터가 필요하지만 데이터 양은 다음 두 가지 주요 요소를 기반으로 합니다. 결과 창 및 적격 모집단.

기본적으로, 고객 AI는 애플리케이션 구성 중에 적절한 모집단 정의가 제공되지 않는 경우 지난 120일 동안 활동이 있었는지 사용자를 찾습니다. 또한 Customer AI에는 예측된 목표 정의를 기반으로 최소 500개의 자격 증명과 500개의 미자격 이벤트(총 1000개)가 필요합니다.

제공된 다음 예에서는 간단한 공식을 사용하여 필요한 최소 데이터 양을 결정합니다. 최소 요구 사항 이상이 있는 경우 모델이 더 정확한 결과를 제공할 수 있습니다. 필요한 최소 금액보다 적은 경우 모델 교육을 위한 충분한 데이터가 없으므로 모델이 실패합니다.

**공식**:

필요한 최소 데이터 길이 = 적격 모집단 + 결과 창

>[!NOTE]
>
> 30은 적격 모집단에 필요한 최소 일 수입니다. 이 값을 제공하지 않으면 기본값은 120일입니다.

예:

- 고객이 30일 이내에 시계를 구입할 가능성이 있는지 여부를 예측 해야 합니다. 지난 60일 동안 일부 웹 활동이 있는 사용자에게 점수를 매기고 싶을 수도 있습니다. 이 경우 필요한 최소 데이터 길이는 60일 + 30일입니다. 적용 가능한 인구는 60일이며 결과 기간은 30일 총 90일입니다.

- 사용자가 7일 이내에 시계를 구입할 가능성이 있는지 여부를 예측하려고 합니다. 이 경우 필요한 최소 데이터 길이는 120일 + 7일입니다. 적격 모집단 기본값은 120일이며 결과 창은 총 127일 동안 7일입니다.

- 고객이 앞으로 7일 이내에 시계를 구입할 가능성이 있는지 여부를 예측 해야 합니다. 지난 7일 동안 일부 웹 활동이 있는 사용자에게 점수를 매기고 싶은 경우도 있습니다. 이 경우 필요한 최소 데이터 길이는 30일 + 7일입니다. 적용 가능한 인구는 최소 30일이 필요하며 결과 기간은 총 37일입니다.

Customer AI는 필요한 최소 데이터 외에도 최신 데이터에서 가장 잘 작동합니다. 이 사용 사례에서는 고객 AI가 사용자의 최근 행동 데이터를 기반으로 미래에 대한 예측을 수행합니다. 즉, 더 최근의 데이터가 더 정확한 예측을 산출할 가능성이 높습니다.

### 예제 시나리오

이 섹션에서는 고객 AI 인스턴스에 대한 다양한 시나리오와 필수 및 권장 이벤트 유형을 설명합니다. 자세한 내용은 [표준 이벤트 테이블](#standard-events) 필드 그룹 및 해당 필드 경로에 대한 자세한 내용은 위에서 확인하십시오.

>[!NOTE]
>
> 필요한 이벤트 유형은 웹 사용자 활동을 명확하고 분명하게 식별하는 데 사용됩니다. 필요한 이벤트 유형의 수는 스키마의 예측 목표 및 구조에 따라 달라집니다. 특정 이벤트 유형이 필요한지 확실하지 않은 경우 CEE 스키마를 구축할 때 해당 이벤트 유형을 포함하는 것이 좋습니다. Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 스트리밍 중인 데이터에 따라 필요한 표준 이벤트를 사용할 수 있어야 합니다.

### 시나리오 1: e-commerce 소매 웹 사이트에서의 구매 전환

**예측 목표:** 웹 사이트에서 특정 의류 제품을 구매하기 위해 자격 있는 프로필의 전환 성향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 2: 미디어 스트리밍 서비스 웹 사이트에서의 구독 전환

**예측 목표:** 표준 또는 프리미엄 플랜과 같은 특정 수준의 구독을 커밋할 자격 있는 프로필에 대한 구독 전환 성향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

이 예제에서는 `order`, `checkouts`, 및 `purchases` 구독을 구매하고 해당 유형을 나타내는 데 사용됩니다.

또한 정확한 모델의 경우 [구독 데이터 유형](../../xdm/data-types/subscription.md).

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 3: 전자 상거래 소매 웹 사이트에서의 이탈

**예측 목표:** 구매 이벤트가 발생하지 않을 가능성을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 4: 전자 상거래 소매 웹 사이트에서 업셀 전환

**예측 목표:** 관련 새 제품을 구매하기 위해 특정 제품을 구매한 모집단의 구매 성향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- 검색

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 5: 온라인 뉴스 콘센트 구독 취소(이탈)

**예측 목표:** 다음 달 서비스에서 가입 해지할 대상 인구의 성향을 예측합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- webVisit
- 검색

또한 정확한 모델의 경우 [구독 데이터 유형](../../xdm/data-types/subscription.md).

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 6: 모바일 애플리케이션 시작

**예측 목표:** 다음 X일 내에 유료 모바일 애플리케이션을 시작할 대상 프로필의 성향을 예측합니다. 이는 &quot;월별 활성 사용자&quot;의 주요 성과 지표(KPI)를 예측하는 것과 비슷합니다.

**필수 표준 이벤트 유형:**

아래 나열된 이벤트 유형은 이 특정 예측 목표를 가진 최적의 고객 AI 출력에 필요합니다. 예측 목표에 따라 필수 이벤트를 제외할 수 있지만, 여러 이벤트를 제외하면 결과가 좋지 않을 수 있습니다.

- 주문
- 체크아웃
- 구매
- webVisit
- applicationClose
- applicationCrashes
- applicationFeatureUsage
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

이 예제에서는 `order`, `checkouts`, 및 `purchases` 모바일 애플리케이션을 구매해야 할 때 사용됩니다.

**추가적인 권장 표준 이벤트 유형:**

나머지 중 하나 [이벤트 유형](#standard-events) 고객 AI 인스턴스를 구성하는 동안 목표 및 적격 모집단 복잡성에 따라 가 필요할 수 있습니다. 특정 데이터 유형에 사용할 수 있는 경우 이 데이터가 스키마에 포함되는 것이 좋습니다.

### 시나리오 7: 실현된 트레이트(Adobe Audience Manager)

**예측 목표:** 실현될 몇 가지 트레이트의 성향을 예측합니다.

**필수 표준 이벤트 유형:**

Adobe Audience Manager의 트레이트를 사용하려면 [Audience Manager 원본 커넥터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). 소스 커넥터는 적절한 필드 그룹이 있는 스키마를 자동으로 만듭니다. 고객 AI에서 사용할 수 있도록 스키마에 대한 추가 이벤트 유형을 수동으로 추가할 필요는 없습니다.

새 고객 AI 인스턴스를 구성하는 경우 `audienceName` 및 `audienceID` 목표를 정의하는 동안 점수를 얻기 위해 특정 트레이트를 선택하는 데 사용할 수 있습니다.

## 고객 AI 출력 데이터

Customer AI는 대상으로 간주되는 개별 프로필에 대해 몇 가지 속성을 생성합니다. 제공된 항목을 기반으로 점수(출력)를 사용하는 두 가지 방법이 있습니다. 실시간 고객 프로필 사용 데이터 세트가 있는 경우 [세그먼트 빌더](../../segmentation/ui/segment-builder.md). 프로필 사용 데이터 세트가 없는 경우 다음을 수행할 수 있습니다 [고객 AI 출력 다운로드](./user-guide/download-scores.md) 데이터 레이크에서 사용할 수 있는 데이터 집합입니다.

에서 출력 데이터 세트를 찾을 수 있습니다 **데이터 세트** Platform에서 사용할 수 있습니다. 모든 Customer AI 출력 데이터 세트는 이름으로 시작합니다 **Customer AI 점수 - Name_of_app**. 마찬가지로 모든 Customer AI 출력 스키마는 이름으로 시작됩니다 **Customer AI 스키마 - Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> 출력 값은 세그먼트를 만들고 정의하는 데 사용할 수 있는 실시간 고객 프로필에서 사용합니다.

아래 표에서는 Customer AI 출력에 있는 다양한 속성에 대해 설명합니다.

| 속성 | 설명 |
| ----- | ----------- |
| 점수 | 고객이 정의된 기간 내에 예측 목표를 달성할 상대적 가능성입니다. 이 값은 전체 모집단과 비교하여 확률 백분율로 간주되지 않고, 개인의 가능성이 높습니다. 이 점수는 0부터 100까지입니다. |
| 확률 | 이 속성은 정의된 기간 내에 예측 목표를 달성하기 위한 프로필의 실제 확률입니다. 여러 목표 간의 출력을 비교할 때에는 백분위수 또는 점수에 대한 확률을 고려하는 것이 좋습니다. 확률은 자주 발생하지 않는 이벤트의 경우 낮은 쪽에 있는 경향이 있으므로 자격을 갖춘 모집단에서 평균 확률을 결정할 때 항상 사용해야 합니다. 0과 1 사이의 확률 범위에 대한 값입니다. |
| 백분위수 | 이 값은 유사한 점수가 있는 다른 프로필과 상대적인 프로필 성능에 대한 정보를 제공합니다. 예를 들어 이탈 시 백분위수 등급이 99인 프로필은 점수가 매겨진 다른 모든 프로필의 99%와 비교하여 대량 교체가 발생할 위험이 높다는 것을 나타냅니다. 백분위수 범위는 1부터 100까지입니다. |
| 성향 유형 | 선택한 성향 유형입니다. |
| 점수 날짜 | 점수가 발생한 날짜입니다. |
| 영향력 있는 요소 | 프로필의 전환 또는 이탈이 예상되는 이유에 대한 예측된 이유입니다. 요소는 다음 속성으로 구성됩니다.<ul><li>코드: 프로필의 예측된 점수에 긍정적인 영향을 주는 프로필 또는 행동 속성입니다. </li><li>값: 프로필 또는 동작 속성의 값입니다.</li><li>중요도: 예측된 점수(낮음, 중간, 높음)에 있는 프로필 또는 동작 속성의 가중치를 나타냅니다</li></ul> |

>[!NOTE]
>
> - 고객 AI는 추가 교육 및 점수 책정을 위해 업데이트된 데이터만 사용합니다. 마찬가지로, 데이터 삭제를 요청하면 Customer AI는 삭제된 데이터를 사용하지 않습니다.
> - 고객 AI는 플랫폼 데이터 세트를 활용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하려면 브랜드는 Platform Privacy Service을 사용하여 소비자 액세스 및 삭제 요청을 제출하여 데이터 레이크, Identity Service 및 실시간 고객 프로필에서 데이터를 제거해야 합니다.
> - 모델의 입출력 작업에 사용하는 모든 데이터 세트는 플랫폼 지침을 따릅니다. Platform 데이터 암호화는 전송 중인 데이터를 위해 적용됩니다. 자세한 내용은 설명서 를 참조하십시오 [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md)


## 다음 단계 {#next-steps}

데이터를 준비하고 모든 자격 증명 및 스키마를 준비한 후에는 [고객 AI 인스턴스 구성](./user-guide/configure.md) 안내서를 따라 시작합니다. 이 안내서에서는 Customer AI에 대한 인스턴스를 만드는 과정을 안내합니다.




