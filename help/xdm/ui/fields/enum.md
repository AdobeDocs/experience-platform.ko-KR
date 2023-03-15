---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;workspace;enum;필드;
solution: Experience Platform
title: UI에서 열거형 필드 및 제안 값 정의
description: Experience Platform 사용자 인터페이스의 문자열 필드에 대한 열거형 및 제안 값을 정의하는 방법을 알아봅니다.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# UI에서 열거형 및 제안 값 정의 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="열거형 및 제안 값"
>abstract="An **열거형** 사전 정의된 값 세트와 일치하는 데이터만 수집하도록 문자열 필드를 제한합니다. 각 열거형 제약 조건에는 **표시 이름** 세분화 UI에서 속성 드롭다운을 채웁니다. **제안 값** 필드의 경우 수집을 제한하지 않고 세그멘테이션에 표시되는 표시 이름만 결정합니다. 공통 클래스 또는 필드 그룹에 속하는 필드를 공유하는 여러 스키마가 있고 각 스키마 간에 해당 필드에 대해 서로 다른 열거형 또는 제안된 값을 정의하는 경우 해당 값이 병합되고 유니온 스키마에 추가됩니다."

XDM(Experience Data Model)에서 문자열 필드에는 해당 필드에 수집되는 값이나 세그먼테이션에서 작동 방식을 보다 잘 제어할 수 있도록 사전 정의된 허용 또는 제안 값 집합이 제공될 수 있습니다.

**[!UICONTROL 열거형]** 문자열 필드에 대해 수집할 수 있는 값을 사전 정의된 세트로 제한합니다. 열거형 필드에 데이터를 수집하려고 하는데 값이 해당 구성에 정의된 값과 일치하지 않으면 수집이 거부됩니다.

열거형과는 대조적으로 **[!UICONTROL 제안 값]** 옵션을 사용하면 수집할 수 있는 값을 제한하지 않는 문자열 필드의 권장 값 집합을 표시할 수 있습니다. 대신, 제안 값은 [세분화 UI](../../../segmentation/ui/overview.md) 문자열 필드를 속성으로 포함할 때.

날짜 [새 필드 정의](./overview.md#define) Adobe Experience Platform 사용자 인터페이스에서 유형을 로 설정 [!UICONTROL 문자열]을(를) 정의할 수 있는 옵션이 제공됩니다. [enum](#enum) 또는 [제안 값](#suggested-values) 해당 필드에 대해.

![UI의 문자열 필드에 대해 활성화된 열거형 및 제안 값 옵션을 보여주는 이미지](../../images/ui/fields/enum/enum-options-selected.png)

이 문서에서는 열거형 및 제안 값을 정의하는 방법을 다룹니다. [!UICONTROL 스키마] UI 작업 공간. UI에서 열거형을 구성하는 방법 및 다운스트림 효과를 포함하여 열거형 및 제안된 값에 대한 빠른 개요는 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 열거형 정의 {#enum}

선택 **[!UICONTROL 열거형 및 제안 값]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 열거형]**. 열거형에 대한 값 제약 조건을 지정할 수 있는 추가 컨트롤이 나타납니다. 구속을 추가하려면 다음을 선택합니다. **[!UICONTROL 행 추가]**.

![UI에서 선택한 열거형 옵션을 보여 주는 이미지](../../images/ui/fields/enum/enum-add-row.png)

아래 **[!UICONTROL 값]** 열에서 필드를 제한할 정확한 값을 제공해야 합니다. 선택적으로 사람 친화적인 기능을 제공할 수 있습니다 **[!UICONTROL 표시 이름]** 을 설정하는 것이 세그먼테이션에서 값이 표시되는 방식에 영향을 줍니다.

계속 사용 **[!UICONTROL 행 추가]** 원하는 제한 및 선택적 레이블을 열거형에 추가하거나 삭제 아이콘(![삭제 아이콘 이미지](../../images/ui/fields/enum/remove-icon.png))을 클릭하여 제품에서 사용할 수 있도록 사전에 추가한 행 옆에 있는 완료되면 다음을 선택합니다. **[!UICONTROL 적용]** 를 클릭하여 스키마에 변경 사항을 적용합니다.

![UI의 문자열 필드에 대해 채워진 열거형 값과 표시 이름을 보여 주는 이미지](../../images/ui/fields/enum/enum-confirm.png)

변경 사항을 반영하도록 캔버스가 업데이트됩니다. 나중에 이 스키마를 탐색할 때 오른쪽 레일 내에서 열거형 필드에 대한 제약 조건을 보고 편집할 수 있습니다.

## 제안 값 정의 {#suggested-values}

선택 **[!UICONTROL 열거형 및 제안 값]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 제안 값]** 추가 컨트롤을 표시합니다. 여기에서 다음을 선택합니다. **[!UICONTROL 행 추가]** 제안 값 추가를 시작합니다.

![UI에서 선택된 제안 값 옵션을 보여 주는 이미지](../../images/ui/fields/enum/suggested-add-row.png)

아래 **[!UICONTROL 표시 이름]** 열에서 세그먼테이션 UI에 표시할 값에 대해 친숙한 이름을 제공합니다. 제안 값을 더 추가하려면 **[!UICONTROL 행 추가]** 다시 한 번 확인하고 필요에 따라 프로세스를 반복합니다. 이전에 추가한 행을 제거하려면 다음을 선택합니다. ![삭제 아이콘](../../images/ui/fields/enum/remove-icon.png) 해당 행 옆에 있습니다.

