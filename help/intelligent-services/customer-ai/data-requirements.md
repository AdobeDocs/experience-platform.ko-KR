---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;고객 ai 입력;고객 ai 출력;데이터 요구 사항
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI의 데이터 요구 사항
topic-legacy: Getting started
description: 고객 AI가 활용하는 필수 이벤트, 입력 및 출력에 대해 자세히 알아봅니다.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 3%

---


# 고객 AI의 입력 및 출력

다음 문서에서는 Customer AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력에 대해 간략하게 설명합니다.

## 시작하기 {#getting-started}

다음은 고객 AI에서 개인화된 마케팅을 위해 성향 모델을 구축하고 타겟 대상을 식별하는 단계입니다.

1. 개요 사용 사례: 성향 모델이 개인화된 마케팅의 대상 고객을 식별하는 데 어떻게 도움이 됩니까? 목표를 달성하기 위한 비즈니스 목표와 이에 상응하는 전술은 무엇입니까? 성향 모델링은 이 프로세스에서 어디에 적합할 수 있습니까?

2. 사용 사례 우선 순위 지정: 비즈니스에 가장 높은 우선 순위는 무엇입니까?

3. Customer AI에서 모델 구축: 이 항목을 살펴보십시오. [빠른 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) 및 다음 참조 [UI 안내서](../customer-ai/user-guide/configure.md) 모델을 만드는 단계별 프로세스입니다.

4. [세그먼트 작성](../customer-ai/user-guide/create-segment.md) 모델 결과를 사용합니다.

5. 이러한 세그먼트를 기반으로 타기팅된 비즈니스 작업을 수행합니다. 결과를 모니터링하고 개선 작업을 반복합니다.

다음은 첫 번째 모델에 대한 예제 구성입니다.  이 문서에 내장된 예제 모델은 고객 AI 모델을 사용하여 향후 30일 이내에 소매업으로 전환할 가능성이 있는 사용자를 예측합니다. 입력 데이터 세트는 Adobe Analytics 데이터 세트입니다.

| 단계.  | 정의 | 예 |
| ---- | ------ | ------- |
| 설정 | 모델에 대한 기본 정보를 지정합니다. | **이름**: 연필 구매 성향 모델 <br> **모델 유형**: 전환 |
| 데이터 선택 | 모델을 만드는 데 사용되는 데이터 세트를 지정합니다. | **데이터 세트**: Adobe Analytics 데이터 세트 <br> **신원**: 각 데이터 세트의 ID 열이 공통 ID로 설정되었는지 확인합니다. |
| 목표 정의 | 목표, 적격 모집단, 사용자 지정 이벤트 및 프로필 속성을 정의합니다. | **예측 목표**: 선택 `commerce.purchases.value` 연필과 같음 <br> **결과 창**: 30일. |
| 옵션 설정 | 모델 새로 고침 일정 설정 및 프로필에 대한 점수 활성화 | **예약**: 매주 <br> **프로필 활성화**: 세분화에 사용할 모델 출력에 대해 활성화해야 합니다. |

## 데이터 개요 {#data-overview}

다음 섹션에서는 고객 AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력에 대해 설명합니다.

고객 AI는 다음 데이터 세트를 분석하여 이탈(고객이 제품 사용을 중단할 가능성이 있는 경우) 또는 전환(고객이 구매할 가능성이 있는 경우) 성향 점수를 예측합니다.

