---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 영역;스키마;스키마;
solution: Experience Platform
title: UI에서 스키마 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마를 만들고 편집하는 방법의 기본 사항에 대해 알아봅니다.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 3dffa9687f3429b970e8fceebd6864a5b61ead21
workflow-type: tm+mt
source-wordcount: '3203'
ht-degree: 0%

---

# UI에서 스키마 만들기 및 편집

이 안내서에서는 Adobe Experience Platform UI에서 조직에 대한 XDM(Experience Data Model) 스키마를 만들고, 편집하고, 관리하는 방법에 대한 개요를 제공합니다.

>[!IMPORTANT]
>
>XDM 스키마는 사용자 지정할 수 있으므로 스키마를 만드는 단계는 스키마에서 캡처하려는 데이터 유형에 따라 달라질 수 있습니다. 따라서 이 문서에서는 UI의 스키마로 수행할 수 있는 기본 상호 작용만 다루며, 클래스, 스키마 필드 그룹, 데이터 유형 및 필드 사용자 지정과 같은 관련 단계는 제외됩니다.
>
>스키마 생성 프로세스를 자세히 살펴보려면 [스키마 만들기 튜토리얼](../../tutorials/create-schema-ui.md) 전체 예제 스키마를 만들고 의 다양한 기능을 숙지하려면 [!DNL Schema Editor].

## 전제 조건

이 안내서에서는 XDM 시스템에 대한 작업 이해가 필요합니다. 다음을 참조하십시오. [XDM 개요](../../home.md) Experience Platform 생태계 내에서 XDM의 역할에 대한 소개 및 [스키마 컴포지션 기본 사항](../../schema/composition.md) 스키마 생성 방법에 대한 개요입니다.

## 새 스키마 만들기 {#create}

>[!NOTE]
>
>이 섹션에서는 UI에서 새 스키마를 수동으로 만드는 방법을 다룹니다. CSV 데이터를 플랫폼으로 수집하는 경우 다음을 선택할 수 있습니다. [해당 데이터를 AI가 생성한 권장 사항에 의해 생성된 XDM 스키마에 매핑합니다](../../../ingestion/tutorials/map-csv/recommendations.md) (현재 Beta 버전). 직접 스키마를 생성할 필요가 없습니다.

다음에서 [!UICONTROL 스키마] 작업 영역, 선택 **[!UICONTROL 스키마 만들기]** 오른쪽 상단 모서리입니다. 표시되는 드롭다운에서 다음 중 하나를 선택할 수 있습니다. **[!UICONTROL XDM 개별 프로필]** 및 **[!UICONTROL XDM ExperienceEvent]** 를 스키마의 기본 클래스로 사용합니다. 또는 다음을 선택할 수 있습니다 **[!UICONTROL 찾아보기]** 사용 가능한 클래스의 전체 목록에서 선택하려면 [새 사용자 정의 클래스 만들기](./classes.md#create) 대신,

![](../../images/ui/resources/schemas/create-schema.png)

클래스를 선택하면 [!DNL Schema Editor] 가 나타나고 스키마의 기본 구조(클래스에서 제공)가 캔버스에 표시됩니다. 여기에서 오른쪽 레일을 사용하여 을(를) 추가할 수 있습니다. **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]** 스키마.

![](../../images/ui/resources/schemas/schema-details.png)

