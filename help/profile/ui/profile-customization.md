---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 프로필 세부 정보 맞춤화
description: '이 안내서에서는 Adobe Experience Platform UI 내에 실시간 고객 프로필 데이터가 표시되는 방식을 사용자 지정하기 위한 단계별 지침을 제공합니다. '
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 세부 맞춤화 {#profile-detail-customization}

Adobe Experience Platform 유저 인터페이스 내에서 고객 프로파일 형태로 [!DNL Real-time Customer Profile] 데이터를 보고 인터랙션할 수 있습니다. UI에 표시되는 프로필 정보는 여러 프로필 조각에서 병합되어 각 개별 고객의 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 세부 사항이 포함됩니다. 프로필에 표시된 기본 필드는 기본 속성을 표시하도록 조직 수준에서 변경할 수도 [!DNL Profile] 있습니다. 이 안내서에서는 플랫폼 UI 내에 데이터가 표시되는 방식을 사용자 지정하기 위한 단계별 지침을 제공합니다. [!DNL Profile]

프로필 [!UICONTROL UI에 대한 전체] 가이드는 [프로필 사용 안내서를](user-guide.md)참조하십시오.

## 카드 순서 변경 및 크기 조정 {#reorder-and-resize-cards}

고객 프로파일의 [!UICONTROL 세부] 정보 탭에서 대시보드 **[!UICONTROL 수정을 선택하여 기존 카드의 크기를 조정하고 순서를 변경할]** 수 있습니다.

![](../images/profile-customization/profiles-modify-dashboard.png)

대시보드를 수정하도록 선택한 후 카드 제목을 선택하고 카드를 원하는 순서로 드래그하여 놓아 카드의 순서를 변경할 수 있습니다. 카드(카드) 오른쪽 하단에 있는 각도 기호를 선택하고 카드를 원하는 크기로 드래그하여 카드 크기를 조정할 수도`⌟`있습니다. 이 예에서 **[!UICONTROL 기본 속성]** 카드 크기가 조정되고 있습니다.

![](../images/profile-customization/profiles-resize-cards.png)

선택한 카드가 원하는 크기에 맞게 조정되고 주변 카드가 동적으로 다시 배치됩니다. 이로 인해 일부 카드가 추가 행으로 이동될 수 있으므로 모든 카드를 보려면 아래로 스크롤해야 합니다. 예를 들어 [!UICONTROL 기본 속성] 카드 크기가 변경되면 [!UICONTROL 연결된 ID] 카드가 더 이상 상단 행에 표시되지 않고 이제 프로필 내의 새 두 번째 행에 표시됩니다(표시되지 않음). 연결된 ID [!UICONTROL 카드를 맨 위] 행으로 되돌리려면 [!UICONTROL 채널 기본 설정] 카드의 현재 위치로 끌어다 놓을 수 있습니다.

![](../images/profile-customization/profiles-card-resized.png)

## 카드 편집 및 제거

카드 크기 조정 및 순서 변경 외에도 특정 카드의 컨텐츠를 편집하고 대시보드에서 일부 카드를 완전히 제거할 수 있습니다. 카드의 오른쪽 상단 모서리에서 줄임표(`...`)를 선택하여 편집하거나 제거합니다. 선택한 카드의 속성에 따라 카드를 편집하거나 제거하는 옵션이 있는 드롭다운이 열립니다.

>[!NOTE]
>
>일부 카드를 편집하거나 제거할 수는 없습니다. 이는 일부 카드에 읽기 전용 또는 필수 정보가 포함되어 있기 때문입니다. 카드의 오른쪽 위 모서리에 줄임표가 없는 경우, 카드에 읽기 전용 AND 필수 정보가 포함되어 있으므로 편집하거나 제거할 수 없습니다. 카드에 타원이 있고 카드를 선택하면 카드를 제거하는 옵션만 표시되므로 카드 정보는 읽기 전용이므로 편집할 수 없습니다.

![](../images/profile-customization/profiles-edit-remove-resized.png)

드롭다운에서 **[!UICONTROL 편집을]** 선택하여 **[!UICONTROL 편집 위젯]** 작업 영역을 엽니다. 이 작업 공간에서는 카드 제목을 업데이트하거나, 보이는 속성을 순서를 변경하거나 제거하거나, 속성 [!UICONTROL 추가] 단추를 사용하여 추가 속성을 추가할 수 있습니다.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## 속성 추가 {#add-attributes}

[ [!UICONTROL 편집] 위젯] 화면에서 카드의 오른쪽 위 **[!UICONTROL 에 있는 속성]** 추가를 선택하여 해당 카드에 속성을 추가합니다.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

[ [!UICONTROL 조합 스키마 필드] 선택] 대화 상자가 열리면 대화 상자의 왼쪽에 아래 중첩된 필드가 있는 전체 [!UICONTROL XDM 개별 프로필] 조합 스키마가 표시됩니다. 조합 스키마에 대한 자세한 내용은 사용 안내서의 [조합 스키마 섹션 [!DNL Profile] 을 참조하십시오](user-guide.md#union-schema).

대화 상자 오른쪽의 **[!UICONTROL 선택한 속성]** 섹션에는 편집 중인 카드에 현재 포함되어 있는 속성이 표시됩니다. 여기에서 속성을 제거하고 순서를 변경할 수도 있습니다. 선택한 속성의 총 수와 단일 카드에 추가할 수 있는 최대 속성 수(20)가 표시됩니다.

![](../images/profile-customization/profiles-select-field-before.png)

사용 가능한 조합 스키마 필드 중 하나를 선택하여 편집 중인 카드의 속성을 사용자 지정할 수 있습니다. 선택한 필드는 해당 필드 옆에 확인 표시가 표시되고 선택한 속성 목록에 자동으로 추가됩니다. 카드에 표시할 모든 속성을 추가한 후에는 **[!UICONTROL 선택을]** 선택하여 [!UICONTROL 편집 위젯] 화면으로 돌아갑니다.

![](../images/profile-customization/profiles-select-field-after.png)

이제 [ [!UICONTROL 편집] 위젯] 화면으로 돌아갈 때 선택 사항을 반영하도록 카드의 속성 목록을 업데이트해야 합니다. 필요에 따라 카드 속성을 제거하거나 순서를 변경하거나 카드 제목을 편집할 수 있습니다. 편집 작업이 완료되면 **[!UICONTROL 저장을 선택하여]** 변경 내용을 저장합니다.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

저장 후 업데이트된 카드 및 속성이 표시되는 [!UICONTROL 세부] 사항 탭으로 돌아갑니다.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Add a new card {#add-a-new-card}

Experience Platform 내의 프로필 모양을 사용자 정의하려면 대시보드에 새 카드를 추가하고 해당 카드에 표시할 속성을 선택할 수 있습니다. 시작하려면 세부 사항 **[!UICONTROL 탭에서 대시보드]** 수정을 [!UICONTROL 선택합니다] .

![](../images/profile-customization/profiles-modify-dashboard.png)

그런 다음 **[!UICONTROL 대시보드의 왼쪽 상단 모서리에서 위젯]** 추가를 선택합니다.

![](../images/profile-customization/profiles-add-widget.png)

새 카드를 추가하도록 선택하면 [!UICONTROL 편집 위젯] 화면이 열립니다. 이 화면에서 새 카드의 제목을 지정하고 표시할 속성을 선택할 수 있습니다. 카드에 속성 추가를 시작하려면 속성 **[!UICONTROL 추가를 선택합니다]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

[ **[!UICONTROL 조합 스키마 필드]** 선택] 대화 상자가 열리면 대화 상자의 왼쪽에 전체 [!UICONTROL XDM 개인 프로필] 조합 스키마와 대화 상자 오른쪽의 [ **[!UICONTROL 선택한 속성]** ] 섹션이 카드에 대해 선택한 속성을 보여 줍니다. 속성 추가에 대한 자세한 내용은 이 문서 앞 [에 나타나는 속성](#add-attributes) 추가 섹션을 참조하십시오.

선택한 속성의 총 수와 단일 카드에 추가할 수 있는 최대 속성 수(20)가 표시됩니다. 이 화면에서 선택한 속성을 제거하고 순서를 변경할 수도 있습니다. 카드에 표시할 모든 속성을 추가한 후에는 **[!UICONTROL 선택을]** 선택하여 [!UICONTROL 편집 위젯] 화면으로 돌아갑니다.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

[ [!UICONTROL 편집] 위젯] 화면으로 돌아갈 때 카드의 속성 목록은 이전 화면에서 선택한 항목을 반영해야 합니다. 필요에 따라 카드 속성의 순서를 변경하거나 제거할 수도 있습니다.

새 카드를 저장하려면 먼저 **[!UICONTROL 카드 제목을]**&#x200B;제공해야 합니다. 그런 다음 **[!UICONTROL 저장을 선택하고 카드]** 생성 과정을 완료할 수 있습니다.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

저장 후 새 카드 및 속성이 표시되는 [!UICONTROL 세부] 사항 탭으로 돌아갑니다.

![](../images/profile-customization/profiles-detail-new-widget.png)

## 기본 카드 복원

언제든지 제거된 기본 카드를 복원할 경우 빠르고 쉽게 복원할 수 있습니다. 먼저 대시보드 **[!UICONTROL 수정을]**&#x200B;선택한 다음 기본 카드 **[!UICONTROL 복원을 선택합니다]**. 기본 카드가 표시되면 **[!UICONTROL 저장을 선택하여]** 변경 사항을 저장하거나, 기본 카드를 복원하려면 **[!UICONTROL 취소를]** 선택할 수 있습니다.

![](../images/profile-customization/profiles-restore-default.png)

## 다음 단계

이 문서의 지침에 따라 카드 추가 및 제거, 카드 세부 사항 및 속성 편집, 카드 순서 변경 및 크기 조정 등 조직의 프로필 보기를 업데이트할 수 있습니다. Experience Platform UI에서 [!DNL Profile] 데이터 작업에 대한 자세한 내용은 [[!DNL Profile] 사용 안내서를 참조하십시오](user-guide.md).