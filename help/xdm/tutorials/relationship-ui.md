---
keywords: Experience Platform;홈;인기 항목;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 편집기;스키마 편집기;스키마;스키마;스키마;스키마;스키마;생성;관계;참조;참조;
solution: Experience Platform
title: 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의합니다.
description: 이 문서에서는 Experience Platform 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# 를 사용하여 두 스키마 간에 일대일 관계 정의 [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="스키마 관계"
>abstract="서로 다른 클래스에 속하는 스키마는 관계 필드를 통해 컨텍스트에 따라 연결되므로 더 복잡한 세그멘테이션 규칙을 작성할 수 있습니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="참조 스키마"
>abstract="관계를 설정할 스키마를 선택합니다. 이 스키마는 현재 스키마와 다른 클래스일 수 있습니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="참조 ID 네임스페이스"
>abstract="참조 스키마의 기본 ID 필드에 대한 네임스페이스(유형)입니다. 관계에 참여하려면 참조 스키마에 설정된 기본 ID 필드가 있어야 합니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 파악하는 기능은 Adobe Experience Platform의 중요한 부분입니다. 구조 내에서 이러한 관계 정의 [!DNL Experience Data Model] (XDM) 스키마를 사용하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

스키마 관계는 결합 스키마 및 [!DNL Real-Time Customer Profile]이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 대상 스키마의 ID를 참조하는 소스 스키마에 전용 관계 필드를 추가해야 합니다.

이 문서에서는 [!DNL Experience Platform] 사용자 인터페이스. API를 사용하여 스키마 관계를 정의하는 단계는 [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md).

>[!NOTE]
>
>Adobe Real-time Customer Data Platform B2B Edition에서 일대일 관계를 만드는 방법에 대한 단계는 다음 안내서를 참조하십시오 [B2B 관계 생성](./relationship-b2b.md).

## 시작하기

