---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics 데이터 커넥터
topic: overview
translation-type: tm+mt
source-git-commit: 662ca170b7416dfb55cfb6b8cbaef640c1f83d31
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Analytics 데이터 커넥터

Adobe Experience Platform을 사용하면 ADC(Analytics Data Connector)를 통해 Adobe Analytics 데이터를 인제스트할 수 있습니다. ADC는 SCDS 형식 데이터 [!DNL Analytics] 를 [!DNL Platform] (XDM) 필드로 변환하여 실시간 [!DNL Analytics] 으로 수집된 데이터를 스트리밍하여 소비별 [!DNL Experience Data Model] (XDM) 필드로 [!DNL Platform]활용합니다.

이 문서에서는 데이터에 대한 개요 [!DNL Analytics] 와 사용 사례를 설명합니다 [!DNL Analytics] .

## Adobe Analytics 및 분석 데이터

[!DNL Analytics] 는 고객에 대한 자세한 정보와 고객이 웹 자산과 상호 작용하는 방법, 디지털 마케팅 비용이 효과적인 위치를 확인하고 향상 영역을 식별하는 데 도움이 되는 강력한 엔진입니다. [!DNL Analytics] 연간 수 조 개의 웹 트랜잭션을 처리하고 ADC를 사용하면 다양한 행동 데이터를 손쉽게 활용할 수 있으며 몇 분 만에 [!DNL Real-time Customer Profile] 더 많은 컨텐츠를 제공할 수 있습니다.

![](./images/analytics-data-experience-platform.png)

높은 수준에서, 전 세계의 다양한 디지털 채널과 데이터 센터에서 데이터를 [!DNL Analytics] 수집합니다. 데이터가 수집되면 들어오는 데이터를 형성하기 위해 방문자 식별, 세분화 및 변형 아키텍처(VISTA) 규칙 및 처리 규칙이 적용됩니다. 원시 데이터가 이러한 경량 처리를 거친 후 소비할 준비가 된 것으로 간주됩니다 [!DNL Real-time Customer Profile]. 앞서 언급한 것과 같은 프로세스에서, 동일한 처리된 데이터는 마이크로 배칭되고 플랫폼 데이터 세트에 수집되어, 데이터 검색 애플리케이션 [!DNL Data Science Workspace]과 기타 데이터 검색 애플리케이션 [!DNL Query Service]이 소비합니다.

처리 [규칙에 대한 자세한 내용은 처리 규칙 개요를](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules.html) 참조하십시오.

## XDM(Experience Data Model)

XDM은 서비스 통신 시 사용하는 애플리케이션에 대한 공통 구조와 정의를 제공하는 공개적으로 문서화된 사양입니다 [!DNL Experience Platform].

XDM 표준을 준수하면 데이터를 일관되게 통합할 수 있으므로 데이터를 손쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요를 참조하십시오](../../../xdm/home.md).

## Adobe Analytics에서 XDM으로 필드를 어떻게 매핑합니까?

사용자 인터페이스를 [!DNL Analytics] 사용하여 [!DNL Experience Platform] 데이터를 가져올 수 있도록 소스 연결이 설정되면 데이터 필드가 자동으로 매핑되고 몇 분 [!DNL Platform] [!DNL Real-time Customer Profile] 내에 수집됩니다. UI [!DNL Analytics] 를 사용하여 소스 연결을 만드는 방법에 대한 지침은 [!DNL Platform] 분석 데이터 커넥터 자습서를 참조하십시오 [](../../tutorials/ui/create/adobe-applications/analytics.md).

및 사이에 발생하는 필드 매핑에 대한 자세한 내용 [!DNL Analytics] 은 [!DNL Experience Platform]Adobe Analytics 필드 매핑 [](./mapping/analytics.md) 안내서를 참조하십시오.

## 플랫폼의 분석 데이터에 대한 예상 지연은 무엇입니까?

| 분석 데이터 | 예상 지연 |
| -------------- | ---------------- |
| 새 데이터 [!DNL Real-time Customer Profile] (A4T가 **활성화되지** 않음) | &lt; 2분 |
| 새 데이터 [!DNL Real-time Customer Profile] (A4T **가 활성화됨** ) | &lt; 15분 |
| Data Lake의 새로운 데이터 | &lt; 45분 |
| 데이터 채우기(데이터 13개월 또는 100억 이벤트 중 더 낮음) | &lt; 4주 |

>[!NOTE] 지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어 Analytics 구현이 파이프라인에 대한 지연 `A4T` 으로 구성된 경우 5-10분으로 증가합니다.

## Analytics 데이터의 기본 식별자

Analytics 데이터 커넥터의 모든 히트에는 ECID 또는 AAID가 존재하는지 여부에 따라 결정되는 기본 식별자가 포함됩니다. ECID가 있는 경우 ECID가 기본 식별자로 지정됩니다. AID가 있는 경우 AAID가 기본 AID로 지정됩니다.