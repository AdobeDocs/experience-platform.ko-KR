---
keywords: Experience Platform;홈;인기 주제;ui;UI;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 편집기;스키마;스키마;스키마;스키마;스키마;스키마;스키마;생성;관계;관계;참조;참조;
solution: Experience Platform
title: 스키마 편집기를 사용하여 두 스키마 간의 관계 정의
description: 이 문서에서는 Experience Platform 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 10%

---

# [!DNL Schema Editor]를 사용하여 두 스키마 간의 일대일 관계 정의 {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="스키마 관계"
>abstract="서로 다른 클래스에 속한 스키마는 관계 필드를 통해 컨텍스트에 따라 연결될 수 있으므로 보다 복잡한 세분화 규칙을 빌드할 수 있습니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="참조 스키마"
>abstract="관계를 설정할 스키마를 선택합니다. 이 스키마는 현재 스키마와 다른 클래스일 수 있습니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="참조 ID 네임스페이스"
>abstract="참조 스키마의 기본 ID 필드에 대한 네임스페이스(유형)입니다. 관계에 참여하려면 참조 스키마에 기본 ID 필드가 설정되어 있어야 합니다. 스키마 관계에 대한 자세한 내용은 설명서를 참조하십시오."

Adobe Experience Platform에서는 다양한 채널에서 고객과 브랜드와의 상호 작용 간의 관계를 이해하는 기능이 중요합니다. 구조 내에서 이러한 관계 정의 [!DNL Experience Data Model] (XDM) 스키마를 사용하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

한편 스키마 관계는 유니온 스키마 및 의 사용을 통해 추론될 수 있다. [!DNL Real-Time Customer Profile], 이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 소스 스키마에 다른 관련 스키마의 ID를 참조하는 전용 관계 필드를 추가해야 합니다.

>[!NOTE]
>
>소스 및 대상 스키마가 모두 동일한 클래스에 속하는 경우 전용 관계 필드는 다음과 같아야 합니다 **아님** 사용합니다. 이 경우 유니온 스키마 UI를 사용하여 관계를 확인합니다. 이 작업을 수행하는 방법에 대한 지침은 [관계 보기](../../profile/ui/union-schema.md#view-relationships) 유니온 스키마 UI 안내서의 섹션.

이 문서는에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다. [!DNL Experience Platform] 사용자 인터페이스. API를 사용하여 스키마 관계를 정의하는 단계는 [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md).

>[!NOTE]
>
>Adobe Real-time Customer Data Platform B2B Edition에서 다대일 관계를 만드는 방법에 대한 단계는 의 안내서를 참조하십시오. [B2B 관계 만들기](./relationship-b2b.md).

## 시작하기

이 튜토리얼을 사용하려면 다음을 이해할 수 있어야 합니다. [!DNL XDM System] 및 의 스키마 편집기 [!DNL Experience Platform] UI. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): 의 XDM 및 그 구현 개요 [!DNL Experience Platform].
* [스키마 컴포지션 기본 사항](../schema/composition.md): XDM 스키마 빌딩 블록 소개.
* [를 사용하여 스키마 만들기 [!DNL Schema Editor]](create-schema-ui.md): 작업 기본 사항을 다루는 튜토리얼 [!DNL Schema Editor].

## 소스 및 참조 스키마 정의

