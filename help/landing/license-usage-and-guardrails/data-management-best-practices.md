---
title: 데이터 관리 라이선스 권한 부여 우수 사례
description: Adobe Experience Platform을 사용하여 라이선스 권한을 보다 효율적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대해 알아봅니다.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 1f3cf3cc57342a23dae2d69c883b5768ec2bba57
workflow-type: tm+mt
source-wordcount: '2957'
ht-degree: 1%

---

# 데이터 관리 라이선스 권한 부여 모범 사례

Adobe Experience Platform은 데이터를 강력한 고객 프로필로 변환하여 실시간으로 업데이트하고 AI 기반 인사이트를 사용하여 모든 채널에 적합한 경험을 제공할 수 있는 개방형 시스템입니다. 소스를 사용하여 다양한 유형, 볼륨 및 기록의 데이터를 Experience Platform으로 가져온 다음, 세그먼테이션 및 개인화부터 분석 및 머신 러닝에 이르기까지 다양한 사용 사례에 맞게 해당 데이터를 입력할 수 있습니다.

Experience Platform은 만들 수 있는 프로필 수와 가져올 수 있는 데이터 양을 설정하는 라이선스를 제공합니다. 소스, 볼륨 또는 데이터 내역을 가져올 수 있는 용량을 고려할 때 데이터 볼륨이 증가하면 라이선스 권한을 초과할 수 있습니다.

Experience Platform을 사용하여 라이선스 권한을 보다 효율적으로 관리하는 데 사용할 수 있는 모범 사례 및 도구에 대해서는 이 안내서를 참조하십시오.

## 기능 요약 {#summary-of-features}

이 문서에 설명된 모범 사례 및 도구를 사용하여 Experience Platform 내에서 라이선스 권한 사용을 보다 효과적으로 관리할 수 있습니다. 이 문서는 모든 Experience Platform 고객에게 가시성과 제어 기능을 제공하는 데 도움이 되는 추가 기능이 출시됨에 따라 업데이트됩니다.

다음 표에서는 라이선스 사용 권한을 보다 효율적으로 관리하기 위해 현재 사용 가능한 기능 목록을 간단히 설명합니다.

