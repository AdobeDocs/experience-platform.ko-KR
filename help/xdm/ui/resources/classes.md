---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;클래스;클래스
solution: Experience Platform
title: UI에서 클래스 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 클래스를 만들고 편집하는 방법을 알아봅니다.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 3a9b97b25980d88e0fff3d71e43407b641e6454d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# UI에서 클래스 만들기 및 편집

Adobe Experience Platform에서 스키마의 클래스는 스키마에 포함할 데이터의 행동 측면(레코드 또는 시계열)을 정의합니다. 이 외에도 클래스는 해당 클래스를 기반으로 하는 모든 스키마에는 여러 호환 데이터 세트를 병합하는 방법을 포함하고 제공해야 하는 가장 작은 수의 공통 속성을 설명합니다.

Adobe은 다음을 포함한 몇 가지 표준(&quot;core&quot;) XDM(Experience Data Model) 클래스를 제공합니다 [!DNL XDM Individual Profile] 및 [!DNL XDM ExperienceEvent]. 이러한 핵심 클래스 외에도 고유한 사용자 지정 클래스를 만들어 조직에 대한 더 구체적인 사용 사례를 설명할 수도 있습니다.

이 문서에서는 Experience Platform UI에서 사용자 정의 클래스를 생성, 편집 및 관리하는 방법에 대한 개요를 제공합니다.

## 전제 조건

이 안내서에서는 XDM 시스템을 작업해야 합니다. 자세한 내용은 [XDM 개요](../../home.md) Experience Platform 에코시스템 내에서 XDM의 역할을 소개합니다. [스키마 구성 기본 사항](../../schema/composition.md) 클래스가 XDM 스키마에 기여하는 방법을 알아봅니다.

이 안내서에는 필요하지 않지만, 다음 튜토리얼도 따르는 것이 좋습니다. [UI에서 스키마 작성](../../tutorials/create-schema-ui.md) 다음과 같은 다양한 기능에 익숙해지다 [!DNL Schema Editor].

## 새 클래스 만들기 {#create}

에서 **[!UICONTROL 스키마]** 작업 영역, 선택 **[!UICONTROL 스키마 만들기]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 찾아보기]** 드롭다운

![](../../images/ui/resources/classes/browse-classes.png)

사용 가능한 클래스 목록에서 선택할 수 있는 대화 상자가 나타납니다. 대화 상자 상단에서 을 선택합니다 **[!UICONTROL 새 클래스 만들기]**. 그런 다음 새 클래스에 표시 이름(클래스의 짧고 설명적이며 고유하며 사용자에게 친숙한 이름), 설명 및 스키마가 정의할 데이터(**[!UICONTROL 레코드]** 또는 **[!UICONTROL 시계열]**).

완료되면 을 선택합니다 **[!UICONTROL 클래스 할당]**.

![](../../images/ui/resources/classes/class-details.png)

