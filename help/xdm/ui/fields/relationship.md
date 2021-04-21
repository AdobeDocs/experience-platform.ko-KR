---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 영역;관계;필드;home;popular topics;api;XDM system;experience data model;ui;workspace;relationship;field
solution: Experience Platform
title: UI에서 관계 필드 정의
description: Experience Platform 사용자 인터페이스에서 관계 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# UI에서 관계 필드 정의

XDM(경험 데이터 모델)에서 [union schema](../../schema/composition.md#union)은 [실시간 고객 프로필](../../../profile/home.md)에도 대해 활성화된 동일한 클래스에 속하는 모든 스키마의 통합 보기입니다. 결합 스키마는 서로 다른 경험 데이터에서 고객을 완전히 나타내기 위해 프로필에서 활용됩니다.

경우에 따라 프로필의 일부일 필요는 없지만 프로필과 관련이 있는 데이터를 인제스트할 수 있습니다. 이러한 유형의 데이터의 예는 고객에게 &quot;가장 선호하는 호텔&quot; 필드가 될 수 있습니다. 사람들이 즐겨찾는 호텔의 속성은 개인의 특성이 아니므로 호텔은 [!DNL XDM Individual Profile]이 아닌 사용자 정의 클래스를 기반으로 별도의 스키마를 표현하는 것이 가장 좋습니다.

결합 스키마는 동일한 클래스를 공유하는 스키마만을 기반으로 하므로, 프로필에 사용하기 위해 &quot;호텔&quot; 스키마를 활성화하면 [!DNL XDM Individual Profile]에 대한 필드 결합 스키마가 포함되지 않습니다. 대신 &quot;호텔&quot;과 조합에 속하는 다른 스키마 간의 관계를 정의해야 합니다. 여기에는 대상 스키마의 기본 ID를 참조하는 소스 스키마에 **관계 필드**&#x200B;을 정의하는 작업이 포함됩니다.

Adobe Experience Platform UI에서 두 스키마 간의 관계를 정의하는 자세한 방법은 [관계 UI 자습서](../../tutorials/relationship-ui.md)를 참조하십시오.
