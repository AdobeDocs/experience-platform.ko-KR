---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블;정책 서비스;데이터 사용 레이블 사용자 안내서
solution: Experience Platform
title: UI에서 데이터 사용 레이블 관리
topic: labels
description: 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스 내에서 데이터 사용 레이블을 사용하여 작업하는 단계를 설명합니다.
translation-type: tm+mt
source-git-commit: 41d01b3aec0afa60dd602716a30cc94402702a70
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---


# UI에서 데이터 사용 레이블 관리

이 사용자 안내서는 [!DNL Experience Platform] 사용자 인터페이스 내에서 데이터 사용 레이블을 사용하여 작업하는 단계를 설명합니다. 안내서를 사용하기 전에 [!DNL Data Governance] 프레임워크에 대한 보다 강력한 소개를 보려면 [[!DNL Data Governance] 개요](../home.md)를 참조하십시오.

## 데이터 세트 수준에서 레이블 관리

데이터 세트 수준에서 데이터 사용 레이블을 관리하려면 기존 데이터 세트를 선택하거나 새 데이터 세트를 만들어야 합니다. Adobe Experience Platform에 로그인한 후 왼쪽 탐색 영역에서 **[!UICONTROL 데이터 집합]**&#x200B;을 선택하여 **[!UICONTROL 데이터 집합]** 작업 영역을 엽니다. 이 페이지에는 조직에 속하는 모든 데이터 세트와 각 데이터 세트에 관련된 유용한 세부 정보가 나열됩니다.

![데이터 작업 공간 내의 데이터 세트 탭](../images/labels/datasets-tab.png)

