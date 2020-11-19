---
title: Adobe Experience Platform 릴리스 정보
description: 'Experience Platform 릴리스 노트: 2020년 9월 9일'
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 9월 9일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다. 카탈로그 작성, 데이터 계보, 데이터 사용 표시, 데이터 액세스 정책, 마케팅 작업을 위한 데이터 액세스 제어 등 다양한 [!DNL Experience Platform] 수준에서 핵심적인 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 세트 레이블 지정 UI 개선 사항 | 큰 스키마 작업을 더 쉽게 하기 위해 데이터 세트 레이블 지정 UI에 새로운 정렬 및 필터링 컨트롤이 추가되었습니다. <ul><li>전체 스키마 경로를 기준으로 필드를 알파벳순으로 정렬합니다.</li><li>필드 경로 이름에 대해 부분 검색을 수행합니다.</li><li>레이블, 선택된 레이블 또는 레이블 카테고리가 없는 필드를 필터링합니다.</li></ul> |

서비스에 대한 자세한 내용은 [데이터 거버넌스](../../data-governance/home.md) 개요를 참조하십시오.

## 대상 {#destinations}

실시간 [고객 데이터 플랫폼](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 UX | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 예약 편집 및 세그먼트 추가와 같은 기본 작업에 쉽게 액세스할 수 있습니다. 자세한 내용은 [대상 작업 공간](../../rtcdp/destinations/destinations-workspace.md) 문서를 참조하십시오. |

자세한 내용은 [대상 개요를 참조하십시오](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 통계 지표 및 이벤트 알림을 사용하여 Adobe Experience Platform의 활동을 모니터링할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe I/O 이벤트 알림 | [!DNL Observability Insights] adobe I/O 이벤트를 활용하여 여러 Experience Platform 서비스에 대한 이벤트 알림을 만듭니다. 알림 페이로드는 구성된 웹 후크로 전송되며, 이를 통해 추가 다운스트림 프로세스를 자동화할 수 있습니다. See the [notifications overview](../../observability/notifications/overview.md) for more information. |

서비스에 대한 자세한 내용은 [[!DNL Observability Insights] 개요를](../../observability/home.md) 참조하십시오.

## [!DNL Privacy Service] {#privacy}

여러 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 자신의 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 를 [!DNL Privacy Service]사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스 및 삭제하기 위한 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| LGPD 지원(브라질) | 이제 브라질의 [!DNL Lei Geral de Proteção de Dados] (LGPD) 규정에 따라 개인 정보 일자리를 창출할 수 있다. 이 일자리들은 규제 규정에 따라 추적된다 `lgpd_bra`. |

서비스에 대한 자세한 내용은 [Privacy Service 개요를](../../privacy-service/home.md) 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 언제 어디에서나 고객의 기대에 부응하는 일관된 경험을 제공할 수 있습니다. 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널의 데이터를 결합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Real-time Customer Profile] [!DNL Profile] 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 뷰어 | 플랫폼 UI에서 프로필 뷰어는 전체 사용자 지정이 가능한 대시보드로 업데이트되었습니다. 이제 사용자는 다음 작업을 수행할 수 있습니다. <ul><li>기본 정보 위젯에서 선택한 표준 및 사용자 지정된 속성을 업데이트합니다.</li><li>사용자 정의 위젯 만들기, 편집 및 제거</li><li>위젯 크기 조정 및 재정렬</li></ul> |

데이터 작업을 위한 자습서 및 모범 사례 [!DNL Real-time Customer Profile]를 비롯한 자세한 내용은 [!DNL Profile] 실시간 고객 프로필 개요를 참조하십시오 [](../../profile/home.md).

## 세분화 서비스 {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 작성하고 [!DNL Real-time Customer Profile] 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 중앙에서 구성 및 관리되므로 모든 Adobe 애플리케이션에서 쉽게 액세스할 수 [!DNL Platform]있습니다.

[!DNL Segmentation Service] 고객 기반 내에서 마케팅 가능한 사람들을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(인구 통계 정보 등) 또는 시간 시리즈 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 내보내기 작업 | 세그먼트를 내보내기 작업의 일부로 평가할 수 있도록 플래그가 추가되었습니다. 따라서 사용자는 단일 작업에서 세그먼테이션과 내보내기를 모두 실행할 수 있습니다. |
| 정책 병합 | 여러 병합 정책을 하나의 일괄 세분화 작업에 포함시킬 수 있습니다. |

자세한 내용 [!DNL Segmentation Service]은 세그멘테이션 [개요를 참조하십시오.](../../segmentation/home.md)

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 자동 매핑 | [!DNL Platform] 사용자가 선택한 대상 스키마 또는 데이터 세트를 기반으로 데이터 통합 워크플로우 동안 자동 매핑에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 유연한 자동 매핑 규칙을 수동으로 조정할 수 있습니다. |
| 향상된 UX | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 예약 편집 및 세그먼트 추가와 같은 기본 작업에 쉽게 액세스할 수 있습니다. 자세한 내용은 데이터 흐름 [모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).
