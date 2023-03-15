---
title: Adobe Experience Platform 릴리스 노트 2020년 4월
description: Adobe Experience Platform에 대한 2020년 4월 릴리스 정보입니다.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 릴리스 노트;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2020년 4월 8일**

Adobe Experience Platform의 새로운 기능:
* [[!DNL Intelligent Services]](#intelligent)

기존 기능에 대한 업데이트:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [데이터 거버넌스](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준의 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다. 또한 마케팅 실무자는 Adobe Experience Cloud, Adobe Experience Platform 및 서드파티 애플리케이션에서 예측을 활성화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 은 마케터에게 설명을 통해 개별 수준에서 고객 예측을 생성할 수 있는 기능을 제공합니다. 영향력있는 요인들의 도움으로 [!DNL Customer AI] 고객이 무엇을 할 수 있고 왜 하는지 알려 줄 수 있습니다. 또한 마케터는 다음과 같은 이점을 얻을 수 있습니다 [!DNL Customer AI] 가장 적절한 오퍼와 메시지를 제공하여 고객 경험을 개인화할 수 있는 예측 및 통찰력. |
| [!DNL Attribution AI] | [!DNL Attribution AI] 는 지정된 결과에 대한 고객 상호 작용의 영향 및 점진적 영향을 계산하는 멀티채널 알고리즘 속성 서비스입니다. 마케터는 [!DNL Attribution AI]를 통해 고객 여정의 각 단계에서 개별 고객과의 인터랙션이 미치는 영향을 파악하여 마케팅 및 광고 비용을 측정하고 최적화할 수 있습니다. |

**알려진 문제**

* 현재 알려진 문제가 없습니다.

에 대한 자세한 내용 [!DNL Intelligent Services] 그리고 무엇을 제공해야 하는지, [Intelligent Services 개요](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화 및 상호 운용성은 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe을 기반으로 하는 (XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 자동 대체 표시 정보 | 다음 [!DNL Schema Registry] 에 구성된 사용자 지정 제목 및 설명 값을 자동으로 적용합니다. `alternateDisplayInfo` 설명자. |
| 스칼라 필드 제한 사항 | 다음 [!DNL Schema Registry] 단일 스키마에서 6000개 이상의 스칼라 필드를 허용하지 않습니다. |
| 성능 점검 | 다음 [!DNL Schema Registry] 의 요구 사항을 충족하기 위해 정비되었습니다. [!DNL Experience Platform] 더 좋아. |

**버그 수정**

* 표준 XDM에서 중첩된 URI 필드에 대해 더 깨끗한 XED 형식을 지원하도록 XDM을 XED 변환으로 업데이트했습니다.

**알려진 문제**

* 알려짐

## 데이터 거버넌스 {#governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 내에서 중요한 역할을 합니다. [!DNL Experience Platform] 카탈로그 작성, 데이터 계보, 데이터 사용 레이블 지정, 데이터 액세스 정책 및 마케팅 작업을 위한 데이터에 대한 액세스 제어 등 다양한 수준에서 사용됩니다.

데이터 거버넌스를 시작하려면 고객 데이터에 적용되는 규정, 계약 의무 및 기업 정책을 철저히 이해해야 합니다. 거기에서 적절한 데이터 사용 레이블을 적용하여 데이터를 분류할 수 있으며, 데이터 사용 정책의 정의를 통해 그 사용을 제어할 수 있다.

데이터 거버넌스 프레임워크는 를 통해 데이터를 분류하고 데이터 사용 정책을 만드는 프로세스를 단순화하고 간소화합니다 [!DNL Experience Platform] 사용자 인터페이스 및 [!DNL Policy Service] API.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI에서 데이터 사용 정책 관리 | 이제 데이터 사용 정책을 내에서 관리할 수 있습니다. **정책** 의 작업 공간 [!DNL Experience Platform] UI. 다음을 참조하십시오. [정책 사용 안내서](../../data-governance/policies/user-guide.md) 추가 정보. |

**알려진 문제**

* None.

자세한 내용은 다음을 참조하십시오. [데이터 거버넌스 개요](../../data-governance/home.md).


## 대상 {#destinations}

위치 [Real-time Customer Data Platform](../../rtcdp/overview.md), 대상은 이러한 파트너에게 데이터를 원활하게 활성화하는 대상 플랫폼과의 사전 구축된 통합입니다.

**새 대상**

Real-Time CDP은 이제 50대 이상으로의 데이터 활성화를 지원합니다 [!DNL Experience Cloud Launch] 확장, 분석 활성화, 개인화 및 기타 사용 사례. 자세한 내용은 아래를 참조하십시오.

| 설명서 | 설명 |
|--- | ---|
| [대상 유형 및 범주](../../destinations/destination-types.md) | 이 문서에서는 Real-Time CDP 인터페이스의 연결과 확장의 차이점을 설명하고 이러한 각 대상을 사용할 시기를 권장합니다. |
| [Experience Platform Launch 확장](../../destinations/catalog/launch-extensions/overview.md) | 이 페이지에서는 다음 항목을 설명합니다. [!DNL Launch] 확장은 , 사용 사례를 나열하는 것이며, 각 확장에 대한 설명서 링크입니다. [!DNL Launch] Real-Time CDP 확장. |

자세한 내용은 다음을 참조하십시오. [대상 개요](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 포함 [!DNL Privacy Service], Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| PDPA 지원 | 이제 태국의 개인 정보 보호법(PDPA)에 따라 개인 정보 보호 요청을 만들고 추적할 수 있습니다. API에서 개인 정보 요청을 할 때 `regulation` 배열이 &quot;pdpa_tha&quot; 값을 허용합니다. |
| UI의 네임스페이스 유형 | 이제 의 요청 빌더에서 다른 네임스페이스 유형을 지정할 수 있습니다. [!DNL Privacy Service] UI. 다음을 참조하십시오. [사용 안내서](../../privacy-service/ui/user-guide.md) 추가 정보. |
| 이전 끝점 사용 중단 | 이전 API 끝점(`data/privacy/gdpr`)은 더 이상 사용되지 않습니다. |

알려진 문제

* None

에 대한 자세한 내용 [!DNL Privacy Service], 다음 문서를 읽는 것부터 시작하십시오. [Privacy Service 개요](../../privacy-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터베이스에 대한 API 및 UI 지원 | 용 새 소스 커넥터 [!DNL Apache Spark] (HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (HDInsights에서) 및 [!DNL Phoenix]. |
| 결제 기반 애플리케이션에 대한 API 및 UI 지원 | 용 새 소스 커넥터 [!DNL PayPal]. |
| 프로토콜 기반 애플리케이션에 대한 API 및 UI 지원 | 용 새 소스 커넥터 [!DNL Generic OData]. |

**알려진 문제**

* None

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
