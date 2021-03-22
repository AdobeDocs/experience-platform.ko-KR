---
solution: Experience Platform
title: 업계 데이터 모델 개요
topic: 개요
description: 표준 XDM(Experience Data Model) 구성 요소를 사용하여 구성할 수 있는 다양한 산업 분야의 표준화된 데이터 모델에 대해 알아보십시오.
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 업계 데이터 모델 개요

XDM(Experience Data Model)을 사용하면 사용자 정의 가능한 스키마를 만들어 비즈니스와 관련된 주요 고객 경험 데이터를 캡처할 수 있습니다. XDM을 준수하는 데이터 모델링 프로세스를 간소화하기 위해 Adobe Experience Platform은 여러 업계에서 일반적으로 사용되는 개념을 캡처하는 다양한 기능의 표준 XDM 구성 요소를 제공합니다.

>[!NOTE]
>
>새로운 표준 XDM 구성 요소는 소비자의 요구 사항에 맞게 지속적으로 출시되고 있습니다. 최신 구성 요소 목록을 보려면 [UI](../../ui/explore.md)의 기존 리소스를 탐색하거나 GitHub에서 [공식 XDM 리포지토리](https://github.com/adobe/xdm/tree/master/components)를 참조하십시오.

기업이 운영하는 업계에 따라 일부 XDM 구성 요소는 다른 구성 요소보다 고객의 요구 사항과 더 관련이 있습니다. 또한 XDM 스키마 간에 설정하는 관계는 업종에 따라 달라집니다.

특정 업계를 기반으로 데이터 모델링 전략을 안내하기 위해 이 가이드는 지원되는 여러 산업 분야의 수직선에 대해 엔티티 관계 다이어그램(ERD)에 대한 참조를 제공합니다.

## 전제 조건

이 안내서에서 참조되는 ERD를 읽으려면 XDM 구성 요소가 양식 스키마와 상호 작용하는 방법 및 XDM 스키마가 Experience Platform에서 전체적으로 작동하는 방식에 대해 잘 알고 있어야 합니다. 계속하기 전에 다음 개요 설명서를 읽었는지 확인하십시오.

* [XDM 시스템 개요](../../home.md):플랫폼 생태계에서 XDM이 작동하는 방식을 살펴볼 수 있습니다.
* [스키마 컴포지션의 기본 사항](../../schema/composition.md):XDM 구성 요소(예: 믹싱, 클래스 및 데이터 유형)가 스키마 구조와 ID 필드 역할에 어떻게 기여하는지를 알아봅니다.

데이터를 XDM에 매핑하는 방법에 대한 일반적인 지침은 [데이터 모델링 모범 사례 가이드](../../schema/best-practices.md)를 검토하는 것이 좋습니다.

## 업계 데이터 모델 ERD {#erds}

아래 ERD로 표시된 업계 수직 모델은 표준화된 방식으로 의도적으로 만들어지며 데이터가 플랫폼에 저장되는 방식을 고려합니다.

지정된 ERD의 경우 에 표시된 각 엔티티는 기본 XDM 클래스를 기반으로 합니다. 지정된 엔티티에 대해 **굵게**&#x200B;에 표시된 각 행은 아래 줄바꿈되지 않은 텍스트로 나열되는 관련 필드와 함께 혼합이나 데이터 유형을 나타냅니다. 주어진 엔티티에 대한 가장 중요한 필드는 빨간색으로 강조 표시됩니다.

>[!NOTE]
>
>일부 엔티티에는 &quot;_ID&quot; 필드가 포함될 수 있습니다. 인제스트될 때 Platform에서 이벤트 또는 프로필 엔터티에 자동으로 할당하는 고유 식별자(`_id`)를 나타냅니다. 하지만 원할 경우 이 필드에 고유한 ID 값을 사용하도록 선택할 수 있습니다.

개별 고객을 식별하는 데 사용할 수 있는 모든 속성은 &quot;기본 ID&quot;로 표시된 이러한 속성 중 하나로 &quot;ID&quot;로 표시됩니다.

쿠키 기반 이벤트는 종종 트랜잭션을 수행한 개인 또는 개인을 확인할 수 없으므로 엔티티 관계는 종속되지 않는 것으로 표시됩니다.

ERD는 다음과 같은 업계별로 제공됩니다.

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)
* [[!UICONTROL Telecommunications]](./telecom.md)

## 다음 단계

이 문서에서는 업계 데이터 모델 ERD의 개요와 이를 해석하는 방법을 제공합니다. ERD를 보려면 위의 목록에서 하나를 선택합니다.