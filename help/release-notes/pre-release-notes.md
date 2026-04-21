---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5d1825bad97d3ec4beece416dc3e0fc9f6ca636d
workflow-type: tm+mt
source-wordcount: '1136'
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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 날짜: 2026년 4월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time CDP](#rtcdp)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft 광고 고객 일치](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | 이메일 주소로 고객을 일치시키고 검색 및 대상 광고를 포함하여 [!DNL Microsoft Advertising Network]에서 고객과 다시 교류하십시오. [!DNL Microsoft Advertising] 계정을 Real-Time CDP에 연결하여 Experience Platform에서 직접 고객 일치 목록 생성 및 관리를 자동화합니다. |
| [!BADGE Beta]{type=Informative} [사용자 지정 대상 편집](../destinations/catalog/advertising/reddit-custom-audience.md) | Experience Platform에서 [!DNL Reddit Ads]&#x200B;(으)로 대상자를 보냅니다. [!DNL Reddit] 계정을 연결하고, ID를 매핑하고, 대상을 활성화하여 [!DNL Reddit]에서 사람들이 관심 영역을 적극적으로 탐색하도록 합니다. |
| [Amazon 광고 v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2]은(는) 모든 새 [!DNL Amazon Ads] 연결의 현재 대상입니다. 기존 [(레거시) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) 연결이 있는 경우 필요한 변경 없이 계속 작동합니다. [!DNL Amazon Ads v2]이(가) [!DNL Ads Data Manager]에 연결되어 확장된 ID 유형, 주소 관련 필드 및 [!DNL Amazon Ads] 제품 간 데이터 공유를 지원하므로 [(레거시) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)에 비해 타깃팅 및 대상 일치율이 향상됩니다. |
| [!DNL Rokt] | [!DNL Rokt]을(를) 사용하여 Experience Platform 대상자를 AI 기반 실시간 의사 결정에 연결하여 보다 정확한 타기팅, 억제 및 개인화를 통해 캠페인 성과를 향상시킵니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항**

| 변수 이름이 아니라, 필터링된 보고서의 머리글로 잘못 표시하는 | 설명 |
| --- | --- |
| 사용자 지정 Personalization 모니터링 지원 | 대상에 대한 모니터링 대시보드에서 [!DNL Custom Personalization]개의 대상을 지원합니다. 모니터링에서 [!DNL Custom Personalization]을(를) 제외한 제한 메모를 제거했습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 필드 그룹 스키마 사용 가시성 | 세부 정보 페이지에서 필드 그룹을 사용하는 스키마를 보고 스키마 메타데이터가 포함된 정렬 가능한 대화 상자에서 탐색합니다. 따라서 다른 곳으로 이동하지 않고도 종속성 및 영향을 빠르게 평가할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [XDM 시스템 개요](../xdm/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하여 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]의 데이터를 쿼리합니다. [!DNL Data Lake]의 데이터 세트에 참여하고 쿼리 결과를 보고, Data Science Workspace 또는 실시간 고객 프로필로의 수집에 사용할 새 데이터 세트로 캡처합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 Distiller Accelerator | SQL을 작성하지 않고 일반적인 분석을 수행하려면 쿼리 서비스 UI에서 Adobe에서 관리하는 매개 변수가 있는 SQL 템플릿을 실행하고 예약하십시오. 이를 통해 분석 워크플로우를 표준화하고 조직 전체에서 신뢰할 수 있는 쿼리 논리를 재사용할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [쿼리 서비스 개요](../query-service/home.md)를 참조하세요.

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP]은(는) 여러 채널에서 실시간으로 데이터를 수집, 처리 및 활성화하여 실행 가능한 통합 고객 프로필을 제공합니다. Real-Time CDP을 사용하면 조직은 기존 데이터 소스를 연결하고 풍부한 대상을 구축 및 활성화할 수 있으며 Experience Platform 내에서 모든 대상이 개인 정보 보호를 준수하는 활성화를 보장할 수 있습니다. 이를 통해 마케터, 분석가 및 IT 팀은 원활한 크로스 채널 마케팅 캠페인을 통해 고객에게 개인화되고 시기적절한 경험을 제공할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Real-Time CDP MCP(Beta) | Real-Time CDP MCP를 사용하여 Real-Time CDP을 AI 에이전트 및 MCP 호환 클라이언트로 가져와 기본 LLM 경험을 통해 직접 Real-Time CDP 도구와 상호 작용할 수 있습니다. MCP 호환 클라이언트(예: Claude, ChatGPT, Claude Code, Codex, Cursor 또는 VS 코드)를 `https://rtcdp-mcp.adobe.io/mcp`에 연결하면 자연어를 사용하여 Experience Platform REST API 호출을 작성하거나 여러 UI 워크플로를 탐색하지 않고도 대상, 대상 구성 및 활성화 실행 기록을 검사할 수 있습니다. 브라우저 기반 Adobe 로그인을 완료하면 다음을 포함한 도구에 대한 읽기 전용 액세스 권한을 갖게 됩니다. <ul><li>기존 대상자 검색</li><li>대상자 멤버십 미리 보기</li><li>목록 대상 유형</li><li>구성된 계정 나열</li><li>구성된 대상 나열</li><li>Source 연결 나열</li><li>Target 연결 나열</li><li>활성화 실행 검사</li></ul>. 각 요청에는 `imsOrgId` 및 `sandboxName` 매개 변수가 있어야 작업을 조직과 샌드박스에 지정할 수 있습니다. 이 Beta 릴리스에서는 쓰기 작업이 지원되지 않습니다. |