완료되면 다음을 선택합니다. **[!UICONTROL 적용]** 를 클릭하여 스키마에 변경 사항을 적용합니다.

![UI의 문자열 필드에 대해 채워진 열거형 값과 표시 이름을 보여 주는 이미지](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>필드의 업데이트된 제안 값이 세분화 UI에 반영되려면 약 5분이 걸립니다.

### 표준 필드에 대한 제안 값 관리

표준 XDM 구성 요소의 일부 필드에는 다음과 같이 제안된 자체 값이 포함됩니다. `eventType` 다음에서 [[!UICONTROL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 표준 필드에 대해 추가 제안 값을 생성할 수 있지만 조직에서 정의하지 않은 제안 값은 수정하거나 제거할 수 없습니다. UI에서 표준 필드를 볼 때 제안된 값이 표시되지만 읽기 전용입니다.

![UI의 문자열 필드에 대해 채워진 열거형 값과 표시 이름을 보여 주는 이미지](../../images/ui/fields/enum/suggested-standard.png)

표준 필드에 대해 제안된 새 값을 추가하려면 다음을 선택합니다. **[!UICONTROL 행 추가]**. 조직에서 이전에 추가한 제안 값을 제거하려면 다음을 선택합니다. ![삭제 아이콘](../../images/ui/fields/enum/remove-icon.png) 해당 행 옆에 있습니다.

![UI의 문자열 필드에 대해 채워진 열거형 값과 표시 이름을 보여 주는 이미지](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 열거형 및 제안된 값에 대한 진화 규칙 {#evolution}

열거형 필드가 있는 스키마를 사용하여 데이터를 Platform으로 수집한 후 스키마 정의에 대한 추가 변경 사항은 시스템에 이미 있는 데이터를 준수해야 합니다. 일반적으로 기존 필드를 변경하면 해당 필드만 변경됩니다 **간단히** 제한적. 필드는 이미 있는 것보다 더 제한적으로 만들 수 없습니다.

열거형 및 제안 값과 관련하여 다음 규칙이 사후 수집을 적용합니다.

* 본인 **CAN** 기존 제안 값으로 표준 및 사용자 정의 필드에 대한 제안 값을 추가합니다.
* 본인 **CAN** 기존 제안 값을 사용하여 사용자 정의 필드에서 제안 값을 제거합니다.
* 본인 **CAN** 기존 사용자 정의 열거형 필드에 새 열거형 값을 추가합니다.
* 본인 **CAN** 사용자 지정 필드의 열거형 값을 제안 값으로만 전환하거나 열거형 또는 제안 값이 없는 문자열로 변환합니다. **이 스위치는 일단 적용되면 실행 취소할 수 없습니다.**
* 본인 **할 수 없음** 표준 필드에서 열거형 또는 제안 값을 제거합니다.
* 본인 **할 수 없음** 기존 열거형이 없는 필드에 열거형 값을 추가합니다.
* 본인 **할 수 없음** 사용자 정의 필드에 대한 기존 열거형 값보다 적은 수의 값을 제거합니다.
* 본인 **할 수 없음** 제안된 값에서 열거형으로 전환합니다.

## 열거형 및 제안 값에 대한 규칙 병합 {#merging}

여러 스키마가 구성이 다른 동일한 열거형 필드를 사용하고 이러한 스키마가 유니온에 포함된 경우, 열거형 차이가 조정되는 방식과 관련하여 특정 규칙이 적용됩니다. 정확한 규칙은 스키마가 동일한 표준 필드를 참조하는지 여부(예: `eventType`) 또는 다른 필드 그룹의 동일한 사용자 지정 필드 경로를 참조하는 경우

동일한 표준 필드를 참조하는 경우:

* 추가 제안 값은 다음과 같습니다 **추가됨** 유니온에.
* 동일한 열거형 키에 대해 제안된 값에 대한 업데이트는 다음과 같습니다 **업데이트됨** 유니온에.

다른 필드 그룹의 동일한 사용자 정의 필드 경로를 참조하는 경우:

* 추가 제안 값은 다음과 같습니다 **추가됨** 유니온에.
* 동일한 추가 제안 값이 두 개 이상의 스키마에 정의되어 있는 경우 해당 값은 다음과 같습니다 **병합됨** 유니온에. 즉, 병합 후 동일한 제안 값이 두 번 나타나지 않습니다.

## 유효성 검사 제한 사항

현재 시스템 제한으로 인해 수집 중에 시스템에서 열거형의 유효성을 검사하지 않는 두 가지 경우가 있습니다.

1. 열거형은 [배열 필드](./array.md).
1. 열거형은 스키마 계층 구조 내에서 두 개 이상의 수준으로 정의됩니다.

## 다음 단계

이 안내서에서는 UI에서 문자열 필드에 대한 열거형 및 제안 값을 정의하는 방법을 다룹니다. 스키마 레지스트리 API를 사용하여 열거형 및 제안 값을 관리하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [튜토리얼](../../tutorials/suggested-values.md).

에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [!DNL Schema Editor], 다음에 대한 개요 참조: [UI의 필드 정의](./overview.md#special).