이제 다음 작업을 수행하여 스키마 구조 작성을 시작할 수 있습니다 [스키마 필드 그룹 추가](#add-field-groups).

## 기존 스키마 편집 {#edit}

>[!NOTE]
>
>스키마가 저장되고 데이터 수집에 사용되면 추가 변경 사항만 수행할 수 있습니다. 다음을 참조하십시오. [스키마 진화 규칙](../../schema/composition.md#evolution) 추가 정보.

기존 스키마를 편집하려면 **[!UICONTROL 찾아보기]** 를 탭한 다음 편집할 스키마의 이름을 선택합니다.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>작업 영역의 검색 및 필터링 기능을 사용하여 스키마를 보다 쉽게 찾을 수 있습니다. 다음 안내서를 참조하십시오 [xdm 리소스 살펴보기](../explore.md) 추가 정보.

스키마를 선택하면 [!DNL Schema Editor] 캔버스에 스키마 구조가 표시된 상태로 나타납니다. 이제 다음을 수행할 수 있습니다. [필드 그룹 추가](#add-field-groups) 스키마로(또는 [개별 필드 추가](#add-individual-fields) (해당 그룹에서), [필드 표시 이름 편집](#display-names), 또는 [기존 사용자 정의 필드 그룹 편집](./field-groups.md#edit) 스키마에 가 사용된 경우

## 스키마에 필드 그룹 추가 {#add-field-groups}

>[!NOTE]
>
>이 섹션에서는 스키마에 기존 필드 그룹을 추가하는 방법을 다룹니다. 새 사용자 정의 필드 그룹을 만들려면 다음 안내서를 참조하십시오. [필드 그룹 만들기 및 편집](./field-groups.md#create) 대신,

내에서 스키마를 열면 [!DNL Schema Editor], 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 시작하려면 다음을 선택합니다. **[!UICONTROL 추가]** 다음에 **[!UICONTROL 필드 그룹]** 왼쪽 레일에서.

![](../../images/ui/resources/schemas/add-field-group-button.png)

스키마에 대해 선택할 수 있는 필드 그룹 목록을 표시하는 대화 상자가 나타납니다. 필드 그룹은 하나의 클래스와만 호환되므로 스키마의 선택한 클래스와 연결된 필드 그룹만 나열됩니다. 기본적으로 나열된 필드 그룹은 조직 내에서 사용 인기에 따라 정렬됩니다.

![](../../images/ui/resources/schemas/field-group-popularity.png)

추가할 필드의 일반 활동 또는 비즈니스 영역을 알고 있는 경우 왼쪽 레일에서 하나 이상의 수직 범주를 선택하여 표시된 필드 그룹 목록을 필터링합니다.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>XDM에서의 산업별 데이터 모델링을 위한 모범 사례에 대한 자세한 내용은 [업계 데이터 모델](../../schema/industries/overview.md).

검색 창을 사용하여 원하는 필드 그룹을 찾을 수도 있습니다. 쿼리와 이름이 일치하는 필드 그룹이 목록 맨 위에 나타납니다. 아래 **[!UICONTROL 표준 필드]**&#x200B;원하는 데이터 속성을 설명하는 필드가 포함된 필드 그룹이 표시됩니다.

![](../../images/ui/resources/schemas/field-group-search.png)

스키마에 추가하려는 필드 그룹의 이름 옆에 있는 확인란을 선택합니다. 목록에서 여러 필드 그룹을 선택할 수 있으며, 선택한 각 필드 그룹이 오른쪽 레일에 표시됩니다.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>나열된 필드 그룹의 경우 정보 아이콘( )에 마우스를 가져다 대거나 집중할 수 있습니다.![](../../images/ui/resources/schemas/info-icon.png)) 필드 그룹이 캡처하는 데이터 종류에 대한 간단한 설명을 볼 수 있습니다. 미리보기 아이콘( )을 선택할 수도 있습니다.![](../../images/ui/resources/schemas/preview-icon.png))를 클릭하여 스키마에 필드 그룹을 추가하기로 결정하기 전에 필드 그룹이 제공하는 필드 구조를 확인합니다.

필드 그룹을 선택한 후 다음을 선택합니다. **[!UICONTROL 필드 그룹 추가]** 를 클릭하여 스키마에 추가합니다.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

다음 [!DNL Schema Editor] 필드 그룹이 제공한 필드가 캔버스에 표시된 상태로 다시 나타납니다.

![](../../images/ui/resources/schemas/field-groups-added.png)

스키마에 필드 그룹을 추가한 후 선택적으로 다음을 수행할 수 있습니다. [기존 필드 제거](#remove-fields) 또는 [새 사용자 정의 필드 추가](#add-fields) 필요에 따라 이러한 그룹에 연결합니다.

### 필드 그룹에서 추가된 필드 제거 {#remove-fields}

스키마에 필드 그룹을 추가한 후에는 필요하지 않은 모든 필드를 제거할 수 있습니다.

>[!NOTE]
>
>필드 그룹에서 필드를 제거하면 작업 중인 스키마에만 영향을 주고 필드 그룹 자체에는 영향을 주지 않습니다. 한 스키마에서 필드를 제거하면 동일한 필드 그룹을 사용하는 다른 모든 스키마에서 해당 필드를 계속 사용할 수 있습니다.

다음 예에서는 표준 필드 그룹입니다 **[!UICONTROL 인구 통계 세부 정보]** 이(가) 스키마에 추가되었습니다. 과 같은 단일 필드를 제거하려면 `taxId`을 클릭하고 캔버스에서 필드를 선택한 다음 를 선택합니다. **[!UICONTROL 제거]** 오른쪽 레일에서.

![단일 필드 제거](../../images/ui/resources/schemas/remove-single-field.png)

제거할 필드가 여러 개인 경우 필드 그룹을 전체적으로 관리할 수 있습니다. 캔버스에서 그룹에 속하는 필드를 선택한 다음 를 선택합니다. **[!UICONTROL 관련 필드 관리]** 오른쪽 레일에서.

![관련 필드 관리](../../images/ui/resources/schemas/manage-related-fields.png)

해당 필드 그룹의 구조를 보여 주는 대화 상자가 나타납니다. 여기에서 제공된 확인란을 사용하여 필요한 필드를 선택하거나 선택 취소할 수 있습니다. 만족스러우면 다음을 선택합니다. **[!UICONTROL 확인]**.

![필드 그룹에서 필드 선택](../../images/ui/resources/schemas/select-fields.png)

스키마 구조에 선택한 필드만 있는 캔버스가 다시 나타납니다.

![필드 추가됨](../../images/ui/resources/schemas/fields-added.png)

### 필드 그룹에 사용자 정의 필드 추가 {#add-fields}

스키마에 필드 그룹을 추가한 후 해당 그룹에 대한 추가 필드를 정의할 수 있습니다. 그러나 한 스키마의 필드 그룹에 추가된 모든 필드는 해당 필드 그룹을 사용하는 다른 모든 스키마에도 표시됩니다.

또한 사용자 정의 필드를 표준 필드 그룹에 추가하면 해당 필드 그룹이 사용자 정의 필드 그룹으로 변환되고 원래 표준 필드 그룹은 더 이상 사용할 수 없습니다.

사용자 지정 필드를 표준 필드 그룹에 추가하려면 [아래 섹션](#custom-fields-for-standard-groups) 특정 지침. 사용자 정의 필드 그룹에 필드를 추가하는 경우 [사용자 정의 필드 그룹 편집](./field-groups.md) 필드 그룹 UI 안내서에서 확인할 수 있습니다.

기존 필드 그룹을 변경하지 않으려면 다음을 수행할 수 있습니다 [새 사용자 정의 필드 그룹 만들기](./field-groups.md#create) 추가 필드를 대신 정의합니다.

## 스키마에 개별 필드 추가 {#add-individual-fields}

특정 사용 사례에 대한 전체 필드 그룹을 추가하지 않으려면 스키마 편집기를 사용하여 개별 필드를 스키마에 직접 추가할 수 있습니다. 다음을 수행할 수 있습니다. [표준 필드 그룹의 개별 필드 추가](#add-standard-fields) 또는 [사용자 정의 필드 추가](#add-custom-fields) 대신,

>[!IMPORTANT]
>
>스키마 편집기에서 기능적으로 스키마에 직접 개별 필드를 추가할 수 있어도 XDM 스키마의 모든 필드는 해당 클래스 또는 해당 클래스와 호환되는 필드 그룹에서 제공해야 한다는 사실은 변경되지 않습니다. 아래 섹션에서 설명했듯이 모든 개별 필드는 스키마에 추가될 때 주요 단계로 클래스 또는 필드 그룹과 여전히 연결되어 있습니다.

### 표준 필드 추가 {#add-standard-fields}

해당 필드 그룹을 미리 알 필요 없이 표준 필드 그룹의 필드를 스키마에 직접 추가할 수 있습니다. 스키마에 표준 필드를 추가하려면 더하기(**+**) 아이콘은 캔버스에서 스키마 이름 옆에 있습니다. An **[!UICONTROL 제목 없는 필드]** 자리 표시자가 스키마 구조에 나타나고 오른쪽 레일이 업데이트되어 필드를 구성하는 컨트롤이 표시됩니다.

![필드 플레이스홀더](../../images/ui/resources/schemas/root-custom-field.png)

아래 **[!UICONTROL 필드 이름]**&#x200B;을(를) 추가하고 싶은 필드의 이름을 입력하십시오. 시스템은 쿼리와 일치하는 표준 필드를 자동으로 검색하여 아래에 나열합니다 **[!UICONTROL 권장 표준 필드]**, 해당 그룹이 속한 필드 그룹을 포함합니다.

![권장 표준 필드](../../images/ui/resources/schemas/standard-field-search.png)

일부 표준 필드는 동일한 이름을 공유하지만 구조는 출신 필드 그룹에 따라 달라질 수 있습니다. 표준 필드가 필드 그룹 구조의 상위 오브젝트 내에 중첩된 경우 하위 필드가 추가되면 상위 필드도 스키마에 포함됩니다.

미리보기 아이콘(![미리 보기 아이콘](../../images/ui/resources/schemas/preview-icon.png)) 표준 필드 옆에 있는 를 클릭하여 필드 그룹의 구조를 보고 중첩된 방법을 더 잘 이해할 수 있습니다. 스키마에 표준 필드를 추가하려면 더하기 아이콘(![더하기 아이콘](../../images/ui/resources/schemas/add-icon.png)).

![표준 필드 추가](../../images/ui/resources/schemas/add-standard-field.png)

캔버스는 필드 그룹 구조 내에 중첩된 상위 필드를 포함하여 스키마에 추가된 표준 필드를 표시하도록 업데이트됩니다. 필드 그룹의 이름은 **[!UICONTROL 필드 그룹]** 왼쪽 레일에서. 동일한 필드 그룹에서 필드를 더 추가하려면 **[!UICONTROL 관련 필드 관리]** 오른쪽 레일에서.

![표준 필드 추가됨](../../images/ui/resources/schemas/standard-field-added.png)

### 사용자 지정 필드 추가 {#add-custom-fields}

표준 필드의 워크플로우와 마찬가지로 사용자 정의 필드를 스키마에 직접 추가할 수도 있습니다.

스키마의 루트 수준에 필드를 추가하려면 더하기(**+**) 아이콘은 캔버스에서 스키마 이름 옆에 있습니다. An **[!UICONTROL 제목 없는 필드]** 자리 표시자가 스키마 구조에 나타나고 오른쪽 레일이 업데이트되어 필드를 구성하는 컨트롤이 표시됩니다.

![루트 사용자 정의 필드](../../images/ui/resources/schemas/root-custom-field.png)

추가하려는 필드 이름을 입력하면 일치하는 표준 필드 검색이 자동으로 시작됩니다. 대신 새 사용자 정의 필드를 만들려면 아래에 첨부된 맨 위 옵션을 선택합니다. **([!UICONTROL 새 필드])**.

![새 필드](../../images/ui/resources/schemas/custom-field-search.png)

필드에 대한 표시 이름 및 데이터 유형을 제공한 후 다음 단계는 상위 XDM 리소스에 필드를 할당하는 것입니다. 스키마에서 사용자 정의 클래스를 사용하는 경우 다음을 선택할 수 있습니다. [지정된 클래스에 필드 추가](#add-to-class) 또는 [필드 그룹](#add-to-field-group) 대신, 그러나 스키마에서 표준 클래스를 사용하는 경우 사용자 지정 필드만 필드 그룹에 할당할 수 있습니다.

#### 필드를 사용자 정의 필드 그룹에 할당 {#add-to-field-group}

>[!NOTE]
>
>이 섹션에서는 사용자 정의 필드 그룹에 필드를 할당하는 방법만 다룹니다. 대신 새 사용자 정의 필드로 표준 필드 그룹을 확장하려면 의 섹션을 참조하십시오. [표준 필드 그룹에 사용자 정의 필드 추가](#custom-fields-for-standard-groups).

아래 **[!UICONTROL 할당 대상]**, 선택 **[!UICONTROL 필드 그룹]**. 스키마에서 표준 클래스를 사용하는 경우 이 옵션만 사용할 수 있으며 기본적으로 이 옵션이 선택되어 있습니다.

그런 다음 연결할 새 필드에 대한 필드 그룹을 선택해야 합니다. 제공된 텍스트 입력 시 필드 그룹의 이름을 입력하십시오. 입력과 일치하는 기존 사용자 정의 필드 그룹이 있는 경우 드롭다운 목록에 표시됩니다. 또는 고유한 이름을 입력하여 대신 새 필드 그룹을 만들 수 있습니다.

![필드 그룹 선택](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>기존 사용자 정의 필드 그룹을 선택하는 경우 변경 사항을 저장한 후 해당 필드 그룹을 사용하는 다른 스키마도 새로 추가된 필드를 상속합니다. 이러한 이유로 이 전달 유형을 원하는 경우에만 기존 필드 그룹을 선택합니다. 그렇지 않으면 대신 새 사용자 정의 필드 그룹을 만들도록 선택해야 합니다.

목록에서 필드 그룹을 선택한 후 다음을 선택합니다. **[!UICONTROL 적용]**.

![필드 적용](../../images/ui/resources/schemas/apply-field.png)

새 필드가 캔버스에 추가되고 아래에 이름 간격이 지정됩니다. [임차인 ID](../../api/getting-started.md#know-your-tenant_id) 표준 XDM 필드와의 충돌을 방지합니다. 새 필드를 연결한 필드 그룹도 아래에 나타납니다. **[!UICONTROL 필드 그룹]** 왼쪽 레일에서.

![임차인 ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>선택한 사용자 정의 필드 그룹에서 제공하는 나머지 필드는 기본적으로 스키마에서 제거됩니다. 이러한 필드 중 일부를 스키마에 추가하려면 그룹에 속한 필드를 선택한 다음 를 선택합니다 **[!UICONTROL 관련 필드 관리]** 오른쪽 레일에서.

#### 필드를 사용자 정의 클래스에 할당 {#add-to-class}

아래 **[!UICONTROL 할당 대상]**, 선택 **[!UICONTROL 클래스]**. 아래의 입력 필드가 현재 스키마의 사용자 지정 클래스 이름으로 바뀌어 새 필드가 이 클래스에 할당됨을 나타냅니다.

![다음 [!UICONTROL 클래스] 새 필드 할당을 위해 선택 중인 옵션입니다.](../../images/ui/resources/schemas/assign-field-to-class.png)

원하는 대로 필드 구성을 계속하고 을(를) 선택합니다 **[!UICONTROL 적용]** 완료 시.

![[!UICONTROL 적용] 새 필드에 대해 선택 중입니다.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

새 필드가 캔버스에 추가되고 아래에 이름 간격이 지정됩니다. [임차인 ID](../../api/getting-started.md#know-your-tenant_id) 표준 XDM 필드와의 충돌을 방지합니다. 왼쪽 레일에서 클래스 이름을 선택하면 새 필드가 클래스 구조의 일부로 표시됩니다.

![캔버스에 표시된 사용자 정의 클래스의 구조에 적용되는 새 필드입니다.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### 표준 필드 그룹 구조에 사용자 정의 필드 추가 {#custom-fields-for-standard-groups}

작업 중인 스키마에 표준 필드 그룹에서 제공하는 개체 유형 필드가 있는 경우 해당 표준 개체에 사용자 지정 필드를 추가할 수 있습니다.

>[!WARNING]
>
>한 스키마의 필드 그룹에 추가된 모든 필드는 해당 필드 그룹을 사용하는 다른 모든 스키마에도 표시됩니다. 또한 사용자 정의 필드를 표준 필드 그룹에 추가하면 해당 필드 그룹이 사용자 정의 필드 그룹으로 변환되고 원래 표준 필드 그룹은 더 이상 사용할 수 없습니다.
>
>이 기능의 베타에 참여한 경우 이전에 맞춤화한 표준 필드 그룹을 알려주는 대화 상자가 표시됩니다. 다음을 선택하면 **[!UICONTROL 승인]**, 나열된 리소스는 사용자 지정 필드 그룹으로 변환됩니다.
>
>![표준 필드 그룹을 변환하는 확인 대화 상자](../../images/ui/resources/schemas/beta-extension-confirmation.png)

시작하려면 더하기(**+**) 아이콘은 표준 필드 그룹에서 제공한 개체의 루트 옆에 있습니다.

![표준 오브젝트에 필드 추가](../../images/ui/resources/schemas/add-field-to-standard-object.png)

표준 필드 그룹을 변환할지 여부를 확인하는 경고 메시지가 나타납니다. 선택 **[!UICONTROL 필드 그룹 만들기 계속]** 계속합니다.

![필드 그룹 전환 확인](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

캔버스는 새 필드에 대한 제목 없는 자리 표시자와 함께 다시 나타납니다. 표준 필드 그룹의 이름이 &quot;([!UICONTROL 확장됨])&quot;를 입력하여 원래 버전에서 수정되었음을 나타냅니다. 여기에서 오른쪽 레일의 컨트롤을 사용하여 필드의 속성을 정의합니다.

![표준 오브젝트에 추가된 필드](../../images/ui/resources/schemas/standard-field-group-converted.png)

변경 사항을 적용하면 표준 개체 내의 테넌트 ID 네임스페이스 아래에 새 필드가 표시됩니다. 이 중첩된 네임스페이스는 동일한 필드 그룹을 사용하는 다른 스키마의 변경 사항을 방지하기 위해 필드 그룹 자체 내에서 필드 이름 충돌을 방지합니다.

![표준 오브젝트에 추가된 필드](../../images/ui/resources/schemas/added-to-standard-object.png)

## 실시간 고객 프로필에 대한 스키마 활성화 {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="프로필에 대한 스키마 활성화"
>abstract="프로필에 대해 스키마를 활성화하면 이 스키마에서 만든 모든 데이터 세트가 실시간 고객 프로필에 참여하며, 이 프로필은 서로 다른 소스의 데이터를 병합하여 각 고객에 대한 전체 보기를 구성합니다. 스키마를 사용하여 데이터를 프로필에 수집하면 비활성화할 수 없습니다. 자세한 내용은 설명서를 참조하십시오."

[실시간 고객 프로필](../../../profile/home.md) 서로 다른 소스의 데이터를 병합하여 각 개별 고객에 대한 전체 보기를 구성합니다. 스키마에 의해 캡처된 데이터가에서 사용할 수 있도록 스키마를 활성화해야 합니다 [!DNL Profile].

>[!IMPORTANT]
>
>에 대한 스키마를 활성화하려면 [!DNL Profile]에 기본 id 필드가 정의되어 있어야 합니다. 다음 안내서를 참조하십시오 [id 필드 정의](../fields/identity.md) 추가 정보.

스키마를 활성화하려면 왼쪽 레일에서 스키마 이름을 선택하여 시작한 다음 **[!UICONTROL 프로필]** 오른쪽 레일에서 전환합니다.

![](../../images/ui/resources/schemas/profile-toggle.png)

스키마를 활성화하고 저장한 후에는 비활성화할 수 없다는 경고가 표시되는 팝오버가 나타납니다. 선택 **[!UICONTROL 사용]** 계속합니다.

![](../../images/ui/resources/schemas/profile-confirm.png)

캔버스가 다시 나타납니다. [!UICONTROL 프로필] 토글 활성화됨.

>[!IMPORTANT]
>
>스키마가 아직 저장되지 않았기 때문에 실시간 고객 프로필에 스키마가 참여하도록 하는 것이 변경되면 되돌릴 수 없습니다. 활성화된 스키마를 저장하면 더 이상 비활성화할 수 없습니다. 다음 항목 선택 **[!UICONTROL 프로필]** 스키마를 비활성화하려면 다시 전환하십시오.

프로세스를 완료하려면 **[!UICONTROL 저장]** 스키마를 저장합니다.

![](../../images/ui/resources/schemas/profile-enabled.png)

이제 실시간 고객 프로필에서 스키마를 사용할 수 있습니다. Platform이 이 스키마를 기반으로 데이터 세트에 데이터를 수집하면 해당 데이터가 통합 프로필 데이터에 통합됩니다.

## 스키마 필드의 표시 이름 편집 {#display-names}

클래스를 할당하고 스키마에 필드 그룹을 추가하면 표준 또는 사용자 지정 XDM 리소스에서 해당 필드를 제공했는지 여부에 관계없이 스키마 필드의 표시 이름을 편집할 수 있습니다.

>[!NOTE]
>
>표준 클래스 또는 필드 그룹에 속하는 필드의 표시 이름은 특정 스키마의 컨텍스트에서만 편집할 수 있습니다. 즉, 한 스키마에서 표준 필드의 표시 이름을 변경해도 동일한 연관된 클래스 또는 필드 그룹을 사용하는 다른 스키마에는 영향을 주지 않습니다.
>
>스키마의 필드에 대한 표시 이름을 변경하면 이러한 변경 사항은 해당 스키마를 기반으로 하는 기존 데이터 세트에 즉시 반영됩니다.

스키마 필드의 표시 이름을 편집하려면 캔버스에서 필드를 선택합니다. 오른쪽 레일에서 새 이름 입력 **[!UICONTROL 표시 이름]**.

![](../../images/ui/resources/schemas/display-name.png)

선택 **[!UICONTROL 적용]** 오른쪽 레일에서 캔버스가 업데이트되어 필드의 새 표시 이름이 표시됩니다. 선택 **[!UICONTROL 저장]** 를 클릭하여 스키마에 변경 사항을 적용합니다.

![](../../images/ui/resources/schemas/display-name-changed.png)

## 스키마 클래스 변경 {#change-class}

스키마가 저장되기 전에 초기 작성 프로세스 동안 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재할당은 매우 신중하게 수행해야 합니다. 필드 그룹은 특정 클래스와만 호환되므로 클래스를 변경하면 캔버스와 추가한 모든 필드가 재설정됩니다.

클래스를 재할당하려면 **[!UICONTROL 할당]** (캔버스 왼쪽)

![](../../images/ui/resources/schemas/assign-class-button.png)

조직에서 정의한 클래스를 포함하여 사용 가능한 모든 클래스의 목록을 표시하는 대화 상자가 나타납니다(소유자: &quot;[!UICONTROL 고객]&quot;) Adobe에서 정의한 표준 클래스입니다.

목록에서 클래스를 선택하여 대화 상자의 오른쪽에 설명을 표시합니다. 다음을 선택할 수도 있습니다. **[!UICONTROL 클래스 구조 미리 보기]** 클래스와 연결된 필드 및 메타데이터를 봅니다. 선택 **[!UICONTROL 클래스 할당]** 계속합니다.

![](../../images/ui/resources/schemas/assign-class.png)

새 클래스를 지정할지 확인하는 대화 상자가 열립니다. 선택 **[!UICONTROL 할당]** 확인할 수 있습니다.

![](../../images/ui/resources/schemas/assign-confirm.png)

수업 변경을 확인한 후 캔버스가 재설정되고 모든 작곡 진행이 손실됩니다.

## 다음 단계

이 문서에서는 Platform UI에서 스키마를 만들고 편집하는 기본 사항에 대해 설명합니다. 다음을 검토하는 것이 좋습니다. [스키마 만들기 튜토리얼](../../tutorials/create-schema-ui.md) 고유한 사용 사례에 대한 사용자 지정 필드 그룹 및 데이터 유형 만들기를 포함하여 UI에서 전체 스키마를 구축하기 위한 포괄적인 워크플로를 제공합니다.

의 기능에 대한 자세한 내용 [!UICONTROL 스키마] 작업 영역에서 다음을 참조하십시오 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md).

에서 스키마를 관리하는 방법을 알아보려면 [!DNL Schema Registry] API에서 다음을 참조하십시오. [스키마 엔드포인트 안내서](../../api/schemas.md).
