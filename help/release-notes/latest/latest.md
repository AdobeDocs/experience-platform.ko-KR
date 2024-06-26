---
title: Adobe Experience Platform 릴리스 노트 2024년 6월
description: Adobe Experience Platform의 2024년 6월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: af27ca20b7d611bb6f6b13b57dfc2df1f643a0b6
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 18%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 6월 18일 수요일**

>[!TIP]
>
>[Experience Platform의 AI 지원](https://platform.adobe.com) 을(를) 이제 사용할 수 있습니다. AI Assistant를 사용하여 Adobe 애플리케이션에서 워크플로를 가속화합니다. [자세히 보기](#ai-assistant) 새 기능에 대해 설명합니다.

Adobe Experience Platform의 새로운 기능:

- [AI 어시스턴트](#ai-assistant)
- [Experience Platform API 인증](#authentication-platform-apis)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [ID 서비스](#identity-service)
- [Privacy Service](#privacy)
- [Segmentation Service](#segmentation)
- [사용 사례 플레이북](#use-case-playbooks)

## AI 어시스턴트 {#ai-assistant}

Adobe Experience Platform의 AI Assistant는 Adobe 애플리케이션에서 워크플로를 가속화하는 데 사용할 수 있는 대화형 경험입니다. AI Assistant를 사용하여 제품 지식을 보다 잘 이해하고, 문제를 해결하거나, 정보를 검색하고, 운영 통찰력을 찾을 수 있습니다. AI Assistant는 Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer 및 Customer Journey Analytics을 지원합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Experience Platform의 AI 지원 | 이제 Experience Platform에서 AI Assistant를 사용할 수 있습니다. AI Assistant는 Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer 및 Customer Journey Analytics을 지원합니다. <br> ![Experience Platform의 AI 지원 .](../2024/assets/june/ai-assistant-full.png "Experience Platform의 AI 지원 ."){width="100" zoomable="yes"} <br> 이 기능에 대한 자세한 내용은 [AI Assistant UI 안내서](../../ai-assistant/ui-guide.md). |
| 제품 지식 질문 지원 | [제품 지식](../../ai-assistant/home.md#product-knowledge) 는 Experience League 설명서에 기반을 둔 개념과 주제로, 뾰족한 학습, 개방형 검색 및 문제 해결에 사용할 수 있습니다. 다음과 같은 AI Assistant 제품 지식 질문을 할 수 있습니다. <ul><li>유사 대상은 무엇입니까?</li><li>프로필 풍부성은 어떻게 계산됩니까?</li><li> 데이터가 수집된 후 프로필 활성화 스키마를 삭제할 수 있습니까?</li></ul> |
| [!BADGE 베타]운영 통찰력 질문에 대한 {type=Informative} 지원 | [Operational insights](../../ai-assistant/home.md#operational-insights) 카운트, 조회 및 계보 영향을 포함한 메타데이터 오브젝트에 대해 AI Assistant가 생성하는 답변입니다. Operational insights는 샌드박스 내의 데이터를 보지 않습니다. 다음과 같은 AI Assistant 운영 인사이트 질문을 할 수 있습니다. <ul><li>활성 상태인 대상은 무엇입니까?</li><li>보유한 데이터 세트는 몇 개입니까?</li><li>라이브 여정에 사용되는 대상자를 나열합니다.</li></ul> Operational Insights 는 속성, 대상, 데이터 흐름, 데이터 세트, 대상, 여정, 스키마 및 소스 도메인에서 지원됩니다. |
| AI Assistant 액세스 | Experience Platform, Real-Time CDP 및 Journey Optimizer용 AI 도우미에 액세스하려면 다음을 포함하는 역할에 추가되어야 합니다. **AI Assistant 활성화** 및 **Operational Insights 보기** 사용 권한. 자세한 내용은 [기능 액세스 안내서](../../ai-assistant/access.md). 다음에 대한 Admin Console을 사용해야 합니다. [Customer Journey Analytics에서 액세스](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

AI Assistant에 대한 자세한 내용은 [AI Assistant 개요](../../ai-assistant/home.md).

## Experience Platform API 인증 {#authentication-platform-apis}

액세스 토큰을 얻는 JWT 방법은 이제 새로운 통합에서 더 이상 사용되지 않으며 더 간단한 OAuth 서버 간 인증 방법으로 대체됩니다.<p>![액세스 토큰을 가져오는 새로운 OAuth 인증 방법(강조 표시).](/help/landing/images/api-authentication/oauth-authentication-method.png "액세스 토큰을 가져오는 새로운 OAuth 인증 방법(강조 표시)."){width="100" zoomable="yes"}</p>

JWT 인증 방법을 사용하는 기존 API 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe는 해당 날짜 이전에 기존 통합을 새로운 OAuth 서버 간 방법으로 마이그레이션할 것을 강력히 권장합니다. [ 서비스 계정(JWT) 자격 증명에서 OAuth 서버 간 자격 증명으로 마이그레이션하는 방법](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)에 관한 안내서를 참조하십시오.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하여 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 검증할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 예약된 키워드 목록에 추가 | 데이터 준비 예약 키워드 목록에 다음 단어가 추가되었습니다.<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul> 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 외부 대상을 내보내기 위한 임시 내보내기 API의 개선 사항 | 이제 임시 내보내기 API를 사용하여 외부(사용자 지정 업로드) 대상을 내보낼 수 있습니다. [자세히 보기](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta) 내보내기 배열 지원의 베타 단계에서 지원되는 추가 함수 | 이전에는 대상을 파일 기반 대상으로 활성화하고 계산된 필드 사용을 선택할 때 데이터 준비를 통해 사용할 수 있는 대상 하위 집합을 사용하는 것으로 제한되었습니다. 이제 이러한 제한이 완화되었으며 고객은 대상을 파일 기반 대상으로 내보낼 때 데이터 준비를 통해 사용할 수 있는 모든 기능에 액세스할 수 있습니다. [자세히 보기](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions). |
| 매핑 단계에서 데이터가 있는 필드만 표시 | 이제 프로필 속성을 대상에 매핑할 때 모든 프로필 속성 간에 전환하거나 데이터가 포함된 프로필 속성만 전환할 수 있습니다. 기본적으로 데이터가 있는 필드만 표시됩니다. 다음에 대한 활성화 안내서 참조: [일괄 처리](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 및 [스트리밍](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) 대상 을 참조하십시오. |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

Adobe Experience Platform Identity Service를 사용하여 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 만들고, 이를 통해 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**예정된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE 베타]{type=Informative} ID 그래프 연결 규칙 | Beta 프로그램 참가자는 ID 그래프 연결 규칙을 사용하여 &quot;공유 장치&quot; 및 기타 그래프 축소 시나리오를 방지하여 시스템에서 개인 엔티티 표현을 보장할 수 있습니다. 이 목표를 달성하기 위해 Beta 프로그램 참가자는 개발 샌드박스 환경의 세 가지 기능에 액세스할 수 있습니다. <ul><li>그래프 알고리즘의 작동 방식을 이해하는 그래프 시뮬레이션 도구입니다.</li><li>고유한 네임스페이스 및 네임스페이스 우선 순위를 구성하는 ID 설정 화면입니다.</li><li>수집된 그래프에 대한 통찰력을 얻기 위한 ID 대시보드.</li></ul> 또한 Beta 프로그램에는 프로필 동작 안정성 개선이 포함됩니다. 자세한 내용은 [id 그래프 연결 규칙](../../identity-service/identity-graph-linking-rules/overview.md) 설명서를 참조하십시오. |

{style="table-layout:auto"}

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).

## [!DNL Privacy Service] {#privacy}

몇 가지 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 포함 [!DNL Privacy Service], Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| Adobe Journey Optimizer에 대한 Privacy Service 지원 | 이제 Privacy Service 기능이 삭제 요청을 처리하기 위해 Adobe Journey Optimizer 프로토콜과 호환됩니다. 다음을 참조하십시오. [Adobe Journey Optimizer 개인 정보 보호 요청 문서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) 추가 정보 또는 목록에 대한 Experience Platform 설명서 [Privacy Service과 통합된 Experience Cloud 애플리케이션](../../privacy-service/experience-cloud-apps.md). |

다음을 참조하십시오. [Privacy Service 개요](../../privacy-service/home.md) 를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 시간 제한 업데이트 | &quot;이번 달&quot;과 &quot;올해&quot;의 비헤이비어가 업데이트되었으며 이제 각각 &quot;월간 누계&quot;와 &quot;연간 누계&quot;를 나타냅니다. 이 변경 사항에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 사용 사례 플레이북 {#use-case-playbooks}

[!DNL Use Case Playbooks] 모든 Adobe Experience Platform 고객에게 추가 비용 없이 제공됩니다. 이제 Experience Platform UI에서 사용 사례 플레이북의 풍부한 갤러리에 액세스하려면 다음을 선택할 수 있습니다. **[!UICONTROL 플레이북]** 왼쪽 탐색에서.

[!DNL Use Case Playbooks] Real-time Customer Data Platform 또는 Adobe Journey Optimizer으로 시작할 때 어려움을 극복하는 데 도움이 되도록 설계되었습니다. 안내서를 제공하고, 의도한 사용 사례에 적합한 에셋을 생성할 방법이나 어디서부터 시작해야 할지 확실하지 않더라도 준비가 되면 프로덕션 환경으로 테스트하고 가져올 수 있는 다양한 에셋을 생성합니다.

시작하려면 다음을 읽으십시오. [사용 사례 플레이북 개요](/help/use-case-playbooks/playbooks/overview.md): 인스턴스를 만들고 생성된 에셋을 다른 샌드박스 환경으로 가져오는 방법을 포함하여 플레이북의 기능, 용도 및 엔드투엔드 데모에 대한 개요를 제공합니다.

다양한 사용 사례 플레이북을 실험하고 탐색하기 위해 영감을 주는 샌드박스에 액세스하고 설정하는 방법에 대해 알아보려면 다음을 참조하십시오. [사용 사례 플레이북으로 이동](/help/use-case-playbooks/playbooks/navigate.md) 문서.

에 대해 자세히 알아보기 [!DNL Use Case Playbooks], 다음 설명서 페이지를 참조하십시오.

- 모든 항목의 목록 가져오기 [이용할 수 있는 플레이북](/help/use-case-playbooks/playbooks/playbooks-list.md), 제품별로 그룹화됨(Real-Time CDP 또는 Journey Optimizer).
- 다음에 대해 알아보기 [권한](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 플레이북과 플레이북이 만드는 자산을 사용해야 합니다.
- 이해 [데이터 인식 기능](/help/use-case-playbooks/playbooks/data-awareness.md) 생성된 에셋을 다른 샌드박스 환경에 복제할 수 있습니다.
