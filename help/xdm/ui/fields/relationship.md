---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;관계;필드;
solution: Experience Platform
title: UI에서 관계 필드 정의
description: Experience Platform 사용자 인터페이스에서 관계 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# UI에서 관계 필드 정의

XDM(Experience Data Model)에서 [조합 스키마](../../schema/composition.md#union) 도 활성화한 동일한 클래스에 속하는 모든 스키마에 대한 통합 보기입니다 [실시간 고객 프로필](../../../profile/home.md). 결합 스키마는 프로필에서 서로 다른 경험 데이터에서 고객을 완전히 대표하도록 활용합니다.

경우에 따라 프로필의 일부일 필요는 없지만 프로필과 관련이 있는 데이터를 수집할 수 있습니다. 이러한 종류의 데이터의 예는 고객이 &quot;가장 좋아하는 호텔&quot; 필드가 될 수 있습니다. 개인이 좋아하는 호텔의 특성은 그 개인의 특성이 아니기 때문에 호텔은 사용자 정의 클래스가 아닌 사용자 정의 클래스를 기반으로 한 별도의 스키마로 가장 잘 표현됩니다 [!DNL XDM Individual Profile].

결합 스키마는 동일한 클래스를 공유하는 스키마만 기반으로 하므로 프로필에 사용하기 위해 &quot;Hotels&quot; 스키마를 활성화하면 [!DNL XDM Individual Profile]. 대신 &quot;호텔&quot;과 조합에 속하는 다른 스키마 간의 관계를 정의해야 합니다. 여기에는 **관계 필드** 대상 스키마의 기본 ID를 참조하는 소스 스키마에서.

Adobe Experience Platform UI에서 두 스키마 간의 관계를 정의하는 자세한 단계는 다음을 참조하십시오. [관계 UI 자습서](../../tutorials/relationship-ui.md).
