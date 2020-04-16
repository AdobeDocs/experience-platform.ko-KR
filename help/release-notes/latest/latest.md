---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트(2020년 4월 8일)
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e4da80338dbfbad70dfb3cf7df9fe589e949e788

---


# Adobe Experience Platform 릴리스 노트

## 릴리스 날짜: 2020년 4월 8일

## XDM(Experience Data Model) 시스템

Adobe Experience Platform의 주요 개념은 표준화 및 상호 운용성 Adobe 기반의 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력의 일환입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 고안된 문서화된 사양입니다. Adobe Experience Platform에서 제공하는 서비스와 커뮤니케이션할 수 있는 모든 애플리케이션에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 신속하고 통합된 방식으로 인사이트를 제공하는 일반적인 표현으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고 세그먼트를 통해 고객 고객을 정의하며 개인화를 위해 고객 속성을 사용할 수 있습니다.

### 새로운 기능

| 기능 | 설명 |
| --- | --- |
| 자동 대체 표시 정보 | 스키마 레지스트리는 `alternateDisplayInfo` 설명자에 구성된 사용자 지정된 제목 및 설명 값을 자동으로 적용합니다. |
| 스칼라 필드 제한 | 스키마 레지스트리는 단일 스키마에서 6000개 이상의 스칼라 필드를 허용하지 않습니다. |
| 성과 점검 | 스키마 레지스트리가 Experience Platform의 요구를 충족하기 위해 재편되었습니다. |

**버그 수정**

* 표준 XDM의 중첩된 URI 필드에 대해 보다 깔끔한 XDM 형식을 지원하도록 변환된 XDM을 XDM으로 업데이트했습니다.

**알려진 문제**

* 알려진 항목

## 데이터 거버넌스

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다. Adobe Experience Platform은 카탈로그 작성, 데이터 계보, 데이터 사용 레이블 지정, 데이터 액세스 정책, 마케팅 활동을 위한 데이터 액세스 제어 등 다양한 수준에서 핵심적인 역할을 합니다.

데이터 거버넌스를 시작하려면 고객 데이터에 적용되는 규정, 계약 의무 및 기업 정책을 철저하게 이해해야 합니다. 여기에서 데이터는 적절한 데이터 사용 레이블을 적용하여 분류할 수 있으며 데이터 사용 정책의 정의를 통해 데이터를 사용할 수 있습니다.

DULE 프레임워크는 Experience Platform 사용자 인터페이스 및 DULE Policy Service API를 통해 데이터를 분류하고 데이터 사용 정책을 만드는 과정을 간소화하고 간소화합니다.

### 새로운 기능

| 기능 | 설명 |
| -----------| ---------- |
| UI에서 데이터 사용 정책 관리 | 이제 경험 플랫폼 UI의 정책 _작업_ 영역에서 데이터 사용 정책을 관리할 수 있습니다. 자세한 내용은 [정책 사용 안내서를](../../data-governance/policies/user-guide.md) 참조하십시오. |

**알려진 문제**

* 없음.

자세한 내용은 데이터 거버넌스 [개요를](../../data-governance/home.md)참조하십시오.


## 대상

Adobe [실시간 고객 데이터 플랫폼에서](../../rtcdp/overview.md)대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에 대한 데이터를 원활하게 활성화할 수 있습니다.

### 새 대상

Adobe Real-time CDP는 50개 이상의 Experience Cloud Launch 익스텐션에 대한 데이터 활성화를 지원하므로 분석, 개인화 및 기타 사용 사례를 지원합니다. 자세한 내용은 아래를 참조하십시오.

| 설명서 | 설명 |
|--- | ---|
| [대상 유형 및 카테고리](/help/rtcdp/destinations/destination-types.md) | 이 문서에서는 Adobe Real-time CDP 인터페이스의 연결과 익스텐션의 차이점을 설명하고 각 대상을 사용할 시기를 권장합니다. |
| [Experience Platform Launch 확장](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 이 페이지에서는 Launch Extensions의 의미와 사용 사례를 나열하고 Adobe Real-time CDP의 각 Launch Extension에 대한 설명서 링크를 제공합니다. |

자세한 내용은 대상 개요를 [참조하십시오](/help/rtcdp/destinations/destinations-overview.md).

## 지능형 서비스

마케팅 분석가 및 전문가는 지능형 서비스를 통해 고객 경험 사용 사례에서 인공 지능과 머신 러닝의 기능을 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학에 대한 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다. 또한 마케팅 전문가는 Adobe Experience Cloud, Adobe Experience Platform 및 타사 애플리케이션에서 예측을 활성화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
|---|---|
| 고객 AI | 고객 AI는 마케터에게 개별 수준에서 고객 예측을 생성할 수 있는 기능을 제공합니다. 고객 AI는 영향력 있는 요소의 도움을 통해 고객의 관심사와 이유를 파악할 수 있습니다. 또한 마케터는 고객 AI 예측과 인사이트를 활용하여 가장 적합한 제안과 메시지를 제공하여 고객 경험을 개인화할 수 있습니다. |
| 기여도 AI | 기여도 분석 AI는 지정된 결과에 대한 고객 인터랙션의 영향과 점진적 영향을 계산하는 멀티채널 알고리즘 방식의 기여도 분석 서비스입니다. 기여도 분석 AI를 사용하면 마케터는 고객 여정의 각 단계에서 개별 고객과의 인터랙션이 미치는 영향을 파악하여 마케팅 및 광고 지출을 측정하고 최적화할 수 있습니다. |

**알려진 문제**

* 현재 알려진 문제가 없습니다.

Intelligent Services 및 Intelligent Services의 제공 사항에 대한 자세한 내용은 Intelligent Services [개요를](../../intelligent-services/home.md)참조하십시오.

## 개인 정보 서비스

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform 개인 정보 보호 서비스는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 개인 정보 보호 서비스를 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스하고 삭제할 수 있는 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국에 있는 개인 정보 보호 법(PDPA)에 따라 개인 정보 요청을 작성하고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열은 &quot;pdpa_tha&quot; 값을 수락합니다. |
| UI의 네임스페이스 유형 | 이제 개인 정보 서비스 UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용 안내서를](../../privacy-service/ui/user-guide.md) 참조하십시오. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

알려진 문제

* 없음

개인정보 보호 서비스에 대한 자세한 내용은 먼저 개인정보 보호 서비스 [개요를](../../privacy-service/home.md)읽으십시오.

## 소스

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 인터랙티브한 UI와 RESTful API를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

### 새로운 기능

| 기능 | 설명 |
| ------- | ----------- |
| 데이터베이스에 대한 API 및 UI 지원 | Apache Spark(HDInsights에서), Azure Synapse Analytics, Azure Table Storage, Hive(HDInsights에서) 및 Phoenix에 대한 새 원본 커넥터입니다. |
| 결제 기반의 애플리케이션에 대한 API 및 UI 지원 | PayPal의 새로운 소스 커넥터 |
| 프로토콜 기반 애플리케이션에 대한 API 및 UI 지원 | 범용 OData의 새 소스 커넥터. |

### 알려진 문제

* 없음

소스에 대한 자세한 내용은 [소스 개요를](../../sources/home.md)참조하십시오.
