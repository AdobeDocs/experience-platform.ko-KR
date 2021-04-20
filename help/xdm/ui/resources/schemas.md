---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;스키마;스키마;;home;popular topics;api;XDM system;experience data model;ui;workspace;schema;schemas
solution: Experience Platform
title: UI에서 스키마 만들기 및 편집
description: Experience Platform 사용자 인터페이스에서 스키마를 만들고 편집하는 방법에 대한 기본 사항을 알아봅니다.
topic: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
translation-type: tm+mt
source-git-commit: 90a0c4e8d47d9bce38c9e13272e4f41f78f46e35
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# UI에서 스키마 만들기 및 편집

이 안내서에서는 Adobe Experience Platform UI에서 조직에 대한 XDM(Experience Data Model) 스키마를 생성, 편집 및 관리하는 방법에 대한 개요를 제공합니다.

>[!IMPORTANT]
>
>XDM 스키마는 매우 사용자 정의할 수 있으므로 스키마를 생성하는 데 필요한 단계는 스키마를 캡처할 데이터 유형에 따라 달라질 수 있습니다. 따라서 이 문서에서는 UI의 스키마로 만들 수 있는 기본 상호 작용만 다룹니다. 클래스 사용자 정의, 혼합, 데이터 유형 및 필드 사용자 지정과 같은 관련 단계는 제외됩니다.
>
>스키마 만들기 프로세스를 자세히 살펴보려면 [스키마 만들기 자습서](../../tutorials/create-schema-ui.md)와 함께 다음 작업을 수행하여 전체 예제 스키마를 만들고 [!DNL Schema Editor]의 많은 기능에 익숙해지십시오.

## 전제 조건

이 가이드를 사용하려면 XDM 시스템에 대한 작업 이해가 필요합니다. Experience Platform 에코시스템 내의 XDM 역할에 대한 소개는 [XDM 개요](../../home.md), 스키마 구성 방법에 대한 개요는 [스키마 구성 기본 사항](../../schema/composition.md)을 참조하십시오.

## 새 스키마 만들기 {#create}

[!UICONTROL Schemas] 작업 영역의 오른쪽 위 모서리에서 **[!UICONTROL Create schema]**&#x200B;을 선택합니다. 나타나는 드롭다운에서 **[!UICONTROL XDM Individual Profile]**&#x200B;과 **[!UICONTROL XDM ExperienceEvent]** 중 하나를 스키마의 기본 클래스로 선택할 수 있습니다. 또는 **[!UICONTROL Browse]**&#x200B;을 선택하여 사용 가능한 클래스의 전체 목록에서 선택하거나, [새 사용자 지정 클래스](./classes.md#create)를 대신 만들 수 있습니다.

![](../../images/ui/resources/schemas/create-schema.png)

클래스를 선택하면 [!DNL Schema Editor]이 표시되고 스키마의 기본 구조(클래스에서 제공)가 캔버스에 표시됩니다. 여기서 오른쪽 레일을 사용하여 스키마에 대해 **[!UICONTROL Display name]** 및 **[!UICONTROL Description]**&#x200B;을 추가할 수 있습니다.

![](../../images/ui/resources/schemas/schema-details.png)

