---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: 스키마 편집기를 사용하여 두 스키마 간의 관계 정의
description: 이 문서에서는 Experience Platform 사용자 인터페이스의 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다.
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 파악할 수 있는 기능은 Adobe Experience Platform의 중요한 부분입니다. XDM(Structure Relationship) 스키마 구조 내에서 이러한 관계를 정의하면 [!DNL Experience Data Model] 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

스키마 관계는 조합 스키마 및 조합 스키마 사용을 통해 유추할 수 있지만, 이 [!DNL Real-time Customer Profile]는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 전용 관계 필드를 대상 스키마의 ID를 참조하는 소스 스키마에 추가해야 합니다.

이 문서에서는 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 [!DNL Experience Platform] 제공합니다. API를 사용하여 스키마 관계를 정의하는 단계는 스키마 레지스트리 API를 사용하여 관계를 [정의하는 자습서를 참조하십시오](relationship-api.md).

## 시작하기

이 자습서에서는 [!DNL XDM System] [!DNL Experience Platform] UI에서 스키마 편집기에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md):XDM 및 XDM 구현에 대한 개요입니다 [!DNL Experience Platform].
* [스키마 컴포지션의 기본 사항](../schema/composition.md):XDM 스키마의 기본 요소 소개
* [다음 아이콘을 사용하여 스키마를 [!DNL Schema Editor]](create-schema-ui.md)만듭니다.작업 기본 사항을 다루는 자습서입니다 [!DNL Schema Editor].

## 소스 및 대상 스키마 정의

