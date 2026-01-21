---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d401707e263f09ccd8575f02a71d7e74899e02db
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 20%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 날짜: 2026년 1월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [Agent Orchestrator](#agent-orchestrator)
- [대상](#destinations)
- [실시간 고객 프로필](#real-time-customer-profile)
- [스키마](#schemas)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator을 사용하면 워크플로우를 자동화하고 여러 채널에서 고객과 상호 작용할 수 있는 AI 기반 에이전트를 구축하고 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Agent Orchestrator의 평가판 동작 | 이제 Agent Orchestrator에서 체험판을 제공하여 고객이 전체 구매를 약속하기 전에 서비스를 탐색 및 테스트할 수 있습니다. 이 구매 전 시도 옵션을 통해 조직은 자체 환경에서 스킬 및 오케스트레이션 기능을 포함하여 Agent Orchestrator의 기능을 평가할 수 있습니다. 이 체험판에서는 AI 기반 에이전트를 구축하고 기존 워크플로우에 통합할 수 있는 방법을 이해하는 데 실습형 경험을 제공합니다. |

{style="table-layout:auto"}

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| 이제 케벨 대상 커넥터를 사용할 수 있습니다. | [[!DNL Kevel]](https://www.kevel.com/)은(는) 혁신적인 상거래 리더가 소매 미디어를 출시하고, 확장하고, 성공할 수 있도록 지원하는 AI 지원 기술 및 전문가 지침을 제공합니다. [!DNL Kevel]의 Retail Media Cloud는 온사이트 및 오프사이트 광고를 위한 타깃팅되고, 귀속되며, 사용자 지정 가능한 광고 형식을 지원합니다. |
| 이제 인덱스 교환 대상 커넥터를 사용할 수 있습니다. | [!DNL Index]은(는) 미디어 소유자가 모든 화면에서 콘텐츠의 가치를 극대화할 수 있도록 지원하는 글로벌 광고 공급측 플랫폼입니다. 20년 이상의 업계 리더십 덕분에 [!DNL Index]은(는) 세계 최대 브랜드와 프리미엄 경험 메이커를 연결하여 고품질의 소비자 경험을 제공합니다. |
| 브레이즈 연결에 대한 지역 엔드포인트 지원 | 이제 대상 구성 흐름 동안 [에서 지원하는 모든 ](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)지역별 끝점[!DNL Braze]을 선택할 수 있습니다. 사용해야 하는 끝점 인스턴스를 [!DNL Braze] 담당자에게 문의하십시오. |
| Liveramp 온보딩을 위한 주간 및 월간 일정 조정 지원 | 이제 Liveramp 온보딩 대상에 대한 주별 및 월별 내보내기 일정을 구성할 수 있습니다. |
| Amazon S3 대상에 대한 AES256 암호화 지원 | 이제 Amazon S3 내보내기에 대해 AES256 암호화를 구성할 수 있습니다. |
| Trade Desk 및 Microsoft Bing 대상을 위한 활성화 경험 개선 | 이제 Trade Desk 및 Microsoft Bing 대상에 최적화된 활성화 경험을 위한 사전 정의된 필수 매핑이 포함됩니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Target 대상에 대한 보호 제한을 업데이트했습니다. | 단일 Adobe Target 대상에 매핑할 수 있는 최대 대상 수가 50개에서 250개로 증가했습니다. 이렇게 하면 Adobe Target이 다른 대상에 대한 표준 대상 제한에 맞춰 조정되므로 대상 활성화 워크플로우에 더 많은 유연성을 제공합니다. 이제 여러 데이터 흐름을 만들지 않고도 Adobe Target 대상에 대해 더 많은 대상을 활성화할 수 있습니다. |
| [대상 편집](/help/destinations/ui/edit-destination.md) 및 [마케팅 작업 편집](/help/destinations/ui/edit-activation.md#edit-marketing-actions) 일반 가용성 | 이제 모든 사용자가 대상 및 마케팅 작업을 편집하는 옵션을 사용할 수 있습니다. |
| 매핑 단계에서 필드 표시 이름 전환 | 이제 스키마 필드를 대상에 매핑할 때 전체 XDM 필드 이름을 표시하는 것과 표시 이름만 표시하는 것 간을 전환할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#real-time-customer-profile}

실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스트리밍 용량 적용 | 이제 Experience Platform에서는 실시간 고객 프로필 및 ID 서비스를 위해 스트리밍 처리량 기능을 적용합니다. 고객이 계약된 스트리밍 용량을 초과하면 데이터는 선입선출 방식으로 큐에 올라가 처리됩니다. 이를 통해 예측 가능한 시스템 성능을 보장하고 용량 위반이 데이터 수집 품질에 영향을 미치지 않도록 할 수 있습니다. 중요 참고 사항: 용량을 초과하면 데이터 레이크에서 스트리밍 업데이트를 사용할 수 없으며, 이 적용은 Adobe Journey Optimizer 라이선스가 있는 고객에게는 적용되지 않으며, 용량이 사용 가능해지면 큐에 있는 데이터가 순차적으로 처리됩니다. |
| Real-Time CDP Prime에 대한 API 액세스 사용 중단 | 경험 이벤트에 대한 API 액세스는 이제 모든 Real-Time CDP Prime 고객에게 더 이상 사용되지 않습니다. 이 변경 사항은 API를 통해 직접 경험 이벤트를 쿼리하는 기능에 영향을 줍니다. Real-Time CDP Ultimate 고객은 사용 사례에 필요한 경우 공식 예외 프로세스를 통해 예외를 요청하여 경험 이벤트 API 액세스를 활성화할 수 있습니다. 이러한 사용 중단은 시스템 성능을 최적화하는 데 도움이 되며 데이터 액세스 패턴에 대한 우수 사례에 부합합니다. |
| 데이터 흐름 실행 모니터링 | 이제 프로필에서 데이터 흐름 실행의 진행 상황과 준비를 모니터링할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Real-Time Customer Profile] 개요](../profile/home.md)를 참조하십시오.

## 스키마 {#schemas}

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 검색, 필터, 태그 및 폴더를 통한 스키마 인벤토리 현대화 | 향상된 조직 및 검색 기능을 제공하기 위해 스키마 찾아보기 페이지를 현대화했습니다. 새로운 기능에는 고급 검색 및 필터링 옵션, 사용자 생성 태그 및 폴더에 대한 지원을 통해 스키마를 구성하고 인라인 작업을 통해 워크플로우를 간소화하는 기능이 포함됩니다. 주요 개선 사항으로는 업데이트된 열(이름, 클래스, 데이터 세트, ID, 관계, 프로필에 대해 활성화, 동작, 스키마 유형, 태그, 생성됨 날짜, 마지막 수정됨), 고급 필터(프로필 표시, 스키마 유형, 클래스, 임의 태그 있음, 생성자, 생성됨 날짜, 수정됨 날짜, 기본 ID 있음, 관계 있음, 기본 ID 네임스페이스), 인라인 작업(편집, 삭제, 레이블 적용, 비관계형 스키마에 대한 데이터 세트 생성, 태그 관리, 폴더로 이동, 패키지에 추가, JSON 구조 복사, 샘플 파일 다운로드) 및 태그와 폴더를 사용하여 스키마를 구성하는 기능이 있습니다. 이러한 향상된 기능은 스키마 리소스에 대한 포괄적인 가시성을 제공하고 샌드박스 수준에서 보다 효율적인 스키마 관리를 가능하게 합니다. |

자세한 내용은 [[!DNL Schemas] 개요](../xdm/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 세분화 모니터링 | 스트리밍 세그멘테이션을 위한 실시간 모니터링은 샌드박스, 데이터 세트 및 대상 수준에서 평가 속도, 지연 시간 및 데이터 품질 지표에 대한 투명성을 제공합니다. 이를 통해 데이터 엔지니어는 용량 위반 및 수집 문제를 식별하는 데 도움이 되는 사전 예방적 경고 및 실행 가능한 인사이트를 얻을 수 있습니다. 모니터링 지표에는 평가 비율, P95 수집 지연은 물론 수신, 평가, 실패 및 건너뛴 기록이 포함됩니다. 데이터 세트별 보기 및 대상별 보기 기능은 자격을 부여하거나 자격을 박탈한 순 신규 프로필에 대한 포괄적인 가시성을 제공합니다. |
| 외부 대상 TTL 새로 고침 | 이제 외부 대상(예: CSV 업로드)은 TTL(Time-to-Live) 설정에 대한 강제 새로 고침 기능을 지원합니다. 이 기능을 사용하면 외부 대상에 대한 TTL 만료를 수동으로 새로 고칠 수 있으므로 대상 라이프사이클 관리를 더욱 세밀하게 제어할 수 있습니다. 이 기능은 초기 TTL 기간 이상 유지해야 하거나 데이터를 다시 업로드하지 않고 다시 활성화해야 하는 대상에 특히 유용합니다. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| [!DNL Oracle Eloqua] V2 원본 | 이제 더 이상 사용되지 않는 커넥터를 대체하는 새 [!DNL Oracle Eloqua] 소스 커넥터를 사용할 수 있습니다. 이 업데이트된 커넥터는 [!DNL Oracle Eloqua]에서 Experience Platform으로 데이터를 수집하기 위한 향상된 기능과 향상된 안정성을 제공합니다. 기존 연결이 더 이상 작동하지 않으므로 기존 커넥터를 사용하는 고객은 새 구현으로 마이그레이션해야 합니다. 새 커넥터는 [!DNL Oracle Eloqua]에 연결하고 마케팅 자동화 데이터를 수집하는 데 필요한 모든 설정 및 구성 단계를 지원합니다. |
| [!DNL Salesforce Marketing Cloud] V2 원본 | 이제 더 이상 사용되지 않는 커넥터를 대체하는 새 [!DNL Salesforce Marketing Cloud] 소스 커넥터를 사용할 수 있습니다. 이 업데이트된 커넥터는 [!DNL Salesforce Marketing Cloud]에서 Experience Platform으로 데이터를 수집하기 위한 향상된 성능과 추가 기능을 제공합니다. 기존 커넥터를 사용하는 고객은 새 구현으로 전환해야 합니다. 새 커넥터에는 [!DNL Salesforce Marketing Cloud]에 연결하고 마케팅 자동화 데이터를 수집하기 위한 포괄적인 설정 지침이 포함되어 있습니다. |

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

