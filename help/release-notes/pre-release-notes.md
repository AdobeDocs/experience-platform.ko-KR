---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

---

# Adobe Experience Platform 프리릴리스 노트

>[!IMPORTANT]
>
>이 문서는 이번 달 릴리스 정보의 **미리 보기**&#x200B;로 작성되었습니다. 릴리스 항목은 변경될 수 있으며 최종 릴리스에서 추가 또는 제거될 수 있습니다.

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 날짜: 2026년 3월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [고급 데이터 라이프사이클 관리](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [대상](#destinations)
- [쿼리 서비스](#query-service)
- [실시간 고객 프로필](#profile)
- [실행 및 운영](#run-and-operate)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 고급 데이터 라이프사이클 관리 {#advanced-data-lifecycle-management}

Experience Platform은 프로그램 수준에서 소비자 기록 및 데이터 세트를 삭제함으로써 저장 데이터를 관리할 수 있도록 해 주는 데이터 위생 기능 세트를 제공합니다. UI의 데이터 라이프사이클 작업 영역을 사용하거나 데이터 위생 API 호출을 통해 데이터 저장소를 효과적으로 관리할 수 있습니다. 이들 기능을 사용하면 정보를 의도대로 사용하고 정확하지 않은 데이터를 수정해야 할 때 업데이트하며 조직 정책에 따라 필요한 경우 삭제할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 다중 데이터 세트 및 프로필 전용 레코드 삭제(API 전용) | 단일 데이터 세트 ID, 쉼표로 구분된 데이터 세트 ID 목록 또는 `ALL`의 리터럴 `datasetId`을(를) 제출하여 하나, 여러 데이터 세트 또는 모든 데이터 세트에서 ID를 삭제할 수 있습니다. `targetServices`을(를) `["identity","profile","ajo"]`(으)로 설정하여 프로필 서비스에 대한 삭제를 제한할 수도 있습니다. 이렇게 하면 데이터 레이크는 변경되지 않습니다. 자세한 내용은 [작업 주문 기록 삭제 가이드](../hygiene/api/workorder.md)를 참조하세요. |

{style="table-layout:auto"}

자세한 내용은 [고급 데이터 라이프사이클 관리 개요](../hygiene/home.md)를 참조하십시오.

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator을 사용하면 워크플로우를 자동화하고 여러 채널에서 고객과 상호 작용할 수 있는 AI 기반 에이전트를 구축하고 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Microsoft 365 Copilot]에 대한 Adobe Marketing Agent | [!DNL Microsoft 365 Copilot]용 Adobe Marketing Agent은 Adobe의 마케팅 인텔리전스를 [!DNL Teams], [!DNL Word], [!DNL PowerPoint] 및 기타 [!DNL Microsoft 365] 앱과 같은 일상적인 도구에 직접 가져오는 임베드된 에이전트입니다. [!DNL Microsoft 365] 워크플로를 종료하지 않고 캠페인을 계획하고, 대상자를 검토하거나 동료와 협업하고, 고객 질문에 답변하고, 데이터에 기반한 결정을 내리는 동안 이 에이전트를 사용하여 Adobe 애플리케이션에서 신뢰할 수 있는 캠페인 인사이트를 가져올 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [Snowflake 일괄 처리](../destinations/catalog/warehouses/snowflake-batch.md) 영역 선택기 | 이제 검색과 드롭다운을 하나의 컨트롤로 결합한 새로운 검색 가능 드롭다운을 사용하여 영역을 보다 쉽게 찾을 수 있습니다. |
| 대상 메타데이터를 [Snowflake 일괄 처리](../destinations/catalog/warehouses/snowflake-batch.md) 대상으로 내보내기 | 이제 이 대상으로 내보낸 파일에 대상 메타데이터가 포함됩니다. 새 테이블 구조는 앞으로 설정된 모든 새 대상 연결에 적용됩니다. 이전 테이블 구조는 더 이상 사용되지 않기 전에 3개월 더 유지됩니다. |
| [!DNL Adobe Advertising Cloud DSP] 연결 | 새 Adobe Advertising DSP 연결은 레거시 연결과 동일한 기능을 제공하며 추가 ID를 지원합니다. |
| [트레이드 데스크 CRM](../destinations/catalog/advertising/tradedesk-emails.md), [크리터](../destinations/catalog/advertising/criteo.md) 및 [Pinterest](../destinations/catalog/advertising/pinterest.md)에 대한 외부 대상 지원 | 이제 사용자 지정 업로드 대상(CSV에서 가져옴), 유사 대상, 페더레이션 대상 및 Adobe Journey Optimizer과 같은 다른 Experience Platform 앱에서 만든 대상을 포함하여 세분화 서비스 세그먼트를 넘어 트레이드 데스크 CRM, 크리터 및 Pinterest에 대한 대상을 활성화할 수 있습니다. 자세한 내용은 각 대상의 카탈로그 페이지에서 [지원되는 대상](../destinations/catalog/advertising/criteo.md#supported-audiences) 섹션을 참조하십시오. |
| 사용자 정의 업로드 대상자 제한 늘림 | 이제 대상 인스턴스당 최대 20개의 사용자 지정 업로드 대상을 활성화할 수 있습니다. 이전에는 이 제한이 10개였습니다. |
| 외부 대상에 대해 [지금 파일 내보내기](../destinations/ui/export-file-now.md) 및 [임시 활성화 API](../destinations/api/ad-hoc-activation-api.md) 지원 | 이제 파일 기반 대상 일괄 처리를 활성화할 때 외부 대상(예: 사용자 지정 업로드, 유사, 페더레이션 및 다른 Experience Platform 앱의 대상)과 함께 UI(파일 내보내기) 및 임시 활성화 API를 사용할 수 있습니다. |
| OAuth 2 및 mTLS를 사용하는 HTTP API 대상 | 이제 인증 끝점에 상호 TLS(mTLS)가 필요한 경우 OAuth 2를 사용하는 HTTP API 대상을 만들고 인증할 수 있습니다. 대상 설정 중 토큰 검색은 이제 mTLS를 지원합니다. |
| ZoomInfo 계정 대상 | 이제 Real-Time Customer Data Platform(B2B)에서 ZoomInfo로 계정 대상을 보낼 수 있습니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항**

| 변수 이름이 아니라, 필터링된 보고서의 머리글로 잘못 표시하는 | 설명 |
| --- | --- |
| [Snowflake 스트리밍](../destinations/catalog/warehouses/snowflake.md) 계정 ID 유효성 검사 | 정규 표현식 유효성 검사기가 계정 ID 단계에 추가되었습니다. 이제 ID를 입력할 때 조직 ID와 계정 ID가 올바른 형식(점으로 구분)인지 확인됩니다. |
| [TikTok](../destinations/catalog/social/tiktok.md) 커넥터 전화 번호 해싱 | 대상 카드에서 잘못 구성되면 전화 번호에서 처리된 ID가 TikTok에 활성화되지 않는 문제가 해결되었습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필 이벤트 시간 선택기 | 이제 프로필 이벤트 탭에서 시간 창을 설정하여 해당 범위 내의 이벤트를 보고 분석할 수 있습니다. 기간을 최대 30일로 설정할 수 있습니다. 기본적으로 지난 48시간 동안의 이벤트를 표시합니다. |

{style="table-layout:auto"}

자세히 알아보려면 [실시간 고객 프로필 개요](../profile/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 데이터 과학 작업 영역에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 Distiller Accelerator | 이제 바로 연결 탭에서 바로 연결을 선택하고, 필요한 매개 변수를 입력하고, 직접 작성하지 않고 생성된 SQL을 실행 또는 예약할 수 있습니다. 원하는 바로 연결을 사용자 정의 템플릿에 복제하여 편집할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [쿼리 서비스 개요](../query-service/home.md)를 참조하세요.

## 실행 및 운영 {#run-and-operate}

실행 및 운영 도구를 사용하여 Experience Platform 구현을 검사, 문제 해결 및 최적화합니다. 예약된 일괄 처리 활성화에 대한 가시성을 확보하고 구성 문제를 식별하며 시스템 안정성을 개선합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [작업 일정](../run-and-operate/job-schedules.md) 일반 가용성 | [!DNL Job Schedules]은(는) 수집에서 대상 활성화에 이르기까지 데이터 파이프라인의 모든 예약된 일괄 처리 작업에 대한 통합 보기를 제공합니다. 비즈니스 운영에 영향을 미치기 전에 실행 상태를 검사하고, 예약 충돌을 식별하고, 구성 문제를 진단합니다. |
| 상태 검사 일반 가용성 | 스키마 및 ID 구성이 잘못되면 잘못된 프로필 생성, 세그먼트 자격 실패 및 부정확한 활성화 등 중요한 다운스트림 문제가 발생합니다. <br>상태 검사는 사후 문제 해결에서 사전 예방적 유지 관리로 접근 방식을 전환합니다. 상태 검사는 샌드박스에서 사용되는 스키마 및 ID를 상시 검사하며 탐색 및 문제를 해결하는 데 사용할 수 있는 문제 요약을 제공합니다. |

{style="table-layout:auto"}

자세한 내용은 [실행 및 작업 개요](../run-and-operate/overview.md), [작업 일정 검사](../run-and-operate/job-schedules.md) 및 [Platform UI 안내서](../landing/ui-guide.md)를 참조하십시오.

## Segmentation Service {#segmentation}

Experience Platform을 사용하면 고객 데이터에서 대상 세그먼트를 만들고, 해당 대상의 전체 라이프사이클 관리를 수행할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Audience Builder의 수집 소스 | 이제 각 속성이 Audience Builder 내의 일괄 처리, 스트리밍 또는 에지 소스에서 발생하는지 여부를 확인하여 잘못되거나 비효율적인 스트리밍 대상을 구축할 수 없습니다. |
| 계정 대상자 빌더에 데이터가 있는 필드만 표시 | 이제 계정 대상을 만들 때 데이터가 포함된 속성만 표시하도록 필터링할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../segmentation/home.md)를 참조하세요.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| 변경 데이터 캡처 지원 향상 | 이제 [!DNL Marketo Engage], [!DNL Microsoft Dynamics] 및 [!DNL Salesforce CRM] 소스에서 변경 데이터 캡처를 사용할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->