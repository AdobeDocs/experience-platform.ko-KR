---
title: Adobe Experience Platform 릴리스 노트 2025년 10월
description: Adobe Experience Platform에 대한 2025년 10월 릴리스 정보입니다.
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 24%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 10월 22일 목요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [Agent Orchestrator](#agent-orchestrator)
- [경고](#alerts)
- [대상](#destinations)
- [Real-Time CDP B2B Edition](#b2b)
- [소스](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator은 Adobe Experience Platform의 새로운 에이전트 레이어입니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Audience 에이전트 | 이제 Audience Agent은 대화형 대상 탐색 및 중복 대상 탐지를 위해 계정 기반 대상을 지원합니다. 자세한 내용은 [Audience 에이전트 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)를 참조하십시오. |

에이전트에 대한 자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/home)를 참조하세요.

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL Alerts] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며 UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 활성화 실패율 경고 | 대상에 대한 새 경고가 추가되었습니다. **활성화 실패율이 임계값을 초과합니다**. 이 경고는 데이터 활성화 중 실패한 레코드 수가 허용된 임계값을 초과하는 경우 사용자에게 알려주므로 활성화 문제에 신속하게 대응할 수 있습니다. 자세한 내용은 [표준 경고 규칙](../../observability/alerts/rules.md)에 대한 설명서를 참조하십시오. |

{style="table-layout:auto"}

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!DNL Adform] | 이 대상을 사용하여 Adobe Real-Time CDP ID(ECID) 및 [!DNL Adform]의 ID Fusion을 기반으로 활성화할 수 있도록 [!DNL Adform]&#x200B;(으)로 Experience Cloud 대상을 보냅니다. [!DNL Adform]의 ID Fusion은 ECID(Experience Cloud ID)를 기반으로 자사 대상을 활성화할 수 있는 ID 확인 서비스입니다. 자세한 내용은 [[!DNL Adform] 설명서](../../destinations/catalog/advertising/adform.md)를 참조하세요 |
| [!DNL Amazon Ads] | 추가 개인 식별자 지원이 추가되었습니다. 여기에는 `firstName`, `lastName`, `street`, `city`, `state`, `zip` 및 `country`과(와) 같은 필드가 포함됩니다. 이러한 필드를 타겟 ID로 매핑하면 대상자 일치율을 향상시킬 수 있습니다. 자세한 내용은 [[!DNL Amazon Ads] 설명서](../../destinations/catalog/advertising/amazon-ads.md)를 참조하세요. |
| [!DNL Snowflake Batch]&#x200B;(제한된 가용성) | 매일 대상자 업데이트를 계정에 공유 테이블로 직접 받으려면 실시간 [!DNL Snowflake] 데이터 공유를 만드십시오. 이 통합은 현재 VA7 지역에 프로비저닝된 고객 조직에서 사용할 수 있습니다. 자세한 내용은 [[!DNL Snowflake Batch] 설명서](../../destinations/catalog/warehouses/snowflake-batch.md)를 참조하세요. |
| [!DNL Snowflake Streaming]&#x200B;(제한된 가용성) | 스트리밍 대상 업데이트를 계정에 공유 테이블로 직접 받으려면 라이브 [!DNL Snowflake] 데이터 공유를 만드십시오. 이 통합은 현재 VA7 지역에 프로비저닝된 고객 조직에서 사용할 수 있습니다. 자세한 내용은 [[!DNL Snowflake Streaming] 설명서](../../destinations/catalog/warehouses/snowflake.md)를 참조하세요. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [대상 수준 모니터링을 지원하는 몇 가지 새로운 대상](../../dataflows/ui/monitor-destinations.md#audience-level-view) | 이제 다음 대상이 대상자 수준 모니터링을 지원합니다. <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] 계정 참여</li><li>[!DNL The Trade Desk]</li></ul> |
| 데이터 세트 내보내기 보호 문제 해결 | 데이터 세트 내보내기 가드레일에 대한 수정 사항이 구현되었습니다. 이전에는 타임스탬프 열이 포함되어 있지만 XDM 경험 이벤트 스키마를 기반으로 하는 _not_&#x200B;인 일부 데이터 세트가 경험 이벤트 데이터 세트로 잘못 처리되어 내보내기가 365일 전환 확인 기간으로 제한되었습니다. 문서화된 365일 전환 확인 가드레일은 이제 경험 이벤트 데이터 세트에만 적용됩니다. XDM 경험 이벤트 스키마 이외의 스키마를 사용하는 데이터 세트는 이제 100억 개의 레코드 가드레일이 제어합니다. 일부 고객은 365일 전환 확인 기간에 잘못 포함된 데이터 세트에 대한 내보내기 횟수가 증가할 수 있습니다. 이를 통해 긴 전환 확인 기간이 있는 예측 워크플로우에 대한 데이터 세트를 내보낼 수 있습니다. 자세한 내용은 [데이터 집합 내보내기 보호](../../destinations/guardrails.md#dataset-exports)를 참조하십시오. |
| 엔터프라이즈 대상에 대한 대상 수준 보고 개선 | 이 릴리스 이후 고객은 선택한 대상과 관련된 대상만 포함하는 더 정확한 대상 보고 번호를 볼 수 있습니다. 이 모니터링 조정을 통해 데이터 흐름에 매핑된 대상자만 보고에 포함되므로 실제 데이터 활성화에 대한 보다 명확한 통찰력을 얻을 수 있습니다. 활성화 중인 데이터 양에는 영향을 주지 않습니다. 보고 정확도를 개선하기 위한 모니터링 개선 사항입니다. |
| 액세스 레이블로 인한 UI 데이터 흐름이 회색으로 표시됨 | 액세스 권한이 없는 대상 데이터 흐름이 완전히 숨겨져서 일부 사용자에게 빈 페이지가 표시되는 문제를 해결하기 위해 이제 UI에 제한된 데이터 흐름을 완전히 생략하는 대신 회색으로 표시됩니다. 자세한 내용은 [액세스 레이블을 사용하여 대상 데이터 흐름에 대한 사용자 액세스를 관리](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know)하는 방법에 대한 설명서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition은 포괄적인 B2B 고객 데이터 관리 기능을 제공하여 조직이 통합된 고객 프로필을 빌드하고, 정교한 B2B 대상자를 생성하며, 다양한 마케팅 채널에서 데이터를 활성화할 수 있도록 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| B2B 엔터티 간의 비표준 관계에 대한 B2B 지원 중단 | 2026년 1월부터 Real-Time CDP B2B edition은 더 이상 B2B 엔터티 간의 **비표준** 관계를 지원하지 않습니다. 따라서 [B2B 네임스페이스 및 스키마 안내서](../../rtcdp/schemas/b2b.md)에 요약된 표준 관계를 사용하도록 B2B 엔터티를 업데이트하는 것이 좋습니다. |

{style="table-layout:auto"}

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 소스에 대한 데이터 세트 생성 변경 | Adobe Analytics과 Experience Platform 간의 데이터 흐름 만들기 프로세스의 일부로 카탈로그 서비스를 통해 데이터 세트가 만들어집니다. 이 데이터 세트는 데이터가 들어오는 컨테이너 역할을 합니다. 현재 이 프로세스에는 Analytics 보고서 세트에서 가져와서 카탈로그 서비스로 보낸 다음 새로 만든 데이터 세트와 연결된 DataSource ID가 포함됩니다. 변경 후에는 데이터 세트를 만드는 동안 더 이상 DataSource ID를 제공하는 옵션을 사용할 수 없습니다. 따라서 Analytics 소스에서 만든 새 데이터 세트에는 더 이상 카탈로그 서비스에서 연결된 데이터 소스 ID가 없습니다. 이 변경 사항은 메타데이터에만 적용되며 데이터 세트의 데이터 저장소를 어떤 방식으로든 변경하지 않습니다. 그러나 카탈로그 서비스에서 제공한 DataSource ID는 Adobe Analytics에 대해 새로 만든 데이터 세트에서 더 이상 사용할 수 없습니다. Adobe Analytics 소스 커넥터에 대한 자세한 내용은 [Adobe Analytics 소스 설명서](../../sources/connectors/adobe-applications/analytics.md)를 참조하십시오. |
| [!DNL Google Ads] 소스의 일반 가용성(API 전용) | [ 소스의  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md)API 버전이 이제 일반 공급 상태입니다. API 설명서에 최신 버전이 이제 `v21`이고 Experience Platform이 모든 버전 v19 이상을 지원함을 반영하여 업데이트했습니다. [UI 버전](../../sources/tutorials/ui/create/advertising/ads.md)은(는) Beta 상태로 유지되며 일회성 수집만 지원합니다. 증분 데이터 수집을 사용하려면 API 경로를 사용합니다. |
| [!DNL Azure Event Hubs] 가상 네트워크 지원 | Adobe은 이제 [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)에 대한 가상 네트워크 연결을 명시적으로 지원하므로 공용 네트워크가 아닌 개인 네트워크를 통해 데이터를 전송할 수 있습니다. 허용 목록에 추가하다 고객은 Experience Platform VNet를 통해 Azure 백본을 통해 개인적으로 이벤트 트래픽을 라우팅하여 데이터 수집 워크플로우에 대한 향상된 보안을 제공할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->