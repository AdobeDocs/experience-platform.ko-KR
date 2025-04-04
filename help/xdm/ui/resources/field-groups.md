---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 영역;필드 그룹;필드 그룹;
solution: Experience Platform
title: UI에서 스키마 필드 그룹 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마 필드 그룹을 만들고 편집하는 방법을 알아봅니다.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 8%

---

# UI에서 스키마 필드 그룹 만들기 및 편집 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="표준 또는 사용자 정의 필드 그룹 필터"
>abstract="사용할 수 있는 필드 그룹의 목록은 생성 방법에 따라 사전에 필터링됩니다. 표준과 사용자 정의 옵션 중에서 선택하려면 라디오 버튼을 선택하십시오. 표준 옵션은 Adobe에서 생성한 엔티티를 표시하며 사용자 정의 옵션은 내 조직 내에서 생성된 엔티티를 표시합니다. 필드 그룹의 생성 및 편집에 대한 자세한 내용은 설명서를 참조하시기 바랍니다."

XDM(Experience Data Model)에서 스키마 필드 그룹은 개인 세부 정보, 호텔 환경 설정 또는 주소와 같은 특정 기능을 구현하는 하나 이상의 필드를 정의하는 재사용 가능한 구성 요소입니다. 필드 그룹은 호환 가능한 클래스를 구현하는 스키마의 일부로 포함하기 위한 것입니다.

필드 그룹은 필드 그룹이 나타내는 데이터(레코드 또는 시계열)의 동작을 기반으로 하여 호환되는 클래스를 정의합니다. 즉, 모든 필드 그룹을 모든 클래스에서 사용할 수 있는 것은 아닙니다.

Adobe Experience Platform은 광범위한 마케팅 사용 사례를 다루는 많은 표준 필드 그룹을 제공합니다. 그러나 사용자 정의 필드 그룹을 만들고 편집하여 XDM 스키마 내에서 비즈니스와 관련된 추가 개념을 정의할 수도 있습니다. 이 안내서에서는 Experience Platform UI에서 조직의 사용자 정의 필드 그룹을 생성, 편집 및 관리하는 방법에 대한 개요를 제공합니다.

## 전제 조건 {#prerequisites}

이 안내서에서는 XDM 시스템에 대한 작업 이해가 필요합니다. Experience Platform 에코시스템 내에서 XDM의 역할에 대한 소개는 [XDM 개요](../../home.md)를, 필드 그룹이 XDM 스키마에 기여하는 방법은 스키마 컴포지션의 [기본 사항](../../schema/composition.md)을 참조하세요.

이 안내서에서는 필요하지 않지만 [UI에서 스키마 작성](../../tutorials/create-schema-ui.md)에 대한 자습서를 따라 [!DNL Schema Editor]의 다양한 기능을 숙지하는 것이 좋습니다.

## 새 필드 그룹 만들기 {#create}

