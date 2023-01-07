---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;필수;필드;
title: UI에서 필수 필드 정의
description: Experience Platform 사용자 인터페이스에서 필수 XDM 필드를 정의하는 방법을 알아봅니다.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# UI에서 필수 필드 정의

XDM(Experience Data Model)에서 필수 필드는 데이터 섭취 중에 특정 레코드 또는 시계열 이벤트를 허용하려면 유효한 값을 제공해야 함을 나타냅니다. 필수 필드에 대한 일반적인 사용 사례에는 사용자 ID 정보 및 타임스탬프가 포함됩니다.

>[!IMPORTANT]
>
>스키마 필드가 필수인지 여부에 관계없이 Platform은 이를 허용하지 않습니다 `null` 또는 수집된 필드의 값이 비어 있습니다. 레코드 또는 이벤트에 특정 필드에 대한 값이 없는 경우 해당 필드의 키는 수집 페이로드에서 제외해야 합니다.

When [새 필드 정의](./overview.md#define) Adobe Experience Platform 사용자 인터페이스에서 을(를) 선택하여 필수 필드로 설정할 수 있습니다 **[!UICONTROL 필수 여부]** 오른쪽 레일에 있는 확인란. 선택 **[!UICONTROL 적용]** 스키마에 변경 사항을 적용하려면

![필수 확인란](../../images/ui/fields/required/root.png)

필드가 테넌트 ID 개체 아래의 루트 수준 속성이면 해당 경로가 바로 아래에 나타납니다 **[!UICONTROL 필수 필드]** 왼쪽 레일에 있습니다.

![루트 수준 필수 필드](../../images/ui/fields/required/applied.png)

필수 필드가 필수 필드로 표시되지 않는 개체 내에 중첩된 경우 중첩된 필드가 아래에 표시되지 않습니다 **[!UICONTROL 필수 필드]** 왼쪽 레일에 있습니다.

아래 예에서는 `internalSKU` 필드는 필수로 설정되지만 상위 개체는 `SKUs` 은 아닙니다. 이 경우 다음과 같은 경우 유효성 검사 오류가 발생하지 않습니다 `SKUs` 하위 필드가 있어도 데이터를 수집할 때 제외됩니다 `internalSKU` 은 필수로 표시됩니다. 다른 말로 하자면 `SKUs` 는 선택 사항이며 반드시 포함해야 합니다 `internalSKU` 포함하는 이벤트의 필드입니다.

![중첩된 필수 필드](../../images/ui/fields/required/nested.png)

스키마에서 항상 중첩 필드가 필수 필드이면 모든 상위 필드도 필수로 설정해야 합니다(테넌트 ID 개체 제외).

![상위 및 하위 필수 필드](../../images/ui/fields/required/parent-and-child.png)

## 다음 단계

이 안내서에서는 UI에서 필수 필드를 정의하는 방법을 다룹니다. 다음 사항에 대한 개요를 참조하십시오. [ui에서 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아봅니다. [!DNL Schema Editor].
