---
keywords: Experience Platform;프로필;실시간 고객 프로필;사용자 인터페이스;UI;사용자 지정;프로필 세부 사항;세부 사항
title: UI의 프로필 세부 사항 사용자 지정
description: 이 안내서에서는 Adobe Experience Platform UI에 실시간 고객 프로필 데이터가 표시되는 방식을 사용자 지정하는 단계별 지침을 제공합니다.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 세부 사용자 지정 {#profile-detail-customization}

Adobe Experience Platform 사용자 인터페이스 내에서 를 보고 상호 작용할 수 있습니다 [!DNL Real-Time Customer Profile] 데이터를 고객 프로필 형식으로 표시합니다. UI에 표시된 프로필 정보가 여러 프로필 조각에서 병합되어 각 개별 고객에 대한 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 세부 사항이 포함됩니다. 프로필에 표시된 기본 필드를 조직 수준에서 변경하여 기본 설정을 표시할 수도 있습니다 [!DNL Profile] 속성을 사용합니다. 이 안내서에서는 다음 방법을 사용자 지정하는 단계별 지침을 제공합니다. [!DNL Profile] 데이터가 Platform UI 내에 표시됩니다.

프로필 UI에 대한 전체 안내서를 보려면 [프로필 UI 안내서](user-guide.md).

## 카드 순서 변경 및 크기 조정 {#reorder-and-resize-cards}

에서 **[!UICONTROL 세부 사항]** 고객 프로필의 탭에서 **[!UICONTROL 프로필 세부 사항 사용자 지정]** 기존 카드의 크기를 조정하고 순서를 조정하려면

![프로필 세부 사항 사용자 지정 단추가 프로필 대시보드에 강조 표시됩니다.](../images/profile-customization/customize-profile-details.png)

대시보드를 수정하도록 선택한 후 카드 제목을 선택하고 카드를 원하는 순서로 드래그 앤 드롭하여 카드 순서를 변경할 수 있습니다. 카드(`⌟`) 카드를 원하는 크기로 드래그합니다. 이 예에서 **[!UICONTROL 기본 속성]** 카드 크기를 조정하고 있습니다.

![크기 조정 단추가 기본 특성 카드 내에 강조 표시됩니다.](../images/profile-customization/resize.png)

선택한 카드가 원하는 크기에 맞게 조정되고 주변 카드가 동적으로 다시 배치됩니다. 이로 인해 일부 카드가 추가 행으로 이동되므로 모든 카드를 보려면 아래로 스크롤해야 할 수 있습니다. 예를 들어,[!UICONTROL 기본 속성]&quot; 카드의 크기가 &quot;[!UICONTROL 연결된 ID]&quot;카드가 더 이상 위쪽 행에 표시되지 않고 이제 프로필 내의 새 두 번째 행에 표시됩니다(표시되지 않음). 를 반환하려면[!UICONTROL 연결된 ID]&quot; 카드를 맨 위 행에 끌어다 놓을 수 있습니다. &quot;[!UICONTROL 채널 환경 설정]&quot; 카드.

![크기가 다시 지정된 카드가 강조 표시됩니다.](../images/profile-customization/resized.png)

## 카드 편집 및 제거

카드 크기 조정 및 순서 조정 외에도 특정 카드의 콘텐츠를 편집하고 대시보드에서 일부 카드를 완전히 제거할 수 있습니다. 줄임표(`...`)을 클릭하여 편집하거나 제거합니다. 선택한 카드의 속성에 따라 카드를 편집하거나 제거하는 옵션이 있는 드롭다운이 열립니다.

>[!NOTE]
>
>일부 카드를 편집하거나 제거할 수는 없습니다. 일부 카드에 읽기 전용 또는 필수 정보가 포함되어 있기 때문입니다. 오른쪽 상단 모서리에 생략 부호가 없는 경우, 여기에는 읽기 전용 AND 필수 정보가 포함되어 있으며 편집하거나 제거할 수 없습니다. 카드에 타원이 있고 카드를 선택할 경우 카드를 제거하는 옵션만 표시되며 카드 정보는 읽기 전용이므로 편집할 수 없습니다.

![카드 편집 드롭다운이 강조 표시됩니다. 여기에는 카드를 편집하거나 제거하는 옵션이 포함됩니다.](../images/profile-customization/edit-card.png)

선택 **[!UICONTROL 편집]** 드롭다운에서 을(를) 열어 **[!UICONTROL 편집 위젯]** 작업 영역에서 카드 제목을 업데이트하거나, 표시된 속성을 다시 정렬하거나, 또는 **[!UICONTROL 속성 추가]** 버튼을 클릭합니다.

![기본 특성 카드가 표시됩니다.](../images/profile-customization/basic-attributes.png)

## 속성 추가 {#add-attributes}

에서 **[!UICONTROL 편집 위젯]** 화면, 선택 **[!UICONTROL 속성 추가]** 카드 오른쪽 상단 모서리에서 해당 카드에 속성을 추가할 수 있습니다.

![기본 특성 카드 내의 속성 추가 단추가 강조 표시됩니다.](../images/profile-customization/add-attributes.png)

이 **[!UICONTROL 결합 스키마 필드 선택]** 대화 상자가 열리면 대화 상자의 왼쪽에 전체 가 표시됩니다 [!UICONTROL XDM 개별 프로필] 아래에 중첩된 필드가 있는 결합 스키마. 결합 스키마에 대한 자세한 내용은 [의 결합 스키마 섹션 [!DNL Profile] 사용 안내서](user-guide.md#union-schema).

다음 **[!UICONTROL 선택한 속성]** 대화 상자의 오른쪽에 있는 섹션에는 현재 편집 중인 카드에 포함된 속성이 표시됩니다. 여기에서 속성을 제거하고 순서를 변경할 수도 있습니다. 선택한 총 속성 수와 단일 카드에 추가할 수 있는 최대 속성 수(20)가 표시됩니다.

![현재 카드의 속성을 구성하는 속성은 강조 표시됩니다.](../images/profile-customization/select-before.png)

사용 가능한 결합 스키마 필드를 선택하여 편집 중인 카드의 속성을 사용자 지정할 수 있습니다. 선택한 필드는 해당 필드 옆에 확인 표시가 표시되고 선택한 속성 목록에 자동으로 추가됩니다. 카드에 표시할 모든 속성을 추가했으면 을 선택합니다 **[!UICONTROL 선택]** 로 돌아가기 **[!UICONTROL 편집 위젯]** 화면.

![새로 추가된 속성이 강조 표시됩니다.](../images/profile-customization/select-after.png)

로 돌아가면 **[!UICONTROL 편집 위젯]** 화면에서 카드의 속성 목록을 업데이트하여 선택 사항을 반영해야 합니다. 필요에 따라 카드 속성을 제거하거나 재정렬하거나 카드 제목을 편집할 수 있습니다. 편집이 완료되면 을(를) 선택합니다 **[!UICONTROL 저장]** 변경 사항을 저장하려면 을 클릭합니다.

![새로 추가된 속성이 편집된 카드에 표시됩니다.](../images/profile-customization/new-attributes.png)

저장한 후 **[!UICONTROL 세부 사항]** 탭입니다.

![새로 추가된 속성이 프로필 대시보드 내의 카드에 표시됩니다.](../images/profile-customization/added-attributes.png)

## 새 카드 추가 {#add-a-new-card}

Experience Platform 내의 프로필 모양을 추가로 사용자 지정하려면 대시보드에 새 카드를 추가하고 해당 카드에 표시할 속성을 선택하도록 선택할 수 있습니다. 시작하려면 다음을 선택합니다 **[!UICONTROL 대시보드 수정]** on **[!UICONTROL 세부 사항]** 탭.

![프로필 세부 사항 사용자 지정 단추가 강조 표시됩니다.](../images/profile-customization/customize-profile-details.png)

다음 을 선택합니다. **[!UICONTROL 위젯 추가]** 대시보드 왼쪽 상단 모서리에서 을(를) 클릭합니다.

![[위젯 추가] 단추가 강조 표시됩니다.](../images/profile-customization/add-widget.png)

새 카드를 추가하도록 선택하면 **[!UICONTROL 편집 위젯]** 새 카드의 제목을 입력하고 표시할 속성을 선택할 수 있는 화면입니다. 카드에 속성을 추가하려면 **[!UICONTROL 속성 추가]**.

![편집 위젯 화면에 빈 새 위젯 카드가 표시됩니다.](../images/profile-customization/edit-widget.png)

이 **[!UICONTROL 결합 스키마 필드 선택]** 대화 상자가 열리면 대화 상자의 왼쪽에 전체 가 표시됩니다 [!UICONTROL XDM 개별 프로필] 결합 스키마 및 **[!UICONTROL 선택한 속성]** 대화 상자 오른쪽의 섹션에 카드에 대해 선택한 속성이 표시됩니다. 속성 추가에 대한 자세한 내용은 [속성 추가 섹션](#add-attributes) 이 문서의 앞부분에 표시됩니다.

선택한 총 속성 수와 단일 카드에 추가할 수 있는 최대 속성 수(20)가 표시됩니다. 이 화면에서 선택한 속성을 제거하고 순서를 변경할 수도 있습니다. 카드에 표시할 모든 속성을 추가했으면 을 선택합니다 **[!UICONTROL 선택]** 로 돌아가기 **[!UICONTROL 편집 위젯]** 화면.

![카드에 추가할 필드가 강조 표시됩니다.](../images/profile-customization/add-widget-attributes.png)

로 돌아가면 **[!UICONTROL 편집 위젯]** 화면에서 카드의 속성 목록은 이전 화면의 선택 사항을 반영해야 합니다. 필요에 따라 카드 속성을 다시 정렬하고 제거할 수도 있습니다.

새 카드를 저장하려면 먼저 **[!UICONTROL 카드 제목]**&#x200B;을 지정하는 경우 다음을 선택할 수 있습니다. **[!UICONTROL 저장]** 카드 만들기 프로세스를 완료합니다.

![편집 위젯 화면에서 새 위젯을 미리 봅니다.](../images/profile-customization/new-widget.png)

저장한 후 **[!UICONTROL 세부 사항]** 새 카드와 속성이 표시되는 탭입니다.

![새 위젯이 프로필 대시보드에 추가됩니다.](../images/profile-customization/added-widget.png)

## 기본 카드 복원

제거되었던 기본 카드를 어느 시점에서든 복원하려는 경우에는 빠르고 쉽게 복원할 수 있습니다. 먼저 을 선택합니다. **[!UICONTROL 대시보드 수정]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 기본 카드 복원]**. 기본 카드가 표시되면 을(를) 선택할 수 있습니다 **[!UICONTROL 저장]** 변경 내용을 저장하려면 을 선택하고 **[!UICONTROL 취소]** 기본 카드를 복원하지 않으려면

![프로필 대시보드에서 기본 카드 복원 단추가 강조 표시됩니다.](../images/profile-customization/restore-default.png)

## 다음 단계

이 문서를 따르면 이제 카드 추가 및 제거, 카드 세부 사항 및 속성 편집, 카드 순서 조정 및 크기 조정 등 조직의 프로필 보기를 업데이트할 수 있습니다. 작업 방법에 대해 자세히 알아보려면 [!DNL Profile] Experience Platform UI의 데이터는 [[!DNL Profile] 사용 안내서](user-guide.md).