다음 섹션에서는 레이블을 적용할 새 데이터 세트를 만드는 단계를 제공합니다. 기존 데이터 세트에 대한 레이블을 편집하려면 목록에서 데이터 세트를 선택하고 데이터 세트](#add-labels)에 데이터 사용 레이블 추가 [로 건너뜁니다.

### 새 데이터 세트 만들기

>[!NOTE]
>
>이 예에서는 사전 구성된 [!DNL Experience Data Model](XDM) 스키마를 사용하여 데이터 세트를 만듭니다. XDM 스키마에 대한 자세한 내용은 스키마 구성](../../xdm/schema/composition.md)의 [XDM 시스템 개요](../../xdm/home.md) 및 [기본 사항을 참조하십시오.

새 데이터 집합을 만들려면 **[!UICONTROL 데이터 집합]** 작업 영역의 오른쪽 위 모서리에 있는 **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 선택합니다.

![](../images/labels/create-dataset.png)

**[!UICONTROL 데이터 세트 만들기]** 화면이 나타납니다. 여기에서 **[!UICONTROL 스키마]**&#x200B;에서 데이터 집합 만들기를 선택합니다.

![스키마에서 데이터 집합 만들기](../images/labels/create-from-dataset.png)

데이터 집합을 만드는 데 사용할 수 있는 모든 사용 가능한 스키마를 나열하는 **[!UICONTROL 스키마 선택]** 화면이 나타납니다. 스키마 옆에 있는 라디오 단추를 선택하여 선택합니다. 오른쪽의 **[!UICONTROL 스키마]** 섹션에는 선택한 스키마에 대한 추가 세부 정보가 표시됩니다. 스키마를 선택하고 나면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![데이터 집합 스키마 선택](../images/labels/select-schema.png)

**[!UICONTROL 데이터 세트 구성]** 화면이 나타납니다. 새 데이터 세트에 대한 이름(필수) 및 설명(선택 사항이지만 권장)을 입력한 다음 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![이름 및 설명을 사용하여 데이터 세트 구성](../images/labels/configure-dataset.png)

새로 만든 데이터 세트에 대한 정보를 표시하는 **[!UICONTROL 데이터 집합 활동]** 페이지가 나타납니다. 이 예에서 데이터 세트의 이름은 &quot;충성도 구성원&quot;이므로 위쪽 탐색에는 **데이터 집합 > 충성도 구성원**&#x200B;이 표시됩니다.

![데이터 세트 활동 페이지](../images/labels/dataset-created.png)

### 데이터 세트 {#add-labels}에 데이터 사용 레이블 추가

새 데이터 집합을 만들거나 **[!UICONTROL 데이터 집합]** 작업 영역의 목록에서 기존 데이터 집합을 선택한 후 **[!UICONTROL 데이터 거버넌스]**&#x200B;를 선택하여 **[!UICONTROL 데이터 거버넌스]** 작업 영역을 엽니다. 작업 공간에서는 데이터 세트 수준 및 필드 수준에서 데이터 사용 레이블을 관리할 수 있습니다.

![데이터 세트 데이터 거버넌스 탭](../images/labels/dataset-governance.png)

데이터 세트 수준에서 데이터 사용 레이블을 편집하려면 먼저 데이터 세트 이름 옆에 있는 연필 아이콘을 선택합니다.

![데이터 세트 수준 레이블 편집](../images/labels/dataset-level-edit.png)

**[!UICONTROL 관리 레이블 편집]** 대화 상자가 열립니다. 대화 상자에서 데이터 세트에 적용할 레이블 옆에 있는 상자를 선택합니다. 이러한 레이블은 데이터 세트 내의 모든 필드에 상속됩니다. 각 확인란을 선택하면 **[!UICONTROL 적용된 레이블]** 헤더가 업데이트되며 선택한 레이블이 표시됩니다. 원하는 레이블을 선택하고 **[!UICONTROL 변경 내용 저장]**&#x200B;을 선택합니다.

![데이터 세트 수준에서 거버넌스 레이블 적용](../images/labels/apply-labels-dataset.png)

데이터 세트 수준에서 적용한 레이블을 보여주는 **[!UICONTROL 데이터 거버넌스]** 작업 영역이 다시 나타납니다. 또한 레이블이 데이터 세트 내의 각 필드에 상속됨을 확인할 수 있습니다.

![필드가 상속한 데이터 세트 레이블](../images/labels/dataset-labels-applied.png)

데이터 세트 수준의 레이블 옆에 &quot;x&quot;가 표시되어 레이블을 제거할 수 있습니다. 각 필드 옆에 상속된 레이블에 &quot;x&quot;가 없고 제거 또는 편집 기능이 없는 &quot;회색으로 표시&quot;가 됩니다. 이것은 **상속된 필드가 읽기 전용이므로 필드 수준에서 제거할 수 없음을 의미합니다.**

**[!UICONTROL 상속된 레이블 표시]** 토글은 기본적으로 설정되어 있으므로 데이터 세트에서 해당 필드로 상속된 레이블을 볼 수 있습니다. 토글을 전환하면 데이터 세트 내에 상속된 모든 레이블이 숨겨집니다.

![상속된 레이블 숨기기](../images/labels/inherited-labels.png)

## 필드 수준에서 레이블 관리

데이터 세트 수준](#add-labels)에서 데이터 사용 레이블을 추가 및 편집하는 작업 과정을 계속하면 해당 데이터 세트에 대한 **[!UICONTROL 데이터 거버넌스]** 작업 공간 내에서 필드 수준 레이블을 관리할 수도 있습니다.[

데이터 사용 레이블을 개별 필드에 적용하려면 필드 이름 옆에 있는 확인란을 선택한 다음 **[!UICONTROL 관리 레이블 편집]**&#x200B;을 선택합니다.

![필드 레이블 편집](../images/labels/field-label-edit.png)

**[!UICONTROL 관리 레이블 편집]** 대화 상자가 나타납니다. 대화 상자에는 선택한 필드, 적용된 레이블 및 상속된 레이블이 표시된 머리글이 표시됩니다. 대화 상자에서 상속된 레이블(C2 및 C5)이 회색으로 표시됩니다. 데이터 세트 수준에서 상속되는 읽기 전용 레이블이므로 데이터 세트 수준에서만 편집할 수 있습니다.

![개별 필드에 대한 관리 레이블 편집](../images/labels/field-label-inheritance.png)

사용할 각 레이블 옆의 확인란을 선택하여 필드 수준 레이블을 선택합니다. 레이블을 선택하면 **[!UICONTROL 적용된 레이블]** 헤더가 업데이트되어 **[!UICONTROL 선택한 필드]** 헤더에 표시된 필드에 적용된 레이블을 표시합니다. 필드 수준 레이블 선택이 끝나면 **[!UICONTROL 변경 내용 저장]**&#x200B;을 선택합니다.

![필드 수준 레이블 적용](../images/labels/apply-labels-field.png)

**[!UICONTROL 데이터 거버넌스]** 작업 영역이 다시 나타납니다. 이 작업 공간은 필드 이름 옆의 행에 선택한 필드 수준 레이블을 표시합니다. 필드 수준 레이블 옆에 &quot;x&quot;가 있으며 레이블을 제거할 수 있습니다.

![필드 수준 레이블을 표시하는 필드](../images/labels/field-labels-applied.png)

필드 수준 레이블을 동시에 적용할 여러 필드를 선택하는 등 추가 필드에 대해 필드 수준 레이블을 계속 추가하고 편집하려면 이 단계를 반복할 수 있습니다.

![여러 필드를 선택하여 필드 수준 레이블을 동시에 적용할 수 있습니다.](../images/labels/multiple-fields.png)

상속은 최상위 수준 아래로(데이터 세트 → 필드)에서만 이동되므로 필드 수준에서 적용된 레이블이 다른 필드나 데이터 세트로 전파되지 않습니다.

## 사용자 지정 레이블 관리

[!DNL Experience Platform] UI의 **[!UICONTROL 정책]** 작업 공간 내에 사용자 지정 사용 레이블을 만들 수 있습니다. 왼쪽 탐색에서 **[!UICONTROL 정책]**&#x200B;을 선택한 다음 **[!UICONTROL 레이블]**&#x200B;을 선택하여 기존 레이블 목록을 봅니다. 여기에서 **[!UICONTROL 레이블 만들기]**&#x200B;를 선택합니다.

![](../images/labels/create-label-btn.png)

**[!UICONTROL 레이블 만들기]** 대화 상자가 나타납니다. 여기에서 새 레이블에 대해 다음 정보를 제공합니다.

* **[!UICONTROL 식별자]**:레이블의 고유 식별자입니다. 이 값은 조회 목적으로 사용되므로 짧고 간결해야 합니다.
* **[!UICONTROL 이름]**:레이블의 친숙한 표시 이름입니다.
* **[!UICONTROL 설명]**:(선택 사항) 추가적인 컨텍스트를 제공하는 레이블에 대한 설명입니다.

완료되면 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

![](../images/labels/create-label.png)

대화 상자가 닫히고 새로 만든 사용자 지정 레이블이 **[!UICONTROL 레이블]** 탭 아래의 목록에 나타납니다.

![](../images/labels/label-created.png)

이제 데이터 세트 및 필드에 대한 사용 레이블을 편집할 때 또는 데이터 사용 정책을 만들 때 **[!UICONTROL 사용자 지정 레이블]** 아래에서 레이블을 선택할 수 있습니다.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## 다음 단계

이제 데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가했으므로 데이터를 [!DNL Experience Platform]에 인제스트할 수 있습니다. 자세한 내용을 보려면 [데이터 통합 문서](../../ingestion/home.md)를 읽으십시오.

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요](../policies/overview.md)를 참조하십시오.

## Journey Orchestration용

다음 비디오는 [!DNL Data Governance]에 대한 이해를 지원하기 위한 비디오이며 데이터 세트 및 개별 필드에 레이블을 적용하는 방법에 대해 개괄적으로 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
