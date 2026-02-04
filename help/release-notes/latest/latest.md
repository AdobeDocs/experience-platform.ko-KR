---
title: Adobe Experience Platform 릴리스 노트 2026년 1월
description: Adobe Experience Platform의 2026년 1월 릴리스 정보.
source-git-commit: f4d5ddc430b0f5b895c1c3ff462c5a79b31956d7
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 21%

---


# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2026년 1월 27일 수요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [Agent Orchestrator](#agent-orchestrator)
- [대상](#destinations)
- [실시간 고객 프로필](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator을 사용하면 워크플로우를 자동화하고 여러 채널에서 고객과 상호 작용할 수 있는 AI 기반 에이전트를 구축하고 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Experience Platform Agents 사용 바인딩된 체험판 | **이제 고객 선택 시 Adobe Experience Platform 에이전트에 무료로 액세스할 수 있습니다**. 체험판을 사용하여 Adobe Experience Platform Agent Orchestrator에서 제공하는 AI Assistant 인터페이스를 통해 에이전트를 탐색하고 상호 작용할 수 있습니다. 이 체험판은 고객의 기존 Experience Cloud 제품 및 환경 컨텍스트 내에서 작동하는 AI 에이전트에 대한 실습 경험을 제공하여 팀이 전체 구매를 약속하기 전에 가치를 평가할 수 있도록 합니다. Adobe Experience Platform 에이전트는 사용자 입력 및 감독에 의해 안내되며 기존 제품 수준 액세스 제어를 준수하여 사용자가 기본 Experience Cloud 애플리케이션 내에서 승인된 작업만 수행하거나 데이터를 볼 수 있도록 합니다. 시작 방법에 대한 자세한 내용은 [Experience Platform 에이전트 사용 제한 평가판 개요](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| 이제 [Kevel 대상](/help/destinations/catalog/advertising/kevel.md) 커넥터를 사용할 수 있습니다. | Adobe Experience Platform용 [!DNL Kevel] 스트리밍 대상을 사용하면 고객이 [!DNL Kevel]의 UserDB 및 세그먼트 관리 API로 직접 Adobe 대상을 활성화하여 광고 결정 시 실시간 타깃팅을 지원할 수 있습니다. [[!DNL Kevel]](https://www.kevel.com/)은(는) 혁신적인 상거래 리더가 소매 미디어를 출시하고, 확장하고, 성공할 수 있도록 지원하는 AI 지원 기술 및 전문가 지침을 제공합니다. [!DNL Kevel]의 Retail Media Cloud는 온사이트 및 오프사이트 광고를 위한 타깃팅되고, 귀속되며, 사용자 지정 가능한 광고 형식을 지원합니다. |
| 이제 [인덱스 교환 대상](/help/destinations/catalog/advertising/index-exchange.md) 커넥터를 사용할 수 있습니다. | 이 대상 커넥터를 사용하여 Adobe Experience Platform의 대상 세그먼트를 [!DNL Index Exchange]의 프로그래밍 방식 광고 플랫폼으로 직접 내보냅니다. [!DNL Index]은(는) 미디어 소유자가 모든 화면에서 콘텐츠의 가치를 극대화할 수 있도록 지원하는 글로벌 광고 공급측 플랫폼입니다. 20년 이상의 업계 리더십 덕분에 [!DNL Index]은(는) 세계 최대 브랜드와 프리미엄 경험 메이커를 연결하여 고품질의 소비자 경험을 제공합니다. |
| 브레이즈 연결에 대한 지역 엔드포인트 지원 | 이제 대상 구성 흐름 동안 [에서 지원하는 모든 ](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)지역별 끝점[!DNL Braze]을 선택할 수 있습니다. 사용해야 하는 끝점 인스턴스를 [!DNL Braze] 담당자에게 문의하십시오. |
| [Liveramp 온보딩](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling)에 대한 주별 및 월별 예약 지원 | 이제 Liveramp 온보딩 대상에 대한 주별 및 월별 내보내기 일정을 구성할 수 있습니다. <br> 이 릴리스는 점진적으로 출시되고 있으며 1월 30일까지 완료될 예정입니다. |
| [트레이드 데스크](../../destinations/catalog/advertising/tradedesk.md) 및 [Microsoft Bing](../../destinations/catalog/advertising/bing.md) 대상에 대한 활성화 경험이 개선되었습니다. | 이제 Trade Desk 및 Microsoft Bing 대상에 최적화된 활성화 경험을 위한 사전 정의된 필수 매핑이 포함됩니다.  <br> 이 릴리스는 점진적으로 출시되고 있으며 1월 30일까지 완료될 예정입니다. ![Trade Desk에 대해 미리 정의된 매핑을 보여 주는 이미지](../2026/assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![Microsoft Bing에 대해 미리 정의된 매핑을 보여 주는 이미지](../2026/assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| [트레이드 데스크 - CRM](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) 연결에 대한 전화 번호 활성화 지원 | 트레이드 데스크 - CRM 대상은 이제 이메일 주소 외에 전화 번호 활성화를 지원합니다. CRM 데이터를 기반으로 대상 타기팅 및 제거를 위해 E.164 형식의 해시된 전화번호와 Trade Desk 계정의 해시된 전화번호(SHA256_E.164 형식)를 모두 활성화할 수 있습니다. 활성화하기 전에 전화 번호를 E.164 형식으로 표준화해야 합니다. |
| [Snowflake 일괄 처리](../../destinations/catalog/warehouses/snowflake-batch.md) 대상 업데이트 | 이제 Snowflake 배치 대상에 대상 구성 중 영역 선택 기능이 포함됩니다. 이제 인스턴스가 프로비저닝되는 특정 Snowflake 지역을 선택하여 최적의 데이터 전송을 보장하고 지역 요구 사항을 준수할 수 있습니다. 또한 기본 병합 정책 제한이 제거되어 병합 정책에 매핑된 대상자를 내보낼 수 있습니다. <br> [!DNL Snowflake] 일괄 처리 대상은 현재 Experience Platform VA7 지역에서 프로비저닝된 Real-Time CDP 고객만 사용할 수 있습니다. |

<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <ul><li>**[!UICONTROL Default]**: Data will be encrypted at rest with the default encryption algorithm set on your bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest with the AES256 algorithm when it lands in S3. **This option takes precedence over any default encryption algorithm configured on your S3 bucket**.</li></ul> This release is being rolled out gradually and will be complete by January 30th.| -->

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 대상에 대한 보호 제한을 업데이트했습니다. | 단일 Adobe Target 대상에 매핑할 수 있는 최대 대상 수가 50개에서 250개로 증가했습니다. 이렇게 하면 Adobe Target이 다른 대상에 대한 표준 대상 제한에 맞춰 조정되므로 대상 활성화 워크플로우에 더 많은 유연성을 제공합니다. 이제 여러 데이터 흐름을 만들지 않고도 Adobe Target 대상에 대해 더 많은 대상을 활성화할 수 있습니다. |
| [대상 편집](/help/destinations/ui/edit-destination.md) 및 [마케팅 작업 편집](/help/destinations/ui/edit-activation.md#edit-marketing-actions) 일반 가용성 | 이제 모든 사용자가 대상 및 마케팅 작업을 편집하는 옵션을 사용할 수 있습니다. |
| 매핑 [단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서 필드 표시 이름 전환 | 이제 스키마 필드를 대상에 매핑할 때 전체 XDM 필드 이름을 표시하는 것과 표시 이름만 표시하는 것 간을 전환할 수 있습니다. <br> ![표시 이름 전환을 보여 주는 화면 기록입니다.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#real-time-customer-profile}

실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [스트리밍 용량](/help/landing/license-usage-and-guardrails/capacity.md) 적용 | 이제 Experience Platform에서는 실시간 고객 프로필 및 ID 서비스를 위해 스트리밍 처리량 기능을 적용합니다. 고객이 계약된 스트리밍 용량을 초과하면 데이터는 선입선출 방식으로 큐에 올라가 처리됩니다. 이를 통해 예측 가능한 시스템 성능을 보장하고 용량 위반이 데이터 수집 품질에 영향을 미치지 않도록 할 수 있습니다. 중요 참고 사항: <ul><li>용량을 초과하면 데이터 레이크에서 스트리밍 업데이트를 사용할 수 없습니다.</li><li>이 적용은 Adobe Journey Optimizer 라이선스가 있는 고객에게는 적용되지 않습니다</li><li>용량이 사용 가능해지면 큐에 있는 데이터가 순차적으로 처리됩니다.</li></ul> 자세한 내용은 [용량 개요](/help/landing/license-usage-and-guardrails/capacity.md)를 참조하십시오. |
| 엔티티 조회 사용 중단 | 이제 모든 Real-Time CDP Prime 고객이 경험 이벤트에 엔티티 조회 API를 더 이상 사용할 수 없습니다. 이러한 사용 중단은 Real-Time CDP을 라이선스 기능에 맞게 조정하는 데 도움이 됩니다. 이 기능을 사용하려는 Real-Time CDP Ultimate 고객은 Adobe 고객 지원 센터에 문의하여 이 기능을 다시 활성화할 수 있습니다.  자세한 내용은 [엔터티 API 안내서](/help/profile/api/entities.md)를 참조하십시오. |
| 프로필 수집 작업 상태 모니터링 | 이제 일괄 프로필 수집 데이터 흐름 실행에 대한 작업 수준 진행률을 모니터링할 수 있습니다. 이 기능은 고객 세분화 및 Adobe Journey Optimizer 조회를 위해 수집이 준비되었는지 여부를 나타내는 중요한 체크포인트를 포함하여 일괄 처리 수집 작업의 현재 진행 상황을 실시간으로 보여 줍니다. 처리하는 데 몇 시간이 걸릴 수 있는 대용량 수집의 경우 이러한 진행 투명성을 통해 작업이 정상적으로 진행되고 있는지 또는 문제가 발생하는지 파악하여 데이터 처리 중 불확실성을 줄일 수 있습니다. 자세한 내용은 [프로필 모니터링 가이드](/help/dataflows/ui/monitor-profiles.md)를 참조하세요. |
| 프로필 뷰어 개선 사항(GA) | 이제 프로필 뷰어에 대한 다음과 같은 개선 사항을 일반적으로 사용할 수 있습니다. <ul><li>**결합된 보기**: 속성, 이벤트 및 인사이트가 단일 보기로 결합되었습니다.</li><li>**AI 생성 인사이트**: 이제 프로필 세부 정보 페이지에 AI 생성 인사이트가 표시되어 프로필에서 생성된 세부 사항을 알 수 있습니다. 이러한 인사이트에는 성향 점수 및 추세 분석과 같은 정보가 포함될 수 있습니다.</li><li>**스타일 업데이트**: 프로필 세부 정보 페이지가 시각적으로 새로 고쳐졌습니다.</li><li>**찾아보기**: 이제 검색 및 사용자 정의 기능이 있는 대화형 카드 기반 캐러셀을 통해 프로필을 탐색할 수 있습니다.</li></ul> 자세한 내용은 [프로필 뷰어 안내서](/help/profile/ui/user-guide.md)를 참조하세요. |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Real-Time Customer Profile] 개요](../../profile/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 외부 대상 데이터 만료 새로 고침 | 이제 외부 대상(예: CSV 업로드)은 데이터 만료 설정에 대한 강제 새로 고침 기능을 지원합니다. 이 기능을 사용하면 외부 대상에 대한 데이터 만료를 수동으로 새로 고칠 수 있으므로 대상 라이프사이클 관리를 보다 효과적으로 제어할 수 있습니다. 이 기능은 초기 데이터 만료 기간 이후에도 유지해야 하거나 데이터를 다시 업로드하지 않고 다시 활성화해야 하는 대상에 특히 유용합니다. 이 기능에 대한 자세한 내용은 [Audience Portal 개요](../../segmentation/ui/audience-portal.md#audience-summary)를 참조하십시오. |
| 대상 유효성 검사 | Experience Platform은 이제 대상의 정확성, 안정성, 확장성을 보장하기 위한 내장된 유효성 검사를 제공합니다. 이러한 검사는 대상 정의를 만드는 동안 자동으로 실시간으로 실행됩니다. 자세한 내용은 [대상 유효성 검사 개요](/help/segmentation/validation.md)를 참조하십시오. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2 원본 | 이제 새 [!DNL Oracle Eloqua] 소스 커넥터를 사용할 수 있습니다. [사용되지 않는 커넥터](/help/sources/connectors/marketing-automation/oracle-eloqua.md)를 바꿉니다. 이 업데이트된 커넥터는 [!DNL Oracle Eloqua]에서 Experience Platform으로 데이터를 수집하기 위한 향상된 기능과 향상된 안정성을 제공합니다. 기존 연결이 더 이상 작동하지 않으므로 기존 커넥터를 사용하는 고객은 새 구현으로 마이그레이션해야 합니다. 새 커넥터는 [!DNL Oracle Eloqua]에 연결하고 마케팅 자동화 데이터를 수집하는 데 필요한 모든 설정 및 구성 단계를 지원합니다. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2 원본 | 이제 새 [!DNL Salesforce Marketing Cloud] 소스 커넥터를 사용할 수 있습니다. [사용되지 않는 커넥터](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md)를 바꿉니다. 이 업데이트된 커넥터는 [!DNL Salesforce Marketing Cloud]에서 Experience Platform으로 데이터를 수집하기 위한 향상된 성능과 추가 기능을 제공합니다. 기존 커넥터를 사용하는 고객은 새 구현으로 전환해야 합니다. 새 커넥터에는 [!DNL Salesforce Marketing Cloud]에 연결하고 마케팅 자동화 데이터를 수집하기 위한 포괄적인 설정 지침이 포함되어 있습니다. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

