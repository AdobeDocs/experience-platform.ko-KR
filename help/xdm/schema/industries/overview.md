---
solution: Experience Platform
title: 업계 데이터 모델 개요
description: 표준 경험 데이터 모델(XDM) 구성 요소를 사용하여 구성할 수 있는 다양한 업계 카테고리에 대한 표준화된 데이터 모델에 대해 알아봅니다.
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 업계 데이터 모델 개요

XDM(경험 데이터 모델) 을 사용하면 사용자 지정이 가능한 스키마를 만들어 비즈니스와 관련된 주요 고객 경험 데이터를 캡처할 수 있습니다. XDM을 준수하도록 데이터를 모델링하는 프로세스를 간소화하기 위해 Adobe Experience Platform은 여러 산업에서 일반적으로 사용되는 개념을 캡처하는 범용 표준 XDM 구성 요소 제품군을 제공합니다.

>[!NOTE]
>
>새로운 표준 XDM 구성 요소는 소비자 요구에 가장 잘 맞도록 지속적으로 출시되고 있습니다. 최신 구성 요소 목록의 경우 다음 작업을 수행할 수 있습니다 [ui에서 기존 리소스 살펴보기](../../ui/explore.md) 또는 [공식 XDM 저장소](https://github.com/adobe/xdm/tree/master/components) GitHub에서.

비즈니스가 운영되는 산업에 따라 일부 XDM 구성 요소는 다른 구성 요소보다 사용자의 요구 사항과 더 관련이 있을 수 있습니다. 또한 XDM 스키마 간에 설정하는 관계는 업계에 따라 달라집니다.

특정 산업을 기반으로 데이터 모델링 전략을 안내하는 데 도움이 되도록 이 안내서에서는 지원되는 여러 업계 카테고리에 대한 엔티티 관계 다이어그램(ERD) 참조를 제공합니다.

## 전제 조건

이 안내서에서 참조하는 ERD를 읽으려면 XDM 구성 요소가 상호 작용하여 스키마를 형성하는 방법과 XDM 스키마가 Experience Platform에서 전체적으로 작동하는 방식을 이해해야 합니다. 계속하기 전에 다음 개요 설명서를 읽었는지 확인하십시오.

* [XDM 시스템 개요](../../home.md): XDM이 플랫폼 생태계에서 작동하는 방식을 알아봅니다.
* [스키마 컴포지션 기본 사항](../../schema/composition.md): XDM 구성 요소(예: 스키마 필드 그룹, 클래스 및 데이터 유형)가 스키마 구조와 ID 필드 역할에 어떻게 기여하는지 알아봅니다.

또한 다음을 검토하는 것이 좋습니다. [data modeling 우수 사례 안내서](../../schema/best-practices.md) 데이터를 XDM에 매핑하는 방법에 대한 일반 지침

## 업계 데이터 모델 ERD {#erds}

ERD는 다음 업계 카테고리에 제공됩니다.

* [[!UICONTROL 리테일]](./retail.md)
* [[!UICONTROL 금융 서비스]](./financial.md)
* [[!UICONTROL 의료 서비스]](./healthcare.md)
* [[!UICONTROL 전기 통신]](./telecom.md)
* [[!UICONTROL 여행 및 접대]](./travel-hospitality.md)

## 다음 단계

이 문서에서는 업계 데이터 모델 ERD와 이를 해석하는 방법에 대한 개요를 제공했습니다. ERD를 보려면 위의 목록에서 하나를 선택하십시오.
