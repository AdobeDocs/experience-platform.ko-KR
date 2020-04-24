---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 사용 레이블 사용 안내서
topic: labels
translation-type: tm+mt
source-git-commit: 475e774d5e7ebac036b42aa94736ba8e22c7185f

---


# 데이터 사용 레이블 사용 안내서

이 사용 안내서에서는 Experience Platform 사용자 인터페이스 내에서 데이터 사용 레이블(DULE 레이블이라고도 함)을 사용하여 작업하는 단계를 다룹니다. 설명서를 사용하기 전에 DULE 프레임워크에 [대한 보다 강력한 소개를](../home.md) 보려면 데이터 거버넌스 개요를 참조하십시오.

## 데이터 세트 수준에서 데이터 사용 레이블 관리

데이터 집합 수준에서 데이터 사용 레이블을 관리하려면 기존 데이터 집합을 선택하거나 새 데이터 집합을 만들어야 합니다. Adobe Experience Platform에 로그인한 후 왼쪽 탐색 **[!UICONTROL Datasets]** 영역에서 선택하여 데이터 세트 _작업 영역을 엽니다_ . 이 페이지에는 각 데이터 세트에 관련된 유용한 세부 정보와 함께 조직에 속한 생성된 모든 데이터 집합이 나열됩니다.

![데이터 작업 공간 내의 데이터 집합 탭](../images/labels/datasets.png)