관계에 정의될 두 개의 스키마를 이미 생성한 것으로 예상됩니다. 데모용으로, 이 자습서는 조직의 로열티 프로그램(&quot;[!DNL Loyalty Members]&quot; 스키마에 정의됨)의 멤버와 자주 사용하는 호텔(&quot;[!DNL Hotels]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마 모두 기본 ID를 정의했고 에 대해 활성화되어야 합니다 [!DNL Real-time Customer Profile]. 스키마 구성 방법에 대한 지침 [이 필요한 경우 스키마 생성 자습서에서 프로필에](./create-schema-ui.md#profile) 사용할 스키마를 활성화하는 방법을 참조하십시오.

스키마 관계는 **대상 스키마 내의 다른 필드를 참조하는** 소스 스키마 **내의 전용 필드로**&#x200B;표현됩니다. 다음 단계에서 &quot;[!DNL Loyalty Members]&quot;는 소스 스키마가 되고 &quot;[!DNL Hotels]&quot;는 대상 스키마로 작동합니다.

참조용으로 다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조에 대해 설명합니다.

### [!DNL Loyalty Members] 스키마

소스 스키마 &quot;[!DNL Loyalty Members]&quot;는 [!DNL XDM Individual Profile] 클래스를 기반으로 하며, UI에서 스키마를 [만들기 위해 자습서에서 생성된 스키마입니다](create-schema-ui.md). 여기에는 몇 개의 `loyalty` 충성도별 필드가 포함된 `_tenantId` 네임스페이스 아래에 개체가 포함됩니다. 이러한 필드 중 `loyaltyId`하나는 [!UICONTROL 이메일] 네임스페이스 아래의 스키마의 기본 ID로사용됩니다. 스키마 **[!UICONTROL 속성]**&#x200B;아래에서 보듯이 이 스키마는 에서 사용할 수 있게 [!DNL Real-time Customer Profile]설정되었습니다.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 스키마

대상 스키마 &quot;[!DNL Hotels]&quot;는 사용자 지정 &quot;[!DNL Hotels]&quot; 클래스를 기반으로 하며 호텔을 설명하는 필드를 포함합니다. 이 `hotelId` 필드는 사용자 지정 네임스페이스 아래의 스키마의 기본 ID로 `hotelId` 사용됩니다. 스키마처럼 이 스키마도 [!DNL Loyalty Members] 활성화되었습니다 [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## 관계 혼합 만들기

>[!NOTE]
>
>이 단계는 소스 스키마에 대상 스키마에 대한 참조로 사용할 전용 문자열 유형 필드가 없는 경우에만 필요합니다. 이 필드가 소스 스키마에 이미 정의된 경우 관계 필드 [를 정의하는 다음 단계로 건너뜁니다](#relationship-field).

두 스키마 간의 관계를 정의하려면 소스 스키마에 대상 스키마에 대한 참조로 사용할 전용 필드가 있어야 합니다. 새 혼합을 만들어 이 필드를 소스 스키마에 추가할 수 있습니다.

먼저 믹싱 **[!UICONTROL 섹션에서]** **[!UICONTROL 추가를]** 선택합니다.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

[ [!UICONTROL 혼합 추가] ] 대화 상자가 나타납니다. 여기에서 [새 **[!UICONTROL 혼합 만들기]를 선택합니다]**. 나타나는 텍스트 필드에 새 혼합에 대한 표시 이름과 설명을 입력합니다. 완료되면 **[!UICONTROL 믹신]** 추가를 선택합니다.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

[혼합] 섹션에 &quot;[!DNL Favorite Hotel]&quot;가 나타나고 **[!UICONTROL 캔버스가 다시]** 나타납니다. 혼합 이름을 선택한 다음 루트 수준 필드 **[!UICONTROL 옆에 있는 필드]** 추가를 `Loyalty Members` 선택합니다.

![](../images/tutorials/relationship/loyalty-add-field.png)

네임스페이스의 캔버스에 새 필드가 `_tenantId` 나타납니다. 필드 **[!UICONTROL 속성]**&#x200B;아래에서 필드에 대한 필드 이름과 표시 이름을 입력하고 해당 유형을 &quot;[!UICONTROL 문자열]&quot;로 설정합니다.

![](../images/tutorials/relationship/relationship-field-details.png)

완료되면 적용을 **[!UICONTROL 선택합니다]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

업데이트된 `favoriteHotel` 필드가 캔버스에 표시됩니다. 저장 **[!UICONTROL 을]** 선택하여 스키마에 대한 변경 사항을 완료합니다.

![](../images/tutorials/relationship/relationship-field-save.png)

## 소스 스키마의 관계 필드 정의 {#relationship-field}

소스 스키마에 전용 참조 필드가 정의되어 있으면 관계 필드로 지정할 수 있습니다.

캔버스에서 `favoriteHotel` 필드를 선택한 다음 관계 **[!UICONTROL 확인란]** 이 **[!UICONTROL 나타날 때까지 필드 속성]** 아래로스크롤합니다. 관계 필드를 구성하는 데 필요한 매개 변수를 표시하려면 이 확인란을 선택합니다.

![](../images/tutorials/relationship/relationship-checkbox.png)

참조 스키마에 대한 드롭다운을 **[!UICONTROL 선택하고]** 관계에 대한 대상 스키마[!DNL Hotels](&quot;이 예제의 경우&quot;)를 선택합니다. 대상 스키마를 사용할 수 [!DNL Profile]있는 경우 **[!UICONTROL 참조 ID 네임스페이스]** 필드는 대상 스키마의 기본 ID의 네임스페이스로 자동으로 설정됩니다. 스키마에 기본 ID가 정의되지 않은 경우 드롭다운 메뉴에서 사용할 네임스페이스를 수동으로 선택해야 합니다. 완료되면 **[!UICONTROL 적용을]** 선택합니다.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

이제 `favoriteHotel` 필드가 대상 스키마의 이름 및 참조 ID 네임스페이스를 표시하여 캔버스에서 관계로 강조 표시됩니다. 저장을 **[!UICONTROL 선택하여]** 변경 사항을 저장하고 워크플로우를 완료합니다.

![](../images/tutorials/relationship/relationship-save.png)

## 다음 단계

이 튜토리얼을 따라 를 사용하여 두 스키마 간에 1:1 관계를 성공적으로 만들었습니다 [!DNL Schema Editor]. API를 사용하여 관계를 정의하는 방법에 대한 단계는 스키마 레지스트리 API를 사용하여 관계를 [정의하는 자습서를 참조하십시오](relationship-api.md).