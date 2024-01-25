---
title: 데이터 관리 라이선스 권한 부여 우수 사례
description: Adobe Experience Platform을 사용하여 라이선스 권한을 보다 효율적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대해 알아봅니다.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2264'
ht-degree: 2%

---

# 데이터 관리 라이선스 권한 부여 모범 사례

Adobe Experience Platform은 데이터를 강력한 고객 프로필로 변환하여 실시간으로 업데이트하고 AI 기반 인사이트를 사용하여 모든 채널에 적합한 경험을 제공할 수 있는 개방형 시스템입니다. 다양한 유형, 볼륨 및 기록의 데이터를 수신하여 소스를 사용하여 Experience Platform 한 다음 해당 데이터를 입력하여 세그멘테이션 및 개인화부터 분석 및 머신 러닝에 이르기까지 다양한 사용 사례를 제공할 수 있습니다.

Platform은 만들 수 있는 프로필 수와 가져올 수 있는 데이터 양을 설정하는 라이선스를 제공합니다. 소스, 볼륨 또는 데이터 내역을 가져올 수 있는 용량을 고려할 때 데이터 볼륨이 증가하면 라이선스 권한을 초과할 수 있습니다.

이 문서에서는 Adobe Experience Platform을 사용하여 라이선스 권한을 보다 효과적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대한 개요를 설명합니다.

## Adobe Experience Platform 데이터 스토리지 이해

Experience Platform은 주로 두 개의 데이터 저장소인 [!DNL data lake] 프로필 스토어.

다음 **[!DNL data lake]** 주로 다음과 같은 용도로 사용됩니다.

* Experience Platform에 데이터를 온보딩하기 위한 준비 영역 역할을 합니다.
* 모든 Experience Platform 데이터를 위한 장기 데이터 저장소 역할을 합니다.
* 데이터 분석 및 데이터 과학과 같은 사용 사례를 활성화합니다.

다음 **프로필 저장소** 은 고객 프로필이 생성되는 곳이며 주로 다음 용도로 사용됩니다.

* 실시간 경험을 지원하는 데 사용되는 프로필의 데이터 저장소 역할을 합니다.
* 세분화, 활성화 및 개인화와 같은 사용 사례를 활성화합니다.

>[!NOTE]
>
>다음에 대한 액세스 권한: [!DNL data lake] 은 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

## 라이선스 사용 {#license-usage}

Experience Platform에 라이선스를 부여하면 SKU에 따라 달라지는 라이선스 사용 권한이 제공됩니다.

**[!DNL Addressable Audience]** - 알려진 프로필과 가명 프로필을 모두 포함하여 계약상 Experience Platform에서 허용되는 총 고객 프로필 수입니다.

**[!DNL Profile Richness]** - Experience Platform 내 프로필 데이터의 평균 크기입니다. 다음을 늘릴 수 있습니다. [!DNL Profile Richness] 풍성함을 구입하여 특권을 부여하다.

다음 [!DNL Profile Richness] 지표는 구입한 라이선스에 따라 다릅니다. 다음에 대한 계산은 두 가지가 있습니다 [!DNL Profile Richness] 사용 가능:

* 특정 시점에 Adobe Real-time Customer Data Platform 내에 저장된 모든 프로덕션 데이터(즉, 실시간 고객 프로필 및 ID 서비스)의 합을 [!DNL Addressable Audience];
* 플랫폼 내에 저장된 모든 데이터의 합계(다음을 포함하지만 이에 국한되지 않음) [!DNL data lake], 실시간 고객 프로필 및 ID 서비스), 지난 12개월 동안 (내에 저장하지 않고) Platform을 통해 스트리밍한 모든 데이터( )를 [!DNL Addressable Audience].

이러한 지표의 사용 가능 여부 및 이러한 각 지표의 특정 정의는 조직이 구입한 라이선스에 따라 다릅니다.

## 라이선스 사용 대시보드