{style="table-layout:auto"}

자세한 내용은 [Real-Time CDP 개요](../rtcdp/home.md)를 참조하세요.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포에 맞추어야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 빠른 복사 | [샌드박스 도구 UI](/help/sandboxes/ui/sandbox-tooling.md#express-copy)에서 한 번의 작업으로 대상 샌드박스에 개체를 복사하려면 빠른 복사를 사용하십시오. 종속 오브젝트는 자동으로 감지되며 대상 샌드박스에서 생성되거나 이미 존재하는 경우 재사용됩니다. |

{style="table-layout:auto"}

자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하세요.

## Segmentation Service {#segmentation-service}

세분화 서비스를 사용하여 고객 데이터에서 대상을 만들고 Experience Platform에서의 전체 라이프사이클을 관리합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스트리밍 세분화 모니터링 | 샌드박스, 데이터 세트 및 세그먼트 수준에서 평가율, 수집 지연 및 데이터 품질 지표에 대한 실시간 가시성을 통해 스트리밍 세분화를 모니터링합니다. 평가율, P95 수집 지연, 수신된 레코드, 평가된 레코드, 실패한 레코드 및 건너뛴 레코드를 포함하는 지표를 봅니다. 또한 세그먼트별로 자격이 부여되고 자격이 부여되는 순 새 프로필을 봅니다. 이러한 통찰력을 사용하여 용량 위반 및 수집 문제가 데이터에 영향을 미치기 전에 식별하십시오. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../segmentation/home.md)를 참조하세요.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| 자동 데이터 흐름 비활성화 | 30일 동안 연속적으로 실패하는 소스 수집 데이터 흐름은 자동으로 비활성화되어 비정상 데이터 흐름을 표시하고 반복된 실패 실행을 줄이는 데 도움이 됩니다. |
| [!DNL Delta Sharing] | [!DNL Delta Sharing] 원본을 사용하여 안전하고 열려 있는 데이터 공유 프로토콜을 통해 델타 테이블을 Experience Platform으로 가져올 수 있습니다. [!DNL Delta Sharing] 연결을 구성하고 수집할 공유 및 테이블을 선택하면 Platform에서 해당 데이터를 데이터 세트로 자동으로 가져와 분석, 세분화 및 활성화에 사용할 수 있습니다. |
| [!DNL Meta Ads]&#x200B;(Beta) | 소스 작업 영역에서 [!DNL Meta Ads] 소스 커넥터(Beta)를 사용하여 [!DNL Meta]을(를) 인증하고, 광고 계정을 선택하고, [!DNL Meta Ads] 캠페인 및 성능 데이터의 Experience Platform 데이터 세트로의 수집을 예약할 수 있습니다. |
| [!DNL Talon.One] | 이제 새 [!DNL Talon.One] 일괄 처리 및 스트리밍 소스를 사용하여 Experience Platform을 [!DNL Talon.One]에 연결할 수 있습니다. 새 소스를 사용하여 Experience Platform에 대한 거래 및 충성도 활동 이벤트뿐만 아니라 충성도 프로필 데이터를 수집할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.
