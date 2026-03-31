---
title: Adobe Experience Platform 릴리스 노트 2026년 3월
description: Adobe Experience Platform의 2026년 3월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: cd09f9e510052f6bae89ff730ba83aa16e95f193
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 19%

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

**릴리스 일자: 2026년 3월 24일 수요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [고급 데이터 라이프사이클 관리](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [용량](#capacity)
- [데이터스트림](#datastreams)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [실시간 고객 프로필](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 고급 데이터 라이프사이클 관리 {#advanced-data-lifecycle-management}

Experience Platform은 소비자 레코드 및 데이터 세트에 대한 프로그래밍 방식 삭제를 통해 저장된 데이터를 관리하는 데 도움이 되는 일련의 데이터 위생 기능을 제공합니다. UI에서 데이터 라이프사이클 작업 공간 또는 데이터 위생 API 호출을 사용하면 데이터 저장소를 효과적으로 관리할 수 있습니다. 이들 기능을 사용하면 정보를 의도대로 사용하고 정확하지 않은 데이터를 수정해야 할 때 업데이트하며 조직 정책에 따라 필요한 경우 삭제할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 다중 데이터 세트 레코드 삭제(API만 해당) | 단일 API 요청에서 하나, 여러 데이터 세트 또는 모든 데이터 세트에서 ID를 삭제하여 데이터 위생 워크플로우를 간소화합니다. 데이터 레이크 레코드를 변경하지 않고 프로필 서비스로만 삭제를 제한할 수도 있습니다. 자세한 내용은 [작업 주문 기록 삭제 가이드](../../hygiene/api/workorder.md)를 참조하세요. |

{style="table-layout:auto"}

자세한 내용은 [고급 데이터 라이프사이클 관리 개요](../../hygiene/home.md)를 참조하십시오.

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator을 사용하여 워크플로우를 자동화하고 여러 채널에서 고객과 상호 작용하는 AI 기반 에이전트를 구축하고 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [Adobe Marketing Agent for [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | [!DNL Microsoft 365 Copilot]용 Adobe Marketing Agent은 Adobe의 마케팅 인텔리전스를 [!DNL Teams], [!DNL Word], [!DNL PowerPoint] 및 기타 [!DNL Microsoft 365] 앱과 같은 일상적인 도구에 직접 가져오는 임베드된 에이전트입니다. [!DNL Microsoft 365] 워크플로를 종료하지 않고 캠페인을 계획하고, 대상을 검토하고, 동료와 협력하여 고객 질문에 답변하고, 데이터에 기반한 결정을 내리는 동안 이 에이전트를 사용하여 Adobe 애플리케이션에서 신뢰할 수 있는 캠페인 인사이트를 가져올 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하십시오.

## 용량 {#capacity}

용량은 조직의 [보호 기능](../../rtcdp/guardrails/overview.md)을 종합적으로 볼 수 있으며, 샌드박스 수준에서 용량을 할당하여 잠재적인 용량 위반을 해결하는 방법에 대한 권장 사항을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 에지 세분화 처리량 | 이제 에지 세그멘테이션 처리량과 관련된 보호 기능을 확인하고 관리할 수 있습니다. 자세한 내용은 [용량 개요](/help/landing/license-usage-and-guardrails/capacity.md#edge-segmentation-throughput)를 참조하십시오. |
| 에지 데이터스트림 모니터링 지원 | 이제 에지 데이터스트림에 대한 실시간 모니터링을 사용할 수 있으므로 처리량 및 기타 지표에 투명성을 제공합니다. 자세한 내용은 [Monitoring Edge 안내서](/help/dataflows/ui/monitor-edge.md)를 참조하십시오. |

## 데이터스트림 {#datastreams}

데이터 스트림은 Adobe Experience Platform 웹 및 모바일 SDK와 Adobe Experience Platform Edge Network Server API를 구현할 때의 서버측 구성을 나타냅니다. SDK의 데이터 스트림 구성 명령은 클라이언트가 상호 작용하는 모든 서비스를 처리합니다.

| 기능 | 설명 |
| --- | --- |
| 동적 데이터 스트림 구성 일반 가용성 | 이제 동적 데이터 스트림 구성을 일반적으로 사용할 수 있습니다. 동적 데이터스트림 구성을 사용하면 데이터스트림에 대해 활성화된 각 서비스에 대해 사용자가 구성할 수 있는 규칙 세트를 정의할 수 있습니다. 이는 각 데이터 유형을 받아야 하는 Experience Cloud 솔루션을 지정합니다. 자세한 내용은 [동적 데이터 스트림 구성 가이드](../../datastreams/configure-dynamic-datastream.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [데이터스트림 개요](../../datastreams/overview.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]은(는) 대상 플랫폼과 미리 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화합니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [Snowflake 일괄 처리](../../destinations/catalog/warehouses/snowflake-batch.md) 영역 선택기 | 이제 검색과 드롭다운을 하나의 컨트롤로 결합한 새로운 검색 가능 드롭다운을 사용하여 영역을 보다 쉽게 찾을 수 있습니다. 이 업데이트는 3월 말까지 배포됩니다. |
| [Snowflake 일괄 처리](../../destinations/catalog/warehouses/snowflake-batch.md) 대상에 대한 새 테이블 구조 | 이제 Snowflake 계정에 공유된 테이블에 별도의 대상 이름 및 대상 원본 열을 포함하는 새 구조가 있습니다. 새 테이블 구조는 앞으로 설정된 모든 새 대상 연결에 적용됩니다. 설정한 새 연결의 경우 두 테이블 구조가 모두 생성됩니다. 새 구조의 접두사는 V2이고 이전 구조는 2026년 6월 말까지 유지되며 그 이후에는 더 이상 사용되지 않습니다. Snowflake 일괄 처리 설명서의 [내보낸 데이터](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) 섹션에서 자세히 알아보십시오. 이 업데이트는 3월 말까지 배포됩니다. |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md) 연결 | 새 Adobe Advertising DSP 연결은 레거시 연결과 동일한 기능을 제공하며 추가 ID를 지원합니다. 새 커넥터를 사용하면 쿠키 기반 ID를 Adobe Advertising DSP으로 내보낼 수도 있습니다. |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md) 연결 | FreeWheel 거래 및 CTV, 비디오 및 디스플레이 전반에 걸친 캠페인에서 타깃팅할 수 있도록 [!DNL Real-Time CDP]명의 대상자를 매일 일괄 처리 파일로 FreeWheel에 보냅니다. 액세스하려면 Adobe 계정 팀에 문의하십시오. |
| [트레이드 데스크 CRM](../../destinations/catalog/advertising/tradedesk-emails.md) 및 [Pinterest](../../destinations/catalog/advertising/pinterest.md)에 대한 외부 대상 지원 | 이제 세분화 서비스를 넘어 트레이드 데스크 CRM, 크리터 및 Pinterest으로의 기원에서 대상을 활성화할 수 있습니다. 여기에는 사용자 지정 업로드 대상(CSV에서 가져옴), 유사 대상, 페더레이션 대상 및 [!DNL Adobe Journey Optimizer] 등의 다른 Experience Platform 앱에서 만든 대상이 포함됩니다. 이 업데이트는 3월 말까지 배포됩니다. 자세한 내용은 각 대상의 카탈로그 페이지에서 [지원되는 대상](../../destinations/catalog/advertising/criteo.md#supported-audiences) 섹션을 참조하십시오. |
| 사용자 지정 업로드 대상에 대한 제한 늘림 | 이제 대상 인스턴스당 최대 20개의 사용자 지정 업로드 대상을 활성화할 수 있습니다. 이전에는 이 제한이 10개였습니다. 자세한 내용은 [대상 보호 기능](../../destinations/guardrails.md#batch-file-based-activation)을 참조하세요. |
| 외부 대상에 대해 [지금 파일 내보내기](../../destinations/ui/export-file-now.md) 및 [임시 활성화 API](../../destinations/api/ad-hoc-activation-api.md) 지원 | 이제 파일 기반 대상 일괄 처리를 활성화할 때 외부 대상(예: 사용자 지정 업로드, 유사, 페더레이션 및 다른 Experience Platform 앱의 대상)과 함께 UI(파일 내보내기) 및 임시 활성화 API를 사용할 수 있습니다. 이 업데이트는 3월 말까지 배포됩니다. |
| OAuth 2 및 mTLS가 있는 [HTTP API](../../destinations/catalog/streaming/http-destination.md) 대상 | 이제 인증 끝점에 상호 TLS(mTLS)가 필요한 경우 OAuth 2를 사용하는 HTTP API 대상을 만들고 인증할 수 있습니다. 대상 설정 중 토큰 검색은 이제 mTLS를 지원합니다. 이 업데이트는 3월 말까지 배포됩니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항**

| 변수 이름이 아니라, 필터링된 보고서의 머리글로 잘못 표시하는 | 설명 |
| --- | --- |
| [TikTok](../../destinations/catalog/social/tiktok.md) 커넥터 전화 번호 해싱 | 대상 카드에서 잘못 구성되면 전화 번호에서 처리된 ID가 TikTok에 활성화되지 않는 문제가 해결되었습니다. 이 수정 사항의 이점을 얻으려면 새 활성화 흐름을 설정하거나 기존 흐름에서 전화번호 매핑을 제거하고 저장한 다음 다시 추가하십시오. |
| [Snowflake 스트리밍](../../destinations/catalog/warehouses/snowflake.md) 및 [Snowflake 일괄 처리](../../destinations/catalog/warehouses/snowflake-batch.md) 계정 ID 유효성 검사 | 정규 표현식 유효성 검사기가 계정 ID 단계에 추가되었습니다. 이제 ID를 입력할 때 조직 ID와 계정 ID가 올바른 형식(점으로 구분)인지 확인됩니다. 이 업데이트는 3월 말까지 배포됩니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform에 가져온 데이터에 대한 공통 구조와 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| XDM 엔티티 작업 및 삭제 지원 | 인라인 테이블 메뉴 및 세부 사항 페이지 헤더 메뉴에서 스키마, 클래스, 필드 그룹 및 데이터 유형에 대한 작업에 직접 액세스합니다. 필요한 권한이 있는 경우 데이터 세트에서 사용되지 않고 프로필에 대해 활성화되지 않은 조직의 엔티티를 삭제할 수도 있습니다. 자세한 내용은 [XDM UI 안내서](../../xdm/ui/explore.md)를 참조하십시오. |

자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#real-time-customer-profile}

실시간 고객 프로파일은 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 전체 보기를 제공합니다. 프로필을 사용하여 모든 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 이벤트 | 이제 프로필을 검색할 때 이벤트의 전환 확인 기간을 설정할 수 있습니다. 이렇게 하면 프로필이 지정된 기간 동안 연결된 이벤트를 볼 수 있습니다. 자세한 내용은 [프로필 UI 안내서](../../profile/ui/user-guide.md#events)를 참조하세요. |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Real-Time Customer Profile] 개요](../../profile/home.md)를 참조하십시오.

## 실행 및 운영 {#run-and-operate}

실행 및 운영 도구를 사용하여 Experience Platform 구현을 검사, 문제 해결 및 최적화합니다. 예약된 일괄 처리 활성화에 대한 가시성을 확보하고 구성 문제를 식별하며 시스템 안정성을 개선합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [작업 일정](../../run-and-operate/job-schedules.md) 일반 가용성 | [!DNL Job Schedules]은(는) 수집에서 대상 활성화에 이르기까지 데이터 파이프라인의 모든 예약된 일괄 처리 작업에 대한 통합 보기를 제공합니다. 비즈니스 운영에 영향을 미치기 전에 실행 상태를 검사하고, 예약 충돌을 식별하고, 구성 문제를 진단합니다. |
| [상태 확인](../../run-and-operate/health-checks.md) 일반 가용성 | 스키마 및 ID 구성이 잘못되면 잘못된 프로필 생성, 세그먼트 자격 실패 및 부정확한 활성화 등 중요한 다운스트림 문제가 발생합니다. <br>상태 검사는 사후 문제 해결에서 사전 예방적 유지 관리로 접근 방식을 전환합니다. 상태 검사는 샌드박스에서 사용되는 스키마 및 ID를 상시 검사하며 탐색 및 문제를 해결하는 데 사용할 수 있는 문제 요약을 제공합니다. |

{style="table-layout:auto"}

자세한 내용은 [실행 및 작업 개요](../../run-and-operate/overview.md), [작업 일정 검사](../../run-and-operate/job-schedules.md) 및 [Platform UI 안내서](../../landing/ui-guide.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 수집 유형 | 이제 속성의 수집 유형을 볼 수 있습니다. 이를 통해 데이터의 출처를 알 수 있으므로 더 나은 대상자를 만들 수 있습니다. 이 기능에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md)를 참조하세요. |
| 요약 데이터 | 이제 계정 및 사용자 기반 대상의 속성에 대한 요약 데이터를 볼 수 있습니다. 계정 대상의 이 기능에 대한 자세한 내용은 계정 [Audience Builder 안내서](../../rtcdp/segmentation/audience-builder.md)를 참조하십시오. 사용자 기반 대상의 이 기능에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md)를 참조하십시오. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 사용하여 외부 스토리지 시스템 및 CRM 서비스를 인증하고 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리합니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| 새로운 IP 주소 허용 목록 | GBR9: Azure에서 Experience Platform에 성공적으로 일괄 처리 소스 연결을 보장하기 위해 허용 목록에 추가하다해야 하는 주소 목록에 영국이 추가되었습니다. 자세한 내용은 [IP 주소 가이드](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)의 목록을 참조하십시오. |
| 변경 데이터 캡처 지원 향상 | 이제 [!DNL Marketo Engage], [!DNL Microsoft Dynamics] 및 [!DNL Salesforce CRM] 소스에서 변경 데이터 캡처를 사용할 수 있습니다. |
| [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md)에 대한 인증 가이드 개선 | [!DNL Google BigQuery] 원본에 대한 인증 가이드가 다음 정보로 확장되었습니다. <ul><li>새로 고침 토큰에 필요한 범위입니다.</li><li>[!DNL Google] ID에 필요한 IAM 역할입니다.</li><li>`largeResultsDataSetId` 사용에 대한 추가 지침입니다.</li></ul> |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
