---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;스키마;스키마
solution: Experience Platform
title: UI에서 스키마 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마를 만들고 편집하는 방법에 대한 기본 사항을 배웁니다.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# UI에서 스키마 만들기 및 편집

이 안내서에서는 Adobe Experience Platform UI에서 조직에 대한 XDM(Experience Data Model) 스키마를 생성, 편집 및 관리하는 방법에 대한 개요를 제공합니다.

>[!IMPORTANT]
>
>XDM 스키마는 사용자 지정할 수 있으므로 스키마를 만드는 단계는 스키마를 캡처하려는 데이터 종류에 따라 다를 수 있습니다. 따라서 이 문서에서는 UI의 스키마로 수행할 수 있는 기본 상호 작용만 다룹니다. 또한 클래스 사용자 지정, 스키마 필드 그룹, 데이터 유형 및 필드와 같은 관련 단계는 제외합니다.
>
>스키마 만들기 프로세스를 자세히 살펴보려면 다음을 수행하십시오. [스키마 만들기 자습서](../../tutorials/create-schema-ui.md) 전체 예제 스키마를 만들고 의 여러 기능에 숙지하십시오 [!DNL Schema Editor].

## 전제 조건

이 안내서에서는 XDM 시스템을 작업해야 합니다. 자세한 내용은 [XDM 개요](../../home.md) Experience Platform 에코시스템 내에서 XDM의 역할을 소개합니다. [스키마 구성 기본 사항](../../schema/composition.md) 스키마 구성 방법에 대한 개요입니다.

## 새 스키마 만들기 {#create}

에서 [!UICONTROL 스키마] 작업 영역, 선택 **[!UICONTROL 스키마 만들기]** 오른쪽 상단 모서리에서 표시되는 드롭다운에서 다음 중 하나를 선택할 수 있습니다 **[!UICONTROL XDM 개별 프로필]** 및 **[!UICONTROL XDM ExperienceEvent]** 를 스키마의 기본 클래스로 사용합니다. 또는 다음을 선택할 수 있습니다 **[!UICONTROL 찾아보기]** 사용 가능한 클래스의 전체 목록에서 선택하거나 [새 사용자 지정 클래스 만들기](./classes.md#create) 을 가리키도록 업데이트하는 것이 좋습니다.

![](../../images/ui/resources/schemas/create-schema.png)

클래스를 선택하면 [!DNL Schema Editor] 가 나타나고 스키마의 기본 구조(클래스에서 제공)가 캔버스에 표시됩니다. 여기에서 오른쪽 레일을 사용하여 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]** 스키마.

![](../../images/ui/resources/schemas/schema-details.png)

