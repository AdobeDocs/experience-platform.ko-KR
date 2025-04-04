---
title: Adobe Experience Platform 릴리스 노트 2022년 9월
description: Adobe Experience Platform에 대한 2022년 9월 릴리스 정보입니다.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 23%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 9월 28일 목요일**

Adobe Experience Platform의 새로운 기능:

- [속성 기반 액세스 제어](#abac)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [감사 로그](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [ID 서비스](#identity-service)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## 속성 기반 액세스 제어 {#abac}

>[!IMPORTANT]
>
>특성 기반 액세스 제어는 2022년 10월부터 활성화됩니다. 얼리 어답터를 원하는 경우 Adobe 담당자에게 문의하십시오.

속성 기반 액세스 제어는 개인 정보 보호를 중시하는 브랜드가 사용자 액세스를 더욱 유연하게 관리할 수 있도록 하는 Adobe Experience Platform의 기능입니다. 스키마 필드 및 세그먼트와 같은 개별 오브젝트를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Experience Platform 사용자에 대해 개별 객체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

조직 관리자는 속성 기반 액세스 제어를 통해 모든 Experience Platform 워크플로 및 리소스에서 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 기타 사용자 지정된 유형의 데이터에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드에만 액세스할 수 있는 사용자 역할과 필드에 해당하는 데이터를 정의할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 속성 기반 액세스 제어 | 특성 기반 액세스 제어를 사용하면 XDM(Experience Data Model) 스키마 필드 및 세그먼트에 조직 또는 데이터 사용 범위를 정의하는 레이블로 레이블을 지정할 수 있습니다. 또한 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드 및 세그먼트에 적용되는 액세스 정책을 정의하여 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 자세한 내용은 [특성 기반 액세스 제어 개요](../../access-control/abac/overview.md)를 참조하십시오. |
| 권한 | 권한은 관리자가 사용자 역할 및 액세스 정책을 정의하여 제품 애플리케이션 내의 기능 및 개체에 대한 액세스 권한을 관리할 수 있는 Experience Cloud 영역입니다. 권한을 통해 역할을 만들고 관리하며, 이러한 역할에 대해 원하는 리소스 권한을 할당하고, 레이블을 활용하고 특정 Experience Platform 리소스에 액세스할 수 있는 사용자 역할을 정의하는 정책을 작성할 수 있습니다. 또한 권한을 사용하여 레이블, 샌드박스 및 특정 역할과 연관된 사용자를 관리할 수 있습니다. 자세한 내용은 [권한 UI 안내서](../../access-control/abac/ui/browse.md)를 참조하십시오. |

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../../access-control/abac/overview.md)를 참조하십시오. 속성 기반 액세스 제어 워크플로에 대한 종합적인 안내서는 [속성 기반 액세스 제어 통합 안내서](../../access-control/abac/end-to-end-guide.md)를 참조하십시오.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능과 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준의 구성을 사용하여 기업의 요구 사항에 맞는 모델을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 통해 마케팅 분석가는 모델 구성을 초안 인스턴스로 저장하고 교육 및 채점 전에 완료될 때까지 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 사용자가 워크플로우에서 정의할 필드가 여러 개 있지만 시간 제한으로 인해 완료할 수 없는 경우가 포함됩니다. 또 다른 시나리오는 하나 이상의 데이터 세트 통계가 처리 중이며 아직 사용할 수 없는 경우입니다. 자세한 내용은 [Attribution AI 사용 안내서](../../intelligent-services/attribution-ai/user-guide.md#governance-policies)를 참조하십시오. |
| 거버넌스 정책 | 사용자가 구성 워크플로를 통해 인스턴스를 만들도록 제출하면 새 정책 시행 서비스가 데이터 사용에 대한 정책 위반 여부를 확인하고 팝오버에 세부 정보를 표시합니다. 데이터 운영 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하는지 확인합니다. |

기여도 AI에 대한 자세한 내용은 [기여도 AI 개요](../../intelligent-services/attribution-ai/overview.md)를 참조하십시오. 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md)를 참조하십시오.

### 고객 AI

