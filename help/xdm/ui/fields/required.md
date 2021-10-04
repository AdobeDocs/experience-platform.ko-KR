---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;필수;필드;
title: UI에서 필수 필드 정의
description: Experience Platform 사용자 인터페이스에서 필수 XDM 필드를 정의하는 방법을 알아봅니다.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# UI에서 필수 필드 정의

XDM(Experience Data Model)에서 필수 필드는 데이터 섭취 중에 특정 레코드 또는 시계열 이벤트를 허용하려면 유효한 값을 제공해야 함을 나타냅니다. 필수 필드에 대한 일반적인 사용 사례에는 사용자 ID 정보 및 타임스탬프가 포함됩니다.

Adobe Experience Platform 사용자 인터페이스에서 [새 필드](./overview.md#define)를 정의하는 경우 오른쪽 레일에서 **[!UICONTROL 필수]** 확인란을 선택하여 필수 필드로 설정할 수 있습니다. 스키마에 변경 사항을 적용하려면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![필수 확인란](../../images/ui/fields/required/root.png)

필드가 테넌트 ID 개체 아래의 루트 수준 속성이면 해당 경로가 왼쪽 레일의 **[!UICONTROL 필수 필드]** 아래에 즉시 나타납니다.

![루트 수준 필수 필드](../../images/ui/fields/required/applied.png)

필수 필드가 필수 필드로 표시되지 않는 개체 내에 중첩된 경우 왼쪽 레일의 **[!UICONTROL 필수 필드]** 아래에 중첩된 필드가 표시되지 않습니다.

아래 예에서 `loyaltyId` 필드는 필수로 설정되지만 상위 개체 `loyalty`은(는) 설정되지 않습니다. 이 경우 하위 필드 `loyaltyId`이 필수로 표시되더라도 데이터를 수집할 때 `loyalty`이 제외되면 유효성 검사 오류가 발생하지 않습니다. 즉, `loyalty`은(는) 선택 사항이지만 포함하는 이벤트에서 `loyaltyId` 필드를 포함해야 합니다.

![중첩된 필수 필드](../../images/ui/fields/required/nested.png)

스키마에서 항상 중첩 필드가 필수 필드이면 모든 상위 필드도 필수로 설정해야 합니다(테넌트 ID 개체 제외).

![상위 및 하위 필수 필드](../../images/ui/fields/required/parent-and-child.png)

## 다음 단계

이 안내서에서는 UI에서 필수 필드를 정의하는 방법을 다룹니다. [!DNL Schema Editor]에서 다른 XDM 필드 유형을 정의하는 방법을 알려면 UI](./overview.md#special)에서 필드 정의 개요를 참조하십시오.[
