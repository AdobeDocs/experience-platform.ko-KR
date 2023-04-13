---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;고객 ai 입력;고객 ai 출력; 데이터 요구 사항
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 고객 AI의 데이터 요구 사항
topic-legacy: Getting started
description: Customer AI에서 활용하는 필수 이벤트, 입력 및 출력에 대해 자세히 알아보십시오.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# 고객 AI의 입출력

다음 문서에서는 Customer AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력에 대해 설명합니다.

## 시작하기 {#getting-started}

다음은 고객 AI에서 개인화된 마케팅을 위한 성향 모델을 만들고 타겟 대상을 식별하는 단계입니다.

1. 개요 사용 사례: 성향 모델은 개인화된 마케팅을 위한 타겟 대상을 식별하는 데 어떻게 도움이 됩니까? 목표를 달성하기 위한 비즈니스 목표 및 대응 전략은 무엇입니까? 성향 모델링이 이 프로세스에 어떤 영향을 줄 수 있습니까?

2. 사용 사례 우선 순위 지정: 이 사업의 최우선 순위는 어느 것입니까?

3. Customer AI에서 모델 구축: 이거 보세요 [빠른 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) 그리고 [UI 안내서](../customer-ai/user-guide/configure.md) 모델을 만드는 단계별 프로세스입니다.

4. [세그먼트 작성](../customer-ai/user-guide/create-segment.md) 모델 결과 사용.

5. 이러한 세그먼트를 기반으로 타겟팅된 비즈니스 작업을 수행합니다. 결과를 모니터링하고 작업을 반복하여 개선합니다.

다음은 첫 번째 모델에 대한 구성 예입니다.  이 문서에 내장된 예제 모델은 Customer AI 모델을 사용하여 향후 30일 이내에 소매업체 대상으로 전환할 사용자를 예측합니다. 입력 데이터 세트는 Adobe Analytics 데이터 세트입니다.

| 단계.  | 정의 | 예 |
| ---- | ------ | ------- |
| 설정 | 모델에 대한 기본 정보를 지정합니다. | **이름**: 연필 구매 성향 모델 <br> **모델 유형**: 전환 |
| 데이터 선택 | 모델을 만드는 데 사용되는 데이터 세트를 지정합니다. | **데이터 집합**: Adobe Analytics 데이터 세트 <br> **ID**: 각 데이터 세트에 대한 ID 열이 공통 ID로 설정되어 있는지 확인합니다. |
| 목표 정의 | 목표, 적격 모집단, 사용자 지정 이벤트 및 프로필 속성을 정의합니다. | **예측 목표**: 선택 `commerce.purchases.value` 연필과 같음 <br> **결과 창**: 30일. |
| 옵션 설정 | 모델 새로 고침에 대한 일정을 설정하고 프로파일에 대한 점수를 사용으로 설정합니다 | **예약**: 주별 <br> **프로필에 사용**: 모델 출력을 세그멘테이션에 사용하려면 이 기능을 활성화해야 합니다. |

## 데이터 개요 {#data-overview}

다음 섹션에서는 Customer AI에서 사용되는 다양한 필수 이벤트, 입력 및 출력에 대해 설명합니다.

고객 AI는 다음 데이터 세트를 분석하여 이탈(고객이 제품 사용을 중단할 가능성이 있는 경우) 또는 전환(고객이 구매 가능성이 있는 경우) 성향 점수를 예측합니다.

