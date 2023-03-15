---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;관계;필드;
solution: Experience Platform
title: UI에서 관계 필드 정의
description: Experience Platform 사용자 인터페이스에서 관계 필드를 정의하는 방법을 알아봅니다.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# UI에서 관계 필드 정의

XDM(경험 데이터 모델)에서 [유니온 스키마](../../schema/composition.md#union) 는 또한 활성화된 동일한 클래스에 속하는 모든 스키마에 대한 통합 보기입니다. [실시간 고객 프로필](../../../profile/home.md). 결합 스키마를 프로필에서 활용하여 다양한 경험 데이터에서 고객에 대한 전체 표현을 구성합니다.

경우에 따라 반드시 프로필의 일부가 아니지만 프로필과 관련된 데이터를 수집할 수도 있습니다. 이러한 종류의 데이터의 예는 고객을 위한 &quot;즐겨 찾는 호텔&quot; 필드일 것입니다. 사용자가 즐겨 찾는 호텔의 속성은 사용자 자신의 속성이 아니므로 호텔은 사용자 정의 클래스보다는 사용자 정의 클래스에 따른 별도의 스키마로 가장 잘 표현됩니다 [!DNL XDM Individual Profile].

유니온 스키마는 동일한 클래스를 공유하는 스키마만 기반으로 하므로 프로필에서 사용하기 위해 &quot;Hotels&quot; 스키마를 활성화하면 의 필드 유니온 스키마가 포함되지 않습니다 [!DNL XDM Individual Profile]. 대신 &quot;호텔&quot;과 유니온에 속하는 다른 스키마 간의 관계를 정의해야 합니다. 여기에는 다음을 정의하는 작업이 포함됩니다. **관계 필드** 참조 스키마의 기본 id를 참조하는 소스 스키마에서.

Adobe Experience Platform UI에서 두 스키마 간의 관계를 정의하는 방법에 대한 자세한 단계는 다음을 참조하십시오. [관계 UI 튜토리얼](../../tutorials/relationship-ui.md).