Real-Time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 통해 마케팅 분석가는 모델 구성을 초안 인스턴스로 저장하고 교육 및 채점 전에 완료될 때까지 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 사용자가 워크플로우에서 정의할 필드가 여러 개 있지만 시간 제한으로 인해 완료할 수 없는 경우가 포함됩니다. 또 다른 시나리오는 하나 이상의 데이터 세트 통계가 처리 중이며 아직 사용할 수 없는 경우입니다. 자세한 내용은 [고객 AI 사용 안내서](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies)를 읽어 보십시오. |
| 거버넌스 정책 | 사용자가 구성 워크플로를 통해 인스턴스를 만들도록 제출하면 새 정책 시행 서비스가 데이터 사용에 대한 정책 위반 여부를 확인하고 팝오버에 세부 정보를 표시합니다. 데이터 운영 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하는지 확인합니다. |

Customer AI에 대한 자세한 내용은 [Customer AI 개요](../../intelligent-services/customer-ai/overview.md)를 참조하십시오. 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md)를 참조하십시오.

## 감사 로그 {#audit-logs}

Experience Platform을 사용하면 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 감사 로그는 누가 무엇을 언제 수행했는지에 대한 정보를 제공합니다.

**업데이트된 기능**

| 기능 | 이름 | 설명 |
| --- | --- | --- |
| 리소스 추가됨 | <ul><li>기여도 AI 인스턴스</li><li>고객 AI 인스턴스</li><li>데이터 스트림</li></ul> | 감사 로그 리소스는 활동이 발생하면 자동으로 기록됩니다. 이 기능이 활성화되어 있으면 로그 수집을 수동으로 활성화할 필요가 없습니다. |

{style="table-layout:auto"}