이제 [mixins](#add-mixins)을(를) 추가하여 스키마 구조 작성을 시작할 수 있습니다.

## 기존 스키마 {#edit} 편집

>[!NOTE]
>
>스키마를 저장 및 데이터 수집에 사용하면 추가 변경 사항만 변경할 수 있습니다. 자세한 내용은 스키마 진화의 [규칙](../../schema/composition.md#evolution)을 참조하십시오.

기존 스키마를 편집하려면 **[!UICONTROL Browse]** 탭을 선택한 다음 편집할 스키마의 이름을 선택합니다.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>작업 공간의 검색 및 필터링 기능을 사용하여 스키마를 쉽게 찾을 수 있습니다. 자세한 내용은 [XDM 리소스](../explore.md)에 대한 가이드를 참조하십시오.

스키마를 선택하면 [!DNL Schema Editor]이 캔버스에 표시된 스키마 구조와 함께 나타납니다. 이제 [스키마에 믹싱](#add-mixins)을 추가하거나, [필드 표시 이름](#display-names) 또는 [이(가) 있는 경우 기존 사용자 정의 믹싱](./mixins.md#edit)을 편집할 수 있습니다.

## 스키마 {#add-mixins}에 믹싱 추가

>[!NOTE]
>
>이 섹션에서는 기존 혼합을 스키마에 추가하는 방법에 대해 설명합니다. 새 사용자 정의 믹싱을 만들려면 대신 [믹싱 만들기 및 편집](./mixins.md#create)의 안내서를 참조하십시오.

[!DNL Schema Editor] 내에서 스키마를 열면 믹스를 사용하여 스키마에 필드를 추가할 수 있습니다. 시작하려면 왼쪽 레일에서 **[!UICONTROL Mixins]** 옆에 있는 **[!UICONTROL Add]**&#x200B;을 선택합니다.

![](../../images/ui/resources/schemas/add-mixin-button.png)

스키마에 대해 선택할 수 있는 혼합 목록이 표시된 대화 상자가 나타납니다. 믹스는 하나의 클래스와 호환되므로 스키마의 선택된 클래스와 연결된 믹스만 나열됩니다. 기본적으로 나열된 믹스는 조직 내의 사용 인기도에 따라 정렬됩니다.

![](../../images/ui/resources/schemas/mixin-popularity.png)

추가할 혼합 필드의 일반 활동 또는 업무 영역을 알고 있는 경우 왼쪽 레일에서 하나 이상의 업계 수직 카테고리를 선택하여 표시된 혼합 목록을 필터링합니다.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>XDM에서 업계별 데이터 모델링에 대한 우수 사례에 대한 자세한 내용은 [업계 데이터 모델](../../schema/industries/overview.md)에 대한 설명서를 참조하십시오.

검색 막대를 사용하여 원하는 믹싱을 찾을 수도 있습니다. 쿼리와 일치하는 이름을 가진 믹스가 목록 맨 위에 표시됩니다. **[!UICONTROL Standard Fields]** 아래에서 원하는 데이터 속성을 설명하는 필드가 포함된 혼합이 표시됩니다.

![](../../images/ui/resources/schemas/mixin-search.png)

스키마에 추가할 믹스의 이름 옆에 있는 확인란을 선택합니다. 목록에서 여러 믹스를 선택할 수 있으며 선택한 각 믹스가 오른쪽 레일에 표시됩니다.

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>나열된 믹싱의 경우 정보 아이콘(![](../../images/ui/resources/schemas/info-icon.png))을 마우스로 가리키거나 초점을 조정하여 믹싱이 캡처하는 데이터의 유형에 대한 간단한 설명을 볼 수 있습니다. 미리 보기 아이콘(![](../../images/ui/resources/schemas/preview-icon.png))을 선택하여 스키마에 추가하기 전에 믹싱에서 제공하는 필드의 구조를 볼 수도 있습니다.

믹스를 선택하고 나면 **[!UICONTROL Add mixin]**&#x200B;을 선택하여 스키마에 추가합니다.

![](../../images/ui/resources/schemas/add-mixin-finish.png)

[!DNL Schema Editor]이(가) 캔버스에 표시된 혼합 제공 필드와 함께 다시 나타납니다.

![](../../images/ui/resources/schemas/mixins-added.png)

## 실시간 고객 프로필에 대한 스키마 활성화 {#profile}

[실시간 고객 프로파일에서는 ](../../../profile/home.md) 서로 다른 소스의 데이터를 수집하여 각 개별 고객에 대한 전체 뷰를 생성합니다. 스키마에서 캡처한 데이터가 이 프로세스에 참여하도록 하려면 [!DNL Profile]에서 사용할 스키마를 활성화해야 합니다.

>[!IMPORTANT]
>
>[!DNL Profile]에 대한 스키마를 활성화하려면 기본 ID 필드를 정의해야 합니다. 자세한 내용은 [ID 필드 정의](../fields/identity.md)의 안내서를 참조하십시오.

스키마를 활성화하려면 왼쪽 레일에서 스키마 이름을 선택하고 오른쪽 레일에서 **[!UICONTROL Profile]** 전환을 선택합니다.

![](../../images/ui/resources/schemas/profile-toggle.png)

스키마가 활성화되고 저장되면 비활성화할 수 없다는 내용의 팝업이 나타납니다. 계속하려면 **[!UICONTROL Enable]**&#x200B;을 선택합니다.

![](../../images/ui/resources/schemas/profile-confirm.png)

캔버스가 다시 나타나고 [!UICONTROL Profile] 토글이 활성화됩니다.

>[!IMPORTANT]
>
>스키마가 아직 저장되지 않았으므로 스키마를 실시간 고객 프로필에 참여하도록 하는 계획을 변경하는 경우 이는 반환되지 않는 점입니다.활성화된 스키마를 저장한 후에는 더 이상 비활성화할 수 없습니다. **[!UICONTROL Profile]** 토글을 다시 선택하여 스키마를 비활성화합니다.

프로세스를 완료하려면 **[!UICONTROL Save]**&#x200B;을 선택하여 스키마를 저장합니다.

![](../../images/ui/resources/schemas/profile-enabled.png)

이제 스키마는 실시간 고객 프로필에서 사용할 수 있습니다. Platform(플랫폼)이 이 스키마를 기반으로 데이터 세트를 인제스트할 때 해당 데이터는 병합된 프로필 데이터에 통합됩니다.

## 스키마 필드 {#display-names} 표시 이름 편집

클래스를 할당하고 스키마에 혼합을 추가한 후에는 표준 또는 사용자 정의 XDM 리소스에서 해당 필드를 제공했는지 여부에 관계없이 스키마 필드의 표시 이름을 편집할 수 있습니다.

>[!NOTE]
>
>표준 클래스 또는 혼합에 속하는 필드의 표시 이름은 특정 스키마 컨텍스트에서만 편집할 수 있습니다. 즉, 하나의 스키마에서 표준 필드의 표시 이름을 변경해도 동일한 관련 클래스나 믹싱을 사용하는 다른 스키마는 영향을 주지 않습니다.

스키마 필드의 표시 이름을 편집하려면 캔버스에서 필드를 선택합니다. 오른쪽 레일에서 **[!UICONTROL Display name]** 아래에 새 이름을 입력합니다.

![](../../images/ui/resources/schemas/display-name.png)

오른쪽 레일에서 **[!UICONTROL Apply]**&#x200B;을 선택하고 캔버스가 업데이트되어 필드의 새 표시 이름을 표시합니다. 스키마에 변경 사항을 적용하려면 **[!UICONTROL Save]**&#x200B;을 선택합니다.

![](../../images/ui/resources/schemas/display-name-changed.png)

## 스키마 클래스 {#change-class} 변경

스키마를 저장하기 전에 초기 컴포지션 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재지정은 매우 주의해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

클래스를 재할당하려면 캔버스의 왼쪽에 있는 **[!UICONTROL Assign]**&#x200B;을 선택합니다.

![](../../images/ui/resources/schemas/assign-class-button.png)

조직에서 정의한 모든 클래스(소유자(&quot;[!UICONTROL Customer]&quot;)와 Adobe에 의해 정의된 표준 클래스를 포함하여 사용 가능한 모든 클래스의 목록을 표시하는 대화 상자가 나타납니다.

목록에서 클래스를 선택하여 대화 상자의 오른쪽에 해당 설명을 표시합니다. **[!UICONTROL Preview class structure]**&#x200B;을 선택하여 클래스와 연관된 필드와 메타데이터를 볼 수도 있습니다. 계속하려면 **[!UICONTROL Assign class]**&#x200B;을 선택합니다.

![](../../images/ui/resources/schemas/assign-class.png)

새 클래스를 지정할 것인지 확인하는 새 대화 상자가 열립니다. **[!UICONTROL Assign]**&#x200B;을 선택하여 확인합니다.

![](../../images/ui/resources/schemas/assign-confirm.png)

클래스 변경을 확인한 후 캔버스가 재설정되고 모든 컴포지션 진행 상태가 손실됩니다.

## 다음 단계

이 문서에서는 플랫폼 UI에서 스키마를 만들고 편집하는 기본 사항에 대해 다룹니다. 고유한 사용 사례에 대한 사용자 정의 믹서와 데이터 형식을 만드는 것을 포함하여 UI에서 전체 스키마를 작성하기 위한 포괄적인 작업 과정을 보려면 [스키마 만들기 자습서](../../tutorials/create-schema-ui.md)를 검토하는 것이 좋습니다.

[!UICONTROL Schemas] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API에서 스키마를 관리하는 방법에 대해 알아보려면 [스키마 끝점 안내서](../../api/schemas.md)를 참조하십시오.
