---
keywords: Experience Platform;홈;인기 항목;데이터 관리;라이선스 자격;라이선스;우수 사례
title: 데이터 관리 라이선스 자격 모범 사례
description: Adobe Experience Platform을 사용하여 라이선스 권한을 보다 효율적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대해 알아봅니다.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 252ca6c62b6b95e3a01211c15d7361146dee5116
workflow-type: tm+mt
source-wordcount: '2130'
ht-degree: 2%

---

# 데이터 관리 라이선스 자격 모범 사례

Adobe Experience Platform은 실시간으로 업데이트되는 강력한 고객 프로필로 데이터를 변환하는 오픈 시스템입니다. 또한 AI 기반의 인사이트를 사용하여 모든 채널에서 최적의 경험을 제공할 수 있습니다. 소스를 사용하여 Experience Platform에 다양한 유형, 볼륨 및 히스토리의 데이터를 수집한 다음, 세그멘테이션 및 개인화부터 분석 및 시스템 학습에 이르는 사용 사례를 제공할 수 있습니다.

플랫폼은 만들 수 있는 프로필 수와 가져올 수 있는 데이터 양을 설정하는 라이선스를 제공합니다. 모든 소스, 볼륨 또는 데이터 기록을 가져올 수 있는 용량이 주어지면 데이터 볼륨이 확장되면 라이선스 자격을 초과할 수 있습니다.

이 문서에서는 Adobe Experience Platform을 사용하여 라이선스 권한을 보다 효과적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대한 개요를 설명합니다.

## Adobe Experience Platform 데이터 저장소 이해

Experience Platform은 주로 다음 두 개의 데이터 리포지토리로 구성됩니다. a [!DNL data lake] 및 프로필 스토어를 참조하십시오.

다음 **[!DNL data lake]** 는 주로 다음 용도로 사용됩니다.

* Experience Platform으로 데이터를 온보딩하기 위한 스테이징 영역 역할을 합니다.
* 모든 Experience Platform 데이터에 대한 장기 데이터 저장소 역할을 합니다.
* 데이터 분석 및 데이터 과학과 같은 사용 사례를 활성화합니다.

다음 **프로필 저장소** 은 고객 프로필이 생성되고 주로 다음 용도로 사용됩니다.

* 실시간 경험을 지원하는 데 사용되는 프로필에 대한 데이터 저장소 역할을 합니다.
* 세그먼테이션, 활성화 및 개인화와 같은 사용 사례를 활성화합니다.

>[!NOTE]
>
>액세스 권한 [!DNL data lake] 은 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

## 라이선스 사용 {#license-usage}

라이센스 Experience Platform 시 SKU에 따라 달라질 수 있는 라이선스 사용 자격이 제공됩니다.

**[!DNL Addressable Audience]** - 알려진 프로필과 익명의 프로필을 포함하여 Experience Platform에서 계약상으로 허용되는 총 고객 프로필 수입니다.

**[!DNL Profile Richness]** - Experience Platform에 있는 프로필 데이터의 평균 크기입니다. 사용자의 [!DNL Profile Richness] 부유한 팩을 구입하여 받을 자격.

다음 [!DNL Profile Richness] 지표는 구입한 라이센스에 따라 다릅니다. 다음 두 가지 계산이 있습니다 [!DNL Profile Richness] 사용 가능:

* 언제든지 Adobe Real-time Customer Data Platform(즉, 실시간 고객 프로필 및 ID 서비스)에 저장된 모든 프로덕션 데이터의 합계를 로 분할합니다. [!DNL Addressable Audience];
* 플랫폼 내에 저장된 모든 데이터의 합계(다음을 포함하되 이에 제한되지 않음) [!DNL data lake], 실시간 고객 프로필 및 ID 서비스 )를 설정하는 것이 좋습니다. [!DNL Addressable Audience].

이러한 지표의 가용성과 이러한 각 지표의 구체적인 정의는 조직이 구입한 라이센스에 따라 다릅니다.

## 라이선스 사용 대시보드

Adobe Experience Platform UI는 플랫폼에 대한 조직의 라이선스 관련 데이터의 스냅숏을 볼 수 있는 대시보드를 제공합니다. 대시보드의 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 스냅샷은 근사값이나 데이터 샘플이 아니며, 대시보드가 실시간으로 업데이트되지 않습니다.

