---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 영역;필드 그룹;필드 그룹;;home;popular topics;api;XDM system;experience data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: UI에서 스키마 필드 그룹 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마 필드 그룹을 만들고 편집하는 방법을 알아봅니다.
topic: 사용 안내서
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# UI에서 스키마 필드 그룹 만들기 및 편집

XDM(경험 데이터 모델)에서 스키마 필드 그룹은 개인 세부 사항, 호텔 환경 설정 또는 주소와 같은 특정 기능을 구현하는 하나 이상의 필드를 정의하는 재사용 가능한 구성 요소입니다. 필드 그룹은 호환 클래스를 구현하는 스키마의 일부로 포함되도록 되어 있습니다.

필드 그룹은 필드 그룹이 나타내는 데이터(레코드 또는 시간 시리즈)의 비헤이비어를 기반으로 호환하는 클래스를 정의합니다. 즉, 모든 클래스에서 일부 필드 그룹을 사용할 수 없습니다.

Adobe Experience Platform은 다양한 마케팅 활용 사례를 포함하는 다양한 표준 필드 그룹을 제공합니다. 그러나 고유한 사용자 지정 필드 그룹을 만들고 편집하여 XDM 스키마 내에서 비즈니스와 관련된 추가 개념을 정의할 수도 있습니다. 이 안내서에서는 플랫폼 UI에서 조직에 대한 사용자 정의 필드 그룹을 만들고, 편집하고, 관리하는 방법에 대한 개요를 제공합니다.

## 전제 조건

이 가이드를 사용하려면 XDM 시스템에 대한 작업 이해가 필요합니다. Experience Platform 에코시스템 내의 XDM 역할에 대한 소개를 보려면 [XDM 개요](../../home.md) 및 필드 그룹이 XDM 스키마에 기여하는 방법에 대한 스키마 컴포지션](../../schema/composition.md)의 [기본 사항을 참조하십시오.

이 안내서는 필요하지 않지만 [!DNL Schema Editor]의 다양한 기능에 익숙해지려면 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성의 자습서를 따르는 것이 좋습니다.

## 새 필드 그룹 {#create} 만들기

새 필드 그룹을 만들려면 먼저 필드 그룹이 추가될 스키마를 선택해야 합니다. [새 스키마 만들기](./schemas.md#create) 또는 [편집할 기존 스키마를 선택하도록 선택할 수 있습니다](./schemas.md#edit).

[!DNL Schema Editor]에 스키마가 열리면 왼쪽 레일의 [!UICONTROL Field groups] 섹션 옆에 있는 **[!UICONTROL Add]**&#x200B;을 선택합니다.

![](../../images/ui/resources/field-groups/add-field-group.png)

조직의 기존 필드 그룹 목록이 표시된 대화 상자가 나타납니다. 대화 상자의 맨 위에서 **[!UICONTROL Create new field group]**&#x200B;을 선택합니다. 여기에서 필드 그룹에 **[!UICONTROL Display name]** 및 **[!UICONTROL Description]**&#x200B;을 제공할 수 있습니다. 완료되면 **[!UICONTROL Add field group]**&#x200B;을 선택합니다.

![](../../images/ui/resources/field-groups/create-field-group.png)

왼쪽 레일에 새 필드 그룹이 나열된 상태로 [!DNL Schema Editor]이 다시 나타납니다. 이 필드는 완전히 새로운 필드 그룹이므로 현재 스키마에 필드를 제공하지 않으므로 캔버스는 변경되지 않습니다. 이제 필드 그룹](#add-fields)에 필드 추가를 시작할 수 있습니다.[

## 기존 필드 그룹 {#edit} 편집

>[!NOTE]
>
>조직에서 정의한 사용자 정의 필드 그룹만 완전히 편집하고 사용자 정의할 수 있습니다. Adobe에 의해 정의된 핵심 필드 그룹의 경우 개별 스키마 컨텍스트 내에서 해당 필드의 표시 이름만 편집할 수 있습니다. 자세한 내용은 [스키마 필드에 대한 표시 이름 편집](./schemas.md#display-names)의 섹션을 참조하십시오.
>
>사용자 지정 필드 그룹이 데이터 수집에 대한 스키마에 저장되고 사용되면 이후 필드 그룹에 추가 변경만 수행할 수 있습니다. 자세한 내용은 스키마 진화의 [규칙](../../schema/composition.md#evolution)을 참조하십시오.

기존 필드 그룹을 편집하려면 먼저 [!DNL Schema Editor] 내에 필드 그룹을 사용하는 스키마를 열어야 합니다. [기존 스키마를 선택하여](./schemas.md#edit)편집하거나 [새 스키마](./schemas.md#create)를 만들고 문제의 필드 그룹을 추가할 수 있습니다.

편집기에서 스키마를 연 후에는 [필드 그룹](#add-fields)에 필드 추가를 시작할 수 있습니다.

## 필드 그룹 {#add-fields}에 필드 추가

[!DNL Schema Editor]의 필드 그룹에 필드를 추가하려면 왼쪽 레일에서 필드 그룹의 이름을 선택한 다음 캔버스에서 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택합니다.

![](../../images/ui/resources/field-groups/add-field.png)

**[!UICONTROL New field]**&#x200B;이 캔버스에 표시되고 필드의 속성을 구성하기 위한 컨트롤을 표시하는 오른쪽 레일이 업데이트됩니다. 필드 그룹을 구성하고 필드 그룹에 추가하는 방법에 대한 특정 단계는 [UI](../fields/overview.md#define)에서 필드 정의 가이드를 참조하십시오.

필드 그룹에 필요한 만큼 필드를 계속 추가합니다. 완료되면 **[!UICONTROL Save]**&#x200B;을 선택하여 스키마와 필드 그룹을 모두 저장합니다.

![](../../images/ui/resources/field-groups/complete-field-group.png)

동일한 필드 그룹이 이미 다른 스키마에서 사용 중이면 새로 추가한 필드가 해당 스키마에 자동으로 나타납니다.

## 다음 단계

이 안내서에서는 플랫폼 UI를 사용하여 필드 그룹을 만들고 편집하는 방법에 대해 설명합니다. [!UICONTROL Schemas] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 필드 그룹을 관리하는 방법에 대해 알아보려면 [필드 그룹 끝점 안내서](../../api/field-groups.md)를 참조하십시오.