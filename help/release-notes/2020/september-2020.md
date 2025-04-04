---
title: Adobe Experience Platform 릴리스 노트 2020년 9월
description: Adobe Experience Platform에 대한 2020년 9월 릴리스 정보입니다.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 35%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2020년 9월 9일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 거버넌스](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 데이터 거버넌스 {#governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 이 기능은 [!DNL Experience Platform] 내 카탈로그 작성, 데이터 계통 확인, 데이터 사용 라벨링, 데이터 액세스 정책, 마케팅 액션을 위한 데이터 액세스 제어 등 다양한 수준에서 주요 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 세트 레이블 지정 UI 개선 사항 | 큰 스키마를 사용하여 보다 쉽게 작업할 수 있도록 데이터 세트 레이블 지정 UI에 몇 가지 새로운 정렬 및 필터링 제어가 추가되었습니다. <ul><li>전체 스키마 경로를 기준으로 알파벳 순서로 필드를 정렬합니다.</li><li>필드 경로 이름에 대해 부분 검색을 수행합니다.</li><li>레이블, 선택한 레이블 또는 레이블 범주가 없는 필드를 필터링합니다.</li></ul> |

서비스에 대한 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하세요.

## 대상 {#destinations}

[Real-Time Customer Data Platform](../../rtcdp/overview.md)에서 대상은 해당 파트너에게 데이터를 원활하게 활성화하는 대상 플랫폼과의 사전 빌드된 통합입니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| UX 개선 사항 | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 예약 편집 및 세그먼트 추가와 같은 기본 작업에 보다 쉽게 액세스할 수 있습니다. 자세한 내용은 [대상 작업 영역](../../destinations/ui/destinations-workspace.md) 문서를 참조하십시오. |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하세요.

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights]을(를) 사용하면 통계 지표 및 이벤트 알림을 사용하여 Adobe Experience Platform에서 활동을 모니터링할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe I/O 이벤트 알림 | [!DNL Observability Insights]은(는) Adobe I/O Events을 사용하여 여러 Experience Platform 서비스에 대한 이벤트 알림을 만듭니다. 알림 페이로드는 구성된 웹후크로 전송되며, 이를 사용하여 추가적인 다운스트림 프로세스를 자동화할 수 있습니다. |

서비스에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하세요.

## [!DNL Privacy Service] {#privacy}

일부 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service]는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]를 사용하면 Adobe Experience Cloud 애플리케이션에서 비공개 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| LGPD 지원 (브라질) | 이제 브라질 [!DNL Lei Geral de Proteção de Dados] (LGPD) 규정에 따라 개인정보 보호 관련 작업을 만들 수 있습니다. 이러한 작업은 규정 코드 `lgpd_bra`에 따라 추적됩니다. |

서비스에 대한 자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. [!DNL Real-Time Customer Profile]을(를) 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile]을(를) 사용하면 모든 고객 인터랙션에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 다양한 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 뷰어 | Experience Platform UI의 프로필 뷰어가 전체 맞춤화가 가능한 대시보드로 업데이트되었습니다. 이제 사용자는 다음 작업을 수행할 수 있습니다. <ul><li>기본 정보 위젯에서 선택한 표준 및 사용자 정의된 속성을 업데이트합니다.</li><li>사용자 정의 위젯 만들기, 편집 및 제거</li><li>위젯 크기 조정 및 재배열</li></ul> |

[!DNL Profile] 데이터 작업에 대한 튜토리얼 및 모범 사례를 포함하여 [!DNL Real-Time Customer Profile]에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 빌드하고 [!DNL Real-Time Customer Profile] 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 [!DNL Experience Platform]에서 중앙에서 구성 및 유지 관리되므로 모든 Adobe 응용 프로그램에서 쉽게 액세스할 수 있습니다.

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 내보내기 작업 | 세그먼트를 내보내기 작업의 일부로 평가할 수 있도록 플래그가 추가되었습니다. 따라서 사용자는 단일 작업에서 세그먼테이션과 내보내기를 모두 실행할 수 있습니다. |
| 병합 정책 | 단일 배치 세분화 작업에 여러 병합 정책을 포함할 수 있습니다. |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세그먼테이션 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 [!DNL Experience Platform] 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform]에서는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 자동 매핑 | [!DNL Experience Platform]은(는) 사용자가 선택한 대상 스키마 또는 데이터 집합을 기반으로 데이터 수집 워크플로 동안 자동 매핑에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 유연한 자동 매핑 규칙을 수동으로 조정할 수 있습니다. |
| UX 개선 사항 | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 일정 편집 및 세그먼트 추가와 같은 기본 작업에 보다 쉽게 액세스할 수 있습니다. 자세한 내용은 [데이터 흐름 모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
