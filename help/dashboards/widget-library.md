---
keywords: Experience Platform;사용자 인터페이스;UI;대시보드;대시보드;프로필;세그먼트;대상;라이센스 사용
title: 위젯 라이브러리를 사용하여 대시보드 위젯 추가 및 만들기
description: '이 안내서에서는 Adobe Experience Platform에서 대시보드 데이터를 시각화하기 위해 표준 위젯을 추가하고 사용자 정의 위젯을 만들기 위한 단계별 지침을 제공합니다. '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# (베타) 위젯 라이브러리 {#widget-library}

>[!IMPORTANT]
>
>대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스 내에서 여러 대시보드를 사용하여 조직의 데이터를 보고 상호 작용할 수 있습니다. 대시보드 보기에 새 위젯을 추가하여 이러한 대시보드 중 일부를 업데이트할 수도 있습니다. Adobe에서 제공하는 표준 위젯 외에도 사용자 정의 위젯을 만들고 조직 전체에서 공유할 수 있습니다.

이 안내서에서는 플랫폼 UI의 [!UICONTROL Profiles] 및 [!UICONTROL Segments] 대시보드에 표시되는 정보를 사용자 지정하기 위해 표준 위젯을 추가하고 사용자 정의 위젯을 만들기 위한 단계별 지침을 제공합니다.

[!UICONTROL Profiles], [!UICONTROL Destinations] 및 [!UICONTROL Segments] 대시보드에서 위젯의 위치와 크기를 수정하는 방법에 대한 자세한 내용은 [대시보드 안내서](modify.md)를 참조하십시오.

>[!NOTE]
>
>[!UICONTROL License usage] 대시보드에 표시된 위젯을 사용자 지정할 수 없습니다. 이 고유 대시보드에 대한 자세한 내용은 [라이센스 사용 대시보드 설명서](guides/license-usage.md)를 참조하십시오.

## 위젯 라이브러리 액세스

모든 대시보드(예: 프로필 대시보드)에서 위젯 라이브러리에 액세스하려면 **[!UICONTROL Modify dashboard]** 뒤에 **[!UICONTROL Widget library]**&#x200B;를 선택할 수 있습니다.

>[!NOTE]
>
>[!UICONTROL Widget library] 단추는 [!UICONTROL Modify dashboard]을(를) 선택한 후에만 나타납니다.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

[!UICONTROL Widget library]에는 [!UICONTROL Standard] 및 [!UICONTROL Custom] 탭이 2개 있습니다.

