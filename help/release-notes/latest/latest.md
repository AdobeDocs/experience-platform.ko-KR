---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
source-git-commit: ea4d17459dcd7abd981260fe6733320b08af15e8
workflow-type: tm+mt
source-wordcount: '3124'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 9월 28일**

Adobe Experience Platform의 새로운 기능:

- [속성 기반 액세스 제어](#abac)
- [데이터 위생](#data-hygiene)
- [[!UICONTROL 개인 정보 콘솔]](#privacy-console)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [감사 로그](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [ID 서비스](#identity-service)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## 속성 기반 액세스 제어 {#abac}

>[!IMPORTANT]
>
>특성 기반 액세스 제어는 2022년 10월부터 사용할 수 있습니다. 얼리 어답터가 되려면 Adobe 담당자에게 문의하십시오.

특성 기반 액세스 제어는 개인 정보 보호 관련 브랜드에게 사용자 액세스를 관리할 수 있는 더 많은 유연성을 제공하는 Adobe Experience Platform 기능입니다. 스키마 필드 및 세그먼트와 같은 개별 객체를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Platform 사용자에 대한 개별 개체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

특성 기반 액세스 제어를 통해 조직의 관리자는 모든 플랫폼 워크플로우 및 리소스에서 사용자의 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 기타 사용자 정의된 데이터 유형에 대한 액세스를 제어할 수 있습니다. 관리자는 해당 필드에 해당하는 특정 필드 및 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 속성 기반 액세스 제어 | 특성 기반 액세스 제어를 사용하면 XDM(Experience Data Model) 스키마 필드와 세그먼트에 조직 또는 데이터 사용 범위를 정의하는 레이블을 지정할 수 있습니다. 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드 및 세그먼트를 포함하는 액세스 정책을 정의하여 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 자세한 내용은 [속성 기반 액세스 제어 개요](../../access-control/abac/overview.md). |
| 권한 | 권한은 관리자가 사용자 역할 및 액세스 정책을 정의하여 제품 응용 프로그램 내의 기능 및 개체에 대한 액세스 권한을 관리할 수 있는 Experience Cloud 영역입니다. 권한을 통해 역할을 만들고 관리하고, 이러한 역할에 대해 원하는 리소스 권한을 할당하고, 레이블을 활용하고 특정 플랫폼 리소스에 액세스할 수 있는 사용자 역할을 정의하는 정책을 작성할 수 있습니다. 또한 권한을 사용하여 특정 역할과 연관된 레이블, 샌드박스 및 사용자를 관리할 수도 있습니다. 자세한 내용은 [권한 UI 안내서](../../access-control/abac/ui/browse.md). |

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../../access-control/abac/overview.md). 속성 기반 액세스 제어 워크플로우에 대한 포괄적인 지침은 [특성 기반 액세스 제어 종단 안내서](../../access-control/abac/end-to-end-guide.md).

## 데이터 위생 {#data-hygiene}

Adobe Experience Platform은 소비자 경험을 오케스트레이션하기 위해 복잡하고 큰 데이터 작업을 관리하는 강력한 도구 세트를 제공합니다. 시간이 지나면서 시스템에 데이터를 수집하면 데이터가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책이 필요하다고 인정하는 경우 삭제되도록 데이터 저장소를 관리하는 것이 점점 더 중요해집니다.

Adobe Experience Platform의 데이터 위생 기능을 사용하면 자동화된 데이터 세트 만료를 예약하고 id로 소비자 데이터를 프로그래밍 방식으로 삭제하여 데이터를 정리할 수 있습니다.

>[!IMPORTANT]
>
>데이터 위생 기능은 Adobe Healthcare Shield 또는 Privacy Shield를 구입한 조직에서만 사용할 수 있습니다.

데이터 위생을 시작하려면 다음 설명서를 참조하십시오.

- [데이터 위생 개요](../../hygiene/home.md): Platform의 데이터 위생 기능에 대한 기본 사항을 살펴보십시오.
- [[!UICONTROL 데이터 위생] UI 안내서](../../hygiene/ui/overview.md): Platform 사용자 인터페이스 내에서 데이터 세트 만료 및 소비자 삭제 요청을 예약하는 방법을 알아봅니다.
- [데이터 위생 API 안내서](../../hygiene/api/overview.md): UI에서 수행할 수 있는 모든 데이터 위생 활동은 프로그래밍 방식으로 수행할 수도 있습니다

## [!UICONTROL 개인 정보 콘솔] {#privacy-console}

다음 [!UICONTROL 개인 정보 콘솔] Experience Platform UI의 탭에서는 다음과 같은 개인 정보 관련 기능의 주요 통찰력에 대한 대시보드 보기를 제공합니다 [Privacy Service의 데이터 주체 요청](../../privacy-service/home.md), [데이터 위생 작업 명령](../../hygiene/home.md), 및 [감사 로그](../../landing/governance-privacy-security/audit-logs/overview.md). 또한 이 콘솔에서는 일반적인 개인 정보 보호 워크플로우를 안내하는 몇 가지 제품 내 사용 사례 안내서도 제공합니다.

자세한 내용은 [개인 정보 콘솔 개요](../../landing/governance-privacy-security/privacy-console.md) 를 참조하십시오.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

마케팅 분석가 및 전문가가 AI/ML 서비스를 통해 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 모델을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 통해 마케팅 분석가는 모델 구성을 초안 인스턴스로 저장하고 교육 및 점수 책정 전에 완료될 때까지 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 사용자에게 워크플로우에서 정의할 필드가 여러 개 있지만 시간 제한으로 인해 완료할 수 없는 경우가 포함됩니다. 또 다른 시나리오는 하나 이상의 데이터 세트 통계가 처리 중이며 아직 사용할 수 없는 경우입니다. 다음 문서를 참조하십시오. [Attribution AI 사용 안내서](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 추가 정보 |
| 거버넌스 정책 | 사용자가 구성 워크플로우를 통해 인스턴스를 생성하도록 제출한 후 새 정책 적용 서비스는 데이터 사용에 대한 정책 위반이 있는지 확인하고 팝오버에 세부 정보를 표시합니다. 이렇게 하면 데이터 작업 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하게 됩니다. |

Attribution AI에 대한 자세한 내용은 [Attribution AI 개요](../../intelligent-services/attribution-ai/overview.md). 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md).

### 고객 AI

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 통해 마케팅 분석가는 모델 구성을 초안 인스턴스로 저장하고 교육 및 점수 책정 전에 완료될 때까지 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 사용자에게 워크플로우에서 정의할 필드가 여러 개 있지만 시간 제한으로 인해 완료할 수 없는 경우가 포함됩니다. 또 다른 시나리오는 하나 이상의 데이터 세트 통계가 처리 중이며 아직 사용할 수 없는 경우입니다. 다음 문서를 참조하십시오. [Customer AI 사용 안내서](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 추가 정보 |
| 거버넌스 정책 | 사용자가 구성 워크플로우를 통해 인스턴스를 생성하도록 제출한 후 새 정책 적용 서비스는 데이터 사용에 대한 정책 위반이 있는지 확인하고 팝오버에 세부 정보를 표시합니다. 이렇게 하면 데이터 작업 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하게 됩니다. |

Customer AI에 대한 자세한 내용은 [Customer AI 개요](../../intelligent-services/customer-ai/overview.md). 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md).

## 감사 로그 {#audit-logs}

Experience Platform을 사용하면 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 감사 로그는 작업을 수행한 사람과 수행한 시기에 대한 정보를 제공합니다.

**업데이트된 기능**

| 기능 | 이름 | 설명 |
| --- | --- | --- |
| 추가된 리소스 | <ul><li>Attribution AI 인스턴스</li><li>고객 AI 인스턴스</li><li>데이터 스트림</li></ul> | 활동이 발생하면 감사 로그 리소스가 자동으로 기록됩니다. 이 기능이 활성화되어 있으면 수동으로 로그 수집을 활성화할 필요가 없습니다. |

{style=&quot;table-layout:auto&quot;}

Platform에서 감사 로그에 의해 추적되는 다양한 리소스 특정 이벤트 유형에 대한 자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 개의 대시보드를 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 사용 중인 레이블 | 위젯 라이브러리에서 볼 때 사용 중 레이블은 대시보드에 기존 위젯이 있는지 쉽게 식별합니다. 따라서 원할 경우 동일한 위젯을 두 번 이상 추가할 수 있지만, 중복을 피하기가 쉽습니다. |
| 사용자 정의 대시보드 | 사용자 정의 대시보드는 사용자 정의 대시보드를 만들고 관리할 수 있도록 하여 통찰력을 높이고 시각화를 사용자 지정하는 데 도움이 됩니다. 사용자 정의 대시보드를 사용하여 맞춤형 위젯을 생성, 추가 및 편집하여 조직과 관련된 주요 지표를 시각화할 수 있습니다. 다음 문서를 참조하십시오. [기능 안내서](../../dashboards/user-defined-dashboards.md) 추가 정보 |
| 고객 데이터 플랫폼 통찰력 데이터 모델 | CDP(Customer Data Platform) 인사이트 데이터 모델 기능은 다양한 프로필, 대상 및 세그멘테이션 위젯에 대한 통찰력을 제공하는 데이터 모델 및 SQL을 표시합니다. 이러한 SQL 쿼리 템플릿을 사용자 지정하여 마케팅 및 주요 성능 지표 사용 사례를 위한 CDP 보고서를 만들 수 있습니다. 그런 다음 이러한 통찰력을 사용자 정의 대시보드에 대한 사용자 지정 위젯으로 사용할 수 있습니다. 다음 문서를 참조하십시오. [CDP 통찰력 데이터 모델 기능 안내서](../../dashboards/cdp-insights-data-model.md) 추가 정보 |
| 대상 겹치기 보고서 위젯 | 이 위젯은 둘 다 사용할 수 있습니다 [!UICONTROL 프로필] 및 [!UICONTROL 세그먼트] 대시보드 . 이 보고서는 선택한 세그먼트에 대해 가장 높은 겹치기 비율 또는 가장 낮은 겹치기 비율 별로 순위가 지정된 대상 목록을 제공합니다. 에서 [!UICONTROL 프로필] 대시보드 사용 가능한 모든 세그먼트의 병합 정책별로 대상 겹침을 필터링하고 볼 수 있습니다. 다음 [!UICONTROL 세그먼트] 대시보드를 사용하면 특정 세그먼트별로 겹치는 대상을 필터링할 수 있습니다.<br>이 분석을 사용하여 새롭고 고성능 세그먼트를 작성하고 동일한 대상을 다른 대상으로 보내지 않습니다. 또한 이 보고서를 통해 숨겨진 인사이트를 식별하여 세그멘테이션을 향상하거나 추적할 고유 프로필을 찾을 수 있습니다. 각각 읽기 [프로필](../../dashboards/guides/profiles.md#audience-overlap-report) 및 [세그먼트](../../dashboards/guides/segments.md#audience-overlap-report) 위젯 가이드로 자세히 알아보십시오. |

자세한 내용은 [!DNL Dashboards]를 보려면 [[!DNL Dashboards] 개요](../../dashboards/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 플랫폼 UI에서 왼쪽 탐색 통합 | 이전에 데이터 수집 UI에 배타적이었던 모든 기능(태그, 이벤트 전달 및 데이터 세트 포함)은 이제 Experience Platform의 왼쪽 탐색 영역에서 카테고리 아래에 있습니다 **[!UICONTROL 데이터 수집]**. 따라서 Platform에서 데이터 수집 기능을 사용할 때 UI 간을 전환할 필요가 없습니다. |
| 태그 및 이벤트 전달의 사용자 속성 | 사용 가능한 목록 작성 시 [!UICONTROL 속성] 태그 및 이벤트 전달에서, 이제 나열된 각 속성이 마지막으로 업데이트된 시간과 업데이트를 수행한 사용자를 표시합니다. |
| [[!DNL User-Agent Client Hints] 웹 SDK에서](../../edge/fundamentals/user-agent-client-hints.md) | 이제 웹 SDK에서 를 지원합니다 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 클라이언트 힌트를 사용하면 웹 사이트 소유자는 [!DNL User-Agent] 하지만 개인 정보 보호 방식으로 사용됩니다. |
| [웹 SDK 페이지별 마이그레이션](../../edge/home.md#migrating-to-web-sdk) | 이제 다음과 같은 다른 Experience Cloud 라이브러리에서 기존 웹 속성을 마이그레이션할 수 있습니다 [!DNL at.js], 웹 SDK에 한 번에 한 페이지 이렇게 하면 모든 페이지를 한 번에 마이그레이션하지 않고도 웹 SDK 마이그레이션에 단계적인 접근 방식이 가능합니다. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 대상 SDK | 이제 Destination SDK은 일괄 처리(또는 파일 기반)를 만들거나 개인 대상을 만드는 파트너와 고객을 완벽하게 지원합니다. 자세한 내용은 다음 설명서 페이지를 참조하십시오. <ul><li>[Destination SDK 개요](/help/destinations/destination-sdk/overview.md)</li><li>[파일 기반 대상 구성](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[파일 기반 대상에 대한 파일 형식 옵션 구성](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[파일 기반 대상 테스트](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**새 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services은 크로스 채널 고객 경험을 디자인하고 시각적 캠페인 운영, 실시간 상호 작용 관리 및 크로스 채널 실행을 위한 환경을 제공할 수 있는 플랫폼을 제공합니다. [Campaign으로 시작](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 이 통합은 Adobe Campaign 버전 8.4 이상에서 작동합니다. 버전 8.4는 2022년 9월 30일에 릴리스될 예정입니다. |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 다음 [!DNL Salesforce CRM] 연락처 및 리드 업데이트를 모두 지원하고 더 빠른 업데이트를 위한 성능 개선 사항을 지원하도록 대상이 업데이트되었습니다. |

{style=&quot;table-layout:auto&quot;}

**새 설명서 또는 업데이트된 설명서**

| 설명서 | 설명 |
| ----------- | ----------- |
| 대상 흐름 서비스 API 설명서 | 다음 [대상 API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/destinations/) 파일 기반 대상에서 작업을 수행하는 방법에 대한 지침을 포함하도록 가 업데이트되었습니다. 나중에 스트리밍 대상에 대한 작업이 추가됩니다. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 열거형 및 추천 값에 대한 UI 지원 | 이제 데이터 유효성 검사를 활성화하는 열거형 외에도 다음을 수행할 수 있습니다 [제안된 값 추가 또는 제거](../../xdm/ui/fields/enum.md) 표준 또는 사용자 지정 문자열 필드의 경우 플랫폼 사용자가 세그먼트를 만들 때 선택할 값의 목록을 친숙한 형식으로 제공합니다. |

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL AJO 분류 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 제안 이벤트가 트리거되는 와 상호 작용한 특정 요소의 속성입니다. |
| 필드 그룹 | [[!UICONTROL MediaAnalytics 상호 작용 세부 사항]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 시간에 따른 미디어 상호 작용을 추적합니다. |
| 필드 그룹 | [[!UICONTROL 미디어 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 미디어 세부 사항 정보를 추적합니다. |
| 필드 그룹 | [[!UICONTROL Adobe CJM ExperienceEvent - 서피스]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Adobe Journey Optimizer에서 경험 이벤트에 대한 서피스를 설명합니다. |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 비헤이비어 | [[!UICONTROL 시계열]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>에 대한 값이 추가되었습니다. `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>에 대해 값이 제거됨 `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 필드 그룹 | (복수) | [여러 필드 설명이 업데이트되었습니다](https://github.com/adobe/xdm/pull/1628/files) Journey Orchestration 구성 요소 간에 공유할 수 있습니다. |
| 필드 그룹 | (복수) | [여러 Adobe Workfront 구성 요소의 제목이 업데이트되었습니다](https://github.com/adobe/xdm/pull/1634/files) 일관성을 위해 |
| 필드 그룹 | [[!UICONTROL AJO 분류 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 여러 필드의 네임스페이스가 `xdm`. |
| 필드 그룹 | [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 새 필드를 추가했습니다. `isReadSegmentTriggerStartEvent`. |
| 필드 그룹 | [[!UICONTROL 예측 웨더]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 변경 `xdm:uvIndex` 필드를 정수 유형에 추가하고 `xdm` 네임스페이스가 누락된 여러 필드에 있는 경우 |
| 필드 그룹 | [[!UICONTROL 미디어 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 및 `xdm:implementationDetails` 이(가) 필드 그룹에서 제거되었습니다. |
| 데이터 유형 | (복수) | [여러 미디어 속성 이름이 업데이트되었습니다.](https://github.com/adobe/xdm/pull/1626/files) 일관성을 위해 여러 데이터 유형에 걸쳐 데이터를 관리합니다. |
| 데이터 유형 | [[!UICONTROL 구현 세부 사항]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 플러터에 대해 알려진 이름이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 관심 영역 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 이제 데이터 유형에서 관심 영역과 연결된 메타데이터 키-값 쌍 목록을 사용할 수 있습니다. |
| 데이터 유형 | [[!UICONTROL 제안 작업]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 의 이름이 로 변경되었습니다. [!UICONTROL 제안 작업]. |
| 데이터 유형 | [[!UICONTROL 제안 이벤트 유형]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 의 이름이 [!UICONTROL 제안 작업]. |
| (복수) | (복수) | 실험적인 특성이 [모든 B2B 구성 요소에서 안정화됨](https://github.com/adobe/xdm/pull/1617/files). |
| (복수) | (복수) | Adobe Journey Optimizer 엔티티가 [안정화](https://github.com/adobe/xdm/pull/1625/files). |
| (복수) | (복수) | 여러 실험 구성 요소에 걸쳐 특정 필드의 네임스페이스가 만들어졌습니다 [일관성을 위해 업데이트됨](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## ID 서비스 {#identity-service}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform Identity 서비스를 사용하면 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 해당 행동을 더 잘 볼 수 있으므로 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 집합 삭제 지원 | 이제 ID 서비스는 를 통해 요청할 때 데이터 세트 삭제를 지원합니다 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI 또는 데이터 위생입니다. 안내서 읽기 [UI에서 데이터 세트 삭제](../../catalog/datasets/user-guide.md#delete-a-dataset) 추가 정보. |

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).

## 쿼리 서비스 {#query-service}

Query Service를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고 구독 API | Adobe Experience Platform Query Service를 사용하면 애드혹 쿼리 및 예약된 쿼리 모두에 대한 경고를 구독할 수 있습니다. 경고는 이메일, Platform UI 또는 두 가지 모두로 수신할 수 있습니다. 현재 쿼리 경고는 [쿼리 서비스 API](https://developer.adobe.com/experience-platform-apis/references/query-service/). 자세한 내용은 [쿼리 경고 설명서](../../query-service/api/alert-subscriptions.md) 추가 정보 |
| 데이터 집합 샘플 | 쿼리 서비스 데이터 세트 샘플을 사용하면 쿼리 정확성 비용 측면에서 처리 시간이 크게 단축된 빅데이터에 대해 예비 쿼리를 수행할 수 있습니다. 자세한 내용은 [데이터 세트 샘플 안내서](../../query-service/sql/dataset-samples.md) 추가 정보 |

자세한 내용은 [!DNL Query Service]를 보려면 [[!DNL Query Service] 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Audience Manager 세그먼트 모집단이 실시간 고객 프로필에 미치는 영향 | 크기 조정 가능한 Audience Manager 세그먼트 모집단을 수집하면 Audience Manager 소스를 사용하여 처음 Audience Manager 세그먼트를 Platform으로 보낼 때 총 프로필 수에 직접적인 영향을 줍니다. 즉, 모든 세그먼트를 선택하면 라이센스 사용 권한을 초과하는 프로필 수가 발생할 수 있습니다. 자세한 내용은 [Audience Manager 소스 개요](../../sources/connectors/adobe-applications/audience-manager.md). 라이센스 사용에 대한 자세한 내용은 [라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md). |
| Adobe Campaign 관리 Cloud Service 지원 | Adobe Campaign 관리 Cloud Service 소스를 사용하여 Adobe Campaign v8.4 게재 및 추적 로그 데이터를 Experience Platform으로 가져옵니다. 안내서 읽기 [UI에서 Adobe Campaign 관리 Cloud Service 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 추가 정보. |
| 배치 소스에 대한 온디맨드 섭취에 대한 API 지원 | 온디맨드 수집 기능을 사용하여 [!DNL Flow Service] API. 생성된 흐름 실행은 1회 수집으로 설정해야 합니다. 자세한 내용은 다음 안내서를 참조하십시오. [api를 사용하여 온디맨드 통합에 대한 흐름 실행 만들기](../../sources/tutorials/api/on-demand-ingestion.md) 추가 정보. |
| 배치 소스에 대한 실패한 데이터 흐름 실행을 다시 시도하는 데 대한 API 지원 | 를 사용하십시오 `re-trigger` API를 통해 실패한 데이터 흐름을 다시 시도하는 작업입니다. 안내서 읽기 [API를 사용하여 실패한 데이터 흐름 다시 시도](../../sources/tutorials/api/retry-flows.md) 추가 정보. |
| 에 대한 행 수준 데이터 필터링을 위한 API 지원 [!DNL Google BigQuery] 및 [!DNL Snowflake] 소스 | 논리 및 비교 연산자를 사용하여 [!DNL Google BigQuery] 및 [!DNL Snowflake] 소스. 안내서 읽기 [API를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md) 추가 정보. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).