다음 [!DNL Schema Editor] 캔버스에 방금 만든 사용자 지정 클래스를 기반으로 하는 새 스키마가 표시됩니다. 아직 클래스에 추가된 필드가 없으므로 스키마에는 `_id` 필드의 모든 리소스에 자동으로 적용되는 시스템 생성 고유 식별자를 나타내는 필드입니다 [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>조직에서 정의한 클래스를 구현하는 스키마를 작성할 때는 스키마 필드 그룹을 호환 클래스와 함께 사용해야 합니다. 정의한 클래스는 새로 만들어지므로 **[!UICONTROL 필드 그룹 추가]** 대화 상자. 대신 다음을 수행해야 합니다 [새 필드 그룹 만들기](./field-groups.md#create) 해당 클래스에서 사용할 수 있습니다. 다음에 새 클래스를 구현하는 스키마를 작성할 때 정의한 필드 그룹이 나열되고 사용할 수 있습니다.

이제 시작할 수 있습니다 [클래스에 필드 추가](#add-fields): 클래스를 사용하는 모든 스키마에서 공유됩니다.

## 기존 클래스 편집 {#edit}

>[!NOTE]
>
>조직에서 정의한 사용자 정의 클래스만 완전히 편집하고 사용자 지정할 수 있습니다. Adobe으로 정의된 코어 클래스의 경우 개별 스키마 컨텍스트 내에서 해당 필드의 표시 이름만 편집할 수 있습니다. 의 섹션을 참조하십시오. [스키마 필드에 대한 표시 이름 편집](./schemas.md#display-names) 자세한 내용
>
>사용자 정의 클래스를 저장하고 데이터 처리에 사용하면 그 이후에 추가 변경만 수행할 수 있습니다. 자세한 내용은 [스키마 진화 규칙](../../schema/composition.md#evolution) 추가 정보.

기존 클래스를 편집하려면 **[!UICONTROL 찾아보기]** 그런 다음 편집할 클래스를 사용하는 스키마 이름을 선택합니다.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>작업 공간의 검색 및 필터링 기능을 사용하여 스키마를 보다 쉽게 찾을 수 있습니다. 다음 안내서를 참조하십시오. [xdm 리소스 탐색](../explore.md) 추가 정보.

다음 [!DNL Schema Editor] 캔버스에 스키마 구조가 표시된 상태로 나타납니다. 이제 시작할 수 있습니다 [클래스에 필드 추가](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## 클래스에 필드 추가 {#add-fields}

스키마에서 사용자 지정 클래스를 사용하는 스키마가 있으면 [!UICONTROL 스키마 편집기]를 눌러 클래스에 필드를 추가할 수 있습니다. 새 필드를 추가하려면 **더하기(+)** 스키마 이름 옆에 있는 아이콘을 클릭합니다.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>클래스에 추가하는 모든 필드는 해당 클래스를 사용하는 모든 스키마에서 사용됩니다. 따라서 모든 스키마 사용 사례에 유용할 필드를 신중하게 고려해야 합니다. 이 클래스의 일부 스키마에서만 사용할 수 있는 필드를 추가하려는 경우 [필드 그룹 만들기](./field-groups.md#create) 을 가리키도록 업데이트하는 것이 좋습니다.

An **[!UICONTROL 제목 없는 필드]** 자리 표시자가 캔버스에 표시되고 오른쪽 레일이 업데이트되어 필드의 속성을 구성하는 컨트롤을 표시합니다. 아래 **[!UICONTROL 할당 대상]**, 선택 **[!UICONTROL 클래스]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

다음 안내서를 참조하십시오. [ui에서 필드 정의](../fields/overview.md#define) 를 추가하여 클래스를 구성하고 클래스에 필드를 추가하는 방법에 대한 특정 단계를 설명합니다. 계속하여 클래스에 필요한 만큼 필드를 추가합니다. 완료되면 을 선택합니다 **[!UICONTROL 저장]** 스키마와 클래스를 모두 저장하려면

![](../../images/ui/resources/classes/save.png)

이 클래스를 사용하는 스키마를 이전에 만든 경우 새로 추가된 필드가 해당 스키마에 자동으로 나타납니다.

## 스키마 클래스 변경 {#schema}

스키마를 저장하기 전에 초기 생성 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다. 다음 안내서를 참조하십시오. [스키마 만들기 및 편집](./schemas.md#change-class) 추가 정보.

## 다음 단계

이 문서에서는 플랫폼 UI를 사용하여 클래스를 만들고 편집하는 방법에 대해 설명합니다. 의 기능에 대한 자세한 내용은 [!UICONTROL 스키마] 작업 영역, 자세한 내용은 [[!UICONTROL 스키마] 작업 공간 개요](../overview.md).

를 사용하여 클래스를 관리하는 방법을 알아보려면 [!DNL Schema Registry] API인 경우 [클래스 끝점 안내서](../../api/classes.md).