* **[!UICONTROL Standard]** 탭에는 Adobe에서 만든 위젯이 포함되어 있으며 이러한 표준 지표를 사용하여 대시보드를 업데이트할 수 있습니다. 대시보드에 표준 위젯을 추가하는 방법에 대한 자세한 내용은 이 안내서의 [표준 위젯](#standard-widgets) 섹션을 참조하십시오.
* **[!UICONTROL Custom]** 탭에서는 조직 내에서 위젯을 만들고 공유할 수 있습니다. 고유한 위젯을 만드는 전체 단계는 이 안내서의 [사용자 정의 위젯](#custom-widgets) 섹션을 참조하십시오.

![](images/customization/widget-library.png)

## 표준 위젯 {#standard-widgets}

**[!UICONTROL Standard]** 탭에는 Adobe으로 만든 위젯이 포함되어 있으며 카테고리로 분류됩니다. 범주를 선택하면 해당 대시보드에 사용할 수 있는 위젯이 표시됩니다. 각 위젯은 지표의 제목, 설명 및 샘플 시각화를 제공하여 카드로 표시됩니다.

>[!NOTE]
>
>위젯은 선택한 카테고리와 일치하는 대시보드에만 추가할 수 있습니다. 예를 들어 [!UICONTROL Profiles] 범주의 위젯만 [!UICONTROL Profiles] 대시보드에 추가할 수 있습니다.

![](images/customization/standard-widgets.png)

대시보드에 추가할 표준 위젯을 선택하려면 위젯을 강조 표시하고 위젯의 확인란을 선택합니다. 위젯이 하나 이상 선택된 경우 **[!UICONTROL Add widget]** 단추가 켜집니다.

>[!NOTE]
>
>위젯 라이브러리의 오른쪽 위 모서리에 있는 카운터는 선택한 총 위젯 수를 표시합니다.

선택한 위젯을 대시보드에 추가하려면 **[!UICONTROL Add widget]**&#x200B;을 선택합니다.

![](images/customization/add-widget.png)

## 사용자 정의 위젯 {#custom-widgets}

>[!IMPORTANT]
>
>조직은 위젯 라이브러리에서 최대 20개의 사용자 정의 위젯을 만들 수 있습니다.

Experience Platform 내의 대시보드 모양을 사용자 정의하려면 위젯을 만들고 조직의 다른 사용자와 공유할 수 있습니다. 위젯 라이브러리에서 **[!UICONTROL Custom]** 탭을 선택하여 사용자 정의 위젯 만들기를 시작합니다. [!UICONTROL Custom] 탭에서 조직에서 만든 모든 위젯이 표시됩니다. 이 예에서 아직 사용자 정의 위젯이 만들어지지 않았습니다.

![](images/customization/custom-widgets.png)

### 특성 선택

사용자 정의 위젯을 만들려면 데이터가 일일 스냅숏의 일부로 포함되도록 실시간 고객 프로필 속성을 식별해야 합니다. 조직에서 프로필 속성을 선택하지 않은 경우 [!UICONTROL Configure schema] 단추가 위젯 라이브러리의 오른쪽 위 모서리에 나타납니다.

하나 이상의 사용자 정의 속성을 선택하면 위젯 라이브러리의 오른쪽 위 모서리에 [!UICONTROL Edit schema] 단추가 나타납니다. **[!UICONTROL Edit schema]**&#x200B;을 선택하여 **[!UICONTROL Select union schema field]** 대화 상자를 열어 선택한 속성을 보고 속성을 더 추가합니다.

>[!IMPORTANT]
>
>조직은 최대 20개의 속성을 선택할 수 있습니다.

![](images/customization/edit-schema.png)

속성을 선택하려면 조합 스키마의 속성으로 이동(또는 검색 사용)하고 속성 옆의 확인란을 선택합니다. 확인란을 선택하면 대화 상자의 오른쪽에 있는 **[!UICONTROL Selected Attributes]** 목록에도 속성이 추가됩니다.

>[!NOTE]
>
>선택할 수 있도록 속성을 표시하려면 다음 중 하나여야 합니다.String, Date, Date-Time, Boolean, Short, Long, Integer 또는 Byte. 맵 및 이중 데이터 유형은 지원되지 않으며 선택할 수 없도록 회색으로 표시됩니다.

추가할 속성을 선택한 후 **[!UICONTROL Save]**&#x200B;을 선택하여 속성을 저장하고 사용자 정의 위젯 탭으로 돌아갑니다.

데이터를 새로 고칠 때 일별 스냅샷 다음에 새로 선택한 속성을 사용할 수 있습니다.

![](images/customization/select-attribute.png)

### 사용자 정의 위젯 만들기

사용자 정의 위젯을 만들려면 위젯 라이브러리의 중심에서 **[!UICONTROL Create]** 을 선택하거나 사용자 정의 위젯이 이미 만들어진 경우 위젯 라이브러리의 오른쪽 위 모서리에서 **[!UICONTROL Create widget]** 을 선택합니다.

![](images/customization/create-widget.png)

**[!UICONTROL Create widget]** 대화 상자에서 새 위젯의 제목과 설명을 제공하고 위젯을 표시할 속성을 선택할 수 있습니다. 속성을 선택하려면 추가하려는 속성 옆에 있는 라디오 단추를 선택합니다.

>[!NOTE]
>
>위젯당 하나의 속성만 선택할 수 있습니다. 또한 속성에 대해 위젯이 이미 만들어지면 해당 속성이 회색으로 표시됩니다.

![](images/customization/create-widget-dialog.png)

새 위젯의 미리 보기가 대화 상자에 나타나고 샘플 데이터가 있는 가로 막대 그래프가 표시됩니다.

>[!NOTE]
>
>현재 모든 속성에 대해 지원되는 유일한 지표는 프로필 수이며 현재 사용자 정의 위젯에 대해 지원되는 유일한 시각화는 가로 막대 그래프입니다.
>
>예제 위젯에 표시되는 데이터는 단지 일러스트레이션 용도로만 사용됩니다. 미리 보기에는 조직의 실제 데이터가 표시되지 않습니다.

![](images/customization/create-widget-select-attribute.png)

새 위젯을 저장하고 [!UICONTROL Custom] 탭으로 돌아가려면 **[!UICONTROL Create]**&#x200B;을 선택합니다. 이제 라이브러리에서 위젯을 선택하고 **[!UICONTROL Add widget]**&#x200B;을 선택하여 새 위젯을 대시보드에 추가할 수 있습니다.

### 사용자 정의 위젯 보관

위젯을 라이브러리에 추가한 후 **[!UICONTROL Archive]** 단추를 사용하여 보관할 수 있습니다. 위젯을 편집하여 제목 또는 설명 필드를 업데이트할 수도 있습니다.

## 다음 단계

이제 이 문서를 읽은 후 [!UICONTROL Widget library]에 액세스하여 이 문서를 사용하여 대시보드에 위젯을 추가하거나 조직의 사용자 정의 위젯을 만들 수 있습니다. 대시보드에서 위젯의 크기 및 위치를 수정하려면 대시보드 안내서](modify.md)수정을 참조하십시오.[
