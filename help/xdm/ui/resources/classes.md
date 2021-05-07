---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 영역;클래스;클래스;XDM;XDM system;experience data model;ui;workspace;class;classes
solution: Experience Platform
title: UI에서 클래스 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 클래스를 만들고 편집하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# UI에서 클래스 만들기 및 편집

XDM(Experience Data Model)에서 클래스는 스키마에 포함할 데이터의 행동 측면(레코드 또는 시간 시리즈)을 정의합니다. 이 외에도 클래스는 해당 클래스를 기반으로 하는 모든 스키마에는 호환이 가능한 여러 데이터 집합을 병합하는 방법을 포함하는 데 필요한 가장 작은 수의 공용 속성을 설명합니다.

Adobe은 [!DNL XDM Individual Profile] 및 [!DNL XDM ExperienceEvent]을 비롯한 여러 표준(&quot;core&quot;) XDM 클래스를 제공합니다. 이러한 핵심 클래스 외에도 사용자 지정 클래스를 만들어 조직에 대한 보다 구체적인 사용 사례를 설명할 수도 있습니다.

이 문서에서는 Adobe Experience Platform UI에서 사용자 정의 클래스를 만들고, 편집하고, 관리하는 방법에 대한 개요를 제공합니다.

## 전제 조건

이 가이드를 사용하려면 XDM 시스템에 대한 작업 이해가 필요합니다. Experience Platform 에코시스템 내의 XDM 역할에 대한 소개는 [XDM 개요](../../home.md), 스키마 구성](../../schema/composition.md)의 기본 사항에 대해 참조하여 클래스가 XDM 스키마에 기여하는 방법을 알아보십시오.[

이 안내서는 필요하지 않지만 [!DNL Schema Editor]의 다양한 기능에 익숙해지려면 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성의 자습서를 따르는 것이 좋습니다.

## 새 클래스 {#create} 만들기

**[!UICONTROL Schemas]** 작업 영역에서 **[!UICONTROL Create schema]**&#x200B;을 선택한 다음 드롭다운에서 **[!UICONTROL Browse]**&#x200B;를 선택합니다.

![](../../images/ui/resources/classes/browse-classes.png)

사용 가능한 클래스 목록에서 선택할 수 있는 대화 상자가 나타납니다. 대화 상자의 맨 위에서 **[!UICONTROL Create new class]**&#x200B;을 선택합니다. 그런 다음 새 클래스에 대해 표시 이름(클래스에 대해 짧고 설명적이며 고유하며 사용자 친화적인 이름), 설명 및 스키마가 정의하는 데이터의 비헤이비어를 제공할 수 있습니다(&quot;[!UICONTROL Record]&quot; 또는 &quot;[!UICONTROL Time-series]&quot;).

완료되면 **[!UICONTROL Assign class]**&#x200B;을 선택합니다.

![](../../images/ui/resources/classes/class-details.png)

방금 만든 사용자 지정 클래스를 기반으로 하는 새 스키마를 캔버스에 표시하는 [!DNL Schema Editor]이 나타납니다. 아직 클래스에 추가된 필드가 없으므로 스키마에는 [!DNL Schema Registry]의 모든 리소스에 자동으로 적용되는 시스템 생성 고유 식별자를 나타내는 `_id` 필드만 포함됩니다.

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>조직에서 정의한 클래스를 구현하는 스키마를 빌드할 때는 스키마 필드 그룹을 호환 가능한 클래스에서만 사용할 수 있습니다. 정의한 클래스는 새로 만들어지므로 **[!UICONTROL Add field group]** 대화 상자에 호환되는 필드 그룹이 없습니다. 대신 [새 필드 그룹](./field-groups.md#create)을 만들어야 해당 클래스에서 사용할 수 있습니다. 다음에 새 클래스를 구현하는 스키마를 작성할 때 정의한 필드 그룹이 나열되고 사용할 수 있습니다.

이제 [클래스](#add-fields)에 필드 추가를 시작할 수 있습니다. 이 작업은 클래스를 사용하는 모든 스키마가 공유합니다.

## 기존 클래스 {#edit} 편집

>[!NOTE]
>
>조직에서 정의한 사용자 정의 클래스만 완전히 편집하고 사용자 정의할 수 있습니다. Adobe에 의해 정의된 핵심 클래스의 경우 개별 스키마 컨텍스트 내에서 해당 필드의 표시 이름만 편집할 수 있습니다. 자세한 내용은 [스키마 필드에 대한 표시 이름 편집](./schemas.md#display-names)의 섹션을 참조하십시오.
>
>사용자 지정 클래스가 저장되고 데이터 수집에 사용되면 이후 추가 변경만 수행할 수 있습니다. 자세한 내용은 스키마 진화의 [규칙](../../schema/composition.md#evolution)을 참조하십시오.

기존 클래스를 편집하려면 **[!UICONTROL Browse]** 탭을 선택한 다음 편집할 클래스를 사용하는 스키마의 이름을 선택합니다.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>작업 공간의 검색 및 필터링 기능을 사용하여 스키마를 쉽게 찾을 수 있습니다. 자세한 내용은 [XDM 리소스](../explore.md)에 대한 가이드를 참조하십시오.

[!DNL Schema Editor]이 캔버스에 표시된 스키마 구조와 함께 나타납니다. 이제 [클래스](#add-fields)에 필드 추가를 시작할 수 있습니다.

![](../../images/ui/resources/classes/edit.png)

## {#add-fields} 클래스에 필드 추가

[!UICONTROL Schema Editor]에 열려 있는 사용자 정의 클래스를 사용하는 스키마가 있으면 클래스에 필드 추가를 시작할 수 있습니다. 새 필드를 추가하려면 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택합니다.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>클래스에 추가하는 모든 필드는 해당 클래스를 사용하는 모든 스키마에서 사용됩니다. 따라서 모든 스키마 사용 사례에서 유용한 필드를 신중하게 고려해야 합니다. 이 클래스 아래의 일부 스키마에서만 사용할 수 있는 필드를 추가하려는 경우 대신 필드 그룹](./field-groups.md#create)을(를) 만들어 해당 스키마에 필드 추가를 고려할 수 있습니다.[

**[!UICONTROL New field]**&#x200B;이 캔버스에 표시되고 필드의 속성을 구성하기 위한 컨트롤을 표시하는 오른쪽 레일이 업데이트됩니다. 클래스를 구성하고 클래스에 필드를 추가하는 방법에 대한 특정 단계는 [UI](../fields/overview.md#define)에서 필드 정의 가이드를 참조하십시오.

클래스에 필요한 만큼 필드를 계속 추가합니다. 완료되면 **[!UICONTROL Save]**&#x200B;을 선택하여 스키마와 클래스를 모두 저장합니다.

![](../../images/ui/resources/classes/save.png)

이전에 이 클래스를 사용하는 스키마를 만든 경우 새로 추가한 필드가 해당 스키마에 자동으로 나타납니다.

## 스키마 {#schema} 클래스 변경

스키마 클래스가 저장되기 전에 초기 생성 프로세스 중에 언제든지 스키마의 클래스를 변경할 수 있습니다. 자세한 내용은 [스키마 만들기 및 편집](./schemas.md#change-class)의 안내서를 참조하십시오.

## 다음 단계

이 문서에서는 플랫폼 UI를 사용하여 클래스를 만들고 편집하는 방법에 대해 설명합니다. [!UICONTROL Schemas] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 클래스를 관리하는 방법에 대해 알아보려면 [클래스 끝점 안내서](../../api/classes.md)를 참조하십시오.