이제 다음을 통해 스키마 구조 작성을 시작할 수 있습니다 [스키마 필드 그룹 추가](#add-field-groups).

## 기존 스키마 편집 {#edit}

>[!NOTE]
>
>스키마를 저장하고 데이터 처리에 사용하면 추가 변경만 수행할 수 있습니다. 자세한 내용은 [스키마 진화 규칙](../../schema/composition.md#evolution) 추가 정보.

기존 스키마를 편집하려면 **[!UICONTROL 찾아보기]** 탭을 클릭한 다음 편집할 스키마의 이름을 선택합니다.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>작업 공간의 검색 및 필터링 기능을 사용하여 스키마를 보다 쉽게 찾을 수 있습니다. 다음 안내서를 참조하십시오. [xdm 리소스 탐색](../explore.md) 추가 정보.

스키마를 선택하면 [!DNL Schema Editor] 캔버스에 표시된 스키마 구조와 함께 나타납니다. 이제 다음을 수행할 수 있습니다 [필드 그룹 추가](#add-field-groups) 스키마로, [필드 표시 이름 편집](#display-names), 또는 [기존 사용자 지정 필드 그룹 편집](./field-groups.md#edit) 스키마에서 적용되는 경우.

## 스키마에 필드 그룹 추가 {#add-field-groups}

>[!NOTE]
>
>이 섹션에서는 스키마에 기존 필드 그룹을 추가하는 방법을 설명합니다. 새 사용자 지정 필드 그룹을 만들려면 다음에 대한 안내서를 참조하십시오 [필드 그룹 만들기 및 편집](./field-groups.md#create) 을 가리키도록 업데이트하는 것이 좋습니다.

스키마 내에서 를 연 후 [!DNL Schema Editor]를 채울 때는 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 시작하려면 다음을 선택합니다 **[!UICONTROL 추가]** 다음으로 이동 **[!UICONTROL 필드 그룹]** 왼쪽 레일에 있습니다.

![](../../images/ui/resources/schemas/add-field-group-button.png)

스키마에 대해 선택할 수 있는 필드 그룹 목록이 표시되는 대화 상자가 나타납니다. 필드 그룹은 한 클래스와만 호환되므로 스키마의 선택한 클래스와 연결된 필드 그룹만 나열됩니다. 기본적으로 나열된 필드 그룹은 조직 내의 사용 인기도에 따라 정렬됩니다.

![](../../images/ui/resources/schemas/field-group-popularity.png)

추가할 필드의 일반 활동 또는 비즈니스 영역을 알고 있는 경우 왼쪽 레일에서 업계 카테고리 중 하나 이상을 선택하여 표시된 필드 그룹 목록을 필터링합니다.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>XDM에서 업계 특정 데이터 모델링을 위한 우수 사례에 대한 자세한 내용은 [업계 데이터 모델](../../schema/industries/overview.md).

검색 막대를 사용하여 원하는 필드 그룹을 찾을 수도 있습니다. 쿼리 이름과 일치하는 필드 그룹이 목록 맨 위에 나타납니다. 아래 **[!UICONTROL 표준 필드]**, 원하는 데이터 속성을 설명하는 필드가 포함된 필드 그룹이 표시됩니다.

![](../../images/ui/resources/schemas/field-group-search.png)

스키마에 추가할 필드 그룹 이름 옆에 있는 확인란을 선택합니다. 목록에서 여러 필드 그룹을 선택할 수 있습니다. 선택한 각 필드 그룹이 오른쪽 레일에 표시됩니다.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>나열된 필드 그룹의 경우 정보 아이콘(![](../../images/ui/resources/schemas/info-icon.png))을 클릭하여 필드 그룹이 캡처하는 데이터 종류에 대한 간단한 설명을 볼 수 있습니다. 미리 보기 아이콘(![](../../images/ui/resources/schemas/preview-icon.png)) 를 클릭하여 스키마에 추가하기 전에 필드 그룹이 제공하는 필드의 구조를 확인합니다.

필드 그룹을 선택하면 **[!UICONTROL 필드 그룹 추가]** 를 추가하여 스키마에 추가합니다.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

다음 [!DNL Schema Editor] 캔버스에 표시된 필드 그룹 제공 필드와 함께 다시 나타납니다.

![](../../images/ui/resources/schemas/field-groups-added.png)

## 실시간 고객 프로필에 대한 스키마 활성화 {#profile}

[실시간 고객 프로필](../../../profile/home.md) 서로 다른 소스의 데이터를 병합하여 각 개별 고객에 대한 전체 보기를 구성합니다. 스키마로 캡처된 데이터를 이 프로세스에 참여하도록 하려면 에서 사용할 스키마를 활성화해야 합니다 [!DNL Profile].

>[!IMPORTANT]
>
>스키마를 활성화하기 위한 [!DNL Profile]에는 기본 id 필드가 정의되어 있어야 합니다. 다음 안내서를 참조하십시오. [id 필드 정의](../fields/identity.md) 추가 정보.

스키마를 활성화하려면 왼쪽 레일에서 스키마 이름을 선택한 다음, **[!UICONTROL 프로필]** 오른쪽 레일에서 전환합니다.

![](../../images/ui/resources/schemas/profile-toggle.png)

스키마가 활성화되고 저장되면 비활성화할 수 없다는 팝업 창이 나타납니다. 선택 **[!UICONTROL 활성화]** 계속하십시오.

![](../../images/ui/resources/schemas/profile-confirm.png)

캔버스가 [!UICONTROL 프로필] 활성화됨 토글.

>[!IMPORTANT]
>
>스키마가 아직 저장되지 않았으므로 스키마가 실시간 고객 프로필에 참여할 수 있도록 하는 방법을 변경할 경우 반환되지 않는 중요한 지점입니다. 활성화된 스키마를 저장하면 더 이상 비활성화할 수 없습니다. 을(를) 선택합니다 **[!UICONTROL 프로필]** 스키마를 비활성화하려면 다시 전환합니다.

프로세스를 완료하려면 **[!UICONTROL 저장]** 스키마를 저장하려면 을 클릭합니다.

![](../../images/ui/resources/schemas/profile-enabled.png)

이제 실시간 고객 프로필에서 사용할 수 있도록 스키마가 활성화됩니다. Platform이 이 스키마를 기반으로 하여 데이터 세트에 데이터를 수집하면 해당 데이터가 병합된 프로필 데이터에 통합됩니다.

## 스키마 필드의 표시 이름 편집 {#display-names}

클래스를 지정하고 필드 그룹을 스키마에 추가하면 해당 필드가 표준 또는 사용자 지정 XDM 리소스에서 제공되었는지 여부에 관계없이 스키마 필드의 표시 이름을 편집할 수 있습니다.

>[!NOTE]
>
>표준 클래스나 필드 그룹에 속하는 필드의 표시 이름은 특정 스키마 컨텍스트에서만 편집할 수 있습니다. 즉, 하나의 스키마에서 표준 필드의 표시 이름을 변경해도 동일한 연관된 클래스 또는 필드 그룹을 사용하는 다른 스키마에는 영향을 주지 않습니다.
>
>스키마 필드에 대한 표시 이름을 변경하면 해당 변경 사항이 해당 스키마를 기반으로 하는 기존 데이터 세트에 즉시 반영됩니다.

스키마 필드의 표시 이름을 편집하려면 캔버스에서 필드를 선택합니다. 오른쪽 레일에서 아래에 새 이름을 입력합니다 **[!UICONTROL 표시 이름]**.

![](../../images/ui/resources/schemas/display-name.png)

선택 **[!UICONTROL 적용]** 오른쪽 레일에서 캔버스가 업데이트되어 필드의 새 표시 이름이 표시됩니다. 선택 **[!UICONTROL 저장]** 스키마에 변경 사항을 적용하려면

![](../../images/ui/resources/schemas/display-name-changed.png)

## 스키마 클래스 변경 {#change-class}

스키마를 저장하기 전에 초기 구성 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재지정은 매우 신중하게 수행해야 합니다. 필드 그룹은 특정 클래스와 호환되기 때문에 클래스를 변경하면 캔버스 및 추가한 필드가 재설정됩니다.

클래스를 재할당하려면 **[!UICONTROL 지정]** 캔버스 왼쪽.

![](../../images/ui/resources/schemas/assign-class-button.png)

조직에서 정의한 클래스(소유자가 &quot;[!UICONTROL 고객]&quot;)도 포함되어 있습니다.

목록에서 클래스를 선택하여 대화 상자의 오른쪽에 해당 설명을 표시합니다. 선택할 수도 있습니다 **[!UICONTROL 미리 보기 클래스 구조]** 를 클릭하여 클래스와 연결된 필드 및 메타데이터를 확인합니다. 선택 **[!UICONTROL 클래스 할당]** 계속하십시오.

![](../../images/ui/resources/schemas/assign-class.png)

새 클래스를 할당할지 확인하는 새 대화 상자가 열립니다. 선택 **[!UICONTROL 지정]** 확인합니다.

![](../../images/ui/resources/schemas/assign-confirm.png)

클래스 변경을 확인한 후 캔버스가 재설정되고 모든 구성 진행 상태가 손실됩니다.

## 다음 단계

이 문서에서는 Platform UI에서 스키마를 만들고 편집하는 기본 사항을 다룹니다. 를 검토하는 것이 좋습니다 [스키마 만들기 자습서](../../tutorials/create-schema-ui.md) 고유한 사용 사례를 위한 사용자 지정 필드 그룹 및 데이터 유형 만들기를 포함하여, UI에서 전체 스키마를 생성하기 위한 포괄적인 워크플로우입니다.

의 기능에 대한 자세한 내용은 [!UICONTROL 스키마] 작업 영역, 자세한 내용은 [[!UICONTROL 스키마] 작업 공간 개요](../overview.md).

에서 스키마를 관리하는 방법을 알아보려면 [!DNL Schema Registry] API인 경우 [스키마 끝점 안내서](../../api/schemas.md).