- 를 사용하여 Adobe Analytics 데이터 [Analytics 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 를 사용하여 Adobe Audience Manager 데이터 [Audience Manager 원본 커넥터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [경험 이벤트 데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [소비자 경험 이벤트 데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

각 데이터 세트가 ECID와 같은 동일한 ID 유형(네임스페이스)을 공유하는 경우 다른 소스에서 여러 데이터 세트를 추가할 수 있습니다. 여러 데이터 세트 추가에 대한 자세한 내용은 [Customer AI 사용 안내서](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>소스 커넥터에서 데이터를 채우는 데 최대 4주가 소요됩니다. 최근에 커넥터를 설정하는 경우 데이터 세트에 고객 AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 다음 문서를 검토하십시오 [내역 데이터](#data-requirements) 예측 목표에 충분한 데이터가 있는지 확인하는 섹션을 참조하십시오.

다음 표에서는 이 문서에서 사용되는 몇 가지 일반적인 용어에 대해 설명합니다.

| 용어 | 정의 |
| --- | --- |
| [XDM(경험 데이터 모델)](../../xdm/home.md) | XDM은 Adobe Experience Platform에서 제공하는 Adobe Experience Cloud이 올바른 사람에게 올바른 메시지를 적시에 적절한 채널에 전달할 수 있도록 하는 기본 프레임워크입니다. Platform은 XDM 시스템을 사용하여 특정 방식으로 데이터를 구성하므로 Platform 서비스에 보다 쉽게 사용할 수 있습니다. |
| [XDM 스키마](../../xdm/schema/composition.md) | Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. 데이터를 Platform에 수집하려면 먼저 데이터 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제한을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 XDM 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. |
| [XDM 클래스](../../xdm/schema/field-constraints.md) | 모든 XDM 스키마에서는 다음과 같이 분류할 수 있는 데이터를 설명합니다 `Experience Event`. 스키마의 데이터 동작은 처음 만들 때 스키마에 할당된 스키마 클래스에 의해 정의됩니다. XDM 클래스는 특정 데이터 동작을 나타내려면 스키마에 포함해야 하는 가장 작은 수의 속성을 설명합니다. |
| [필드 그룹](../../xdm/schema/composition.md) | 스키마에 필드를 하나 이상 정의하는 구성 요소입니다. 필드 그룹은 해당 필드가 스키마 계층에 표시되는 방식을 적용하므로 포함된 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 해당 필드별로 식별되는 특정 클래스와 호환됩니다 `meta:intendedToExtend` 속성을 사용합니다. |
| [데이터 유형](../../xdm/schema/composition.md) | 스키마에 대해 하나 이상의 필드를 제공할 수 있는 구성 요소입니다. 그러나 필드 그룹과 달리 데이터 형식은 특정 클래스에 한정되지 않습니다. 따라서 데이터 형식을 보다 유연하게 사용하여 여러 스키마에서 다시 사용할 수 있는 공통 데이터 구조를 설명하거나 다른 클래스를 사용할 수 있습니다. 이 문서에 설명된 데이터 유형은 CEE 및 Adobe Analytics 스키마에서 모두 지원됩니다. |
| [실시간 고객 프로필](../../profile/home.md) | 실시간 고객 프로필은 타겟팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계되는 데이터와, Experience Platform에 사용하는 시스템에서 발생한 개별 이벤트와 관련된 실행 가능한 타임스탬프 계정이 포함되어 있습니다. |

## 고객 AI 입력 데이터 {#customer-ai-input-data}

Adobe Analytics 및 Adobe Audience Manager과 같은 입력 데이터 세트의 경우, 각 소스 커넥터는 연결 프로세스 중에 기본적으로 이러한 표준 필드 그룹(상거래, 웹, 애플리케이션 및 검색)에 있는 이벤트를 직접 매핑합니다. 아래 표는 고객 AI에 대한 기본 표준 필드 그룹의 이벤트 필드를 보여줍니다.

Adobe Analytics 데이터 또는 Audience Manager 데이터 매핑에 대한 자세한 내용은 Analytics 필드 매핑 또는 Audience Manager을 참조하십시오 [필드 매핑 안내서](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

위의 커넥터 중 하나를 통해 채워지지 않는 입력 데이터 세트에 대해 Experience Event 또는 소비자 Experience 이벤트 XDM 스키마를 사용할 수 있습니다. 스키마 만들기 프로세스 중에 추가 XDM 필드 그룹을 추가할 수 있습니다. 필드 그룹은 표준 필드 그룹 또는 플랫폼의 데이터 표현과 일치하는 사용자 지정 필드 그룹과 같은 Adobe에서 제공할 수 있습니다.

>[!IMPORTANT]
>
>데이터가 이러한 입력 데이터 세트에 채워지고 있는지 확인해야 합니다. 입력 데이터 세트에 표준 필드 그룹의 이벤트가 없는 경우 구성 워크플로우 동안 사용자 지정 이벤트를 추가해야 합니다. 사용자 지정 이벤트에 대한 세부 사항을 참조하십시오.

### 고객 AI에서 사용하는 표준 필드 그룹 {#standard-events}

경험 이벤트는 다양한 고객 행동을 결정하는 데 사용됩니다. 데이터 구성 방식에 따라 아래 나열된 이벤트 유형은 고객의 모든 행동을 포괄하지 않을 수 있습니다. 웹 또는 다른 채널별 사용자 활동을 명확하고 분명하게 식별하는 데 필요한 데이터가 있는 필드를 결정하는 것은 여러분에게 달려 있습니다. 예측 목표에 따라 필요한 필수 필드가 변경될 수 있습니다.

>[!NOTE]
>
>Adobe Analytics 또는 Adobe Audience Manager 데이터를 사용하는 경우 데이터를 캡처하는 데 필요한 표준 이벤트를 사용하여 스키마가 자동으로 생성됩니다. 데이터를 캡처하기 위해 고유한 사용자 지정 EE 스키마를 만드는 경우 데이터를 캡처하는 데 필요한 필드 그룹을 고려해야 합니다.

Customer AI는 기본적으로 이 4개의 표준 필드 그룹의 이벤트를 사용합니다. 상거래, 웹, 애플리케이션 및 검색. 아래 나열된 표준 필드 그룹의 각 이벤트에 대한 데이터가 필요하지 않지만 특정 시나리오에는 특정 이벤트가 필요합니다. 사용 가능한 표준 필드 그룹의 이벤트가 있는 경우 스키마에 포함하는 것이 좋습니다. 예를 들어 구매 이벤트를 예측하기 위해 Customer AI 모델을 만들어야 하는 경우 상거래 및 웹 페이지 세부 사항 필드 그룹의 데이터를 가져오는 것이 유용합니다.

플랫폼 UI에서 필드 그룹을 보려면 **[!UICONTROL 스키마]** 왼쪽 레일의 탭을 선택하고 **[!UICONTROL 필드 그룹]** 탭.

| 필드 그룹 | 이벤트 유형 | XDM 필드 경로 |
| --- | --- | --- |
| [!UICONTROL 상거래 세부 사항] | 주문 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 체크아웃 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 구매 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemoval | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpen | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL 웹 세부 사항] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 애플리케이션 세부 정보] | applicationClose | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsage | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 검색 세부 사항] | 검색 | `search.keywords` |

또한 고객 AI는 구독 데이터를 사용하여 더 나은 이탈 모델을 구축할 수 있습니다. 구독 데이터는 [[!UICONTROL 구독]](../../xdm/data-types/subscription.md) 데이터 형식 형식입니다. 대부분의 필드는 선택 사항이지만 최적의 이탈 모델의 경우 다음과 같은 필드를 최대한 많은 필드에 데이터를 제공하는 것이 좋습니다. `startDate`, `endDate`, 및 기타 관련 세부 사항. 이 기능에 대한 추가 지원을 받으려면 계정 팀에 문의하십시오.

### 사용자 지정 이벤트 및 프로필 속성 추가 {#add-custom-events}

기본 [표준 이벤트 필드](#standard-events) 고객 AI에서 사용하는 경우 [사용자 지정 이벤트 구성](./user-guide/configure.md#custom-events) 를 클릭하여 모델에서 사용하는 데이터를 늘립니다.

#### 사용자 지정 이벤트를 사용해야 하는 경우

데이터 세트 선택 단계에서 선택한 데이터 세트에 데이터 세트가 포함될 때 사용자 지정 이벤트가 필요합니다 *없음* Customer AI에서 사용하는 기본 이벤트 필드 고객 AI에는 결과가 아닌 하나 이상의 사용자 동작 이벤트에 대한 정보가 필요합니다.

사용자 지정 이벤트는 다음과 같은 경우에 유용합니다.

- 모델에 도메인 지식 또는 이전 전문 지식 통합

- 예측 모델 품질 개선.

- 추가 인사이트 및 해석

사용자 지정 이벤트에 대한 가장 적합한 후보는 결과를 예측할 수 있는 도메인 지식이 포함된 데이터입니다. 사용자 지정 이벤트의 몇 가지 일반적인 예는 다음과 같습니다.

- 계정 등록

- 뉴스레터 구독

- 고객 서비스에 전화 걸기

다음은 특정 업계 사용자 지정 이벤트 예입니다.

| 업종 | 사용자 정의 이벤트 |
| --- | --- |
| 소매 | 매장 내 트랜잭션<br>클럽 카드 등록<br>클립 모바일 쿠폰. |
| 엔터테인먼트 | 구매 시즌 멤버십 <br> 비디오 스트리밍. |
| 숙박 | 레스토랑 예약 <br> 구매 충성도 포인트. |
| 여행 | 알려진 여행자 정보 구매 마일을 추가합니다. |
| 커뮤니케이션 | 계획 업그레이드/다운그레이드/취소. |

사용자 지정 이벤트는 선택하려면 사용자가 시작한 작업을 나타내야 합니다. 예를 들어 &quot;이메일 전송&quot;은 사용자가 아닌 마케터가 시작한 작업이므로 사용자 지정 이벤트로 사용해서는 안 됩니다.

### 이전 데이터

고객 AI에는 모델 교육을 위한 이전 데이터가 필요합니다. 시스템 내에 데이터가 존재하는 데 필요한 기간은 두 가지 주요 요소로 결정됩니다. 결과 창 및 적격 모집단.

기본적으로 고객 AI는 애플리케이션 구성 중에 적절한 모집단 정의가 제공되지 않는 경우 지난 45일 동안 활동이 수행되었는지 찾습니다. 또한 Customer AI에는 예측된 목표 정의를 기반으로 한 내역 데이터에서 최소 500개의 자격 증명과 500개의 미자격 이벤트(총 1000개)가 필요합니다.

다음 예에서는 필요한 최소 데이터 양을 결정하는 데 도움이 되는 간단한 수식의 사용을 보여줍니다. 최소 요구 사항보다 많은 데이터가 있는 경우 모델이 더 정확한 결과를 제공할 수 있습니다. 필요한 최소 금액보다 적은 경우 모델 교육을 위한 데이터가 충분하지 않으므로 모델이 실패합니다.

**공식**:

시스템 내에 존재하는 데이터의 최소 필수 기간을 결정하려면

- 기능을 만드는 데 필요한 최소 데이터는 30일입니다. 자격 전환 확인 기간과 30일 비교:

   - 자격 전환 확인 기간이 30일을 초과하는 경우 데이터 요구 사항 = 자격 전환 창 + 결과 창.

   - 그렇지 않으면 데이터 요구 사항 = 30일 + 결과 창.

** 적격 모집단을 정의할 조건이 두 개 이상 있는 경우 자격 전환 확인 기간은 가장 긴 조건입니다.

>[!NOTE]
>
>30은 적격 모집단에 필요한 최소 일 수입니다. 제공되지 않으면 기본값이 45일입니다.

**예**:

- 지난 60일 동안 웹 활동이 있는 고객의 경우 다음 30일 이내에 시치를 구매할지 여부를 예측해야 합니다.

   - 자격 전환 확인 기간 = 60일

   - 결과 창 = 30일

   - 데이터 필수 = 60일 + 30일 = 90일

- 사용자가 7일 이내에 시계를 구입할 가능성이 있는지 여부를 예측하려고 합니다 **사용 안 함** 명시적 적격한 모집단을 제공합니다. 이 경우 적격 모집단 기본값은 &quot;최근 45일 동안 활동이 있었던 사람&quot;이고 결과 창은 7일입니다.

   - 자격 전환 확인 기간 = 45일

   - 결과 창 = 7일

   - 데이터 필수 = 45일 + 7일 = 52일

- 지난 7일 동안 웹 활동이 있는 사용자를 위해 고객이 다음 7일 내에 시계를 구매할 것 같은지 예측하려고 합니다.

   - 자격 전환 확인 기간 = 7일

   - 기능을 만드는 데 필요한 최소 데이터 = 30일

   - 결과 창 = 7일

   - 데이터 필수 = 30일 + 7일 = 37일

Customer AI에는 시스템 내에 데이터가 존재하기 위해 최소 시간이 필요하지만 최신 데이터에서도 가장 잘 작동합니다. Customer AI는 보다 최근의 행동 데이터를 사용하여 사용자의 향후 행동을 보다 정확하게 예측할 수 있을 것입니다.

## 고객 AI 출력 데이터 {#customer-ai-output-data}

Customer AI는 대상으로 간주되는 개별 프로필에 대해 몇 가지 속성을 생성합니다. 제공된 항목을 기반으로 점수(출력)를 사용하는 두 가지 방법이 있습니다. 실시간 고객 프로필 사용 데이터 세트가 있는 경우 [세그먼트 빌더](../../segmentation/ui/segment-builder.md). 프로필 사용 데이터 세트가 없는 경우 다음을 수행할 수 있습니다 [고객 AI 출력 다운로드](./user-guide/download-scores.md) 데이터 레이크에서 사용할 수 있는 데이터 집합입니다.

플랫폼에서 출력 데이터 세트를 찾을 수 있습니다 **데이터 세트** 작업 공간. 모든 Customer AI 출력 데이터 세트는 이름으로 시작합니다 **Customer AI 점수 - NAME_OF_APP**. 마찬가지로 모든 Customer AI 출력 스키마는 이름으로 시작됩니다 **Customer AI 스키마 - Name_of_app**.

![고객 AI에 있는 출력 데이터 세트의 이름](./images/user-guide/cai-schema-name-of-app.png)

아래 표에서는 Customer AI 출력에 있는 다양한 속성에 대해 설명합니다.

| 속성 | 설명 |
| ----- | ----------- |
| [!UICONTROL 점수] | 고객이 정의된 기간 내에 예측 목표를 달성할 상대적 가능성입니다. 이 값은 전체 모집단과 비교하여 확률 백분율로 간주되지 않고, 개인의 가능성이 높습니다. 이 점수는 0부터 100까지입니다. |
| 확률 | 이 속성은 정의된 기간 내에 예측 목표를 달성하기 위한 프로필의 실제 확률입니다. 서로 다른 목표의 출력을 비교할 때에는 백분위수 또는 점수에 대한 확률을 고려해야 합니다. 확률은 자주 발생하지 않는 이벤트의 경우 낮은 쪽에 있는 경향이 있으므로 자격을 갖춘 모집단에서 평균 확률을 결정할 때 항상 사용해야 합니다. 0과 1 사이의 확률 범위에 대한 값입니다. |
| 백분위수 | 이 값은 유사한 점수가 있는 다른 프로필과 상대적인 프로필 성능에 대한 정보를 제공합니다. 예를 들어 이탈 시 백분위수 등급이 99인 프로필은 점수가 매겨진 다른 모든 프로필의 99%와 비교하여 대량 교체가 발생할 위험이 높다는 것을 나타냅니다. 백분위수 범위는 1부터 100까지입니다. |
| 성향 유형 | 선택한 성향 유형입니다. |
| 점수 날짜 | 점수가 발생한 날짜입니다. |
| 영향력 있는 요소 | 프로필의 전환 또는 이탈이 예상되는 이유에 대해 이러한 예측이 가능합니다. 이러한 요소는 다음 속성으로 구성됩니다.<ul><li>코드: 프로필의 예측된 점수에 긍정적인 영향을 주는 프로필 또는 행동 속성입니다. </li><li>값: 프로필 또는 동작 속성의 값입니다.</li><li>중요도: 예측된 점수(낮음, 중간, 높음)에 있는 프로필 또는 동작 속성의 가중치를 나타냅니다</li></ul> |

## 다음 단계 {#next-steps}

데이터를 준비하고 모든 자격 증명과 스키마가 있는지 확인한 후에는 [고객 AI 인스턴스 구성](./user-guide/configure.md) 고객 AI 인스턴스를 만들기 위한 단계별 자습서를 안내하는 안내서입니다.