새 필드 그룹을 만들려면 먼저 필드 그룹을 추가할 스키마를 선택해야 합니다. [새 스키마를 만들거나](./schemas.md#create) [편집할 기존 스키마를 선택](./schemas.md#edit)할 수 있습니다.

[!DNL Schema Editor]에서 스키마를 열면 왼쪽 레일의 [!UICONTROL 필드 그룹] 섹션 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

![](../../images/ui/resources/field-groups/add-field-group.png)

표시되는 대화 상자에서 **[!UICONTROL 새 필드 그룹 만들기]**&#x200B;를 선택합니다. 여기에서 필드 그룹에 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]**&#x200B;을 제공할 수 있습니다. 완료되면 **[!UICONTROL 필드 그룹 추가]**&#x200B;를 선택합니다.

![](../../images/ui/resources/field-groups/create-field-group.png)

새 필드 그룹이 왼쪽 레일에 나열되어 [!DNL Schema Editor]이(가) 다시 나타납니다. 완전히 새로운 필드 그룹이므로 현재 스키마에 필드를 제공하지 않으므로 캔버스는 변경되지 않습니다. 이제 [필드 그룹에 필드 추가](#add-fields)를 시작할 수 있습니다.

![](../../images/ui/resources/field-groups/field-group-added.png)

## 필드 그룹 필터링 {#filter}

사용할 수 있는 필드 그룹의 목록은 생성 방법에 따라 사전에 필터링됩니다. 기본 설정은 Adobe에서 정의한 필드 그룹을 표시합니다. 그러나 목록을 필터링하여 조직에서 만든 목록을 표시할 수도 있습니다. 라디오 단추를 선택하여 [!UICONTROL 표준]과(와) [!UICONTROL 사용자 지정] 옵션 중에서 선택하십시오. [!UICONTROL 표준] 옵션은 Adobe에서 만든 엔터티를 표시하고 [!UICONTROL 사용자 지정] 옵션은 조직 내에서 만든 엔터티를 표시합니다.

[!UICONTROL Standard] 및 [!UICONTROL Custom]이 강조 표시된 [!UICONTROL 스키마] 작업 영역의 [!UICONTROL 필드 그룹] 탭](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)![

## 기존 필드 그룹 편집 {#edit}

>[!NOTE]
>
>조직에서 정의한 사용자 정의 필드 그룹만 완전히 편집하고 사용자 정의할 수 있습니다. Adobe에서 정의한 코어 필드 그룹의 경우 해당 필드에 대한 표시 이름만 개별 스키마의 컨텍스트 내에서 편집할 수 있습니다. 이러한 속성은 자물쇠 아이콘(![자물쇠 아이콘)으로 스키마 편집기에 표시됩니다.](/help/images/icons/lock-closed.png)). 자세한 내용은 [스키마 필드에 대한 표시 이름 편집](./schemas.md#display-names)의 섹션을 참조하십시오.
>
>사용자 정의 필드 그룹이 데이터 수집을 위해 스키마에 저장되고 사용된 후에는 필드 그룹에 추가 변경만 수행할 수 있습니다. 자세한 내용은 [스키마 진화의 규칙](../../schema/composition.md#evolution)을 참조하십시오.

기존 필드 그룹을 편집하려면 먼저 [!DNL Schema Editor] 내에서 필드 그룹을 사용하는 스키마를 열어야 합니다. [편집할 기존 스키마를 선택](./schemas.md#edit)하거나 [새 스키마를 만들기](./schemas.md#create)하고 해당 필드 그룹을 추가할 수 있습니다.

편집기에서 스키마를 열면 [필드 그룹에 필드 추가](#add-fields)를 시작할 수 있습니다.

## 필드 그룹에 필드 추가 {#add-fields}

>[!NOTE]
>
>이 섹션은 사용자 정의 필드 그룹에 필드를 추가하는 데 중점을 둡니다. 표준 필드 그룹에 사용자 지정 필드를 추가하는 방법에 대한 자세한 내용은 [스키마 UI 안내서](./schemas.md#custom-fields-for-standard-groups)를 참조하십시오.

사용자 지정 필드 그룹에 필드를 추가하려면 캔버스에서 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택하여 시작하십시오.

![](../../images/ui/resources/field-groups/add-field.png)

**[!UICONTROL 제목 없는 필드]** 자리 표시자가 캔버스에 나타나고 오른쪽 레일이 업데이트되어 필드의 속성을 구성하는 컨트롤을 표시합니다. 다른 필드 형식을 구성하는 방법에 대한 특정 단계는 [UI의 필드 정의](../fields/overview.md#define)에 대한 안내서를 참조하십시오.

**[!UICONTROL 할당 대상]**&#x200B;에서 **[!UICONTROL 필드 그룹]** 옵션을 선택한 다음 드롭다운을 사용하여 목록에서 원하는 필드 그룹을 선택합니다. 필드 그룹의 이름을 입력하여 결과의 범위를 좁힐 수 있습니다.

![](../../images/ui/resources/field-groups/select-field-group.png)

**[!UICONTROL 할당 대상]**&#x200B;에서 **[!UICONTROL 필드 그룹]** 옵션을 선택한 다음 드롭다운을 사용하여 목록에서 원하는 필드 그룹을 선택합니다. 필드 그룹의 이름을 입력하여 결과의 범위를 좁힐 수 있습니다.

![](../../images/ui/resources/field-groups/select-field-group.png)

필드가 스키마에 추가되면 선택한 필드 그룹에 할당됩니다. 필드 그룹에 필요한 만큼 필드를 계속 추가합니다. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마와 필드 그룹을 모두 저장합니다.

![](../../images/ui/resources/field-groups/complete-field-group.png)

동일한 필드 그룹이 다른 스키마에서 이미 사용 중인 경우 새로 추가된 필드가 해당 스키마에 자동으로 표시됩니다.

## 다음 단계 {#next-steps}

이 안내서에서는 Experience Platform UI를 사용하여 필드 그룹을 만들고 편집하는 방법에 대해 다룹니다. [!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 필드 그룹을 관리하는 방법에 대해 알아보려면 [필드 그룹 끝점 안내서](../../api/field-groups.md)를 참조하십시오.