이 자습서에서는 을(를) 제대로 이해하고 있어야 합니다 [!DNL XDM System] 및 의 스키마 편집기 [!DNL Experience Platform] UI. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 의 구현에 대한 개요입니다 [!DNL Experience Platform].
* [스키마 작성 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소 소개.
* [를 사용하여 스키마 만들기 [!DNL Schema Editor]](create-schema-ui.md): 작업 기본 사항을 다루는 자습서입니다 [!DNL Schema Editor].

## 소스 및 대상 스키마 정의

이미 관계에 정의될 두 개의 스키마를 생성한 것으로 예상됩니다. 데모 목적으로 이 자습서에서는 조직의 충성도 프로그램(&quot;에 정의됨) 멤버 간의 관계를 만듭니다[!DNL Loyalty Members]&quot; schema) 및 favorite hotel([!DNL Hotels]&quot; 스키마)를 만듭니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-Time Customer Profile]. 의 섹션을 참조하십시오. [프로필에서 사용할 스키마 활성화](./create-schema-ui.md#profile) 스키마 만들기 자습서에서 스키마를 구성하는 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서에서 를 참조하십시오.

스키마 관계는 **소스 스키마** 는 **대상 스키마**. 다음에 나오는 단계에서, &quot;[!DNL Loyalty Members]&quot; 은 소스 스키마이고 &quot;[!DNL Hotels]는 대상 스키마로 작동합니다.

참조용으로 다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조를 설명합니다.

### [!DNL Loyalty Members] 스키마

소스 스키마 &quot;[!DNL Loyalty Members]&quot; [!DNL XDM Individual Profile] 클래스 및 는 의 자습서에서 만들어진 스키마입니다 [UI에서 스키마 만들기](create-schema-ui.md). 여기에는 다음이 포함됩니다 `loyalty` 개체 아래의 `_tenantId` 네임스페이스에 따라 다릅니다. 이 필드 중 하나는 `loyaltyId`는 의 [!UICONTROL 이메일] 네임스페이스. 아래에 표시됨 **[!UICONTROL 스키마 속성]**&#x200B;에서 사용할 수 있도록 이 스키마가 활성화되었습니다. [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 스키마

대상 스키마 &quot;[!DNL Hotels]&quot; 은(는) 사용자 지정 &quot;[!DNL Hotels]&quot; 클래스로, 호텔을 설명하는 필드를 포함합니다.

![](../images/tutorials/relationship/hotels.png)

관계에 참여하려면 대상 스키마에 기본 ID가 있어야 합니다. 이 예에서 `hotelId` 필드는 사용자 지정 &quot;호텔 ID&quot; id 네임스페이스를 사용하여 기본 ID로 사용됩니다.

![호텔 프라이머리 아이덴티티](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>사용자 지정 ID 네임스페이스를 만드는 방법을 알아보려면 [ID 서비스 설명서](../../identity-service/namespaces.md#manage-namespaces).

기본 ID가 설정되면 대상 스키마가에 대해 활성화되어 있어야 합니다 [!DNL Real-Time Customer Profile].

![프로필에 사용](../images/tutorials/relationship/hotel-profile.png)

## 관계 스키마 필드 그룹 만들기

>[!NOTE]
>
>이 단계는 소스 스키마에 대상 스키마 참조로 사용할 전용 문자열 유형 필드가 없는 경우에만 필요합니다. 이 필드가 소스 스키마에 이미 정의된 경우 다음 단계로 건너뜁니다 [관계 필드 정의](#relationship-field).

두 스키마 간의 관계를 정의하려면 소스 스키마에 대상 스키마 참조로 사용할 전용 필드가 있어야 합니다. 새 스키마 필드 그룹을 만들어 소스 스키마에 이 필드를 추가할 수 있습니다.

선택 **[!UICONTROL 추가]** 에서 **[!UICONTROL 필드 그룹]** 섹션을 참조하십시오.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

다음 [!UICONTROL 필드 그룹 추가] 대화 상자가 나타납니다. 여기에서 을 선택합니다. **[!UICONTROL 새 필드 그룹 만들기]**. 표시되는 텍스트 필드에 새 필드 그룹에 대한 표시 이름과 설명을 입력합니다. 선택 **[!UICONTROL 필드 그룹 추가]** 완료됨.

![](../images/tutorials/relationship/create-field-group.png)

캔버스가 &quot;[!DNL Favorite Hotel]&quot; **[!UICONTROL 필드 그룹]** 섹션을 참조하십시오. 필드 그룹 이름을 선택하고 을 선택합니다 **[!UICONTROL 필드 추가]** 루트 레벨 옆에 `Loyalty Members` 필드.

![](../images/tutorials/relationship/loyalty-add-field.png)

캔버스에서 새 필드가 나타납니다 `_tenantId` 네임스페이스. 아래 **[!UICONTROL 필드 속성]**&#x200B;를 채울 때 필드의 필드 이름과 표시 이름을 지정하고 유형을 &quot;&quot;로 설정합니다.[!UICONTROL 문자열]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

완료되면 을 선택합니다 **[!UICONTROL 적용]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

업데이트된 내용 `favoriteHotel` 필드가 캔버스에 나타납니다. 선택 **[!UICONTROL 저장]** 스키마 변경 작업을 완료하려면 다음을 수행하십시오.

![](../images/tutorials/relationship/relationship-field-save.png)

## 소스 스키마에 대한 관계 필드 정의 {#relationship-field}

소스 스키마에 전용 참조 필드가 정의되면 이를 관계 필드로 지정할 수 있습니다.

>[!NOTE]
>
>아래 단계에서는 캔버스에서 오른쪽 레일 컨트롤을 사용하여 관계 필드를 정의하는 방법을 설명합니다. Real-Time CDP B2B Edition에 대한 액세스 권한이 있는 경우 를 사용하여 일대일 관계를 정의할 수도 있습니다 [동일한 대화 상자](./relationship-b2b.md#relationship-field) 일대일 관계를 만들 때

을(를) 선택합니다 `favoriteHotel` 캔버스에서 필드를 아래로 스크롤한 다음 **[!UICONTROL 필드 속성]** 까지 **[!UICONTROL 관계]** 확인란이 표시됩니다. 관계 필드 구성에 필요한 매개 변수를 표시하려면 확인란을 선택합니다.

![](../images/tutorials/relationship/relationship-checkbox.png)

에 대한 드롭다운을 선택합니다. **[!UICONTROL 참조 스키마]** 관계를 위한 대상 스키마(&quot;[!DNL Hotels]&quot;(이 예에서 ) 대상 스키마가 [!DNL Profile], **[!UICONTROL 참조 ID 네임스페이스]** 필드는 대상 스키마의 기본 id 네임스페이스로 자동으로 설정됩니다. 스키마에 기본 ID가 정의되지 않은 경우, 드롭다운 메뉴에서 사용할 네임스페이스를 수동으로 선택해야 합니다. 선택 **[!UICONTROL 적용]** 완료됨.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

다음 `favoriteHotel` 이제 필드가 캔버스에서 관계로 강조 표시되어 대상 스키마의 이름 및 참조 id 네임스페이스가 표시됩니다. 선택 **[!UICONTROL 저장]** 변경 사항을 저장하고 워크플로우를 완료하려면

![](../images/tutorials/relationship/relationship-save.png)

## 다음 단계

이 자습서를 따라 를 사용하여 두 스키마 간에 일대일 관계를 성공적으로 만들었습니다 [!DNL Schema Editor]. API를 사용하여 관계를 정의하는 방법에 대한 단계는 [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md).