Adobe Experience Platform UI는 Platform에 대한 조직 라이선스 관련 데이터의 스냅샷을 볼 수 있는 대시보드를 제공합니다. 대시보드의 데이터는 스냅샷이 생성된 특정 시점에 나타나는 것과 동일하게 표시됩니다. 스냅샷은 근사치도 데이터 샘플도 아니며 대시보드가 실시간으로 업데이트되지 않습니다.

자세한 내용은 다음 안내서를 참조하십시오. [platform UI에서 라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 데이터 관리 모범 사례

다음 섹션에서는 데이터를 보다 효율적으로 관리하기 위해 따라야 할 모범 사례에 대해 간략히 설명합니다.

### 데이터 이해

Adobe Experience Platform의 모든 데이터가 동일한 것은 아닙니다. 일부 데이터는 조밀하지만 값이 낮을 수 있고, 다른 데이터는 희소하지만 값이 높을 수 있습니다. 일부 데이터는 생성되자마자 가치가 떨어질 수 있지만, 다른 데이터는 몇 년이 아니더라도 몇 개월 동안 가치가 있을 수 있습니다.

데이터의 가치를 이해하는 데 고려해야 할 세 가지 차원이 있습니다.

| 차원 | 설명 | 예 |
| --- | --- | --- |
| 볼륨 | 수집된 데이터의 양과 총계를 나타냅니다. | 웹 클릭 수 - 볼륨이 높고 충실도가 보통입니다. 값이 빠르게 감소할 수 있습니다. |
| Timespan | 수집된 데이터가 계속 가치 있게 유지되는 기간을 나타냅니다. | 오프라인 구매 - 볼륨 및 정확도는 낮지만 오랜 기간 동안 유용할 수 있습니다. |
| 충실도 | 정보로 데이터가 얼마나 풍부한지 나타냅니다. | 고객 계정 - 볼륨이 낮지만 충실도가 높음. 고객의 일생 이상으로 가치 있을 수 있습니다. |

### 데이터 관리 도구 {#data-management-tools}

데이터 사용량이 라이선스 권한 제한 내에 남아 있는지 확인할 때 고려해야 할 두 가지 중앙 시나리오가 있습니다.

### 플랫폼으로 가져올 데이터

플랫폼의 하나 또는 여러 시스템으로 데이터를 수집할 수 있습니다. 즉, [!DNL data lake] 및/또는 프로필 스토어 이것은 다양한 다른 사용 사례에 대해 두 시스템 모두에 다른 데이터가 존재할 수 있음을 의미한다. 예를 들어 내역 데이터를 [!DNL data lake], 하지만 프로필 저장소에는 없습니다. 프로필 수집을 위한 데이터 세트를 활성화하여 프로필 스토어에 전송할 데이터를 선택할 수 있습니다.

>[!NOTE]
>
>다음에 대한 액세스 권한: [!DNL data lake] 은 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 보관할 데이터

데이터 수집 필터와 만료 규칙을 모두 적용하여 사용 사례에서 더 이상 사용되지 않는 데이터를 제거할 수 있습니다. 일반적으로 동작 데이터(예: Analytics 데이터)는 레코드 데이터(예: CRM 데이터)보다 훨씬 많은 스토리지를 사용합니다. 예를 들어 많은 Platform 사용자는 레코드 데이터의 프로필과 비교하여 동작 데이터만으로 채워지는 프로필의 최대 90%를 보유하고 있습니다. 따라서 행동 데이터를 관리하는 것은 라이선스 권한 내에서 규정 준수를 보장하는 데 매우 중요합니다.

라이선스 사용 권한 내에 유지하기 위해 활용할 수 있는 다양한 도구가 있습니다.

* [수집 필터](#ingestion-filters)
* [프로필 저장소](#profile-service)

### ID 서비스 및 대응 가능 대상 {#identity-service}

대응 가능 대상자는 고객 프로필의 총 수를 참조하므로 ID 그래프는 총 대응 가능 대상 권한 수에 포함되지 않습니다.

그러나 ID 그래프 제한은 ID 분할로 인해 대응 가능 대상에 영향을 줄 수 있습니다. 예를 들어 가장 오래된 ECID를 그래프에서 제거하면 ECID가 실시간 고객 프로필에 익명 프로필로 계속 존재합니다. 다음을 설정할 수 있습니다. [익명 프로필 데이터 만료](../../profile/pseudonymous-profiles.md) 이 행동을 회피하기 위해서. 자세한 내용은 [id 서비스 데이터 보호](../../identity-service/guardrails.md).

### 수집 필터 {#ingestion-filters}

수집 필터를 사용하면 사용 사례에 필요한 데이터만 가져올 수 있으며 필요하지 않은 모든 이벤트는 필터링됩니다.

| 수집 필터 | 설명 |
| --- | --- |
| Adobe Audience Manager 소스 필터링 | Adobe Audience Manager 소스 연결을 만들 때 로 가져올 세그먼트 및 트레이트를 선택하고 선택할 수 있습니다. [!DNL data lake] Audience Manager 데이터를 완전히 섭취하지 않고 실시간 고객 프로필을 확인할 수 있습니다. 다음 안내서를 참조하십시오 [Audience Manager 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 추가 정보. |
| Adobe Analytics 데이터 준비 | 다음을 사용할 수 있습니다. [!DNL Data Prep] 기능 : Analytics 소스 연결을 만들어 사용 사례에 필요하지 않은 데이터를 필터링합니다. 까지 [!DNL Data Prep]프로필에 게시해야 하는 속성/열을 정의할 수 있습니다. 데이터가 프로필에 게시되어야 하는지 또는 에만 게시되어야 하는지 여부를 플랫폼에 알리는 조건문을 제공할 수도 있습니다. [!DNL data lake]. 다음 안내서를 참조하십시오 [analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 추가 정보. |
| 프로필에 대한 데이터 세트 활성화/비활성화 지원 | 실시간 고객 프로필로 데이터를 수집하려면 프로필 스토어에서 사용할 데이터 세트를 활성화해야 합니다. 이렇게 하면 가 을(를) 추가합니다. [!DNL Addressable Audience] 및 [!DNL Profile Richness] 권한. 고객 프로필 사용 사례에 더 이상 데이터 세트가 필요하지 않으면 해당 데이터 세트의 프로필 통합을 비활성화하여 데이터가 라이센스 규정을 준수하는지 확인할 수 있습니다. 다음 안내서를 참조하십시오 [프로필에 대한 데이터 세트 활성화 및 비활성화](../../catalog/datasets/enable-for-profile.md) 추가 정보. |
| Web SDK 및 Mobile SDK 데이터 제외 | 웹 및 모바일 SDK에서 수집하는 데이터에는 자동으로 수집되는 데이터와 개발자가 명시적으로 수집하는 데이터의 두 가지 유형이 있습니다. 라이선스 준수를 보다 효율적으로 관리하려면 컨텍스트 설정을 통해 SDK의 구성에서 자동 데이터 수집을 비활성화하면 됩니다. 사용자 정의 데이터는 개발자가 제거하거나 설정할 수도 없습니다. 다음 안내서를 참조하십시오 [sdk 기본 사항 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals) 추가 정보. |
| 서버 측 전달 데이터 제외 | 서버측 전달을 사용하여 데이터를 Platform으로 전송하는 경우, 규칙 작업에서 매핑을 제거하여 모든 이벤트에서 데이터를 제외하거나 규칙에 조건을 추가하여 특정 이벤트에 대해서만 데이터가 실행되도록 전송할 데이터를 제외할 수 있습니다. 다음에서 설명서를 참조하십시오. [이벤트 및 조건](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if) )를 참조하십시오. |
| 소스 수준에서 데이터 필터링 | 연결을 만들고 Experience Platform에 대한 데이터를 수집하기 전에 논리 및 비교 연산자를 사용하여 소스에서 행 수준 데이터를 필터링할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [를 사용하여 소스에 대한 행 수준 데이터 필터링 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### 프로필 저장소 {#profile-service}

프로필 저장소는 다음 구성 요소로 구성됩니다.

| 프로필 저장소 구성 요소 | 설명 |
| --- | --- |
| 프로필 조각 | 각 고객 프로필은 여러 고객으로 구성됩니다 **프로필 조각** 병합되어 해당 고객에 대한 단일 보기가 형성되었습니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에 여러 개의 브랜드가 있습니다 **프로필 조각** 여러 데이터 세트에 표시되는 단일 고객과 관련이 있습니다. 이러한 조각이 Platform으로 수집되면 ID 그래프를 사용하여 함께 결합되어 해당 고객을 위한 단일 프로필을 만듭니다. **프로필 조각** 연결된 레코드 데이터 및/또는 시계열 데이터가 있는 id 네임스페이스를 식별자로 구성합니다. |
| 레코드 데이터(속성) | 프로필은 많은 항목으로 구성된 주제, 조직 또는 개인의 표현입니다 **속성** (또한으로 알려짐) **레코드 데이터**). 예를 들어, 제품 프로필에는 SKU 및 설명이 포함될 수 있지만, 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함됩니다. **레코드 데이터** 일반적으로 부피가 낮거나 중간 정도이지만 장기간 동안 유용합니다. |
| 시계열 데이터(비헤이비어) | **시계열 데이터** 는 사용자 동작에 대한 정보를 제공합니다. 표준 스키마 클래스 XDM(Experience Data Model)으로 표현 [!DNL ExperienceEvent], 시계열 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 시청한 비디오와 같은 이벤트를 설명할 수 있습니다. 행동의 가치는 시간이 지남에 따라 감소할 수 있습니다. |
| ID 네임스페이스(ID) | 고객 데이터가 합쳐지면에서 를 사용하여 단일 프로필로 병합됩니다. **id 네임스페이스**&#x200B;및 더 많은 정보가 사용자에 대해 알려짐에 따라 이러한 id를 함께 연결하는 기능이 제공됩니다. 다음을 참조하십시오. [id 네임스페이스 개요](../../identity-service/features/namespaces.md) 추가 정보. |

{style="table-layout:auto"}

#### 프로필 저장소 구성 보고서

프로필 저장소의 구성을 이해하는 데 도움이 되는 다양한 보고서가 있습니다. 이러한 보고서는 라이선스 사용을 보다 잘 최적화하기 위해 경험 이벤트 만료를 설정하는 방법과 위치에 대해 정보에 입각한 결정을 내리는 데 도움이 됩니다.

* **데이터 세트 중복 보고서 API**: 대응 가능 대상에게 가장 많은 영향을 주는 데이터 세트를 표시합니다. 이 보고서를 사용하여 다음 항목을 식별할 수 있습니다. [!DNL ExperienceEvent] 만료를 설정할 데이터 세트입니다. 다음 튜토리얼 참조: [데이터 세트 중복 보고서 생성](../../profile/tutorials/dataset-overlap-report.md) 추가 정보.
* **ID 중복 보고서 API**: 주소 지정 가능한 대상자에게 가장 많은 기여를 하는 ID 네임스페이스를 표시합니다. 다음 튜토리얼 참조: [id 중복 보고서 생성](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 추가 정보.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 익명 프로필 데이터 만료 {#pseudonymous-profile-expirations}

이 기능을 사용하면 프로필 스토어에서 오래된 익명 프로필을 자동으로 제거할 수 있습니다. 이 기능에 대한 자세한 내용은 [익명 프로필 데이터 만료 개요](../../profile/pseudonymous-profiles.md).

#### 경험 이벤트 만료 {#event-expirations}

이 기능을 사용하면 사용 사례에 더 이상 중요하지 않은 프로필 사용 데이터 세트에서 동작 데이터를 자동으로 제거할 수 있습니다. 의 개요 보기 [경험 이벤트 만료](../../profile/event-expirations.md) 데이터 세트에 대해 활성화되면 이 프로세스가 작동하는 방식에 대한 자세한 내용.

## 라이선스 사용 규정 준수에 대한 모범 사례 요약 {#best-practices}

다음은 라이선스 사용 권한을 더 잘 준수하도록 하기 위해 따를 수 있는 몇 가지 권장 모범 사례 목록입니다.

* 사용 [라이선스 사용 대시보드](../../dashboards/guides/license-usage.md) 고객 사용 트렌드를 추적 및 모니터링합니다. 이를 통해 발생할 수 있는 잠재적 초과 기간을 미리 확보할 수 있습니다.
* 구성 [수집 필터](#ingestion-filters) 세분화 및 개인화 사용 사례에 필요한 이벤트를 식별하여. 이를 통해 사용 사례에 필요한 중요한 이벤트만 보낼 수 있습니다.
* 다음만 있는지 확인합니다. [프로필에 대해 데이터 세트 활성화됨](#ingestion-filters) 세분화 및 개인화 사용 사례에 필요합니다.
* 구성 [경험 이벤트 만료](#event-expirations) 및 [익명 프로필 데이터 만료](#pseudonymous-profile-expirations) 웹 데이터와 같은 고주파 데이터의 경우.
* 주기적으로 다음을 확인합니다. [프로필 구성 보고서](#profile-store-composition-reports) 프로필 스토어 구성을 이해할 수 있습니다. 이를 통해 라이선스 사용 소비에 가장 많이 기여하는 데이터 소스를 이해할 수 있습니다.

## 기능 요약 및 가용성 {#feature-summary}

이 문서에 설명된 모범 사례 및 도구는 Adobe Experience Platform 내에서 라이선스 자격 사용을 더 잘 관리하는 데 도움이 됩니다. 모든 Experience Platform 고객에게 가시성과 제어 기능을 제공하는 데 도움이 되는 추가 기능이 출시되면 이 문서를 업데이트할 예정입니다.

다음 표에서는 라이선스 사용 권한을 보다 효율적으로 관리하기 위해 현재 사용 가능한 기능 목록을 간단히 설명합니다.

| 기능 | 설명 |
| --- | --- |
| [프로필에 대한 데이터 세트 활성화/비활성화](../../catalog/datasets/user-guide.md) | 실시간 고객 프로필에 데이터 세트 수집을 활성화하거나 비활성화합니다. |
| [경험 이벤트 만료](../../profile/event-expirations.md) | 프로필 활성화 데이터 세트에 수집된 모든 이벤트에 만료 시간을 적용합니다. 이 기능을 활성화하려면 Adobe 계정 팀이나 고객 지원 센터에 문의하십시오. |
| [Adobe Analytics 데이터 준비 필터](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 적용 [!DNL Kafka] 수집에서 불필요한 데이터를 제외하는 필터 |
| [Adobe Audience Manager 소스 커넥터 필터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Audience Manager 소스 연결 필터를 적용하여 불필요한 데이터를 수집에서 제외 |
| [Alloy SDK 데이터 필터](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals) | 수집에서 불필요한 데이터를 제외하려면 Alloy 필터 적용 |
| [이벤트 전달 데이터 필터](../../tags/ui/event-forwarding/overview.md) | 서버측 적용 [!DNL Kafka] 불필요한 데이터를 수집에서 제외하는 필터입니다.  다음에서 설명서를 참조하십시오. [태그 규칙](../../tags/ui/managing-resources/rules.md) 추가 정보. |
| [라이선스 사용 대시보드 UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Experience Platform을 위해 조직 라이선스 관련 데이터의 스냅숏 보기 |
| [데이터 세트 중복 보고서 API](../../profile/tutorials/dataset-overlap-report.md) | 대응 가능 대상에 가장 많이 기여하는 데이터 세트를 출력합니다. |
| [ID 중복 보고서 API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 대응 가능 대상에 가장 많은 기여를 하는 ID 네임스페이스를 출력합니다. |

{style="table-layout:auto"}
