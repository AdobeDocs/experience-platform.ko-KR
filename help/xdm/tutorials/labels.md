---
title: 스키마에 대한 데이터 사용 레이블 관리
description: Adobe Experience Platform UI의 XDM(Experience Data Model) 스키마 필드에 데이터 사용 레이블을 추가하는 방법을 알아봅니다.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 3d49b5c503ec0fd92f0639abf366d7652566fac7
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 스키마에 대한 데이터 사용 레이블 관리

>[!IMPORTANT]
>
>스키마 기반 레이블 지정이 [속성 기반 액세스 제어](../../access-control/abac/overview.md)은 현재 미국 기반 의료 고객을 위해 제한된 릴리스에서 사용할 수 있습니다. 이 기능은 완전히 릴리스되면 모든 Real-time Customer Data Platform 고객이 사용할 수 있습니다.

Adobe Experience Platform으로 가져오는 모든 데이터는 XDM(Experience Data Model) 스키마에 의해 제한됩니다. 이 데이터는 조직 또는 법적 규정에 의해 정의된 사용 제한을 받을 수 있습니다. 이를 설명하기 위해 플랫폼을 사용하면 [데이터 사용 레이블](../../data-governance/labels/overview.md).

스키마 필드에 적용되는 레이블은 해당 특정 필드에 포함된 데이터에 적용되는 사용 정책을 나타냅니다.

레이블을 개별 데이터 세트(및 해당 데이터 세트 내의 필드)에 적용할 수 있지만 스키마 수준에서 레이블을 적용할 수도 있습니다. 레이블을 스키마에 직접 적용할 때 이러한 레이블은 해당 스키마를 기반으로 하는 모든 기존 및 향후 데이터 세트에 전파됩니다.

또한 하나의 스키마에 추가하는 모든 필드 레이블은 공유 클래스 또는 필드 그룹에서 동일한 필드를 사용하는 다른 모든 스키마로 전파됩니다. 이렇게 하면 전체 데이터 모델에서 유사한 필드에 대한 사용 규칙이 일관되도록 할 수 있습니다.

이 자습서에서는 플랫폼 UI에서 스키마 편집기를 사용하여 스키마에 레이블을 추가하는 단계를 설명합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 편집기](../ui/overview.md): Platform UI에서 스키마 및 기타 리소스를 만들고 관리하는 방법을 알아봅니다.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): 레이블이 지정된 데이터에 대해 수행할 수 있거나 수행할 수 없는 마케팅 작업을 정의하는 정책을 사용하여 플랫폼 작업에 대한 데이터 사용 제한을 적용하기 위한 인프라를 제공합니다.

## 레이블을 추가할 스키마나 필드를 선택합니다 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="거버넌스 레이블 편집"
>abstract="스키마 필드에 레이블을 적용하여 해당 특정 필드에 포함된 데이터에 적용되는 사용 정책을 나타냅니다."

레이블 추가를 시작하려면 먼저 다음을 수행해야 합니다 [편집할 기존 스키마 선택](../ui/resources/schemas.md#edit) 또는 [새 스키마 만들기](../ui/resources/schemas.md#create) 스키마 편집기에서 해당 구조를 보려면 다음과 같이 하십시오.

개별 필드의 레이블을 편집하려면 캔버스에서 필드를 선택한 다음 을(를) 선택할 수 있습니다 **[!UICONTROL 액세스 관리]** 오른쪽 레일에 있습니다.

![스키마 편집기 캔버스에서 필드를 선택합니다](../images/tutorials/labels/manage-access.png)

을(를) 선택할 수도 있습니다 **[!UICONTROL 레이블]** 탭을 선택하고 목록에서 원하는 필드를 선택한 다음 를 선택합니다 **[!UICONTROL 거버넌스 레이블 편집]** 오른쪽 레일에 있습니다.

![에서 필드를 선택합니다 [!UICONTROL 레이블] 탭](../images/tutorials/labels/select-field-on-labels-tab.png)

전체 스키마의 레이블을 편집하려면 연필 아이콘(![](../images/tutorials/labels/pencil-icon.png)) 내의 스키마 이름 옆에 표시됩니다. **[!UICONTROL 레이블]** 탭.

![에서 스키마 이름을 선택합니다 [!UICONTROL 레이블] 탭](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>레이블 사용이 조직의 정책에 따라 다운스트림 작업에 미치는 영향을 설명하는 스키마나 필드의 레이블을 처음 편집하려고 할 때 면책조항 메시지가 나타납니다. 선택 **[!UICONTROL 계속]** 계속 편집하려면 다음을 수행하십시오.
>
>![레이블 사용 면책조항](../images/tutorials/labels/disclaimer.png)

## 스키마 또는 필드의 레이블 편집

선택한 필드의 레이블을 편집할 수 있는 대화 상자가 나타납니다. 개별 객체 유형 필드를 선택한 경우 오른쪽 레일에는 적용된 레이블이 전파되는 하위 필드가 나열됩니다.

![선택한 필드가 표시됩니다.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>전체 스키마에 대한 필드를 편집하는 경우, 오른쪽 레일에는 적용 가능한 필드가 나열되지 않고 대신 스키마 이름을 표시합니다.

표시된 목록을 사용하여 스키마나 필드에 추가할 레이블을 선택합니다. 레이블을 선택하면 **[!UICONTROL 적용된 레이블]** 섹션을 업데이트하여 지금까지 선택한 레이블을 표시합니다.

![적용된 레이블 표시](../images/tutorials/labels/applied-labels.png)

표시된 레이블을 유형별로 필터링하려면 왼쪽 레일에서 원하는 카테고리를 선택합니다. 새 사용자 지정 레이블을 만들려면 **[!UICONTROL 레이블 만들기]**.

![표시된 레이블을 필터링하거나 새 레이블을 만듭니다](../images/tutorials/labels/filter-and-create-custom.png)

선택한 레이블에 만족하면 을(를) 선택합니다 **[!UICONTROL 저장]** 를 눌러 필드 또는 스키마에 적용합니다.

![선택한 레이블을 저장합니다](../images/tutorials/labels/save-labels.png)

다음 **[!UICONTROL 레이블]** 스키마에 적용된 레이블을 표시하는 탭이 다시 나타납니다.

![적용된 필드 레이블](../images/tutorials/labels/field-labels-added.png)

## 다음 단계

이 안내서에서는 스키마 및 필드에 대한 데이터 사용 레이블을 관리하는 방법을 다룹니다. 스키마 수준이 아닌 특정 데이터 세트에 추가하는 방법을 포함하여 데이터 사용 레이블 관리에 대한 자세한 내용은 다음을 참조하십시오. [데이터 사용 레이블 UI 안내서](../../data-governance/labels/user-guide.md).
