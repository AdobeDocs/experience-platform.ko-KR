---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 695b8486211c2fee03bc29243d65d5bbf6d561db
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 33%

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

**릴리스 날짜: 2026년 2월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [Agent Orchestrator](#agent-orchestrator)
- [경고](#alerts)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator을 사용하면 워크플로우를 자동화하고 여러 채널에서 고객과 상호 작용할 수 있는 AI 기반 에이전트를 구축하고 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 온보딩 에이전트 | 데이터 온보딩 에이전트를 사용하여 소스 연결 구성, 데이터 품질 유효성 검사, 의미 체계 강화 적용, 스키마 검토 및 유효성 검사, 데이터 수집 실행 등을 수행할 수 있습니다. B2C 및 B2B 플로우 모두에 대한 단계별 워크플로우를 따르고, 예상되는 출력을 검토하고, 일반적인 문제를 해결합니다. |
| 데이터 Distiller 에이전트 | Data Distiller 에이전트를 사용하여 자연어에서 SQL 작업을 생성하고, SQL 성능을 최적화하고, SQL 오류를 복구하고, SQL 작업을 예약 및 관리하고, 작업 상태를 모니터링할 수 있습니다. 시작하려면 보호 기능, 필요한 권한 및 문제 해결 지침을 검토하십시오. |
| 데이터 수집 에이전트 | 데이터 수집 에이전트를 사용하면 복잡한 데이터 수집 구성에 대한 컨텍스트 내 지침을 얻을 수 있고, 대화형 통찰력을 통해 데이터 수집 개체 간에 계보, 종속성 및 관계를 탐색할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [Agent Orchestrator 설명서](https://experienceleague.adobe.com/ko/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)를 참조하세요.

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL Alerts] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며 UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 고객 응대 경고에 대한 [!DNL Slack] 통합 | 이제 [!DNL Slack]에게 고객 응대 경고를 제공할 수 있습니다. 단계별 자습서에 따라 [!DNL Slack] 통합을 설정하고 [!DNL Slack] 작업 영역에서 바로 경고 알림을 받을 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Observability Insights] 개요](../observability/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform 데이터 수집에서는 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network 및 기타 대상으로 전송할 수 있는 기술 집합을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Platform 태그 확장 관리 | 새로운 확장 관리 기능을 사용하여 개발, 비공개 및 공개 배포에 대한 조직의 확장을 업로드, 패키지 및 릴리스할 수 있습니다. 최상위 수준 회사 보기에서 소유한 확장과 함께 공유 비공개 확장을 찾습니다. 이 기능은 웹, Edge 및 모바일 확장을 지원합니다. |

{style="table-layout:auto"}

자세한 내용은 [데이터 수집 설명서](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!DNL ZoomInfo] 계정 대상 | 이제 B2B CDP 사용자는 새 [!DNL ZoomInfo] 계정 대상 커넥터를 통해 [!DNL ZoomInfo]에 계정 수준 데이터를 활성화할 수 있습니다. 계정 대상자를 [!DNL ZoomInfo]&#x200B;(으)로 보내려면 커넥터를 설정하십시오. |
| [!DNL Snowflake] 일괄 처리를 일반적으로 사용할 수 있음 | [!DNL Snowflake] 일괄 처리 대상이 일반 가용성으로 이동되었습니다. 이제 내보낸 데이터의 병합 정책 ID 열을 타임스탬프, 매핑 속성 및 대상 멤버십과 같은 기존 열과 함께 볼 수 있습니다. |
| [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 대상에 대한 AES256 암호화 지원 | 이제 Amazon S3 내보내기에 대해 AES256 암호화를 구성할 수 있습니다. 다음 두 옵션 중에서 선택합니다. <ul><li>**[!UICONTROL Default]**: Experience Platform은 버킷에 설정된 기본 암호화 알고리즘으로 사용 중인 데이터를 암호화합니다.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform은 내보내기에 `s3:x-amz-server-side-encryption": "AES256` 헤더를 추가하고 S3에 도달할 때 AES256 알고리즘으로 사용하지 않는 데이터를 암호화합니다. **이 옵션은 S3 버킷에서 구성한 기본 암호화 알고리즘보다 우선합니다**.</li></ul> |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform에 가져온 데이터에 대한 공통 구조와 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스키마 인벤토리 조직 및 검색 | 이제 스키마 찾아보기 페이지에 향상된 검색 및 필터링, 인라인 작업 및 사용자 정의 태그와 폴더에 대한 지원이 포함됩니다. 이러한 업데이트를 통해 샌드박스 간 스키마를 더 쉽게 찾고, 구성하고, 관리할 수 있을 뿐 아니라 수동 탐색 및 유지 관리 작업을 줄일 수 있습니다. |

자세한 내용은 [[!DNL XDM] 개요](../xdm/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 데이터 과학 작업 영역에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Data Distiller 연간 계산 재설정 날짜 정렬(제한된 릴리스) | 이제 Data Distiller 연간 계산 시간이 라이선스가 구매되거나 갱신되는 시기를 기준으로 Data Distiller 계약 기념일에 재설정됩니다. 이렇게 하면 라이선스 사용 보고가 계약 조건에 맞게 조정되며 현재 사용 값으로 1회 조정될 수 있습니다. |
| Data Distiller 세션 관리(제한된 릴리스) | 승인된 관리자는 UI를 통해 조직 및 샌드박스 내에서 활성 쿼리 서비스 및 Data Distiller 세션을 보고 관리할 수 있습니다. 세션 관리를 사용하여 유휴 세션을 식별하고 종료하여 용량을 확보합니다. 내장된 안전 장치를 사용하면 활성 쿼리가 있는 세션을 종료할 수 없습니다. 이 기능은 감사를 위한 모든 제거 작업을 로그하여 영향을 받는 사용자에게 알립니다. 이 기능에 액세스하려면 **쿼리 세션 관리** 권한이 필요합니다. |

{style="table-layout:auto"}

자세한 내용은 [쿼리 서비스 개요](../query-service/home.md)를 참조하세요.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| [!DNL Databricks] 원본 커넥터의 Unity 카탈로그 지원 | 이제 [!DNL Databricks] 원본 커넥터가 Unity 카탈로그를 지원합니다. 소스 연결을 구성할 때 Unity 카탈로그를 사용하는 방법에 대해 알아보려면 업데이트된 [[!DNL Databricks]](../sources/connectors/databases/databricks.md) 설명서를 읽어 보십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.
