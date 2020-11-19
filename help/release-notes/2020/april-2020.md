---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 8%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 4월 8일**

Adobe Experience Platform의 새로운 기능:
* [[!DNL Intelligent Services]](#intelligent)

기존 기능 업데이트:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 마케팅 분석가 및 전문가는 고객 경험 사례에서 인공 지능과 머신 러닝의 기능을 활용할 수 있습니다. 따라서 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다. 또한 마케팅 전문가는 Adobe Experience Cloud, Adobe Experience Platform 및 타사 애플리케이션에서 예측을 활성화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 마케터에게는 이에 대한 설명이 포함된 개별 수준에서 고객 예측을 생성할 수 있는 강력한 기능이 제공됩니다. 영향력 있는 요소의 도움을 통해 고객의 관심사와 이유를 파악할 [!DNL Customer AI] 수 있습니다. 또한 마케터는 [!DNL Customer AI] 예측 및 인사이트를 통해 가장 적합한 제안과 메시지를 제공하여 고객 경험을 개인화할 수 있습니다. |
| [!DNL Attribution AI] | [!DNL Attribution AI] 는 지정된 결과에 대한 고객 인터랙션의 영향과 점진적 효과를 계산하는 다중 채널 알고리즘 속성 서비스입니다. 마케터는 [!DNL Attribution AI]를 통해 고객 여정의 각 단계에서 개별 고객과의 인터랙션이 미치는 영향을 파악하여 마케팅 및 광고 비용을 측정하고 최적화할 수 있습니다. |

**알려진 문제**

* 현재 알려진 문제가 없습니다.

제공 내용 [!DNL Intelligent Services] 에 대한 자세한 내용은 [지능형 서비스 개요를 참조하십시오](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화와 상호 운용성은 그 이면의 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 공개적으로 문서화된 사양입니다. 이 소프트웨어는 Adobe Experience Platform의 서비스와 통신하기 위해 모든 애플리케이션에 대한 공통 구조와 정의를 제공합니다. 모든 고객 경험 데이터는 XDM 표준을 준수하여 보다 빠르고 통합된 방식으로 인사이트를 제공하는 공통 표현에 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고 세그먼트를 통해 고객 고객을 정의하며 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 자동 대체 표시 정보 | 설명자에 구성된 사용자 지정 제목 및 설명 값을 [!DNL Schema Registry] 자동으로 `alternateDisplayInfo` 적용합니다. |
| 스칼라 필드 제한 | 단일 스키마에서 6000개 [!DNL Schema Registry] 이상의 스칼라 필드를 허용하지 않습니다. |
| 성능 점검 | 그 [!DNL Schema Registry] 는 더 나은 요구를 충족시키기 위해 재편되었다 [!DNL Experience Platform] . |

**버그 수정**

* 표준 XDM에서 중첩된 URI 필드에 대한 더 깔끔한 XDM 형식을 지원하도록 변환되어 있는 XDM을 XDM으로 업데이트했습니다.

**알려진 문제**

* 알려진 항목

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] 는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다. 카탈로그 작성, 데이터 계보, 데이터 사용 표시, 데이터 액세스 정책, 마케팅 작업을 위한 데이터 액세스 제어 등 다양한 [!DNL Experience Platform] 수준에서 핵심적인 역할을 합니다.

데이터 거버넌스를 시작하려면 고객 데이터에 적용되는 규정, 계약 의무 및 기업 정책을 철저하게 이해해야 합니다. 여기에서, 데이터는 적절한 데이터 사용 레이블을 적용하여 분류할 수 있으며, 데이터 사용 정책의 정의를 통해 데이터를 사용할 수 있습니다.

이 [!DNL Data Governance] 프레임워크는 [!DNL Experience Platform] 사용자 인터페이스 및 [!DNL Policy Service] API를 통해 데이터를 분류하고 데이터 사용 정책을 만드는 과정을 간소화하고 간소화합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI에서 데이터 사용 정책 관리 | 이제 UI의 **정책** 작업 영역에서 데이터 사용 정책을 관리할 수 [!DNL Experience Platform] 있습니다. 자세한 내용은 [정책 사용 안내서를](../../data-governance/policies/user-guide.md) 참조하십시오. |

**알려진 문제**

* None.

자세한 내용은 [데이터 거버넌스 개요를 참조하십시오](../../data-governance/home.md).


## 대상 {#destinations}

실시간 [고객 데이터 플랫폼](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

Adobe 실시간 CDP는 50개 이상의 확장을 대상으로 데이터 활성화를 지원하므로 분석, 개인화 및 기타 사용 사례를 활용할 수 있습니다 [!DNL Experience Cloud Launch] . 자세한 내용은 아래를 참조하십시오.

| 설명서 | 설명 |
|--- | ---|
| [대상 유형 및 카테고리](/help/rtcdp/destinations/destination-types.md) | 이 문서에서는 Adobe 실시간 CDP 인터페이스의 연결과 익스텐션의 차이점과 이러한 각 대상을 사용할 시기를 권장합니다. |
| [Experience Platform Launch 확장](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 이 페이지에서는 어떤 확장 기능을 [!DNL Launch] 사용하는지, 사용 사례를 나열하고, Adobe 실시간 CDP의 각 익스텐션 [!DNL Launch] 에 대한 설명서 링크를 설명합니다. |

자세한 내용은 대상 [개요를 참조하십시오](/help/rtcdp/destinations/destinations-overview.md).

## [!DNL Privacy Service] {#privacy}

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 를 [!DNL Privacy Service]사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스 및 삭제하기 위한 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국에 있는 개인 정보 보호법(PDPA)에 따라 개인 정보 요청을 생성하고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열은 &quot;pdpa_tha&quot; 값을 수락합니다. |
| UI의 네임스페이스 유형 | 이제 [!DNL Privacy Service] UI의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. 자세한 내용은 [사용자 가이드](../../privacy-service/ui/user-guide.md) 를 참조하십시오. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

알려진 문제

* None

자세한 내용 [!DNL Privacy Service]은 먼저 [Privacy Service 개요를 읽어 보십시오](../../privacy-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터베이스에 대한 API 및 UI 지원 | (HDInsights [!DNL Apache Spark] ), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage](HDInsights [!DNL Hive] ) 및 등의 새 소스 커넥터 [!DNL Phoenix]를 사용할 수 있습니다. |
| 결제 기반의 애플리케이션에 대한 API 및 UI 지원 | 새 소스 커넥터 [!DNL PayPal]. |
| 프로토콜 기반 애플리케이션에 대한 API 및 UI 지원 | 새 소스 커넥터 [!DNL Generic OData]. |

**알려진 문제**

* None

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).