관계에 정의될 두 개의 스키마를 이미 생성했을 것으로 예상됩니다. 이 자습서에서는 데모를 위해 조직의 충성도 프로그램 구성원(&quot;에 정의됨) 간의 관계를 만듭니다.[!DNL Loyalty Members]&quot;스키마) 및 즐겨 찾는 호텔(&quot;에 정의됨)[!DNL Hotels]&quot;스키마).

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 정의된 기본 ID가 있어야 하며 를 활성화할 수 있습니다. [!DNL Real-Time Customer Profile]. 의 섹션을 참조하십시오. [프로필에서 사용할 스키마 활성화](./create-schema-ui.md#profile) 에 따라 스키마를 구성하는 방법에 대한 지침이 필요한 경우 스키마 만들기 튜토리얼에서 참조하십시오.

스키마 관계는 내의 전용 필드로 표시됩니다 **소스 스키마** 이(가) 내의 다른 필드를 가리킵니다. **참조 스키마**. 다음 단계에서 &quot;[!DNL Loyalty Members]&quot;&quot;은 소스 스키마가 되지만,&quot;[!DNL Hotels]&quot;은 참조 스키마 역할을 합니다.

다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조를 설명합니다.

### [!DNL Loyalty Members] 스키마

소스 스키마 &quot;[!DNL Loyalty Members]&quot;은(는) [!DNL XDM Individual Profile] 클래스(충성도 프로그램의 구성원을 설명하는 필드 포함). 이 필드 중 하나, `personalEmail.addess`는 아래에 있는 스키마의 기본 ID 역할을 합니다. [!UICONTROL 이메일] 네임스페이스입니다. 아래에서 보는 바와 같이 **[!UICONTROL 스키마 속성]**, 이 스키마는에서 사용할 수 있도록 설정되었습니다. [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 스키마

참조 스키마 &quot;[!DNL Hotels]&quot;은(는) 사용자 정의&quot;를 기반으로 합니다.[!DNL Hotels]&quot; 클래스이며, 호텔을 설명하는 필드가 포함되어 있습니다. 관계에 참여하려면 참조 스키마에 기본 ID도 정의되어 있어야 하며 사용할 수 있어야 합니다. [!UICONTROL 프로필]. 이 경우, `_tenantId.hotelId`사용자 지정 을 사용하여 스키마의 기본 ID로 작동합니다.[!DNL Hotel ID]&quot;id 네임스페이스.

![프로필 활성화](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>사용자 정의 ID 네임스페이스를 만드는 방법을 알아보려면 [Identity Service 설명서](../../identity-service/features/namespaces.md#manage-namespaces).

## 관계 필드 그룹 만들기

>[!NOTE]
>
>이 단계는 소스 스키마에 참조 스키마의 기본 ID에 대한 포인터로 사용할 전용 문자열 유형 필드가 없는 경우에만 필요합니다. 이 필드가 소스 스키마에 이미 정의되어 있는 경우 의 다음 단계로 건너뜁니다. [관계 필드 정의](#relationship-field).

두 스키마 간의 관계를 정의하려면 소스 스키마에 참조 스키마의 기본 ID를 나타내는 전용 필드가 있어야 합니다. 새 스키마 필드 그룹을 만들거나 기존 스키마 필드 그룹을 확장하여 소스 스키마에 이 필드를 추가할 수 있습니다.

의 경우 [!DNL Loyalty Members] 스키마, 새 항목 `preferredHotel` 충성도 멤버가 회사 방문을 선호하는 호텔을 표시하기 위해 필드가 추가됩니다. 더하기 아이콘( )을 선택하여 시작합니다.**+**)을 클릭하여 소스 스키마 이름 옆에 추가합니다.

![](../images/tutorials/relationship/loyalty-add-field.png)

캔버스에 새 필드 자리 표시자가 나타납니다. 아래 **[!UICONTROL 필드 속성]**, 필드 이름과 필드 표시 이름을 입력하고 해당 유형을 &quot;로 설정합니다.[!UICONTROL 문자열]&quot;. 아래 **[!UICONTROL 할당 대상]**&#x200B;를 클릭하고, 확장할 기존 필드 그룹을 선택하거나, 고유한 이름을 입력하여 새 필드 그룹을 만듭니다. 이 경우 새 &quot;[!DNL Preferred Hotel]&quot;필드 그룹이 생성되었습니다.

![](../images/tutorials/relationship/relationship-field-details.png)

완료되면 다음을 선택합니다. **[!UICONTROL 적용]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

업데이트됨 `preferredHotel` 캔버스에 나타나는 필드는 `_tenantId` 개체는 사용자 지정 필드이므로, 선택 **[!UICONTROL 저장]** 을 클릭하여 스키마에 대한 변경 사항을 완료합니다.

![](../images/tutorials/relationship/relationship-field-save.png)

## 소스 스키마에 대한 관계 필드 정의 {#relationship-field}

소스 스키마에 전용 참조 필드가 정의되면 이를 관계 필드로 지정할 수 있습니다.

>[!NOTE]
>
>아래 단계에서는 캔버스에서 오른쪽 레일 컨트롤을 사용하여 관계 필드를 정의하는 방법을 다룹니다. Real-Time CDP B2B 에디션에 액세스할 수 있는 경우 [동일한 대화 상자](./relationship-b2b.md#relationship-field) 다대일 관계를 만들 때처럼.

다음 항목 선택 `preferredHotel` 캔버스에서 필드를 입력한 다음 아래로 스크롤합니다. **[!UICONTROL 필드 속성]** 종료 시간: **[!UICONTROL 관계]** 확인란이 표시됩니다. 확인란을 선택하여 관계 필드를 구성하는 데 필요한 매개 변수를 표시합니다.

![](../images/tutorials/relationship/relationship-checkbox.png)

다음에 대한 드롭다운 선택 **[!UICONTROL 참조 스키마]** 관계에 대한 참조 스키마를 선택합니다(&quot;[!DNL Hotels]이 예제에서는 &quot;입니다. 아래 **[!UICONTROL 참조 ID 네임스페이스]**, 참조 스키마 id 필드의 네임스페이스 선택(이 경우, &quot;[!DNL Hotel ID]&quot;). 선택 **[!UICONTROL 적용]** 완료 시.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

다음 `preferredHotel` 이제 필드가 캔버스에서 관계로 강조 표시되어 참조 스키마의 이름을 표시합니다. 선택 **[!UICONTROL 저장]** 변경 사항을 저장하고 워크플로우를 완료합니다.

![](../images/tutorials/relationship/relationship-save.png)

## 다음 단계

이 자습서에 따라 를 사용하여 두 스키마 간의 일대일 관계를 성공적으로 만들었습니다. [!DNL Schema Editor]. API를 사용하여 관계를 정의하는 방법에 대한 단계는 의 자습서를 참조하십시오. [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md).
