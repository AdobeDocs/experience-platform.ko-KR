---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;필드 그룹;필드 그룹;
solution: Experience Platform
title: UI에서 스키마 필드 그룹 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마 필드 그룹을 만들고 편집하는 방법을 알아봅니다.
topic-legacy: user guide
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# UI에서 스키마 필드 그룹 만들기 및 편집

XDM(Experience Data Model)에서 스키마 필드 그룹은 개인 세부 사항, 호텔 환경 설정 또는 주소와 같은 특정 기능을 구현하는 필드를 하나 이상 정의하는 재사용 가능한 구성 요소입니다. 필드 그룹은 호환 클래스를 구현하는 스키마의 일부로 포함되기 위한 것입니다.

필드 그룹은 필드 그룹이 나타내는 데이터(레코드 또는 시계열)의 동작을 기반으로 호환되는 클래스를 정의합니다. 즉, 모든 필드 그룹을 모든 클래스에서 사용할 수는 없습니다.

Adobe Experience Platform에서는 광범위한 마케팅 사용 사례를 다루는 많은 표준 필드 그룹을 제공합니다. 그러나 고유한 사용자 지정 필드 그룹을 만들고 편집하여 XDM 스키마 내에서 비즈니스에 관련된 추가 개념을 정의할 수도 있습니다. 이 안내서에서는 Platform UI에서 조직의 사용자 지정 필드 그룹을 작성, 편집 및 관리하는 방법에 대한 개요를 제공합니다.

## 전제 조건

이 안내서에서는 XDM 시스템을 작업해야 합니다. Experience Platform 에코시스템 내에서 XDM의 역할에 대한 소개는 [XDM 개요](../../home.md) 를 참조하고, 필드 그룹이 XDM 스키마에 기여하는 방법은 스키마 구성](../../schema/composition.md)의 기본 사항을 참조하십시오.[

이 안내서에는 필요하지 않지만 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성을 위한 튜토리얼도 따라 [!DNL Schema Editor]의 다양한 기능에 익숙해지는 것이 좋습니다.

## 새 필드 그룹 만들기 {#create}

새 필드 그룹을 만들려면 먼저 필드 그룹이 추가될 스키마를 선택해야 합니다. [새 스키마](./schemas.md#create) 또는 [편집할 기존 스키마를 선택하도록 선택할 수 있습니다](./schemas.md#edit).

[!DNL Schema Editor]에 스키마가 열리면 왼쪽 레일의 [!UICONTROL 필드 그룹] 섹션 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

![](../../images/ui/resources/field-groups/add-field-group.png)

조직의 기존 필드 그룹 목록을 표시하는 대화 상자가 나타납니다. 대화 상자의 맨 위에서 **[!UICONTROL 새 필드 그룹 만들기]**&#x200B;를 선택합니다. 여기에서 필드 그룹에 대해 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]**&#x200B;을 제공할 수 있습니다. 완료되면 **[!UICONTROL 필드 그룹 추가]**&#x200B;를 선택합니다.

![](../../images/ui/resources/field-groups/create-field-group.png)

왼쪽 레일에 새 필드 그룹이 나열되어 있는 [!DNL Schema Editor] 이 다시 나타납니다. 이 그룹은 완전히 새로운 필드 그룹이므로 현재 스키마에 필드를 제공하지 않으므로 캔버스는 변경되지 않은 상태로 유지됩니다. 이제 [필드를 필드 그룹](#add-fields)에 추가할 수 있습니다.

## 기존 필드 그룹 편집 {#edit}

>[!NOTE]
>
>조직에서 정의한 사용자 정의 필드 그룹만 완전히 편집하고 사용자 지정할 수 있습니다. Adobe으로 정의된 코어 필드 그룹의 경우 개별 스키마 컨텍스트 내에서 해당 필드의 표시 이름만 편집할 수 있습니다. 자세한 내용은 [스키마 필드에 대한 표시 이름 편집](./schemas.md#display-names)의 섹션을 참조하십시오.
>
>사용자 지정 필드 그룹이 저장되고 데이터 수집을 위해 스키마에 사용되면, 이후에 필드 그룹에 추가 변경만 수행할 수 있습니다. 자세한 내용은 스키마 진화 규칙](../../schema/composition.md#evolution)을 참조하십시오.[

기존 필드 그룹을 편집하려면 먼저 [!DNL Schema Editor] 내에서 필드 그룹을 사용하는 스키마를 열어야 합니다. [편집할 기존 스키마를 선택하거나](./schemas.md#edit)새 스키마](./schemas.md#create)를 만들고 해당 필드 그룹을 추가할 수 있습니다.[

편집기에서 스키마를 열면 [필드 그룹](#add-fields)에 필드를 추가할 수 있습니다.

## 필드 그룹에 필드 추가 {#add-fields}

[!DNL Schema Editor] 의 필드 그룹에 필드를 추가하려면 왼쪽 레일에서 필드 그룹의 이름을 선택한 다음 캔버스에서 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택합니다.

![](../../images/ui/resources/field-groups/add-field.png)

**[!UICONTROL 새 필드]**&#x200B;가 캔버스에 나타나고 오른쪽 레일이 업데이트되어 필드의 속성을 구성하는 컨트롤을 표시합니다. 필드 그룹에 필드를 구성하고 추가하는 방법에 대한 특정 단계는 UI](../fields/overview.md#define)에서 필드 정의 의 안내서를 참조하십시오.[

필드 그룹에 필요한 만큼 필드를 계속 추가합니다. 완료되면 **[!UICONTROL 저장]** 을 선택하여 스키마와 필드 그룹을 모두 저장합니다.

![](../../images/ui/resources/field-groups/complete-field-group.png)

동일한 필드 그룹을 이미 다른 스키마에 사용하는 경우, 새로 추가된 필드가 해당 스키마에 자동으로 표시됩니다.

## 다음 단계

이 안내서에서는 플랫폼 UI를 사용하여 필드 그룹을 만들고 편집하는 방법에 대해 설명합니다. [!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 공간 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 필드 그룹을 관리하는 방법에 대한 자세한 내용은 [필드 그룹 엔드포인트 가이드](../../api/field-groups.md)를 참조하십시오.