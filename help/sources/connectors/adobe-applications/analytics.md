---
keywords: Experience Platform;홈;인기 항목;분석 소스 커넥터;분석;분석;Analytics;home;popular topics
solution: Experience Platform
title: 보고서 세트 데이터용 Adobe Analytics 소스 커넥터
topic-legacy: overview
description: 이 문서에서는 Analytics의 개요를 제공하며 Analytics 데이터의 사용 사례에 대해 설명합니다.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 3%

---

# 보고서 세트 데이터용 Adobe Analytics 소스 커넥터

Adobe Experience Platform을 사용하면 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터를 인제스트할 수 있습니다. [!DNL Analytics] 소스 커넥터는 SCDS 형식 [!DNL Analytics] 데이터를 플랫폼별 소비를 위해 [!DNL Experience Data Model](XDM) 필드로 변환하여 실시간으로 [!DNL Analytics]에서 수집한 데이터를 플랫폼으로 스트리밍합니다.

이 문서에서는 [!DNL Analytics]의 개요를 제공하며 [!DNL Analytics] 데이터의 사용 사례에 대해 설명합니다.

## Adobe Analytics 및 분석 데이터

[!DNL Analytics] 강력한 엔진으로 고객에 대한 자세한 정보와 고객이 웹 자산과 상호 작용하는 방법, 디지털 마케팅 비용이 효과적인 위치를 확인하고 향상 영역을 식별할 수 있습니다. [!DNL Analytics] 연간 수 조개에 달하는 웹 트랜잭션을 처리하고  [!DNL Analytics] 소스 커넥터를 사용하면 이 풍부한 행동 데이터를 손쉽게 활용하고 신속하게 데이터 [!DNL Real-time Customer Profile] 를 보강할 수 있습니다.

![](./images/analytics-data-experience-platform.png)

높은 수준에서 [!DNL Analytics]은 전세계 여러 디지털 채널과 데이터 센터의 데이터를 수집합니다. 데이터가 수집되면, VISTA(Visitor Identification, Segmentation and Transformation Architecture) 규칙 및 처리 규칙이 들어오는 데이터를 형성하는 데 적용됩니다. 원시 데이터가 이러한 경량 처리를 거친 후 [!DNL Real-time Customer Profile]에 의해 소비될 준비가 된 것으로 간주됩니다. 앞서 언급한 것과 같은 프로세스에서, 동일한 처리된 데이터는 마이크로 묶어서 플랫폼 데이터세트에 수집하여 [!DNL Data Science Workspace], [!DNL Query Service] 및 기타 데이터 검색 애플리케이션별로 소비합니다.

처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules.html)를 참조하십시오.

## 경험 데이터 모델(XDM)

XDM은 Experience Platform에서 서비스와 통신하는 데 사용할 응용 프로그램의 공통 구조와 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 일관되게 통합할 수 있으므로 데이터를 손쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md)를 참조하십시오.

## Adobe Analytics에서 XDM으로 필드를 매핑하는 방법은 무엇입니까?

플랫폼 사용자 인터페이스를 사용하여 [!DNL Analytics] 데이터를 Experience Platform으로 가져오기 위해 소스 연결이 설정되면 데이터 필드가 자동으로 매핑되고 몇 분 내에 [!DNL Real-time Customer Profile]에 수집됩니다. 플랫폼 UI를 사용하여 [!DNL Analytics]으로 소스 연결을 만드는 방법에 대한 지침은 [Analytics 소스 커넥터 자습서](../../tutorials/ui/create/adobe-applications/analytics.md)를 참조하십시오.

[!DNL Analytics] 및 Experience Platform 사이에 발생하는 필드 매핑에 대한 자세한 내용은 [Adobe Analytics 필드 매핑](./mapping/analytics.md) 안내서를 참조하십시오.

## 플랫폼의 분석 데이터에 대한 예상 지연은 무엇입니까?

| 분석 데이터 | 예상 지연 |
| -------------- | ---------------- |
| [!DNL Real-time Customer Profile](A4T **이(가) 활성화되지 않음**) 새 데이터 | &lt; 2분 |
| [!DNL Real-time Customer Profile](A4T **이(가)**&#x200B;이(가) 활성화됨) 새 데이터 | &lt; 15분 |
| Data Lake의 새로운 데이터 | &lt; 90분 |
| 데이터 채우기(13개월 데이터 또는 100억 이벤트 중 더 낮음) | &lt; 4주 |

>[!NOTE]
>
>지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어 [!DNL Analytics] 구현이 `A4T`로 구성된 경우 파이프라인에 대한 지연이 5-10분으로 증가합니다.

## [!DNL Analytics] 데이터의 기본 식별자

[!DNL Analytics] 소스 커넥터의 모든 히트에는 ECID 또는 AAID가 있는지 여부에 따라 결정되는 기본 식별자가 포함됩니다. ECID가 있으면 ECID가 기본 식별자로 지정됩니다. AID가 있는 경우 AID가 1차 AID로 지정됩니다.
