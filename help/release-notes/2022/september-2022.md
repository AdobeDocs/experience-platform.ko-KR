---
title: Adobe Experience Platform 릴리스 노트 - 2022년 9월
description: Adobe Experience Platform에 대한 2022년 9월 릴리스 노트입니다.
source-git-commit: a3f12b9524d393441923cd11e09ed3e406814691
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 9월 28일**

Adobe Experience Platform의 기존 기능 업데이트:

- [XDM(경험 데이터 모델)](#xdm)
- [ID 서비스](#identity-service)
- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [소스](#sources)

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

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

마케팅 분석가 및 전문가가 AI/ML 서비스를 통해 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 모델을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 사용하면 마케팅 분석가가 구성 중에 모델 구성을 초안 인스턴스로 저장하고 교육 및 점수 책정 전에 완료될 때까지 초안을 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 포함되지만, 제한되어 있지는 않습니다. 구성 워크플로우에서 정의할 필드가 여러 개 있는 경우 한 번의 이동으로 완료할 수 없거나, 하나 이상의 데이터 세트 통계(예: 열 완전성)가 사용되기 전에 처리하는 데 시간이 걸릴 수 있습니다. 다음 문서를 참조하십시오. [Attribution AI 사용 안내서](../../intelligent-services/attribution-ai/user-guide.md) 추가 정보 |
| 거버넌스 정책 | 사용자가 구성 워크플로우를 통해 인스턴스를 생성하도록 제출한 후 새 정책 적용 서비스는 데이터 사용에 대한 정책 위반이 있는지 확인하고 팝오버에 세부 정보를 표시합니다. 이렇게 하면 데이터 작업 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하게 됩니다. |

Attribution AI에 대한 자세한 내용은 [Attribution AI 개요](../../intelligent-services/attribution-ai/overview.md). 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md).

### 고객 AI

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다.

| 기능 | 설명 |
| --- | --- |
| 초안 인스턴스 저장 | 이 새로운 기능을 사용하면 마케팅 분석가가 구성 중에 모델 구성을 초안 인스턴스로 저장하고 교육 및 점수 책정 전에 완료될 때까지 초안을 계속 편집할 수 있습니다. 이 기능이 유용한 시나리오에는 포함되지만, 제한되어 있지는 않습니다. 구성 워크플로우에서 정의할 필드가 여러 개 있는 경우 한 번의 이동으로 완료할 수 없거나, 하나 이상의 데이터 세트 통계(예: 열 완전성)가 사용되기 전에 처리하는 데 시간이 걸릴 수 있습니다. 다음 문서를 참조하십시오. [Customer AI 사용 안내서](../../intelligent-services/customer-ai/user-guide/configure.md) 추가 정보 |
| 거버넌스 정책 | 사용자가 구성 워크플로우를 통해 인스턴스를 생성하도록 제출한 후 새 정책 적용 서비스는 데이터 사용에 대한 정책 위반이 있는지 확인하고 팝오버에 세부 정보를 표시합니다. 이렇게 하면 데이터 작업 및 마케팅 작업이 Adobe Experience Platform에 구성된 데이터 사용 정책을 준수하게 됩니다. |

Customer AI에 대한 자세한 내용은 [Customer AI 개요](../../intelligent-services/customer-ai/overview.md). 데이터 거버넌스 정책에 대한 자세한 내용은 [정책 개요](../../data-governance/policies/overview.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Audience Manager 세그먼트 모집단이 실시간 고객 프로필에 미치는 영향 | 크기 조정 가능한 Audience Manager 세그먼트 모집단을 수집하면 Audience Manager 소스를 사용하여 처음 Audience Manager 세그먼트를 Platform으로 보낼 때 총 프로필 수에 직접적인 영향을 줍니다. 즉, 모든 세그먼트를 선택하면 라이센스 사용 권한을 초과하는 프로필 수가 발생할 수 있습니다. 자세한 내용은 [Audience Manager 소스 개요](../../sources/connectors/adobe-applications/audience-manager.md). 라이센스 사용에 대한 자세한 내용은 [라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).