Experience Platform의 감사 로그에서 추적되는 다양한 리소스 관련 이벤트 유형에 대한 자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md)를 참조하십시오.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 사용 중 레이블 | 위젯 라이브러리에서 볼 때 사용 중 레이블은 대시보드에 기존 위젯이 있는지 쉽게 식별합니다. 이렇게 하면 원하는 경우 동일한 위젯을 두 번 이상 추가할 수 있지만 중복을 쉽게 방지할 수 있습니다. |
| 사용자 정의 대시보드 | 사용자 정의 대시보드를 사용하면 사용자 정의 대시보드를 작성하고 관리할 수 있으므로 신속하게 통찰력을 얻고 시각화를 맞춤화할 수 있습니다. 사용자 정의 대시보드를 사용하여 맞춤형 위젯을 만들고, 추가하고, 편집하여 조직과 관련된 주요 지표를 시각화할 수 있습니다. 자세한 내용은 [기능 안내서](../../dashboards/standard-dashboards.md)를 읽어 보십시오. |
| Customer Data Platform Insights 데이터 모델 | CDP(Customer Data Platform) Insights 데이터 모델 기능은 다양한 프로필, 대상 및 세그멘테이션 위젯에 대한 통찰력을 제공하는 데이터 모델 및 SQL을 노출합니다. 이러한 SQL 쿼리 템플릿을 사용자 정의하여 마케팅 및 주요 성능 지표 사용 사례에 대한 CDP 보고서를 만들 수 있습니다. 그런 다음 이러한 인사이트를 사용자 정의 대시보드에 대한 사용자 정의 위젯으로 사용할 수 있습니다. 자세한 내용은 [CDP Insights 데이터 모델 기능 안내서](../../dashboards/data-models/cdp-insights-data-model-b2c.md)를 참조하십시오. |
| 대상 중복 보고서 위젯 | 이 위젯은 [!UICONTROL 프로필] 및 [!UICONTROL 세그먼트] 대시보드 모두에서 사용할 수 있습니다. 이 보고서는 선택한 세그먼트에 대해 가장 높거나 가장 낮은 오버랩 비율로 순위가 매겨진 대상자 목록을 제공합니다. [!UICONTROL 프로필] 대시보드에서 사용 가능한 모든 세그먼트의 병합 정책으로 대상자를 필터링하고 볼 수 있습니다. [!UICONTROL 세그먼트] 대시보드를 사용하면 특정 세그먼트별로 대상 겹침을 필터링할 수 있습니다.<br>이 분석을 사용하여 새로운 고성능 세그먼트를 작성하고 동일한 대상자를 다른 대상으로 보내지 마십시오. 또한 이 보고서는 숨겨진 인사이트를 식별하여 세그먼테이션을 개선하거나 추적할 고유한 프로필을 찾는 데 도움이 됩니다. 자세한 내용은 해당 [프로필](../../dashboards/guides/profiles.md#audience-overlap-report) 및 [세그먼트](../../dashboards/guides/audiences.md#audience-overlap-report) 위젯 안내서를 참조하십시오. |

[!DNL Dashboards]에 대한 자세한 내용은 [[!DNL Dashboards] 개요](../../dashboards/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Experience Platform UI에서 왼쪽 탐색 통합 | 이전에 데이터 수집 UI에 독점적이었던 모든 기능(태그, 이벤트 전달 및 데이터스트림 포함)은 이제 Experience Platform의 왼쪽 탐색을 통해 범주 **[!UICONTROL 데이터 수집]**&#x200B;에서 사용할 수 있습니다. 이렇게 하면 Experience Platform에서 데이터 수집 기능을 사용할 때 UI 간을 전환할 필요가 없습니다. |
| 태그 및 이벤트 전달의 사용자 속성 | 태그 및 이벤트 전달에 사용 가능한 [!UICONTROL 속성]을 나열할 때 이제 나열된 각 속성이 마지막으로 업데이트된 시간과 업데이트를 수행한 사용자를 표시합니다. |
| 이벤트 전달용 [[!DNL Snap Conversions API] 확장](https://exchange.adobe.com/apps/ec/108550) | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Snapchat Conversions API]에 데이터를 보낼 수 있습니다. API 인증 및 사용 방법에 대한 자세한 내용은 이 [[!DNL Snapchat Marketing API] 설명서](https://marketingapi.snapchat.com/docs/conversion.html)를 참조하십시오. |
| [Web SDK의 사용자 에이전트 클라이언트 힌트](/help/web-sdk/use-cases/client-hints.md) | 이제 웹 SDK에서 [사용자 에이전트 클라이언트 힌트](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)를 지원합니다. 클라이언트 힌트를 사용하면 웹 사이트 소유자가 [!DNL User-Agent] 문자열에서 사용할 수 있는 동일한 정보의 대부분에 액세스할 수 있지만 보다 개인정보 보호에 특화되었습니다. |
| [웹 SDK 페이지별 마이그레이션](../../web-sdk/home.md#migrating-to-web-sdk) | 이제 기존 웹 속성을 다른 Experience Cloud 라이브러리(예: [!DNL at.js])에서 웹 SDK으로 한 번에 한 페이지씩 마이그레이션할 수 있습니다. 이렇게 하면 모든 페이지를 한 번에 마이그레이션할 필요 없이 웹 SDK 마이그레이션에 대한 단계별 접근 방식이 활성화됩니다. |
| [[!DNL Adobe Journey Optimizer] 데이터스트림 지원](../../datastreams/overview.md#aep) | 이제 데이터 스트림에 대한 Adobe Experience Platform 서비스에서 [!DNL Adobe Journey Optimizer]을(를) 지원합니다. 이 옵션을 사용하면 [!DNL Adobe Journey Optimizer]에서 웹 및 앱 기반 인바운드 채널을 사용할 수 있습니다. |

{style="table-layout:auto"}

Experience Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| Destination SDK | 이제 Destination SDK은 일괄 처리(또는 파일 기반) 프로덕션 또는 비공개 대상을 만드는 파트너와 고객을 위해 모든 지원을 제공합니다. 자세한 내용은 다음 설명서 페이지를 참조하십시오. <ul><li>[Destination SDK 개요](../../destinations/destination-sdk/overview.md)</li><li>[파일 기반 대상 구성](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[파일 기반 대상에 대한 파일 서식 옵션 구성](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[파일 기반 대상 테스트](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**새 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services은 크로스채널 고객 경험을 디자인할 수 있는 플랫폼과 시각적 캠페인 오케스트레이션, 실시간 상호 작용 관리 및 크로스채널 실행 환경을 제공합니다. [Campaign 시작](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 이 통합은 [Adobe Campaign 버전 8.4 이상](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1)에서 작동합니다. |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | [!DNL Salesforce CRM] 대상이 연락처 및 잠재 고객 업데이트를 모두 지원하고 더 빠른 업데이트를 위한 성능 개선을 지원하도록 업데이트되었습니다. |

{style="table-layout:auto"}

**새로운 설명서 또는 업데이트된 설명서**

| 설명서 | 설명 |
| ----------- | ----------- |
| 대상 플로우 서비스 API 설명서 | 파일 기반 대상에서 작업을 수행하는 방법에 대한 지침을 포함하도록 [대상 API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/destinations/)가 업데이트되었습니다. 스트리밍 대상에 대한 작업은 나중에 추가됩니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 열거형 및 제안 값에 대한 UI 지원 | 이제 데이터 유효성 검사를 활성화하는 열거형 외에도 표준 또는 사용자 지정 문자열 필드에 대해 [제안 값을 추가 또는 제거](../../xdm/ui/fields/enum.md)할 수 있으므로 Experience Platform 사용자는 세그먼트를 만들 때 선택할 수 있는 친근한 값 목록을 가질 수 있습니다. |

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL AJO 분류 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 제안 이벤트가 트리거된 와 상호 작용한 특정 요소의 속성입니다. |
| 필드 그룹 | [[!UICONTROL MediaAnalytics 인터랙션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 시간 경과에 따른 미디어 상호 작용을 추적합니다. |
| 필드 그룹 | [[!UICONTROL 미디어 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 미디어 세부 정보를 추적합니다. |
| 필드 그룹 | [[!UICONTROL Adobe CJM ExperienceEvent - 표면]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Adobe Journey Optimizer의 경험 이벤트에 대한 표면을 설명합니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 비헤이비어 | [[!UICONTROL 시계열]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>`eventType`에 대한 값을 추가했습니다.<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>`eventType`에 대한 값을 제거했습니다.<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 필드 그룹 | (다수) | Journey Orchestration 구성 요소에서 [여러 필드 설명을 업데이트했습니다](https://github.com/adobe/xdm/pull/1628/files). |
| 필드 그룹 | (다수) | [일관성을 위해 여러 Adobe Workfront 구성 요소의 제목을 업데이트했습니다](https://github.com/adobe/xdm/pull/1634/files). |
| 필드 그룹 | [[!UICONTROL AJO 분류 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 여러 필드의 네임스페이스를 `xdm`(으)로 업데이트했습니다. |
| 필드 그룹 | [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 새 필드 `isReadSegmentTriggerStartEvent`을(를) 추가했습니다. |
| 필드 그룹 | [[!UICONTROL 예측된 날씨]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | `xdm:uvIndex` 필드를 정수 유형으로 변경하고 `xdm` 네임스페이스를 누락된 여러 필드에 추가했습니다. |
| 필드 그룹 | [[!UICONTROL 미디어 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 및 `xdm:implementationDetails`이(가) 필드 그룹에서 제거되었습니다. |
| 데이터 유형 | (다수) | 일관성을 위해 여러 데이터 형식에서 [여러 미디어 속성 이름을 업데이트했습니다](https://github.com/adobe/xdm/pull/1626/files). |
| 데이터 유형 | [[!UICONTROL 구현 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 플러터에 대해 알려진 이름이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 관심 영역 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 이제 데이터 형식은 관심 영역과 연결된 메타데이터 키-값 쌍의 목록을 수락할 수 있습니다. |
| 데이터 유형 | [[!UICONTROL 제안 작업]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields]의 이름이 [!UICONTROL 제안 작업]&#x200B;(으)로 바뀌었습니다. |
| 데이터 유형 | [[!UICONTROL 제안 이벤트 유형]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 이름이 [!UICONTROL 제안 작업]&#x200B;(으)로 바뀌었습니다. |
| (다수) | (다수) | 실험 속성이 모든 B2B 구성 요소에서 [안정화되었습니다](https://github.com/adobe/xdm/pull/1617/files). |
| (다수) | (다수) | Adobe Journey Optimizer 엔터티가 [안정화](https://github.com/adobe/xdm/pull/1625/files)되었습니다. |
| (다수) | (다수) | 여러 실험 구성 요소에서 특정 필드의 네임스페이스가 일관성을 위해 [업데이트되었습니다](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 이러한 문제는 고객 데이터가 서로 다른 시스템 간에 분산되어 각 고객이 여러 개의 &quot;ID&quot;를 가지고 있는 것처럼 보이는 경우 더욱 어려워집니다.

Adobe Experience Platform Identity Service를 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객과 고객의 행동을 더 잘 볼 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 삭제 지원 | 이제 ID 서비스가 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI 또는 데이터 위생을 통해 요청할 때 데이터 세트 삭제를 지원합니다. 자세한 내용은 [UI에서 데이터 세트 삭제](../../catalog/datasets/user-guide.md#delete-a-dataset)에 대한 안내서를 참조하십시오. |

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하세요.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 데이터 과학 작업 영역에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고 구독 API | Adobe Experience Platform 쿼리 서비스를 사용하면 애드혹 및 예약된 쿼리 모두에 대한 경고를 구독할 수 있습니다. 경고는 이메일로 받거나 Experience Platform UI 내에서 또는 두 가지 모두로 받을 수 있습니다. 현재 쿼리 경고는 [쿼리 서비스 API](https://developer.adobe.com/experience-platform-apis/references/query-service/)를 사용해야만 구독할 수 있습니다. |
| 데이터 세트 샘플 | 쿼리 서비스 데이터 세트 샘플을 사용하면 쿼리 정확도 비용으로 처리 시간을 크게 단축하면서 빅 데이터에 대한 탐색적 쿼리를 수행할 수 있습니다. 자세한 내용은 [데이터 집합 샘플 가이드](../../query-service/key-concepts/dataset-samples.md)를 참조하세요. |

[!DNL Query Service]에 대한 자세한 내용은 [[!DNL Query Service] 개요](../../query-service/home.md)를 참조하십시오.

자세한 내용은 [쿼리 경고 설명서](../../query-service/api/alert-subscriptions.md)를 참조하세요.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Audience Manager 세그먼트 모집단이 실시간 고객 프로필에 미치는 영향 | 크기 조정 가능한 Audience Manager 세그먼트 모집단의 수집은 Audience Manager 소스를 사용하여 Audience Manager 세그먼트를 Experience Platform에 처음 보낼 때 총 프로필 수에 직접적인 영향을 미칩니다. 즉, 모든 세그먼트를 선택하면 라이선스 사용 권한을 초과하는 프로필 수가 발생할 수 있습니다. 자세한 내용은 [Audience Manager 원본 개요](../../sources/connectors/adobe-applications/audience-manager.md)를 참조하세요. 라이선스 사용에 대한 자세한 내용은 [라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md)에 대한 설명서를 참조하세요. |
| Adobe Campaign Managed Cloud Service 지원 | Adobe Campaign Managed Cloud Service 소스를 사용하여 Adobe Campaign v8.4 게재 및 추적 로그 데이터를 Experience Platform으로 가져옵니다. 자세한 내용은 [UI에서 Adobe Campaign 관리 Cloud Service 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/campaign.md)에 대한 안내서를 참조하십시오. |
| 배치 소스의 온디맨드 수집을 위한 API 지원 | [!DNL Flow Service] API를 사용하여 지정된 데이터 흐름에 대한 임시 흐름 실행을 만들려면 온디맨드 수집을 사용합니다. 만들어진 흐름 실행은 일회성 수집으로 설정해야 합니다. 자세한 내용은 [API를 사용하여 온디맨드 수집에 대한 흐름 실행 만들기](../../sources/tutorials/api/on-demand-ingestion.md)에 대한 안내서를 참조하십시오. |
| 실패한 데이터 흐름을 재시도하기 위한 API 지원은 배치 소스에 대해 실행됩니다 | `re-trigger` 작업을 사용하여 실패한 데이터 흐름을 API를 통해 다시 시도하세요. 자세한 내용은 [API를 사용하여 실패한 데이터 흐름 실행 다시 시도](../../sources/tutorials/api/retry-flows.md)에 대한 안내서를 참조하십시오. |
| [!DNL Google BigQuery] 및 [!DNL Snowflake] 소스에 대한 행 수준 데이터 필터링을 위한 API 지원 | 논리 및 비교 연산자를 사용하여 [!DNL Google BigQuery] 및 [!DNL Snowflake] 원본에 대한 행 수준 데이터를 필터링하십시오. 자세한 내용은 [API를 사용하여 소스의 데이터를 필터링](../../sources/tutorials/api/filter.md)하는 방법에 관한 안내서를 참조하십시오. |

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.
