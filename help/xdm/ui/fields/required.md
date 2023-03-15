---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;필수;필드;
title: UI에서 필수 필드 정의
description: Experience Platform 사용자 인터페이스에서 필수 XDM 필드를 정의하는 방법을 알아봅니다.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# UI에서 필수 필드 정의

XDM(Experience Data Model)에서 필수 필드는 데이터 수집 중에 특정 레코드나 시계열 이벤트를 적용하려면 유효한 값을 제공해야 함을 나타냅니다. 필수 필드에 대한 일반적인 사용 사례에는 사용자 ID 정보와 타임스탬프가 포함됩니다.

>[!IMPORTANT]
>
>스키마 필드의 필요 여부에 관계없이 Platform은 를 승인하지 않습니다 `null` 또는 수집된 모든 필드의 값이 비어 있습니다. 레코드나 이벤트에 특정 필드에 대한 값이 없는 경우 해당 필드의 키를 수집 페이로드에서 제외해야 합니다.

날짜 [새 필드 정의](./overview.md#define) Adobe Experience Platform 사용자 인터페이스에서 다음을 선택하여 필수 필드로 설정할 수 있습니다. **[!UICONTROL 필수]** 오른쪽 레일의 확인란 선택 **[!UICONTROL 적용]** 변경 사항을 스키마에 적용합니다.

![필수 확인란](../../images/ui/fields/required/root.png)

필드가 테넌트 ID 개체 아래의 루트 수준 속성이면 해당 경로는 **[!UICONTROL 필수 필드]** 왼쪽 레일에서.

![루트 레벨 필수 필드](../../images/ui/fields/required/applied.png)

그러나 필수 필드가 필수 필드로 표시되지 않은 오브젝트 내에 중첩된 경우 중첩된 필드는 아래에 표시되지 않습니다 **[!UICONTROL 필수 필드]** 왼쪽 레일에서.

아래 예에서는 `internalSKU` 필드가 필요에 따라 설정되지만 상위 오브젝트 `SKUs` 아님. 이 경우 다음과 같은 경우에는 유효성 검사 오류가 발생하지 않습니다 `SKUs` 하위 필드가 있더라도 데이터 수집 시 제외됨 `internalSKU` 필수 항목으로 표시됩니다. 즉, 반면에 `SKUs` 은(는) 선택 사항이며 다음을 포함해야 합니다. `internalSKU` 포함된 이벤트의 필드.

![중첩된 필수 필드](../../images/ui/fields/required/nested.png)

스키마에서 중첩된 필드가 항상 필요하도록 하려면 테넌트 ID 개체를 제외하고 모든 상위 필드도 필요에 따라 설정해야 합니다.

![상위 및 하위 필수 필드](../../images/ui/fields/required/parent-and-child.png)

## 다음 단계

이 안내서에서는 UI에서 필수 필드를 정의하는 방법을 다룹니다. 의 개요 보기 [UI의 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [!DNL Schema Editor].
