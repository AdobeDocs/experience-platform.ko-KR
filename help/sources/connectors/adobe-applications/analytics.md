---
keywords: Experience Platform;홈;인기 항목;Analytics 소스 커넥터;분석;Analytics
solution: Experience Platform
title: 보고서 세트 데이터용 Adobe Analytics 소스 커넥터
topic-legacy: overview
description: 이 문서에서는 Analytics에 대한 개요를 제공하며 Analytics 데이터의 사용 사례를 설명합니다.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 9defe1c3087c2f1284ceedede9d274a51cf97b96
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 보고서 세트 데이터용 Adobe Analytics 소스 커넥터

Adobe Experience Platform에서는 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. [!DNL Analytics] 소스 커넥터는 [!DNL Analytics]에서 수집한 데이터를 실시간으로 플랫폼으로 스트리밍하여 SCDS 형식의 [!DNL Analytics] 데이터를 XDM([!DNL Experience Data Model]) 필드로 변환하여 플랫폼별로 소비합니다.

이 문서에서는 [!DNL Analytics] 개요를 제공하며 [!DNL Analytics] 데이터의 사용 사례를 설명합니다.

## Adobe Analytics 및 Analytics 데이터

[!DNL Analytics] 는 고객에 대해 자세히 알아보고 고객이 웹 자산과 상호 작용하는 방법, 디지털 마케팅 비용이 효과적인 위치를 확인하고 개선 영역을 식별하는 데 도움이 되는 강력한 엔진입니다. [!DNL Analytics] 매년 수조 개의 웹 트랜잭션을 처리하고  [!DNL Analytics] 소스 커넥터를 사용하면 이러한 풍부한 행동 데이터를 손쉽게 활용하고 단 몇 분  [!DNL Real-time Customer Profile] 안에 을 보강할 수 있습니다.

![](./images/analytics-data-experience-platform.png)

높은 수준에서 [!DNL Analytics]은(는) 전 세계의 다양한 디지털 채널 및 여러 데이터 센터에서 데이터를 수집합니다. 데이터가 수집되면 들어오는 데이터를 형성하기 위해 방문자 식별, 세그먼테이션 및 변환 아키텍처(VISTA) 규칙 및 처리 규칙이 적용됩니다. 원시 데이터가 이러한 경량 처리를 거친 후에는 [!DNL Real-time Customer Profile]에서 사용할 준비가 된 것으로 간주됩니다. 앞서 언급한 것과 동일한 프로세스에서 동일한 처리된 데이터는 마이크로 일괄 처리되어 [!DNL Data Science Workspace], [!DNL Query Service] 및 기타 데이터 검색 응용 프로그램이 소비할 수 있도록 플랫폼 데이터 세트에 수집됩니다.

처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html)를 참조하십시오.

## XDM(경험 데이터 모델)

XDM은 Experience Platform 시 서비스와 통신하는 데 사용할 응용 프로그램에 대한 공통 구조 및 정의를 제공하는 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 균일하게 통합할 수 있으므로 데이터를 보다 쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md)를 참조하십시오.

## Adobe Analytics에서 XDM으로 필드를 매핑하려면 어떻게 해야 합니까?

플랫폼 사용자 인터페이스를 사용하여 [!DNL Analytics] 데이터를 Experience Platform으로 가져오기 위한 소스 연결이 설정되면 데이터 필드가 자동으로 매핑되어 분 내에 [!DNL Real-time Customer Profile]에 수집됩니다. 플랫폼 UI를 사용하여 [!DNL Analytics]과(와) 소스 연결을 만드는 방법에 대한 지침은 [Analytics 소스 커넥터 자습서](../../tutorials/ui/create/adobe-applications/analytics.md)를 참조하십시오.

[!DNL Analytics] 과 Experience Platform 사이에 발생하는 필드 매핑에 대한 자세한 내용은 [Adobe Analytics 필드 매핑](./mapping/analytics.md) 안내서를 참조하십시오.

## 플랫폼에서 Analytics 데이터의 예상 대기 시간은 어떻게 됩니까?

플랫폼의 분석 데이터에 대한 예상 대기 시간은 아래 표에 요약되어 있습니다. 지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어 Analytics 구현이 `A4T`으로 구성된 경우 파이프라인에 대한 지연 시간이 5~10분으로 늘어납니다.

| 분석 데이터 | 예상 지연 |
| -------------- | ---------------- |
| [!DNL Real-time Customer Profile] 새 데이터(A4T **활성화되지 않음**) | &lt; 2분 |
| [!DNL Real-time Customer Profile] (A4T **is**&#x200B;가 활성화됨)에 대한 새 데이터 | &lt; 15분 |
| Data Lake의 새로운 데이터 | &lt; 90분 |
| 데이터 채우기(데이터 13개월 또는 100억 개 이벤트 중 더 낮음) | &lt; 4주 |

>[!NOTE]
>
>Analytics 채우기 데이터는 [!DNL Profile]에 수집되지 않으므로 라이선스 프로필에서 계산되지 않습니다.

## [!DNL Analytics] 데이터의 기본 식별자

[!DNL Analytics] 소스 커넥터의 모든 히트에는 ECID 또는 AAID가 있는지 여부에 따라 달라지는 기본 식별자가 포함되어 있습니다. ECID가 있는 경우 ECID가 기본 식별자로 지정됩니다. AAID가 있는 경우, AAID가 기본 AID로 지정됩니다.