다음 섹션에서는 레이블을 적용할 새 데이터 세트를 만드는 단계를 제공합니다. 기존 데이터 세트에 대한 레이블을 편집하려면 목록에서 데이터 세트를 선택하고 데이터 세트에 데이터 사용 레이블을 [추가하려면 건너뛰십시오](#add-labels).

### 새 데이터 집합 만들기

>[!NOTE] 이 예에서 데이터 집합은 미리 구성된 XDM(Experience Data Model) 스키마를 사용하여 만들어집니다. XDM 스키마에 대한 자세한 내용은 XDM [시스템 개요](../../xdm/home.md) 및 스키마 [컴포지션의](../../xdm/schema/composition.md)기본 사항을 참조하십시오.

새 데이터 세트를 만들려면 작업 **[!UICONTROL Create Dataset]** 영역의 오른쪽 위 모서리에서 을 클릭합니다 _[!UICONTROL Datasets]_.

![](../images/labels/create_dataset.png)

화면이 _[!UICONTROL Create Dataset]_나타납니다. 여기에서 을 클릭합니다&#x200B;**[!UICONTROL Create Dataset from Schema]**.

![스키마에서 데이터 집합 만들기](../images/labels/dataset_create.png)

데이터 집합을 만드는 데 사용할 수 있는 모든 사용 가능한 스키마를 나열하는 _[!UICONTROL Select Schema]_화면이 나타납니다. 스키마 옆에 있는 라디오 단추를 클릭하여 선택합니다. 오른쪽의_[!UICONTROL Schemas]_ 섹션에는 선택한 스키마에 대한 추가 정보가 표시됩니다. 스키마를 선택하고 나면 을 클릭합니다 **[!UICONTROL Next]**.

![데이터 집합 스키마 선택](../images/labels/dataset_schema.png)

데이터 _세트 구성_ 화면이 나타납니다. 새 데이터 세트에 대한 **이름** (필수) 및 **설명** (선택 사항이지만 권장)을 입력한 다음 **[!UICONTROL Finish]**&#x200B;을 클릭합니다.

![이름 및 설명이 있는 데이터 집합 구성](../images/labels/dataset_configure.png)

새로 만든 데이터 세트에 대한 정보를 표시하는 _[!UICONTROL Dataset Activity]_페이지가 나타납니다. 이 예에서 데이터 세트의 이름은 &quot;충성도 구성원&quot;이므로 맨 위 탐색은 데이터 집합 > 충성도_&#x200B;구성원을 보여줍니다&#x200B;_.

![데이터 집합 활동 페이지](../images/labels/dataset_activity.png)

### 데이터 세트에 데이터 사용 레이블 추가 {#add-labels}

새 데이터 세트를 만들거나 _[!UICONTROL Datasets]_작업 영역의 목록에서 기존 데이터 세트를 선택한 후 을 클릭하여&#x200B;**[!UICONTROL Data Governance]**_[!UICONTROL Data Governance]_ 작업 공간을 엽니다. 작업 영역을 사용하면 데이터 집합 수준 및 필드 수준에서 데이터 사용 레이블을 관리할 수 있습니다.

![데이터 집합 데이터 거버넌스 탭](../images/labels/dataset_data_governance.png)

데이터 집합 수준에서 데이터 사용 레이블을 편집하려면 먼저 데이터 집합 이름 옆에 있는 연필 아이콘을 클릭합니다.

![데이터 세트 수준 레이블 편집](../images/labels/dataset_labels_edit_button.png)

대화 _[!UICONTROL Edit Governance Labels]_상자가 열립니다. 대화 상자에서 데이터 세트에 적용할 레이블 옆에 있는 상자를 선택합니다. 이러한 레이블은 데이터 세트 내의 모든 필드에서 상속됩니다. 각 상자를 선택하면_[!UICONTROL Applied Labels]_ 머리글이 업데이트되고 선택한 레이블이 표시됩니다. 원하는 레이블을 선택한 후 을 클릭합니다 **[!UICONTROL Save Changes]**.

<img alt="데이터 세트 수준에서 거버넌스 레이블 적용" src="../images/labels/apply-labels-dataset.png" width="700"><br>

데이터 집합 수준에서 적용한 레이블을 보여주는 작업 영역이 다시 _[!UICONTROL Data Governance]_나타납니다. 또한 레이블이 데이터 세트 내의 각 필드에 상속됨을 확인할 수 있습니다.

![필드가 상속한 데이터 세트 레이블](../images/labels/dataset_inherited_labels.png)

데이터 세트 수준의 레이블 옆에 &quot;x&quot;가 표시되어 레이블을 제거할 수 있습니다. 각 필드 옆에 상속된 레이블에 &quot;x&quot;가 없으며 제거 또는 편집 기능이 없는 &quot;회색으로 표시됨&quot;이 표시됩니다. 이는 **상속된 필드가 읽기 전용이므로**&#x200B;필드 수준에서 제거할 수 없기 때문입니다.

기본적으로 전환 **[!UICONTROL Show Inherited Labels]** 설정은 켜짐으로 설정되어 있으므로 데이터 세트에서 해당 필드로 상속된 레이블을 볼 수 있습니다. 전환으로 전환하면 데이터 세트 내에서 상속된 모든 레이블이 숨겨집니다.

![상속된 레이블 숨기기](../images/labels/hide_inherited_labels.png)

## 데이터 세트 필드 수준에서 데이터 사용 레이블 관리

데이터 세트 수준에서 [데이터 사용 레이블을](#add-labels)추가 및 편집하는 워크플로우를 계속 진행할 수 있고 해당 데이터 세트에 대한 _[!UICONTROL Data Governance]_작업 공간 내에서 필드 수준 레이블을 관리할 수도 있습니다.

데이터 사용 레이블을 개별 필드에 적용하려면 필드 이름 옆에 있는 확인란을 선택한 다음 을 **[!UICONTROL Edit Governance Labels]**&#x200B;클릭합니다.

![필드 레이블 편집](../images/labels/fields_single_field.png)

대화 상자가 _[!UICONTROL Edit Governance Labels]_나타납니다. 대화 상자에는 선택한 필드, 적용된 레이블 및 상속된 레이블이 표시된 머리글이 표시됩니다. 대화 상자에서 상속된 레이블(C2 및 C5)이 회색으로 표시됩니다. 데이터 집합 수준에서 상속되는 읽기 전용 레이블이므로 데이터 집합 수준에서만 편집할 수 있습니다.

<img alt="개별 필드에 대한 거버넌스 레이블 편집" src="../images/labels/field-label-inheritance.png" width="700"><br>

사용할 각 레이블 옆의 확인란을 클릭하여 필드 수준 레이블을 선택합니다. 레이블을 선택하면 헤더가 업데이트되어 _[!UICONTROL Applied Labels]__[!UICONTROL Selected Fields]_ 헤더에 표시된 필드에 적용된 레이블이 표시됩니다. 필드 수준 레이블 선택이 끝나면 을 클릭합니다 **[!UICONTROL Save Changes]**.

<img alt="필드 수준 레이블 적용" src="../images/labels/apply-labels-field.png" width="700"><br>

이제 필드 이름 옆에 있는 행에 선택한 필드 수준 레이블이 표시되는 작업 영역이 다시 나타납니다. _[!UICONTROL Data Governance]_필드 수준 레이블 옆에 레이블을 제거할 수 있는 &quot;x&quot;가 있습니다.

![필드 수준 레이블을 표시하는 필드](../images/labels/fields_show_field_level_labels.png)

이러한 단계를 반복하여 필드 수준 레이블을 동시에 적용할 여러 필드를 선택하는 등 추가 필드에 대해 필드 수준 레이블을 계속 추가하고 편집할 수 있습니다.

![여러 필드를 선택하여 필드 수준 레이블을 동시에 적용할 수 있습니다.](../images/labels/fields_select_multiple.png)

상속은 최상위 수준 아래로(데이터 세트→필드)에서만 이동하므로 필드 수준에 적용된 레이블이 다른 필드나 데이터 세트에 전파되지 않습니다.

## 다음 단계

데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가했으므로 이제 데이터를 Experience Platform으로 인제스트할 수 있습니다. 자세한 내용은 [데이터 수집 설명서를](../../ingestion/home.md)참조하십시오.

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요를](../policies/overview.md)참조하십시오.

## Journey Orchestration용

다음 비디오에서는 데이터 거버넌스에 대한 이해를 지원하고 데이터 세트 및 개별 필드에 레이블을 적용하는 방법을 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
