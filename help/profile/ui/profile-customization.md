---
keywords: Experience Platform;프로필;실시간 고객 프로필;사용자 인터페이스;UI;사용자 지정;프로필 세부 정보;세부 정보
title: UI의 프로필 세부 정보 사용자 정의
description: 이 안내서는 Adobe Experience Platform UI 내에서 실시간 고객 프로필 데이터가 표시되는 방식을 맞춤화하기 위한 단계별 지침을 제공합니다.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 세부 정보 사용자 지정 {#profile-detail-customization}

Adobe Experience Platform 사용자 인터페이스에서 [!DNL Real-Time Customer Profile] 데이터를 고객 프로필 형식으로 보고 상호 작용할 수 있습니다. UI에 표시되는 프로필 정보가 여러 프로필 조각에서 함께 병합되어 각 개별 고객에 대한 단일 뷰를 형성합니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정 등의 세부 사항이 포함됩니다. 프로필에 표시되는 기본 필드를 조직 수준에서 변경하여 기본 [!DNL Profile] 특성을 표시할 수도 있습니다. 이 안내서에서는 Experience Platform UI 내에서 [!DNL Profile] 데이터가 표시되는 방식을 사용자 지정하는 단계별 지침을 제공합니다.

프로필 UI에 대한 전체 안내서는 [프로필 UI 안내서](user-guide.md)를 참조하십시오.

## 카드 순서 조정 및 크기 조정 {#reorder-and-resize-cards}

고객 프로필의 **[!UICONTROL 세부 정보]** 탭에서 **[!UICONTROL 프로필 세부 정보 사용자 지정]**&#x200B;을 선택하여 기존 카드의 크기를 조정하고 순서를 변경할 수 있습니다.

![프로필 대시보드에 프로필 세부 정보 사용자 지정 단추가 강조 표시되어 있습니다.](../images/profile-customization/customize-profile-details.png)

대시보드를 수정하도록 선택한 후 카드 제목을 선택하고 카드를 원하는 순서로 드래그 앤 드롭하여 카드 순서를 변경할 수 있습니다. 카드의 오른쪽 아래(`⌟`) 모서리에 있는 각도 기호를 선택하고 카드를 원하는 크기로 드래그하여 카드의 크기를 조정할 수도 있습니다. 이 예제에서는 **[!UICONTROL 기본 특성]** 카드의 크기를 조정하고 있습니다.

![크기 조정 단추가 기본 특성 카드 내에서 강조 표시됩니다.](../images/profile-customization/resize.png)

선택한 카드가 원하는 크기로 조정되고 주변 카드가 동적으로 재배치됩니다. 이로 인해 일부 카드가 추가 행으로 이동되어 모든 카드를 보려면 아래로 스크롤해야 할 수 있습니다. 예를 들어 &quot;[!UICONTROL 기본 특성]&quot; 카드 크기가 조정되면 &quot;[!UICONTROL 연결된 ID]&quot; 카드는 더 이상 맨 위 행에 표시되지 않고 이제 프로필 내의 새 두 번째 행에 표시됩니다(표시되지 않음). 맨 위 행에 &quot;[!UICONTROL 연결된 ID]&quot; 카드를 반환하려면 &quot;[!UICONTROL 채널 환경 설정]&quot; 카드의 현재 위치로 끌어다 놓을 수 있습니다.

![크기가 조정된 카드가 강조 표시되어 있습니다.](../images/profile-customization/resized.png)

## 카드 편집 및 제거

카드 크기 조정 및 재정렬 외에도 특정 카드의 내용을 편집하고 대시보드에서 일부 카드를 완전히 제거할 수 있습니다. 카드의 오른쪽 상단 모서리에서 줄임표(`...`)를 선택하여 편집하거나 제거합니다. 그러면 선택한 카드의 속성에 따라 카드를 편집하거나 제거할 수 있는 옵션이 있는 드롭다운이 열립니다.

>[!NOTE]
>
>모든 카드를 편집하거나 제거할 수 있는 것은 아닙니다. 일부 카드에 읽기 전용 또는 필수 정보가 포함되어 있기 때문입니다. 오른쪽 상단 모서리에 줄임표가 없는 카드는 읽기 전용 AND 필수 정보를 포함하고 있으며 편집하거나 제거할 수 없습니다. 카드에 모서리에 줄임표가 있고 이 카드를 선택하면 카드를 제거할 수 있는 옵션만 표시되는 경우 카드 정보는 읽기 전용이며 편집할 수 없습니다.

![카드 편집 드롭다운이 강조 표시됩니다. 여기에는 카드를 편집하거나 제거하는 옵션이 포함됩니다.](../images/profile-customization/edit-card.png)

드롭다운에서 **[!UICONTROL 편집]**&#x200B;을(를) 선택하여 **[!UICONTROL 위젯 편집]** 작업 영역을 엽니다. 여기서 카드 제목을 업데이트하거나, 표시되는 특성을 다시 정렬하거나, 제거하거나, **[!UICONTROL 특성 추가]** 단추를 사용하여 특성을 추가할 수 있습니다.

![기본 특성 카드가 표시됩니다.](../images/profile-customization/basic-attributes.png)

## 속성 추가 {#add-attributes}

**[!UICONTROL 위젯 편집]** 화면에서 카드의 오른쪽 상단 모서리에 있는 **[!UICONTROL 특성 추가]**&#x200B;를 선택하여 해당 카드에 특성을 추가합니다.

![기본 특성 카드에 특성 추가 단추가 강조 표시됩니다.](../images/profile-customization/add-attributes.png)

**[!UICONTROL 유니온 스키마 필드 선택]** 대화 상자가 열리면 대화 상자의 왼쪽에 전체 [!UICONTROL XDM 개별 프로필] 유니온 스키마가 표시되고 아래에 필드가 중첩됩니다. 유니온 스키마에 대한 자세한 내용은  [!DNL Profile] 사용 안내서[&#128279;](user-guide.md#union-schema)의 유니온 스키마 섹션을 참조하십시오.

대화 상자 오른쪽의 **[!UICONTROL 선택한 특성]** 섹션에는 편집 중인 카드에 현재 포함된 특성이 표시됩니다. 여기에서 속성을 제거하고 순서를 변경할 수도 있습니다. 선택된 총 속성 수와 단일 카드에 추가할 수 있는 최대 속성 수(20개)가 표시됩니다.

![현재 카드의 특성을 구성하는 특성이 강조 표시됩니다.](../images/profile-customization/select-before.png)

사용 가능한 유니온 스키마 필드를 선택하여 편집 중인 카드의 속성을 사용자 정의할 수 있습니다. 필드를 선택할 때 파일 경로 이름이나 표시 이름을 표시하도록 선택할 수 있습니다. 이 두 디스플레이 간을 전환하려면 **[!UICONTROL 디스플레이 이름 표시]** 전환을 선택합니다.

![프로필 세부 정보 페이지에서 [!UICONTROL 표시 이름 표시] 토글이 강조 표시됩니다.](../images/profile-customization/show-display-names.png)

선택한 필드 옆에 확인 표시가 나타나고 선택한 속성 목록에 자동으로 추가됩니다. 카드에 표시하려는 모든 특성을 추가한 후 **[!UICONTROL 위젯 편집]** 화면으로 돌아가려면 **[!UICONTROL 선택]**&#x200B;을 선택하세요.

![새로 추가된 특성이 강조 표시됩니다.](../images/profile-customization/select-after.png)

**[!UICONTROL 위젯 편집]** 화면으로 돌아가면 이제 카드의 특성 목록이 업데이트되어 선택 사항을 반영합니다. 필요에 따라 카드 특성을 제거하거나 순서를 변경하거나 카드 제목을 편집할 수 있습니다. 편집이 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 내용을 저장합니다.

![새로 추가된 특성이 편집된 카드에 표시됩니다.](../images/profile-customization/new-attributes.png)

저장한 후 업데이트된 카드 및 특성이 표시되는 **[!UICONTROL 세부 정보]** 탭으로 돌아갑니다.

![새로 추가된 특성이 프로필 대시보드 내 카드에 표시됩니다.](../images/profile-customization/added-attributes.png)

## 새 카드 추가 {#add-a-new-card}

Experience Platform 내의 프로필 모양을 추가로 사용자 정의하려면 대시보드에 새 카드를 추가하도록 선택하고 해당 카드에 표시할 속성을 선택할 수 있습니다. 시작하려면 **[!UICONTROL 세부 정보]** 탭에서 **[!UICONTROL 대시보드 수정]**&#x200B;을 선택하세요.

![프로필 세부 정보 사용자 지정 단추가 강조 표시됩니다.](../images/profile-customization/customize-profile-details.png)

그런 다음 대시보드 왼쪽 상단 모서리에서 **[!UICONTROL 위젯 추가]**&#x200B;를 선택합니다.

![위젯 추가 단추가 강조 표시됩니다.](../images/profile-customization/add-widget.png)

새 카드를 추가하도록 선택하면 **[!UICONTROL 위젯 편집]** 화면이 열립니다. 이 화면에서 새 카드의 제목을 입력하고 카드를 표시할 특성을 선택할 수 있습니다. 카드에 특성을 추가하려면 **[!UICONTROL 특성 추가]**&#x200B;를 선택하십시오.

![위젯 편집 화면에 빈 새 위젯 카드가 표시됩니다.](../images/profile-customization/edit-widget.png)

**[!UICONTROL 유니온 스키마 필드 선택]** 대화 상자가 열리면 대화 상자의 왼쪽에 전체 [!UICONTROL XDM 개별 프로필] 유니온 스키마가 표시되고 대화 상자의 오른쪽에 있는 **[!UICONTROL 선택한 특성]** 섹션에는 카드에 대해 선택한 특성이 표시됩니다. 특성 추가에 대한 자세한 내용은 이 문서의 앞부분에 나오는 특성 추가에 대한 [섹션](#add-attributes)을 참조하십시오.

선택된 총 속성 수와 단일 카드에 추가할 수 있는 최대 속성 수(20개)가 표시됩니다. 이 화면에서 선택한 속성을 제거하고 순서를 변경할 수도 있습니다. 카드에 표시할 특성을 모두 추가한 후에는 **[!UICONTROL 선택]**&#x200B;을 선택하여 **[!UICONTROL 위젯 편집]** 화면으로 돌아갑니다.

![카드에 추가할 필드가 강조 표시됩니다.](../images/profile-customization/add-widget-attributes.png)

**[!UICONTROL 위젯 편집]** 화면으로 돌아가면 카드의 속성 목록이 이전 화면에서 선택한 사항을 반영해야 합니다. 필요에 따라 카드 속성을 재정렬하고 제거할 수도 있습니다.

새 카드를 저장하려면 먼저 **[!UICONTROL 카드 제목]**&#x200B;을 제공해야 합니다. 그러면 **[!UICONTROL 저장]**&#x200B;을 선택하고 카드 만들기 프로세스를 완료할 수 있습니다.

![위젯 편집 화면에서 새 위젯을 미리 봅니다.](../images/profile-customization/new-widget.png)

저장한 후 새 카드 및 특성이 표시되는 **[!UICONTROL 세부 정보]** 탭으로 돌아갑니다.

![새 위젯이 프로필 대시보드에 추가되었습니다.](../images/profile-customization/added-widget.png)

## 기본 카드 복원

어느 시점에서든 이후에 제거된 기본 카드를 복원하려는 경우 빠르고 쉽게 복원할 수 있습니다. 먼저 **[!UICONTROL 대시보드 수정]**&#x200B;을 선택한 다음 **[!UICONTROL 기본 카드 복원]**&#x200B;을 선택합니다. 기본 카드가 표시되면 **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 내용을 저장하거나, 기본 카드를 복원하지 않으려면 **[!UICONTROL 취소]**&#x200B;를 선택할 수 있습니다.

![기본 카드 복원 단추가 프로필 대시보드에 강조 표시되어 있습니다.](../images/profile-customization/restore-default.png)

## 다음 단계

이 문서에 따라 이제 카드 추가 및 제거, 카드 세부 정보 및 속성 편집, 카드 재정렬 및 크기 조정을 포함하여 조직의 프로필 보기를 업데이트할 수 있습니다. Experience Platform UI에서 [!DNL Profile] 데이터를 사용하는 방법에 대한 자세한 내용은 [[!DNL Profile] 사용 안내서](user-guide.md)를 참조하십시오.
