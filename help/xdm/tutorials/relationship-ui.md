---
keywords: Experience Platform;홈;인기 항목;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 편집기;스키마 편집기;스키마;스키마;스키마;스키마;스키마;생성;관계;참조;참조;
solution: Experience Platform
title: 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의합니다.
description: 이 문서에서는 Experience Platform 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 497a515a872efdeeda270d0aa90b1fc99898ad4d
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# [!DNL Schema Editor] 을 사용하여 두 스키마 간의 관계를 정의합니다.

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 파악하는 기능은 Adobe Experience Platform의 중요한 부분입니다. XDM([!DNL Experience Data Model]) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

스키마 관계는 결합 스키마와 [!DNL Real-time Customer Profile]을 사용하여 유추할 수 있지만 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 대상 스키마의 ID를 참조하는 소스 스키마에 전용 관계 필드를 추가해야 합니다.

이 문서에서는 [!DNL Experience Platform] 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다. API를 사용하여 스키마 관계를 정의하는 단계는 [스키마 레지스트리 API](relationship-api.md)를 사용하여 관계를 정의하는 자습서를 참조하십시오.

## 시작하기

이 자습서에서는 [!DNL XDM System] UI의 [!DNL Experience Platform] 스키마 편집기에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 의 구현에 대한 개요입니다 [!DNL Experience Platform].
* [스키마 작성 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소 소개.
* [ [!DNL Schema Editor]](create-schema-ui.md)를 사용하여 스키마 만들기: 를 사용하는 작업의 기본 사항을 다루는 자습서입니다  [!DNL Schema Editor].

## 소스 및 대상 스키마 정의

이미 관계에 정의될 두 개의 스키마를 생성한 것으로 예상됩니다. 데모 목적으로 이 자습서에서는 조직의 충성도 프로그램(&quot;[!DNL Loyalty Members]&quot; 스키마에 정의됨)의 멤버와 즐겨찾는 호텔(&quot;[!DNL Hotels]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-time Customer Profile]에 대해 활성화되어 있어야 합니다. 스키마 구성 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서의 [프로필](./create-schema-ui.md#profile)에서 사용할 스키마 활성화 섹션을 참조하십시오.

스키마 관계는 **대상 스키마** 내의 다른 필드를 참조하는 **소스 스키마** 내의 전용 필드로 표시됩니다. 다음에 이어지는 단계에서는 &quot;[!DNL Loyalty Members]&quot;이 소스 스키마가 되고, &quot;[!DNL Hotels]&quot;은 대상 스키마로 작동합니다.

참조용으로 다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조를 설명합니다.

### [!DNL Loyalty Members] 스키마

소스 스키마 &quot;[!DNL Loyalty Members]&quot;은 [!DNL XDM Individual Profile] 클래스를 기반으로 하며, 이 스키마는 [UI](create-schema-ui.md)에서 스키마를 만들기 위해 자습서에서 만들어진 스키마입니다. 여기에는 `_tenantId` 네임스페이스 아래에 `loyalty` 개체가 포함되어 있으며 몇 가지 충성도 관련 필드가 포함됩니다. 이러한 필드 중 하나인 `loyaltyId` 는 [!UICONTROL Email] 네임스페이스 아래에 있는 스키마의 기본 ID로 사용됩니다. **[!UICONTROL 스키마 속성]**&#x200B;에 표시되는 대로 이 스키마는 [!DNL Real-time Customer Profile]에서 사용하도록 설정되었습니다.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 스키마

대상 스키마 &quot;[!DNL Hotels]&quot;은(는) 사용자 지정 &quot;[!DNL Hotels]&quot; 클래스를 기반으로 하며, 호텔을 설명하는 필드를 포함합니다.

![](../images/tutorials/relationship/hotels.png)

관계에 참여하려면 대상 스키마에 기본 ID가 있어야 합니다. 이 예에서 `hotelId` 필드는 사용자 지정 &quot;Hotel ID&quot; ID 네임스페이스를 사용하여 기본 ID로 사용됩니다.

![호텔 프라이머리 아이덴티티](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>사용자 지정 ID 네임스페이스를 만드는 방법을 알아보려면 [ID 서비스 설명서](../../identity-service/namespaces.md#manage-namespaces)를 참조하십시오.

기본 ID가 설정되면 [!DNL Real-time Customer Profile]에 대해 대상 스키마를 활성화해야 합니다.

![프로필에 사용](../images/tutorials/relationship/hotel-profile.png)

## 관계 스키마 필드 그룹 만들기

>[!NOTE]
>
>이 단계는 소스 스키마에 대상 스키마 참조로 사용할 전용 문자열 유형 필드가 없는 경우에만 필요합니다. 이 필드가 소스 스키마에 이미 정의된 경우 [관계 필드](#relationship-field)를 정의하는 다음 단계로 건너뜁니다.

두 스키마 간의 관계를 정의하려면 소스 스키마에 대상 스키마 참조로 사용할 전용 필드가 있어야 합니다. 새 스키마 필드 그룹을 만들어 소스 스키마에 이 필드를 추가할 수 있습니다.

먼저 **[!UICONTROL 필드 그룹]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

[!UICONTROL 필드 그룹 추가] 대화 상자가 나타납니다. 여기에서 **[!UICONTROL 새 필드 그룹 만들기]**&#x200B;를 선택합니다. 표시되는 텍스트 필드에 새 필드 그룹에 대한 표시 이름과 설명을 입력합니다. 완료되면 **[!UICONTROL 필드 그룹 추가]**&#x200B;를 선택합니다.

![](../images/tutorials/relationship/create-field-group.png)

캔버스가 다시 나타나고 &quot;[!DNL Favorite Hotel]&quot;이 **[!UICONTROL 필드 그룹]** 섹션에 표시됩니다. 필드 그룹 이름을 선택한 다음 루트 수준 `Loyalty Members` 필드 옆에 있는 **[!UICONTROL 필드 추가]**&#x200B;를 선택합니다.

![](../images/tutorials/relationship/loyalty-add-field.png)

새 필드가 캔버스에 `_tenantId` 네임스페이스 아래에 나타납니다. **[!UICONTROL 필드 속성]**&#x200B;에서 필드의 필드 이름과 표시 이름을 제공하고 해당 유형을 &quot;[!UICONTROL String]&quot;으로 설정합니다.

![](../images/tutorials/relationship/relationship-field-details.png)

완료되면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![](../images/tutorials/relationship/relationship-field-apply.png)

업데이트된 `favoriteHotel` 필드가 캔버스에 나타납니다. **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마에 대한 변경 사항을 완료합니다.

![](../images/tutorials/relationship/relationship-field-save.png)

## 소스 스키마에 대한 관계 필드 정의 {#relationship-field}

소스 스키마에 전용 참조 필드가 정의되면 이를 관계 필드로 지정할 수 있습니다.

캔버스에서 `favoriteHotel` 필드를 선택한 다음 **[!UICONTROL 관계]** 확인란이 나타날 때까지 **[!UICONTROL 필드 속성]** 아래에서 아래로 스크롤합니다. 관계 필드 구성에 필요한 매개 변수를 표시하려면 확인란을 선택합니다.

![](../images/tutorials/relationship/relationship-checkbox.png)

**[!UICONTROL 참조 스키마]**&#x200B;에 대한 드롭다운을 선택하고 관계의 대상 스키마( 이 예에서 &quot;[!DNL Hotels]&quot;)를 선택합니다. 대상 스키마가 [!DNL Profile]에 대해 활성화되어 있으면 **[!UICONTROL 참조 ID 네임스페이스]** 필드가 대상 스키마의 기본 ID의 네임스페이스로 자동으로 설정됩니다. 스키마에 기본 ID가 정의되지 않은 경우, 드롭다운 메뉴에서 사용할 네임스페이스를 수동으로 선택해야 합니다. 완료되면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

이제 `favoriteHotel` 필드가 캔버스에서 관계로 강조 표시되어 대상 스키마의 이름 및 참조 ID 네임스페이스를 표시합니다. **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 사항을 저장하고 워크플로우를 완료합니다.

![](../images/tutorials/relationship/relationship-save.png)

## 다음 단계

이 자습서를 따라 [!DNL Schema Editor] 을 사용하여 두 스키마 간에 일대일 관계를 성공적으로 만들었습니다. API를 사용하여 관계를 정의하는 방법에 대한 단계는 스키마 레지스트리 API](relationship-api.md)를 사용하여 관계를 정의하는 의 자습서를 참조하십시오.[