| 기능 | 설명 |
| --- | --- |
| [데이터 집합 UI - 경험 이벤트 데이터 유지](../../catalog/datasets/user-guide.md#data-retention-policy) | 데이터 레이크 및 프로필 스토어의 데이터에 대한 고정 보존 기간을 구성합니다. 구성된 보존 기간이 종료되면 레코드가 삭제됩니다. |
| [실시간 고객 프로필에 대한 데이터 세트 활성화/비활성화](../../catalog/datasets/user-guide.md) | 실시간 고객 프로필에 데이터 세트 수집을 활성화하거나 비활성화합니다. |
| [프로필 스토어의 경험 이벤트 만료](../../profile/event-expirations.md) | 프로필 활성화 데이터 세트에 수집된 모든 이벤트에 만료 시간을 적용합니다. 이 기능을 활성화하려면 Adobe 계정 팀이나 고객 지원 센터에 문의하십시오. |
| [Adobe Analytics 데이터 준비 필터](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | [!DNL Kafka] 필터를 적용하여 불필요한 데이터를 수집에서 제외합니다. |
| [Adobe Audience Manager 소스 커넥터 필터](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Audience Manager 소스 연결 필터를 적용하여 불필요한 데이터를 수집에서 제외합니다. |
| [이벤트 전달 데이터 필터](../../tags/ui/event-forwarding/overview.md) | 불필요한 데이터를 수집에서 제외하려면 서버측 [!DNL Kafka] 필터를 적용하십시오.  자세한 내용은 [태그 규칙](../../tags/ui/managing-resources/rules.md)에 대한 설명서를 참조하십시오. |
| [라이선스 사용 대시보드 UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 라이선스가 부여된 권한과 비교하여 조직의 Experience Platform 제품 소비를 모니터링합니다. 일일 사용량 스냅샷, 예측 트렌드 및 자세한 샌드박스 수준 데이터를 액세스하여 사전 예방적 라이센스 관리를 지원합니다. |
| [데이터 집합 중복 보고서 API](../../profile/tutorials/dataset-overlap-report.md) | 대응 가능 대상에 가장 많이 기여하는 데이터 세트를 출력합니다. |
| [Identity Overlap Report API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 대응 가능 대상에 가장 많은 기여를 하는 ID 네임스페이스를 출력합니다. |
| [익명 프로필 데이터 만료](../../profile/pseudonymous-profiles.md) | 익명 프로필에 대한 데이터 만료 시간을 구성하고 프로필 저장소에서 데이터를 자동으로 제거합니다. |

{style="table-layout:auto"}

## Experience Platform 데이터 스토리지 이해

Experience Platform은 주로 데이터 레이크와 프로필 저장소, 이렇게 두 개의 데이터 저장소로 구성됩니다.

데이터 레이크는 주로 다음 용도로 사용됩니다.

* Experience Platform에 데이터를 온보딩하기 위한 준비 영역 역할을 합니다.
* 모든 Experience Platform 데이터를 위한 장기 데이터 저장소 역할을 합니다.
* 데이터 분석 및 데이터 과학과 같은 사용 사례를 활성화합니다.

**프로필 저장소**&#x200B;는 고객 프로필을 만드는 곳이며 주로 다음 용도로 사용됩니다.

* 실시간 경험을 지원하는 데 사용되는 프로필의 데이터 저장소 역할을 합니다.
* 세분화, 활성화 및 개인화와 같은 사용 사례를 활성화합니다.

>[!NOTE]
>
>[!DNL data lake]에 대한 액세스는 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

## 라이선스 사용 {#license-usage}

Experience Platform에 라이선스를 부여하면 SKU에 따라 달라지는 라이선스 사용 권한이 제공됩니다.

**[!DNL Addressable Audience]**: 알려진 프로필과 가명 프로필을 모두 포함하여 Experience Platform에서 계약상 허용되는 총 고객 프로필 수입니다.

**[!DNL Total Data Volume]**: 실시간 고객 프로필에서 참여 워크플로우에서 사용할 수 있는 총 데이터 양입니다.

이러한 지표의 사용 가능 여부 및 이러한 각 지표의 특정 정의는 조직이 구입한 라이선스에 따라 다릅니다.

## 라이선스 사용 대시보드

Adobe Experience Platform UI는 Experience Platform에 대한 조직 라이선스 관련 데이터의 스냅샷을 볼 수 있는 대시보드를 제공합니다. 대시보드의 데이터는 스냅샷이 생성된 특정 시점에 나타나는 것과 동일하게 표시됩니다. 스냅샷은 근사치도 데이터 샘플도 아니며 대시보드가 실시간으로 업데이트되지 않습니다.

자세한 내용은 [Experience Platform UI에서 라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md#license-usage-dashboard-data)에 대한 안내서를 참조하십시오.

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

### Experience Platform에 가져올 데이터

Experience Platform의 하나 또는 여러 시스템, 즉 [!DNL data lake] 및/또는 프로필 스토어로 데이터를 수집할 수 있습니다. 이것은 다양한 다른 사용 사례에 대해 두 시스템 모두에 다른 데이터가 존재할 수 있음을 의미한다. 예를 들어, [!DNL data lake]에 이전 데이터를 저장할 수 있지만 프로필 저장소에는 저장할 수 없습니다. 프로필 수집을 위한 데이터 세트를 활성화하여 프로필 스토어에 전송할 데이터를 선택할 수 있습니다.

>[!NOTE]
>
>[!DNL data lake]에 대한 액세스는 구입한 제품 SKU에 따라 달라질 수 있습니다. 제품 SKU에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 보관할 데이터

데이터 수집 필터와 만료 규칙을 모두 적용하여 사용 사례에서 더 이상 사용되지 않는 데이터를 제거할 수 있습니다. 일반적으로 동작 데이터(예: Analytics 데이터)는 레코드 데이터(예: CRM 데이터)보다 훨씬 많은 스토리지를 사용합니다. 예를 들어 많은 Experience Platform 사용자는 레코드 데이터의 프로필과 비교하여 동작 데이터만으로 채워지는 프로필이 최대 90% 이상입니다. 따라서 행동 데이터를 관리하는 것은 라이선스 권한 내에서 규정 준수를 보장하는 데 매우 중요합니다.

라이선스 사용 권한 내에 유지하기 위해 활용할 수 있는 다양한 도구가 있습니다.

* [수집 필터](#ingestion-filters)
* [프로필 저장소](#profile-service)

### ID 서비스 및 대응 가능 대상 {#identity-service}

대응 가능 대상자는 고객 프로필의 총 수를 참조하므로 ID 그래프는 총 대응 가능 대상 권한 수에 포함되지 않습니다.

그러나 ID 그래프 제한은 ID 분할로 인해 대응 가능 대상에 영향을 줄 수 있습니다. 예를 들어 가장 오래된 ECID를 그래프에서 제거하면 ECID가 실시간 고객 프로필에 익명 프로필로 계속 존재합니다. 이 동작을 우회하도록 [익명 프로필 데이터 만료](../../profile/pseudonymous-profiles.md)을 설정할 수 있습니다. 자세한 내용은 ID 서비스 데이터에 대한 [보호 기능](../../identity-service/guardrails.md)을 참조하세요.

### 수집 필터 {#ingestion-filters}

수집 필터를 사용하면 사용 사례에 필요한 데이터만 가져올 수 있으며 필요하지 않은 모든 이벤트는 필터링됩니다.

| 수집 필터 | 설명 |
| --- | --- |
| Adobe Audience Manager 소스 필터링 | Adobe Audience Manager 소스 연결을 만들 때 Audience Manager 데이터를 완전히 수집하는 대신 [!DNL data lake] 및 실시간 고객 프로필로 가져올 세그먼트와 트레이트를 선택하고 선택할 수 있습니다. 자세한 내용은 [Audience Manager 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)에 대한 안내서를 참조하십시오. |
| Adobe Analytics 데이터 준비 | Analytics 소스 연결을 만들 때 [!DNL Data Prep] 기능을 사용하여 사용 사례에 필요하지 않은 데이터를 필터링할 수 있습니다. [!DNL Data Prep]을(를) 통해 프로필에 게시해야 하는 특성/열을 정의할 수 있습니다. 데이터를 프로필에 게시할지 아니면 [!DNL data lake]에만 게시할지를 Experience Platform에 알리는 조건문을 제공할 수도 있습니다. 자세한 내용은 [Analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md)에 대한 안내서를 참조하십시오. |
| 프로필에 대한 데이터 세트 활성화/비활성화 지원 | 실시간 고객 프로필로 데이터를 수집하려면 프로필 스토어에서 사용할 데이터 세트를 활성화해야 합니다. 이렇게 하면 [!DNL Addressable Audience] 및 [!DNL Total Data Volume] 권한에 추가됩니다. 고객 프로필 사용 사례에 더 이상 데이터 세트가 필요하지 않으면 해당 데이터 세트의 프로필 통합을 비활성화하여 데이터가 라이센스 규정을 준수하는지 확인할 수 있습니다. 자세한 내용은 [프로필에 대한 데이터 세트 활성화 및 비활성화](../../catalog/datasets/enable-for-profile.md)에 대한 안내서를 참조하십시오. |
| 웹 SDK 및 모바일 SDK 데이터 제외 | 웹 및 모바일 SDK에서 수집하는 데이터에는 자동으로 수집되는 데이터와 개발자가 명시적으로 수집하는 데이터의 두 가지 유형이 있습니다. 라이선스 준수를 보다 잘 관리하려면 컨텍스트 설정을 통해 SDK의 구성에서 자동 데이터 수집을 비활성화하면 됩니다. 사용자 정의 데이터는 개발자가 제거하거나 설정할 수도 없습니다. |
| 서버 측 전달 데이터 제외 | 서버측 전달을 사용하여 Experience Platform으로 데이터를 전송하는 경우 규칙 작업에서 매핑을 제거하여 모든 이벤트에서 데이터를 제외하거나 규칙에 조건을 추가하여 특정 이벤트에 대해서만 데이터가 실행되도록 전송할 데이터를 제외할 수 있습니다. 자세한 내용은 [이벤트 및 조건](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if)에 대한 설명서를 참조하십시오. |
| 소스 수준에서 데이터 필터링 | 연결을 만들고 Experience Platform으로 데이터를 수집하기 전에 논리 및 비교 연산자를 사용하여 소스에서 행 수준 데이터를 필터링할 수 있습니다. 자세한 내용은 [API [!DNL Flow Service] 를 사용하여 소스에 대한 &#x200B;](../../sources/tutorials/api/filter.md)행 수준 데이터 필터링에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

### 프로필 저장소 {#profile-service}

프로필 저장소는 다음 구성 요소로 구성됩니다.

| 프로필 저장소 구성 요소 | 설명 |
| --- | --- |
| 프로필 조각 | 각 고객 프로필은 병합되어 해당 고객에 대한 단일 보기를 형성하는 여러 **프로필 조각**&#x200B;으로 구성됩니다. 예를 들어, 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 나타나는 해당 단일 고객과 관련된 여러 **프로필 조각**&#x200B;이 있습니다. 이러한 조각을 Experience Platform에 수집하면 ID 그래프를 사용하여 함께 결합함으로써 해당 고객을 위한 단일 프로필을 만듭니다. **프로필 조각**&#x200B;은(는) 연결된 레코드 데이터 및/또는 시계열 데이터가 있는 ID 네임스페이스를 식별자로 구성합니다. |
| 레코드 데이터(속성) | 프로필은 많은 **특성**(**레코드 데이터**)으로 구성된 주체, 조직 또는 개인을 나타냅니다. 예를 들어, 제품 프로필에는 SKU 및 설명이 포함될 수 있지만, 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함됩니다. **레코드 데이터**&#x200B;은(는) 대개 볼륨이 낮거나 보통이지만 오랜 기간 동안 유용합니다. |
| 시계열 데이터(비헤이비어) | **시계열 데이터**&#x200B;에서 사용자 동작에 대한 정보를 제공합니다. 표준 스키마 클래스 XDM(경험 데이터 모델) [!DNL ExperienceEvent]이(가) 나타내는 시계열 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 시청한 비디오와 같은 이벤트를 설명할 수 있습니다. 행동의 가치는 시간이 지남에 따라 감소할 수 있습니다. |
| ID 네임스페이스(ID) | 고객 데이터가 결합되면 **ID 네임스페이스**&#x200B;를 사용하여 단일 프로필로 병합되고 사용자에 대해 더 많은 정보가 알려짐에 따라 이러한 ID를 함께 연결하는 기능이 제공됩니다. 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/features/namespaces.md)를 참조하십시오. |

{style="table-layout:auto"}

### 프로필 저장소 구성 보고서

프로필 저장소의 구성을 이해하는 데 도움이 되는 다양한 보고서가 있습니다. 이러한 보고서는 라이선스 사용을 보다 잘 최적화하기 위해 경험 이벤트 만료를 설정하는 방법과 위치에 대해 정보에 입각한 결정을 내리는 데 도움이 됩니다.

* **데이터 세트 중복 보고서 API**: 주소 지정 가능한 대상자에게 가장 많이 기여하는 데이터 세트를 표시합니다. 이 보고서를 사용하여 만료를 설정할 [!DNL ExperienceEvent]개의 데이터 세트를 식별할 수 있습니다. 자세한 내용은 [데이터 집합 중복 보고서 생성](../../profile/tutorials/dataset-overlap-report.md)에 대한 자습서를 참조하십시오.
* **ID 중복 보고서 API**: 주소 지정 가능한 대상자에게 가장 많이 기여하는 ID 네임스페이스를 표시합니다. 자세한 내용은 [ID 중복 보고서 생성](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report)에 대한 자습서를 참조하십시오.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### 익명 프로필 데이터 만료 {#pseudonymous-profile-expirations}

프로필 저장소에서 사용 사례에 더 이상 유효하지 않거나 유용하지 않은 데이터를 자동으로 제거하려면 익명 프로필 데이터 만료 기능을 사용하십시오. 익명 프로필 데이터 만료는 이벤트 및 프로필 레코드를 모두 제거합니다. 따라서 이 설정을 사용하면 지정 가능한 대상 볼륨이 줄어듭니다. 이 기능에 대한 자세한 내용은 [익명 프로필 데이터 만료 개요](../../profile/pseudonymous-profiles.md)를 참조하세요.

### 데이터 세트 UI - 경험 이벤트 데이터 세트 유지 {#data-retention}

데이터 세트 만료 및 보존 설정을 구성하여 데이터 레이크 및 프로필 스토어의 데이터에 대해 고정 보존 기간을 적용합니다. 보존 기간이 종료되면 데이터가 삭제됩니다. 경험 이벤트 데이터 만료는 이벤트만 제거하고 프로필 클래스 데이터는 제거하지 않으므로 라이선스 사용 지표에서 [총 데이터 볼륨](total-data-volume.md)이 줄어듭니다. 자세한 내용은 [데이터 보존 정책 설정](../../catalog/datasets/user-guide.md#data-retention-policy)에 대한 안내서를 참조하십시오.

### 프로필 경험 이벤트 만료 {#event-expirations}

동작 데이터가 사용 사례에 더 이상 중요하지 않으면 프로필 활성화 데이터 세트에서 동작 데이터를 자동으로 제거하도록 만료 시간을 구성합니다. 자세한 내용은 [경험 이벤트 만료](../../profile/event-expirations.md)에 대한 개요를 참조하십시오.

## 라이선스 사용 규정 준수에 대한 모범 사례 요약 {#best-practices}

다음은 라이선스 사용 권한을 더 잘 준수하도록 하기 위해 따를 수 있는 몇 가지 권장 모범 사례 목록입니다.

* [라이선스 사용 대시보드](../../dashboards/guides/license-usage.md)를 사용하여 고객 사용 트렌드를 추적하고 모니터링하세요. 이를 통해 발생할 수 있는 잠재적 초과 기간을 미리 확보할 수 있습니다.
* 세분화 및 개인화 사용 사례에 필요한 이벤트를 식별하여 [수집 필터](#ingestion-filters)를 구성하십시오. 이를 통해 사용 사례에 필요한 중요한 이벤트만 보낼 수 있습니다.
* 세분화 및 개인화 사용 사례에 필요한 [프로필에 대해 활성화된 데이터 세트](#ingestion-filters)만 있는지 확인하십시오.
* 웹 데이터와 같은 고주파 데이터에 대해 [경험 이벤트 만료](../../catalog/datasets/user-guide.md#data-retention-policy) 및 [익명 프로필 데이터 만료](../../profile/pseudonymous-profiles.md)을(를) 구성합니다.
* 데이터 레이크에서 경험 이벤트 데이터 세트에 대한 [TTL(Time-to-Live) 보존 정책](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)을 구성하여 오래된 레코드를 자동으로 제거하고 라이선스 권한에 맞게 저장소 사용을 최적화합니다.
* 프로필 저장소 구성을 이해하려면 [프로필 구성 보고서](#profile-store-composition-reports)를 정기적으로 확인하십시오. 이를 통해 라이선스 사용 소비에 가장 많이 기여하는 데이터 소스를 이해할 수 있습니다.

## 사용 사례: 라이선스 사용 규정 준수

### 이 사용 사례를 고려하는 이유

데이터 레이크와 프로필 스토리지 모두에 대해 **라이선스 사용 규정**&#x200B;을 준수하도록 함으로써 과다 사용을 방지하고, 비용을 최적화하고, 데이터 보존 정책을 비즈니스 요구 사항에 맞게 조정할 수 있습니다.

### 전제 조건 및 계획

계획 프로세스에서 다음 전제 조건을 고려하십시오.

* **액세스 및 권한**:
   * 경험 이벤트 TTL을 사용할 수 있는 **데이터 세트 관리** 권한이 있는지 확인하십시오.
   * 익명 프로필 TTL을 사용하려면 **프로필 설정 관리**&#x200B;가 있는지 확인하십시오.
* **데이터 보존 정책 이해**:
   * 데이터 보존 및 규정 준수에 관한 조직 정책
   * 데이터 분석 및 세그먼테이션 전환 확인 기간에 대한 비즈니스 요구 사항

### 사용할 UI 기능, Experience Platform 구성 요소 및 Experience Cloud 제품

이 사용 사례를 성공적으로 구현하려면 Adobe Experience Platform의 여러 영역을 사용해야 합니다. 이러한 모든 영역에 대해 필요한 속성 기반 액세스 제어 권한이 있는지 확인하거나 시스템 관리자에게 권한을 요청하십시오.

* 라이선스 사용 대시보드 - 샌드박스 수준에서 현재 자격 사용을 봅니다.
* 데이터 세트 관리 - 데이터 세트 수준 보존 정책을 모니터링하고 관리합니다.
* 대상(실시간 고객 프로필) - 세그먼테이션 규칙 전환 확인 기간이 데이터 유지 기간에 맞게 조정되도록 합니다.
* 모니터링 및 경고 - 업데이트를 추적하고 데이터 세트 유지 작업에 대한 통찰력을 받습니다.

### 사용 사례 달성 방법: 단계별 지침

추가 설명서에 대한 링크를 포함하는 아래 섹션을 읽어 위의 높은 수준 개요에서 각 단계를 완료합니다.

**현재 라이선스 사용량 확인**

먼저 **라이선스 사용량 대시보드**(으)로 이동하여 샌드박스 수준에서 자격 사용량을 검토합니다.

>[!BEGINTABS]

>[!TAB 프로덕션 샌드박스]

라이선스 사용 지표를 보려면 [!UICONTROL Metrics] 인터페이스를 사용하십시오. 인터페이스는 기본적으로 프로덕션 샌드박스에 대한 정보를 표시합니다.

![프로덕션 샌드박스에 대한 라이선스 사용 지표를 표시하는 라이선스 사용 대시보드 UI입니다.](../images/data-management/prod-sandbox.png)

>[!TAB 개발 샌드박스]

개발 샌드박스와 관련된 라이선스 사용 지표를 보려면 [!UICONTROL Development]을(를) 선택하십시오.

![개발 샌드박스에 대한 라이선스 사용 지표를 표시하는 라이선스 사용 대시보드 UI입니다.](../images/data-management/dev-sandbox.png)

>[!ENDTABS]

자세한 내용은 [라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md)에 대한 설명서를 참조하세요.

**데이터 집합 수준 저장소 사용량 분석**

**데이터 세트 찾아보기 보기**&#x200B;를 사용하여 데이터 레이크와 실시간 고객 프로필 모두에 대한 데이터 세트 사용 지표를 검토하십시오. **[!UICONTROL Data Lake Storage]** 또는 **[!UICONTROL Profile Storage]**&#x200B;의 열 헤더를 선택한 다음 팝업 패널에서 **[!UICONTROL Sort Descending]**&#x200B;을(를) 선택합니다.

>[!BEGINTABS]

>[!TAB 데이터 레이크 저장소]

데이터 레이크의 데이터 세트는 저장소 크기별로 정렬됩니다. 이 기능을 사용하여 데이터 레이크의 가장 큰 스토리지 소비자를 식별합니다.

![가장 큰 데이터 레이크에서 가장 작은 데이터 레이크로 정렬된 데이터 세트입니다.](../images/data-management/data-lake-storage.png)

>[!TAB 프로필 저장소]

프로필의 데이터 세트는 저장소 크기별로 정렬됩니다. 이 기능을 사용하여 프로필의 가장 큰 스토리지 소비자를 식별합니다.

![프로필의 데이터 세트가 가장 큰 것부터 가장 작은 것까지 정렬되었습니다.](../images/data-management/profile-storage.png)

>[!ENDTABS]

**보존 규칙 평가 및 구성**

그런 다음 Analytics 및 세그멘테이션에 대한 라이선스 제한 및 비즈니스 요구 사항에 따라 데이터 세트에 적절한 보존 정책이 있는지 확인합니다. 데이터 세트의 보존 정책을 보려면 데이터 세트 옆에서 줄임표(`...`)를 선택한 다음 **[!UICONTROL Set data retention policy]**&#x200B;을(를) 선택합니다.

![데이터 집합 옵션이 있는 팝업 패널, &quot;데이터 보존 정책 설정&quot; 포함](../images/data-management/set-retention-policy.png)

*[!UICONTROL Set dataset retention]* 인터페이스가 나타납니다. 이 인터페이스를 사용하여 데이터 세트에 대한 보존 정책을 구성합니다. 또한 데이터 레이크나 프로필에서 데이터 세트가 사용하고 있는 스토리지 공간의 양을 보는 데 사용할 수도 있습니다.

![데이터 집합 보존 설정 인터페이스입니다.](../images/data-management/dataset-retention.png)

영향 예측기를 사용하여 데이터 세트의 유지 영향을 추가로 분석할 수 있습니다. 보존 기간과 만료되도록 설정된 총 저장소 비율을 표시하는 차트를 보려면 **[!UICONTROL View ExperienceEvent data distribution]**&#x200B;을(를) 선택하십시오.

완료되면 **[!UICONTROL Save]** 선택

![데이터 집합 보존 인터페이스 내의 영향 예측자입니다.](../images/data-management/impact-forecaster.png)

**보존 변경 내용의 유효성 검사**

보존 정책을 적용하면 다음 도구를 사용하여 변경 사항을 확인할 수 있습니다.

* 데이터 집합 찾아보기 보기의 [데이터 집합 사용 지표](../../catalog/datasets/user-guide.md#enhanced-visibility-of-retention-periods-and-storage-metrics).
* [모니터링 대시보드](../../dataflows/ui/monitor.md)를 통해 보존의 영향을 보고 분석할 수 있습니다.
* 일별 스냅숏, 예측 트렌드 및 샌드박스 수준 인사이트를 볼 수 있는 [라이선스 사용 대시보드](../../dashboards/guides/license-usage.md)입니다.