자세한 내용은 [플랫폼 UI에서 라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 데이터 관리 우수 사례

다음 섹션에서는 데이터를 보다 효율적으로 관리하기 위해 따라야 할 모범 사례에 대해 설명합니다.

### 데이터 이해

Adobe Experience Platform에서 모든 데이터가 동일한 것은 아닙니다. 일부 데이터는 조밀하지만 가치가 낮은 반면, 다른 데이터는 희소하지만 가치가 높은 것입니다. 일부 데이터는 생성되는 즉시 가치를 상실하지만 다른 데이터는 몇 년이 아닌 경우 몇 개월 동안 유용할 수 있습니다.

데이터 값을 이해하는 데 고려해야 할 세 가지 차원이 있습니다.

| 차원 | 설명 | 예 |
| --- | --- | --- |
| 볼륨 | 수집된 데이터의 양과 총계를 나타냅니다. | 웹 클릭 수 - 대량 및 순차적 조정 값은 빠르게 감소할 수 있습니다. |
| 타임판 | 수집된 데이터가 계속 중요한 상태를 유지하는 시간을 나타냅니다. | 오프라인 구매 - 볼륨과 충실도를 조정하지만 장기간 동안 유용할 수 있습니다. |
| Fidelity | 데이터가 정보와 함께 얼마나 풍부한지를 나타냅니다. | 고객 계정 - 부피가 낮지만 정확도가 높습니다. 고객의 생애 이상으로 가치 있을 수 있습니다. |

### 데이터 관리 도구 {#data-management-tools}

데이터 사용이 라이선스 자격 제한 내에 유지되도록 할 때 고려해야 할 두 가지 중앙 시나리오가 있습니다.

### 플랫폼으로 가져올 데이터

Platform에서 하나 이상의 시스템으로 데이터를 수집할 수 있습니다. 즉, [!DNL data lake] 및/또는 프로필 스토어를 참조하십시오. 즉, 서로 다른 여러 사용 사례를 위해 두 시스템에 서로 다른 데이터가 있을 수 있습니다. 예를 들어 [!DNL data lake]하지만 프로필 저장소에 없습니다. 프로필 수집을 위해 데이터 세트를 활성화하여 프로필 저장소로 전송할 데이터를 선택할 수 있습니다.

>[!NOTE]
>
>액세스 권한 [!DNL data lake] 은 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 어떤 데이터를 보관해야 합니까?

데이터 수집 필터와 만료 규칙을 모두 적용하여 사용 사례에서 더 이상 사용되지 않는 데이터를 제거할 수 있습니다. 일반적으로 행동 데이터(예: Analytics 데이터)는 레코드 데이터(예: CRM 데이터)보다 훨씬 더 많은 저장소를 사용합니다. 예를 들어, 많은 Platform 사용자가 레코드 데이터와 비교하여 동작 데이터만으로 채워지는 프로필의 최대 90% 이상을 가지고 있습니다. 따라서 라이선스 권한 내에서 규정을 준수하려면 행동 데이터를 관리하는 것이 중요합니다.

라이선스 사용 권한 내에서 유지할 수 있는 다양한 도구가 있습니다.

* [수집 필터](#ingestion-filters)
* [프로필 저장소](#profile-service)

### 수집 필터 {#ingestion-filters}

수집 필터를 사용하면 사용 사례에 필요한 데이터만 가져오고 필요하지 않은 모든 이벤트를 필터링할 수 있습니다.

| 수집 필터 | 설명 |
| --- | --- |
| Adobe Audience Manager 소스 필터링 | Adobe Audience Manager 소스 연결을 만들 때 로 가져올 세그먼트와 트레이트를 선택하고 선택할 수 있습니다 [!DNL data lake] Audience Manager 데이터를 전체적으로 섭취하는 대신 실시간 고객 프로필을 사용하십시오. 다음 안내서를 참조하십시오. [Audience Manager 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 추가 정보. |
| Adobe Analytics 데이터 준비 | 다음을 사용할 수 있습니다 [!DNL Data Prep] 분석 소스 연결을 만들어 사용 사례에 필요하지 않은 데이터를 필터링할 때의 기능. 사용 [!DNL Data Prep]를 사용하면 프로필에 게시해야 하는 속성/열을 정의할 수 있습니다. 또한 데이터가 프로필에 게시되어야 하는지 아니면 단지 [!DNL data lake]. 다음 안내서를 참조하십시오. [analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 추가 정보. |
| 프로필에 대한 데이터 세트 활성화/비활성화 지원 | 실시간 고객 프로필에 데이터를 수집하려면 프로필 저장소에서 사용할 데이터 세트를 활성화해야 합니다. 이렇게 하면 가 [!DNL Addressable Audience] 및 [!DNL Profile Richness] 권한 부여. 데이터 세트가 더 이상 고객 프로필 사용 사례에 필요하지 않으면 해당 데이터 세트의 Profile 통합을 비활성화하여 데이터가 라이센스를 준수하도록 유지할 수 있습니다. 다음 안내서를 참조하십시오. [프로필에 대한 데이터 세트 활성화 및 비활성화](../../catalog/datasets/enable-for-profile.md) 추가 정보. |
| 웹 SDK 및 모바일 SDK 데이터 제외 | 웹 및 Mobile SDK에서 수집하는 데이터에는 두 가지 유형이 있습니다. 자동으로 수집된 데이터와 개발자가 명시적으로 수집하는 데이터입니다. 라이선스 호환성을 더 잘 관리하기 위해 컨텍스트 설정을 통해 SDK 구성에서 자동 데이터 수집을 비활성화할 수 있습니다. 사용자 지정 데이터는 개발자가 제거하거나 설정할 수도 없습니다. 다음 안내서를 참조하십시오. [sdk 기본 사항 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 추가 정보. |
| 서버 측 전달 데이터 제외 | 서버측 전달을 사용하여 Platform에 데이터를 보내는 경우 규칙 작업의 매핑을 제거하여 모든 이벤트에서 제외하거나 특정 이벤트에 대해서만 데이터가 실행되도록 규칙에 조건을 추가하여 어떤 데이터가 전송되는지 제외할 수 있습니다. 다음 문서를 참조하십시오. [이벤트 및 조건](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 추가 정보. |

{style="table-layout:auto"}

### 프로필 저장소 {#profile-service}

프로필 저장소는 다음 구성 요소로 구성됩니다.

| 프로필 저장소 구성 요소 | 설명 |
| --- | --- |
| 프로필 조각 | 각 고객 프로필은 여러 개로 구성됩니다 **프로필 조각** 이러한 ID가 병합되어 해당 고객에 대한 단일 뷰를 형성했습니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에 여러 개가 있습니다 **프로필 조각** 여러 데이터 세트에 나타나는 해당 단일 고객과 관련되어 있습니다. 이러한 조각을 Platform에 수집하면 ID 그래프를 사용하여 함께 결합하여 해당 고객에 대한 단일 프로필을 만듭니다. **프로필 조각** id 네임스페이스로 구성되며, 연결된 레코드 데이터 및/또는 시계열 데이터가 있습니다. |
| 레코드 데이터(속성) | 프로필은 여러 항목으로 구성된 주체, 조직 또는 개인을 나타냅니다 **속성** ( **레코드 데이터**). 예를 들어 제품 프로필에 SKU 및 설명이 포함될 수 있지만, 사람의 프로필에 이름, 성 및 이메일 주소와 같은 정보가 포함되어 있습니다. **데이터 기록** 는 일반적으로 부피가 낮거나 조정되지만 장기간 동안 중요합니다. |
| 시계열 데이터(동작) | **시계열 데이터** 사용자 동작에 대한 정보를 제공합니다. 표준 스키마 클래스 XDM(Experience Data Model)로 표시됩니다 [!DNL ExperienceEvent], 시계열 데이터는 장바구니에 추가되는 항목, 클릭된 링크, 열람된 비디오와 같은 이벤트를 설명할 수 있습니다. 행동의 값은 시간이 지남에 따라 줄어들 수 있습니다. |
| ID 네임스페이스(ID) | 고객 데이터가 함께 제공되면 **id 네임스페이스**, 그리고 사용자에 대해 더 많은 정보가 알려진 대로 이러한 ID를 함께 결합하는 기능. 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md) 추가 정보. |

{style="table-layout:auto"}



#### 프로필 저장소 구성 보고서

프로필 저장소의 구성을 이해하는 데 도움이 되는 많은 보고서를 사용할 수 있습니다. 이러한 보고서는 라이선스 사용을 더 잘 최적화하기 위해 경험 이벤트 만료를 설정하는 방법 및 위치에 대한 올바른 결정을 내리는 데 도움이 됩니다.

* **데이터 집합 Overlap Report API**: 대응 가능 대상에 가장 많이 기여하는 데이터 세트를 표시합니다. 이 보고서를 사용하여 어떤 [!DNL ExperienceEvent] 에 대한 만료를 설정하는 데이터 세트입니다. 다음에서 자습서를 참조하십시오. [데이터 집합 중복 보고서 생성](../../profile/tutorials/dataset-overlap-report.md) 추가 정보.
* **ID Overlap Report API**: 대응 가능 대상에 가장 많이 기여하는 ID 네임스페이스를 노출합니다. 다음에서 자습서를 참조하십시오. [id 중복 보고서 생성](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 추가 정보.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 경험 이벤트 만료 {#event-expirations}

이 기능을 사용하면 사용 사례에 더 이상 중요하지 않은 프로필 사용 데이터 세트에서 동작 데이터를 자동으로 제거할 수 있습니다. 다음 사항에 대한 개요를 참조하십시오. [경험 이벤트 만료](../../profile/event-expirations.md) 데이터 세트에 대해 활성화한 후 이 프로세스가 작동하는 방식에 대한 자세한 내용은 을 참조하십시오.

## 라이센스 사용 규정 준수에 대한 모범 사례 요약 {#best-practices}

다음은 라이선스 사용 권한을 더 잘 준수하기 위해 따라야 할 몇 가지 권장 모범 사례 목록입니다.

* 를 사용하십시오 [라이선스 사용 대시보드](../../dashboards/guides/license-usage.md) 고객 사용 트렌드를 추적 및 모니터링합니다. 이를 통해 발생할 수 있는 모든 잠재적인 초과 상황을 미리 파악할 수 있습니다.
* 구성 [수집 필터](#ingestion-filters) 세그먼테이션 및 개인화 사용 사례에 필요한 이벤트 식별 이를 통해 사용 사례에 필요한 중요한 이벤트만 보낼 수 있습니다.
* 다음과 같은 경우에만 [프로필에 대해 활성화된 데이터 세트](#ingestion-filters) 세그먼테이션 및 개인화 사용 사례에 필요합니다.
* 구성 [경험 이벤트 만료](#event-expirations) 웹 데이터와 같은 빈도가 높은 데이터의 경우.
* 정기적으로 [프로필 구성 보고서](#profile-store-composition-reports) 프로필 저장소 컴포지션을 이해하기 위한 것입니다. 이를 통해 라이선스 사용에 가장 많이 기여하는 데이터 소스를 파악할 수 있습니다.

## 기능 요약 및 가용성 {#feature-summary}

이 문서에 설명된 우수 사례 및 도구는 Adobe Experience Platform 내에서 라이선스 자격 사용을 더 잘 관리하는 데 도움이 됩니다. 이 문서는 모든 Experience Platform 고객에게 가시성과 제어력을 제공하는 데 도움이 되는 추가 기능이 릴리스되면 업데이트됩니다.

다음 표는 라이선스 사용 권한을 보다 효율적으로 관리하기 위해 현재 사용 가능한 기능 목록을 정리해 놓은 것입니다.

| 기능 | 설명 |
| --- | --- |
| [프로필에 대한 데이터 세트 활성화/비활성화](../../catalog/datasets/user-guide.md) | 실시간 고객 프로필에 데이터 세트 수집을 활성화하거나 비활성화합니다. |
| [경험 이벤트 만료](../../profile/event-expirations.md) | 프로필 사용 데이터 세트에 수집된 모든 이벤트에 대해 만료 시간을 적용합니다. 이 기능을 사용하려면 Adobe 지원 담당자에게 문의하십시오. |
| [Adobe Analytics 데이터 준비 필터](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 적용 [!DNL Kafka] 불필요한 데이터를 수집에서 제외하는 필터 |
| [Adobe Audience Manager 소스 커넥터 필터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Audience Manager 소스 연결 필터를 적용하여 불필요한 데이터를 수집에서 제외 |
| [Alloy SDK 데이터 필터](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 합금 필터를 적용하여 불필요한 데이터를 수집에서 제외 |
| [이벤트 전달 데이터 필터](../../tags/ui/event-forwarding/overview.md) | 서버측 적용 [!DNL Kafka] 불필요한 데이터를 수집에서 제외하는 필터.  다음 문서를 참조하십시오. [태그 규칙](../../tags/ui/managing-resources/rules.md) 추가 정보. |
| [라이선스 사용 대시보드 UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Experience Platform을 위해 조직의 라이선스 관련 데이터에 대한 스냅샷 보기 |
| [데이터 집합 Overlap Report API](../../profile/tutorials/dataset-overlap-report.md) | 대응 가능 대상에 가장 많이 기여하는 데이터 세트를 출력합니다 |
| [ID Overlap Report API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 대응 가능 대상에 가장 많이 기여하는 ID 네임스페이스를 출력합니다 |

{style="table-layout:auto"}