- 를 사용하는 Adobe Analytics 데이터 [Analytics 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 를 사용하는 Adobe Audience Manager 데이터 [Audience Manager 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [경험 이벤트 데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [고객 경험 이벤트 데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

각 데이터 세트가 ECID와 같은 동일한 ID 유형(네임스페이스)을 공유하는 경우 서로 다른 소스에서 여러 데이터 세트를 추가할 수 있습니다. 여러 데이터 세트 추가에 대한 자세한 내용은 [Customer AI 사용 안내서](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>소스 커넥터는 데이터를 채우는 데 최대 4주가 소요됩니다. 최근 커넥터를 설정하는 경우 데이터 세트에 Customer AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 다음을 검토하십시오. [내역 데이터](#data-requirements) 예측 목표에 적합한 데이터가 충분한지 확인하는 섹션입니다.

다음 표에서는 이 문서에 사용되는 몇 가지 일반적인 용어를 간략하게 설명합니다.

| 용어 | 정의 |
| --- | --- |
| [경험 데이터 모델 (XDM)](../../xdm/home.md) | XDM은 Adobe Experience Platform에서 제공하는 Adobe Experience Cloud이 정확한 순간에 정확한 메시지를 적합한 사람에게 전달할 수 있는 기본 프레임워크입니다. Platform은 XDM 시스템을 사용하여 플랫폼 서비스에 보다 쉽게 사용할 수 있도록 데이터를 특정 방식으로 구성합니다. |
| [XDM 스키마](../../xdm/schema/composition.md) | Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. 데이터를 Platform에 수집하려면 먼저 데이터의 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제약 조건을 제공하는 스키마를 구성해야 합니다. 스키마는 기본 XDM 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. |
| [XDM 클래스](../../xdm/schema/field-constraints.md) | 모든 XDM 스키마는 분류할 수 있는 데이터를 설명합니다. `Experience Event`. 스키마의 데이터 비헤이비어는 스키마가 처음 생성될 때 스키마에 할당된 스키마의 클래스에 의해 정의됩니다. XDM 클래스는 특정 데이터 동작을 나타내기 위해 스키마에 포함해야 하는 최소 속성 수를 설명합니다. |
| [필드 그룹](../../xdm/schema/composition.md) | 스키마에서 하나 이상의 필드를 정의하는 구성 요소입니다. 필드 그룹은 필드가 스키마의 계층 구조에 표시되는 방식을 적용하므로 포함되는 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 클래스에서 식별되는 특정 클래스와만 호환됩니다. `meta:intendedToExtend` 특성. |
| [데이터 유형](../../xdm/schema/composition.md) | 스키마에 하나 이상의 필드를 제공할 수도 있는 구성 요소입니다. 그러나 필드 그룹과 달리 데이터 유형은 특정 클래스에 제한되지 않습니다. 이렇게 하면 데이터 형식이 잠재적으로 다른 클래스를 사용하는 여러 스키마에서 재사용 가능한 일반적인 데이터 구조를 설명하는 보다 유연한 옵션이 됩니다. 이 문서에 설명된 데이터 유형은 CEE 및 Adobe Analytics 스키마 모두에서 지원됩니다. |
| [실시간 고객 프로필](../../profile/home.md) | 실시간 고객 프로필은 타깃팅되고 개인화된 경험 관리를 위한 중앙 집중식 고객 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계된 데이터와, Experience Platform 시 사용하는 시스템에서 발생한 개별 이벤트와 관련된 실행 가능한 타임스탬프가 지정된 계정이 포함됩니다. |

## 고객 AI 입력 데이터 {#customer-ai-input-data}

Adobe Analytics 및 Adobe Audience Manager과 같은 입력 데이터 세트의 경우 각 소스 커넥터가 연결 프로세스 중에 기본적으로 이러한 표준 필드 그룹(Commerce, Web, Application 및 Search)의 이벤트를 직접 매핑합니다. 아래 표는 고객 AI에 대한 기본 표준 필드 그룹의 이벤트 필드를 보여줍니다.

Adobe Analytics 데이터 또는 Audience Manager 데이터 매핑에 대한 자세한 내용은 Analytics 필드 매핑 또는 Audience Manager 을 참조하십시오 [필드 매핑 안내서](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

위의 커넥터 중 하나를 통해 채워지지 않은 입력 데이터 세트에 대해 경험 이벤트 또는 소비자 경험 이벤트 XDM 스키마를 사용할 수 있습니다. 스키마 생성 프로세스 중에 추가 XDM 필드 그룹을 추가할 수 있습니다. 필드 그룹은 표준 필드 그룹 또는 사용자 정의 필드 그룹과 같은 Adobe에 의해 제공될 수 있으며, 이는 플랫폼의 데이터 표현과 일치합니다.

>[!IMPORTANT]
>
>데이터가 이러한 입력 데이터 세트에 채워져 있는지 확인해야 합니다. 입력 데이터 세트에 표준 필드 그룹의 이벤트가 없는 경우 구성 워크플로우 중에 사용자 지정 이벤트를 추가해야 합니다. 사용자 지정 이벤트에 대한 세부 사항을 참조하십시오.

### 고객 AI에서 사용하는 표준 필드 그룹 {#standard-events}

경험 이벤트는 다양한 고객 행동을 결정하는 데 사용됩니다. 데이터의 구성 방식에 따라 아래에 나열된 이벤트 유형이 고객의 모든 행동을 포괄하는 것은 아닐 수 있습니다. 웹 또는 기타 채널별 사용자 활동을 명확하고 명확하게 식별하는 데 필요한 데이터가 있는 필드는 사용자가 결정합니다. 예측 목표에 따라 필요한 필수 필드가 변경될 수 있습니다.

>[!NOTE]
>
>Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 데이터를 캡처하는 데 필요한 표준 이벤트를 사용하여 스키마가 자동으로 생성됩니다. 데이터를 캡처하기 위해 자신만의 사용자 지정 EE 스키마를 만드는 경우 데이터를 캡처하는 데 필요한 필드 그룹을 고려해야 합니다.

고객 AI는 기본적으로 상거래, 웹, 애플리케이션, 검색 등 네 가지 표준 필드 그룹의 이벤트를 사용합니다. 아래 나열된 표준 필드 그룹의 각 이벤트에 대한 데이터가 있을 필요는 없지만 특정 이벤트는 특정 시나리오에 필요합니다. 사용 가능한 표준 필드 그룹에 이벤트가 있는 경우 스키마에 포함하는 것이 좋습니다. 예를 들어 구매 이벤트를 예측하기 위한 고객 AI 모델을 생성하려는 경우 상거래 및 웹 페이지 세부 정보 필드 그룹의 데이터를 보유한 것이 유용합니다.

Platform UI에서 필드 그룹을 보려면 **[!UICONTROL 스키마]** 왼쪽 레일에서 탭을 클릭한 다음 을 선택합니다. **[!UICONTROL 필드 그룹]** 탭.

| 필드 그룹 | 이벤트 유형 | XDM 필드 패스 |
| --- | --- | --- |
| [!UICONTROL 상거래 세부 정보] | 주문 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | 제품 목록 보기 수 | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 체크아웃 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 구매 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpen | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | 제품 보기 | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL 웹 세부 정보] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 애플리케이션 세부 정보] | applicationClose | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsage | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | application우선 실행 | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunch | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrade | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 세부 정보 검색] | 검색 | `search.keywords` |

또한 고객 AI는 구독 데이터를 사용하여 더 나은 이탈 모델을 구축할 수 있습니다. 을(를) 사용하는 각 프로필에 구독 데이터가 필요합니다. [[!UICONTROL 구독]](../../xdm/data-types/subscription.md) 데이터 유형 형식입니다. 대부분의 필드는 선택 사항이지만 최적의 이탈 모델의 경우 다음과 같이 가능한 한 많은 필드에 대한 데이터를 제공하는 것이 좋습니다. `startDate`, `endDate`및 기타 관련 세부 정보. 이 기능에 대한 추가 지원은 계정 팀에 문의하십시오.

### 사용자 지정 이벤트 및 프로필 속성 추가 {#add-custom-events}

기본값 외에 포함하려는 정보가 있는 경우 [표준 이벤트 필드](#standard-events) 고객 AI에서 사용하는 [사용자 지정 이벤트 구성](./user-guide/configure.md#custom-events) 를 클릭하여 모델에서 사용하는 데이터를 증가시킵니다.

#### 사용자 지정 이벤트 사용 시기

사용자 지정 이벤트는 데이터 세트 선택 단계에서 선택한 데이터 세트에 가 포함된 경우 필요합니다 *없음* 고객 AI에서 사용하는 기본 이벤트 필드. 고객 AI에는 결과 이외의 사용자 행동 이벤트에 대한 정보가 하나 이상 필요합니다.

사용자 지정 이벤트는 다음 작업에 유용합니다.

- 도메인 지식 또는 사전 전문 지식을 모델에 통합.

- 예측 모델 품질을 개선합니다.

- 추가적인 통찰력과 해석 확보.

사용자 지정 이벤트에 대한 최상의 후보는 결과를 예측할 수 있는 도메인 지식이 포함된 데이터입니다. 사용자 지정 이벤트의 몇 가지 일반적인 예는 다음과 같습니다.

- 계정 등록

- 뉴스레터 구독

- 고객 서비스에 전화 걸기

다음은 일련의 업종별 사용자 지정 이벤트 예입니다.

| 업종 | 사용자 정의 이벤트 |
| --- | --- |
| 소매 | 매장 내 거래<br>클럽 카드 등록<br>클립 모바일 쿠폰. |
| 엔터테인먼트 | 구매 시즌 멤버십 <br> 비디오를 스트리밍합니다. |
| 접대 | 레스토랑 예약 <br> 충성도 포인트를 구매합니다. |
| 여행 | 알려진 여행자 정보 구매 마일을 추가합니다. |
| 커뮤니케이션 | 업그레이드/다운그레이드/취소 플랜입니다. |

사용자 지정 이벤트를 선택하려면 사용자가 시작한 작업을 표시해야 합니다. 예를 들어 &quot;이메일 보내기&quot;는 사용자가 아닌 마케터가 시작한 작업이므로 사용자 지정 이벤트로 사용해서는 안 됩니다.

### 이전 데이터

고객 AI는 모델 교육을 위해 이전 데이터가 필요합니다. 시스템 내에 데이터가 존재하는 데 필요한 기간은 결과 창과 적격 모집단의 두 가지 주요 요소에 의해 결정됩니다.

기본적으로 고객 AI는 애플리케이션 구성 중에 적격한 모집단 정의가 제공되지 않으면 지난 45일 동안 활동이 있었던 사용자를 찾습니다. 또한 고객 AI는 예측된 목표 정의를 기반으로 내역 데이터에서 최소 500개의 자격 획득 이벤트와 500개의 비자격 이벤트(총 1000개)를 필요로 합니다.

다음 예제에서는 필요한 최소 데이터 양을 결정하는 데 도움이 되는 간단한 공식을 사용하는 방법을 보여 줍니다. 최소 요구 사항보다 많은 데이터가 있는 경우 모델이 더 정확한 결과를 제공할 수 있습니다. 필요한 최소 금액 미만의 데이터가 있는 경우 모델 교육을 위한 데이터가 충분하지 않으므로 모델이 실패합니다.

**공식**:

시스템 내에 존재하는 데이터의 최소 필요 기간을 결정하려면 다음 작업을 수행하십시오.

- 기능을 만드는 데 필요한 최소 데이터는 30일입니다. 적격성 전환 확인 기간을 30일과 비교:

   - 자격 전환 확인 기간이 30일보다 큰 경우 데이터 요구사항 = 자격 전환 확인 기간 + 결과 창.

   - 그렇지 않으면 데이터 요구사항 = 30일 + 결과 창.

** 적격 모집단을 정의하는 조건이 두 개 이상인 경우 적격성 전환 확인 기간이 가장 깁니다.

>[!NOTE]
>
>30은 적격 모집단에 필요한 최소 일 수입니다. 이 값을 제공하지 않는 경우 기본값은 45일입니다.

**예**:

- 지난 60일 동안 웹 활동이 있었던 고객을 위해 고객이 향후 30일 이내에 시계를 구매할 가능성이 있는지 예측하려고 합니다.

   - 자격 전환 확인 기간 = 60일

   - 결과 창 = 30일

   - 필요한 데이터 = 60일 + 30일 = 90일

- 사용자가 앞으로 7일 이내에 시계를 구매할 가능성이 있는지 예측하려고 합니다 **없이** 명시적 적격 모집단을 제공합니다. 이 경우, 적격 모집단은 &quot;최근 45일 동안 활동이 있었던 사람&quot;으로 기본 설정되고 결과 창은 7일입니다.

   - 자격 전환 확인 기간 = 45일

   - 결과 창 = 7일

   - 필요한 데이터 = 45일 + 7일 = 52일

- 지난 7일 동안 웹 활동이 있었던 고객을 위해 고객이 향후 7일 이내에 시계를 구매할 가능성이 있는지 예측하려고 합니다.

   - 자격 전환 확인 기간 = 7일

   - 기능을 만드는 데 필요한 최소 데이터 = 30일

   - 결과 창 = 7일

   - 필요한 데이터 = 30일 + 7일 = 37일

고객 AI는 시스템 내에 데이터가 존재하기 위해 최소 기간이 필요하지만 최근 데이터에서도 가장 잘 작동합니다. 고객 AI는 보다 최근의 행동 데이터를 사용하여 사용자의 미래 행동에 대한 보다 정확한 예측을 제공할 수 있습니다.

## 고객 AI 출력 데이터 {#customer-ai-output-data}

고객 AI는 자격이 있는 것으로 간주되는 개별 프로필에 대해 여러 속성을 생성합니다. 프로비저닝된 내용을 기반으로 점수(출력)를 소비하는 두 가지 방법이 있습니다. 실시간 고객 프로필이 활성화된 데이터 세트가 있는 경우 [세그먼트 빌더](../../segmentation/ui/segment-builder.md). 프로필이 활성화된 데이터 세트가 없는 경우 다음을 수행할 수 있습니다 [고객 AI 출력 다운로드](./user-guide/download-scores.md) 데이터 레이크에서 데이터 세트를 사용할 수 있습니다.

플랫폼에서 출력 데이터 세트를 찾을 수 있습니다. **데이터 세트** 작업 영역. 모든 Customer AI 출력 데이터 세트는 이름으로 시작합니다 **Customer AI 스코어 - NAME_OF_APP**. 마찬가지로 모든 Customer AI 출력 스키마는 이름으로 시작합니다. **고객 AI 스키마 - Name_of_app**.

![Customer AI의 출력 데이터 세트 이름](./images/user-guide/cai-schema-name-of-app.png)

아래 표는 고객 AI의 출력에 있는 다양한 속성에 대해 설명합니다.

| 속성 | 설명 |
| ----- | ----------- |
| [!UICONTROL 점수] | 고객이 정의된 시간대 내에 예측된 목표를 달성할 상대적 가능성. 이 값은 확률 백분율이 아니라 전체 모집단과 비교한 개인의 가능성으로 다루어야 한다. 이 점수의 범위는 0부터 100까지입니다. |
| 가능성 | 이 속성은 정의된 시간대 내에 예측된 목표를 달성하기 위한 프로파일의 실제 확률이다. 서로 다른 목표에 대한 출력을 비교할 때는 백분위수나 점수에 대한 확률을 고려하는 것이 좋습니다. 확률은 빈번하게 발생하지 않는 사건에 대해 낮은 편인 경향이 있으므로, 적격 모집단에서 평균 확률을 결정할 때 항상 사용해야 합니다. 확률 값의 범위는 0과 1 사이입니다. |
| 백분위수 | 이 값은 점수가 비슷한 다른 프로필과 관련된 프로필의 성능에 대한 정보를 제공합니다. 예를 들어, 이탈에 대한 백분위수 순위가 99인 프로필은 점수가 매겨진 다른 모든 프로필의 99%와 비교하여 이탈의 위험이 더 높음을 나타냅니다. 백분위수의 범위는 1부터 100까지입니다. |
| 성향 유형 | 선택한 성향 유형. |
| 스코어 날짜 | 채점이 발생한 날짜. |
| 영향력 있는 요인 | 이는 프로필이 전환되거나 이탈할 가능성이 높은 이유에 대한 예측되는 이유입니다. 이러한 요소는 다음 속성으로 구성됩니다.<ul><li>코드: 프로필의 예측된 점수에 긍정적인 영향을 주는 프로필 또는 행동 속성. </li><li>값: 프로필 또는 동작 속성의 값입니다.</li><li>중요도: 예측된 점수(낮음, 중간, 높음)에 대한 프로필 또는 행동 속성의 가중치를 나타냅니다.</li></ul> |

## 다음 단계 {#next-steps}

데이터를 준비하고 모든 자격 증명 및 스키마가 제자리에 있는지 확인한 후 [Customer AI 인스턴스 구성](./user-guide/configure.md) 안내서에서는 고객 AI 인스턴스를 만드는 단계별 자습서를 안내합니다.