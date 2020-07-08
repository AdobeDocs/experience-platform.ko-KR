---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics 데이터 커넥터
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Analytics 데이터 커넥터

Adobe Experience Platform을 사용하면 ADC(Analytics 데이터 커넥터)를 통해 Adobe Analytics 데이터를 인제스트할 수 있습니다. ADC는 Adobe Analytics에서 수집한 데이터를 실시간으로 Platform으로 스트리밍하여 Platform에 의한 소비를 위해 SCDS 형식의 Analytics 데이터를 XDM(Experience Data Model) 필드로 변환합니다.

이 문서에서는 Adobe Analytics의 개요를 제공하며 Analytics 데이터의 사용 사례를 설명합니다.

## Adobe Analytics 및 Analytics 데이터

Adobe Analytics은 고객에 대한 자세한 정보와 고객이 웹 자산과 상호 작용하는 방법, 디지털 마케팅 비용이 효과적인 위치를 확인하고 향상 영역을 식별할 수 있는 강력한 엔진입니다. Adobe Analytics은 연간 수 조 개의 웹 트랜잭션을 처리하고 ADC를 통해 이러한 풍부한 행동 데이터를 손쉽게 활용하고 몇 분 만에 실시간 고객 프로파일을 강화할 수 있습니다.

![](./images/analytics-data-experience-platform.png)

높은 수준의 Adobe Analytics은 전 세계의 다양한 디지털 채널 및 데이터 센터에서 데이터를 수집합니다. 데이터가 수집되면 들어오는 데이터를 형성하기 위해 방문자 식별, 세분화 및 변형 아키텍처(VISTA) 규칙 및 처리 규칙이 적용됩니다. Raw 데이터가 이러한 경량 처리를 거친 후 실시간 고객 프로필에서 사용할 준비가 된 것으로 간주됩니다. 앞서 언급한 것과 유사한 프로세스에서, 처리된 동일한 데이터는 마이크로 배칭되고 데이터 과학 작업 공간, 쿼리 서비스 및 기타 데이터 검색 응용 프로그램에서 사용하기 위해 Platform 데이터 세트에 수집됩니다.

처리 [규칙에 대한 자세한 내용은 처리 규칙 개요를](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules.html) 참조하십시오.

## XDM(Experience Data Model)

XDM은 Adobe Experience Platform에서 서비스와 통신하는 데 사용하는 애플리케이션에 대한 공통 구조와 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 일관되게 통합할 수 있으므로 데이터를 손쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요를 참조하십시오](../../../xdm/home.md).

## Adobe Analytics에서 XDM으로 필드를 매핑하려면 어떻게 해야 합니까?

Platform 사용자 인터페이스를 사용하여 Analytics 데이터를 Experience Platform으로 가져오기 위해 소스 연결이 설정되면 데이터 필드가 자동으로 매핑되고 몇 분 내에 실시간 고객 프로파일에 수집됩니다. Platform UI를 사용하여 Adobe Analytics와의 소스 연결을 만드는 방법에 대한 지침은 [Analytics 데이터 커넥터 자습서를 참조하십시오](../../tutorials/ui/create/adobe-applications/analytics.md).

Analytics과 Experience Platform 간에 발생하는 필드 매핑에 대한 자세한 내용은 [Adobe Analytics 필드 매핑](./mapping/analytics.md) 안내서를 참조하십시오.

## Platform의 Analytics 데이터에 대한 예상 지연은 무엇입니까?

| 분석 데이터 | 예상 지연 |
| -------------- | ---------------- |
| 실시간 고객 프로필에 대한 새 데이터(A4T가 **활성화되지 않음** ) | &lt; 2분 |
| 실시간 고객 프로필에 대한 새 데이터(A4T **가** 활성화됨) | &lt; 15분 |
| Data Lake의 새로운 데이터 | &lt; 45분 |
| 데이터 채우기(데이터 13개월 또는 100억 이벤트 중 더 낮음) | &lt; 4주 |

>[!NOTE]
>
>지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어, Analytics 구현이 파이프라인에 대한 지연 `A4T` 으로 구성된 경우 5-10분으로 증가합니다.