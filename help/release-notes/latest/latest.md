---
title: Adobe Experience Platform 릴리스 정보 2025년 8월
description: Adobe Experience Platform의 2025년 8월 릴리스 정보입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ac180f045dd3cc7e8ad9de702a3672630d668ee5
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 40%

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

**릴리스 일자: 2025년 9월 23일 수요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [Agent Orchestrator](#agent-orchestrator)
- [경고](#alerts)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [실시간 고객 프로필](#profile)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator은 Adobe Experience Platform의 새로운 에이전트 계층입니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator은 Adobe Experience Platform의 새로운 에이전트 계층입니다. 플랫폼의 풍부한 데이터와 고객 지식을 활용하도록 설계된 Experience Platform Agent Orchestrator은 특별히 설계된 전문 Adobe Experience Platform 에이전트 뒤에 숨겨진 정보와 추론을 강화하여 복잡한 의사 결정 및 문제 해결 작업을 사람의 감독 하에 신속하고 규모에 맞게 실행할 수 있도록 합니다. AI 어시스턴트와 같은 대화 인터페이스에서 자연어를 통해 질문을 하거나 도움을 요청하면 Agent Orchestrator이 전문 에이전트에게 자동으로 전화를 걸어 정확한 답변을 얻을 수 있다. Agent Orchestrator은 대화 기록을 기억하여, 맥락을 반복하지 않고 자연스럽게 이전 질문을 기반으로 할 수 있으며, 여러 에이전트의 통찰력을 결합하여 명확하고 통합된 응답을 제공합니다. 자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하세요. |
| Audience Agent | Audience Agent을 사용하면 중요한 대상 크기 변경 감지, 중복 대상 감지, 대상 인벤토리 탐색 및 대상 크기 검색을 포함하여 대상에 대한 인사이트를 볼 수 있습니다. 자세한 내용은 [Audience Agent 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)를 참조하세요. |

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home)를 참조하세요.

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며, 원하는 경우 UI 자체 또는 이메일 알림을 통해 알림 메시지를 수신할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필 수집 경고 스트리밍 | 이제 데이터 흐름 수준에서 스트리밍 수집을 위한 두 개의 새 경고를 구독할 수 있습니다. <ul><li>스트리밍 수집 실패율 초과</li><li>스트리밍 수집 건너뛰기 비율 초과</li></ul> 플랫폼 내 또는 이메일 경고는 기본 임계값 또는 사용자가 정의한 사용자 지정 임계값에 대한 임계값이 초과되면 알려줍니다. 자세한 내용은 [프로필 경고](../../observability/alerts/rules.md#profile) 안내서를 참조하십시오. |

{style="table-layout:auto"}

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) 커넥터 | 이제 새로운 [!DNL Snowflake Batch] 커넥터를 사용할 수 있으며, 특정 사용 사례에 대해 스트리밍 커넥터에 대한 대안을 제공합니다. |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) 암호화 지원 | 이제 RSA 형식의 공개 키를 연결하여 내보낸 파일을 암호화할 수 있으므로 다른 클라우드 스토리지 대상이 중요한 정보를 제공하는 것과 동일한 수준의 보안을 제공합니다. |
| [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) 대상에 대한 인증 만료 세부 정보 | [!DNL Pinterest] 대상에 대한 인증 만료 정보가 이제 Experience Platform 인터페이스에 직접 표시되므로 데이터 흐름이 중단되기 전에 인증이 만료되고 갱신되는 시점을 확인할 수 있습니다. **[[!UICONTROL 계정]](../../destinations/ui/destinations-workspace.md#accounts)** 또는 **[[!UICONTROL 찾아보기]](../../destinations/ui/destinations-workspace.md#browse)** 탭의 **[!UICONTROL 계정 만료 일자]** 열에서 토큰 만료 일자를 모니터링할 수 있습니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Experience Platform UI의 향상된 대상 관리 기능 | [[!UICONTROL 찾아보기]](../../destinations/ui/destinations-workspace.md#browse) 및 [[!UICONTROL 계정]](../../destinations/ui/destinations-workspace.md#accounts) 탭에서 새로운 정렬 기능을 사용하여 대상 관리 워크플로를 개선합니다. 이제 계정 인증이 곧 만료될 때 시각적 표시기도 볼 수 있습니다. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| 영구 열 너비 설정 | 이제 페이지에서 멀리 이동하여 다시 열 너비로 설정하면 열 너비가 유지됩니다. 예를 들어 [[!UICONTROL 찾아보기]](../../destinations/ui/destinations-workspace.md#browse) 탭에서 열 너비를 조정하면 다른 곳으로 이동하여 해당 탭으로 돌아갈 때 사용자 지정 열 너비가 동일하게 유지됩니다. |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform에 가져온 데이터에 대한 공통 구조와 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 모델 기반 스키마 | 모델 기반 스키마를 사용하여 데이터 모델링을 간소화하십시오. 이제 포괄적인 방법 예제와 지침을 통해 스키마를 더 쉽게 만들 수 있습니다. 이 기능은 현재 Campaign Orchestration 라이선스 소유자가 사용할 수 있으며 GA 시점에 데이터 Distiller 고객으로 확장되어 데이터 모델링에 더 쉽게 액세스하고 효율적으로 작업할 수 있습니다. 이 기능에는 시계열 데이터 및 변경 데이터 캡처 기능에 대한 지원이 포함됩니다. |
| Data Mirror | 모델 기반 스키마를 사용하여 클라우드 데이터 웨어하우스(예: Snowflake, Databricks, BigQuery)의 행 수준 변경 사항을 Adobe Experience Platform으로 수집합니다. Data Mirror은 기존 데이터베이스 구조를 데이터 레이크에 직접 미러링하여 업스트림 ETL을 제거하고 관계, 버전 관리 및 삭제를 유지합니다. 변경 데이터 캡처 기능이 있는 시계열 및 레코드 이벤트 스키마 동작이 모두 지원됩니다. 이 기능은 현재 Campaign Orchestration 라이선스 소유자에 대해 사용할 수 있으며 Customer Journey Analytics 고객을 포함하여 이번 제한된 릴리스를 통해 확장될 예정입니다. 자세한 내용은 [Data Mirror 설명서](../../xdm/data-mirror/overview.md)를 참조하세요. 액세스하려면 Adobe 담당자에게 문의하십시오. |

자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 뷰어 개선 사항 | 2025년 9월 릴리스에는 프로필 뷰어에 대한 다음과 같은 개선 사항이 포함됩니다. <ul><li>**보기 결합**: 특성, 이벤트 및 인사이트가 단일 보기로 결합되었습니다.</li><li>**AI 생성 인사이트**: 이제 프로필 세부 정보 페이지에 AI 생성 인사이트가 표시되어 프로필에서 생성된 세부 정보를 알 수 있습니다. 이러한 통찰력에는 성향 점수 및 트렌드 분석과 같은 정보가 포함될 수 있습니다.</li><li>**스타일 업데이트**: 프로필 세부 정보 페이지가 시각적으로 새로 고쳐졌습니다.</li><li>**찾아보기**: 이제 검색 및 사용자 지정이 포함된 대화형 카드 기반 캐러셀을 통해 프로필을 탐색할 수 있습니다.</li></ul> |

자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하세요.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 경험 이벤트 사용 중단이 있는 계정 대상자 | B2B 아키텍처 업그레이드 이후 경험 이벤트가 있는 계정 대상은 더 이상 지원되지 않습니다. 대신, 새로운 세그먼트 세그먼트 접근 방식을 사용하십시오. 경험 이벤트로 사람 대상을 만든 다음, 계정 대상을 만들 때 해당 사람 대상을 참조하십시오. 이렇게 하면 B2B 대상 만들기에 대한 보다 유연하고 유지 관리할 수 있는 접근 방식이 제공됩니다. |

**중요 업데이트**

| 업데이트 | 설명 |
| ------- | ----------- |
| 대상자 예상 자동 새로 고침 되돌리기 | 대상자 추정에 대한 자동 새로 고침 개선 사항이 되돌려졌습니다. 대상자 예상은 세그먼트 빌더 내에서 계속 생성되지만 자동 새로 고침 기능은 제거되었습니다. |
| 외부 대상 | 9월 30일부터 세그먼트 빌더에서 통합 검색을 통해 외부 대상자를 검색합니다. 세그먼트 일치 를 사용하는 경우 세그먼트 빌더 내에서 이전 경험을 활성화할 수 있습니다. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 일반 가용성의 새로운 소스 | 이제 다음 소스가 GA에 포함되었습니다. 여러 소스 커넥터가 Beta에서 GA로 업데이트되었습니다. <ul><li>[Acxiom 데이터 수집](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom 잠재 고객 데이터 수집](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. 이러한 소스는 이제 완전히 지원되며 프로덕션 용도로 사용할 수 있습니다. |
| [!DNL Snowflake] 키 쌍 인증 지원 | 키 쌍 인증을 지원하여 Snowflake 연결에 대한 보안을 개선했습니다. 기본 인증(사용자 이름/암호)은 2025년 11월까지 더 이상 사용되지 않으므로, 고객은 개선된 보안을 위해 키 쌍 인증으로 마이그레이션하는 것이 좋습니다. 자세한 내용은 [[!DNL Snowflake] 설명서](../../sources/connectors/databases/snowflake.md)를 참조하세요. |
| 소스에서의 비공개 링크 지원 일반 가용성 | 이제 선택한 소스 그룹에 **개인 링크**&#x200B;를 사용할 수 있습니다. 이 기능을 사용하면 소스가 연결할 수 있는 비공개 엔드포인트를 만들 수 있습니다. 비공개 엔드포인트를 사용하면 공용 인터넷을 우회하는 연결과 데이터 흐름을 설정하여 중요한 데이터에 대한 보안을 강화하고 네트워크를 격리할 수 있습니다. 비공개 링크에 대한 지원은 다음 소스에서 사용할 수 있습니다. <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. 자세한 내용은 API에서 [개인 링크 만들기](../../sources/tutorials/api/private-link.md) 및 UI에서 [개인 링크 만들기](../../sources/tutorials/ui/private-link.md)에 대한 안내서를 참조하십시오. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

<!--
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Use the [[!DNL Capillary Streaming Events] source](../../sources/connectors/loyalty/capillary.md) to stream loyalty data from your [!DNL Capillary] account to Experience Platform. |
-->