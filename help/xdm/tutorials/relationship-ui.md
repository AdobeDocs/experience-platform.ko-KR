---
keywords: Experience Platform;홈;인기 주제;ui;UI;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 편집기;스키마;스키마;스키마;스키마;스키마;스키마;스키마;만들기;관계;관계;참조;참조;
solution: Experience Platform
title: 스키마 편집기를 사용하여 두 스키마 간의 관계 정의
description: 이 문서에서는 Experience Platform 사용자 인터페이스의 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 9%

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

Adobe Experience Platform에서는 다양한 채널에서 고객과 브랜드와의 상호 작용 간의 관계를 이해하는 기능이 중요합니다. [!DNL Experience Data Model]&#x200B;(XDM) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

유니온 스키마와 [!DNL Real-Time Customer Profile]을(를) 사용하여 스키마 관계를 유추할 수 있지만 이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 소스 스키마에 다른 관련 스키마의 ID를 참조하는 전용 관계 필드를 추가해야 합니다.

>[!NOTE]
>
>원본 스키마와 대상 스키마가 모두 같은 클래스에 속하는 경우 전용 관계 필드를 **사용하지 않음**&#x200B;해야 합니다. 이 경우 유니온 스키마 UI를 사용하여 관계를 확인합니다. 이 작업을 수행하는 방법에 대한 지침은 공용 구조체 스키마 UI 가이드의 [관계 보기](../../profile/ui/union-schema.md#view-relationships) 섹션에서 찾을 수 있습니다.

이 문서에서는 [!DNL Experience Platform] 사용자 인터페이스에서 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 제공합니다. API를 사용하여 스키마 관계를 정의하는 단계는 [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md)에 대한 자습서를 참조하십시오.

>[!NOTE]
>
>Adobe Real-Time Customer Data Platform B2B edition에서 다대일 관계를 만드는 방법에 대한 단계는 [B2B 관계 만들기](./relationship-b2b.md)에 대한 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 [!DNL Experience Platform] UI의 [!DNL XDM System] 및 스키마 편집기에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 [!DNL Experience Platform]의 구현에 대한 개요입니다.
* [스키마 컴포지션 기본 사항](../schema/composition.md): XDM 스키마 빌딩 블록 소개.
* [을(를) 사용하여 스키마를 만듭니다 [!DNL Schema Editor]](create-schema-ui.md): [!DNL Schema Editor] 작업의 기본 사항에 대한 자습서입니다.

## 소스 및 참조 스키마 정의

관계에 정의될 두 개의 스키마를 이미 생성했을 것으로 예상됩니다. 이 자습서에서는 데모용으로 조직의 충성도 프로그램 구성원(&quot;[!DNL Loyalty Members]&quot; 스키마에 정의됨)과 즐겨 찾는 호텔(&quot;[!DNL Hotels]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-Time Customer Profile]에 대해 사용할 수 있어야 합니다. 스키마를 적절하게 구성하는 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서에서 [프로필에 사용할 스키마 활성화](./create-schema-ui.md#profile)에 대한 섹션을 참조하십시오.

스키마 관계는 **참조 스키마** 내의 다른 필드를 가리키는 **소스 스키마** 내의 전용 필드로 표시됩니다. 다음 단계에서 &quot;[!DNL Loyalty Members]&quot;은(는) 소스 스키마가 되고 &quot;[!DNL Hotels]&quot;은(는) 참조 스키마로 작동합니다.

다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조를 설명합니다.

### [!DNL Loyalty Members] 스키마

원본 스키마 &quot;[!DNL Loyalty Members]&quot;은(는) 충성도 프로그램의 구성원을 설명하는 필드를 포함하는 [!DNL XDM Individual Profile] 클래스를 기반으로 합니다. 이러한 필드 중 하나인 `personalEmail.addess`은(는) [!UICONTROL 전자 메일] 네임스페이스에서 스키마의 기본 ID로 사용됩니다. **[!UICONTROL 스키마 속성]**&#x200B;에서 볼 수 있듯이 이 스키마는 [!DNL Real-Time Customer Profile]에서 사용할 수 있도록 설정되었습니다.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 스키마

참조 스키마 &quot;[!DNL Hotels]&quot;은(는) 사용자 지정 &quot;[!DNL Hotels]&quot; 클래스를 기반으로 하며 호텔을 설명하는 필드를 포함합니다. 관계에 참여하려면 참조 스키마에 기본 ID가 정의되어 있어야 하며 [!UICONTROL Profile]에 대해 사용할 수 있어야 합니다. 이 경우 `_tenantId.hotelId`은(는) 사용자 지정 &quot;[!DNL Hotel ID]&quot; ID 네임스페이스를 사용하여 스키마의 기본 ID 역할을 합니다.

![프로필에 사용](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>사용자 지정 ID 네임스페이스를 만드는 방법을 알아보려면 [ID 서비스 설명서](../../identity-service/features/namespaces.md#manage-namespaces)를 참조하세요.

## 관계 필드 그룹 만들기

>[!NOTE]
>
>이 단계는 소스 스키마에 참조 스키마의 기본 ID에 대한 포인터로 사용할 전용 문자열 유형 필드가 없는 경우에만 필요합니다. 이 필드가 원본 스키마에 이미 정의되어 있는 경우 [관계 필드 정의](#relationship-field)의 다음 단계로 건너뜁니다.

두 스키마 간의 관계를 정의하려면 소스 스키마에 참조 스키마의 기본 ID를 나타내는 전용 필드가 있어야 합니다. 새 스키마 필드 그룹을 만들거나 기존 스키마 필드 그룹을 확장하여 소스 스키마에 이 필드를 추가할 수 있습니다.

[!DNL Loyalty Members] 스키마의 경우 충성도 멤버가 회사 방문을 선호하는 호텔을 나타내기 위해 새 `preferredHotel` 필드가 추가됩니다. 소스 스키마 이름 옆에 있는 더하기 아이콘(**+**)을 선택하여 시작합니다.

![](../images/tutorials/relationship/loyalty-add-field.png)

캔버스에 새 필드 자리 표시자가 나타납니다. **[!UICONTROL 필드 속성]**&#x200B;에서 필드의 필드 이름과 표시 이름을 입력하고 해당 형식을 &quot;[!UICONTROL 문자열]&quot;(으)로 설정하십시오. **[!UICONTROL 할당 대상]**&#x200B;에서 확장할 기존 필드 그룹을 선택하거나 고유한 이름을 입력하여 새 필드 그룹을 만드십시오. 이 경우 새 &quot;[!DNL Preferred Hotel]&quot; 필드 그룹이 만들어집니다.

![](../images/tutorials/relationship/relationship-field-details.png)

완료되면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![](../images/tutorials/relationship/relationship-field-apply.png)

업데이트된 `preferredHotel` 필드는 사용자 지정 필드이므로 `_tenantId` 개체 아래에 있는 캔버스에 표시됩니다. **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마에 대한 변경 내용을 완료합니다.

![](../images/tutorials/relationship/relationship-field-save.png)

## 소스 스키마에 대한 관계 필드 정의 {#relationship-field}

소스 스키마에 전용 참조 필드가 정의되면 이를 관계 필드로 지정할 수 있습니다.

>[!NOTE]
>
>관계는 문자열 또는 문자열 배열 필드에서만 지원됩니다.

캔버스에서 `preferredHotel` 필드를 선택한 다음 **[!UICONTROL 필드 속성]** 사이드바에서 **[!UICONTROL 관계 추가]**&#x200B;를 선택하십시오.

![필드 속성 사이드바에서 관계 추가가 강조 표시된 스키마 편집기.](../images/tutorials/relationship/add-relationship.png)

[!UICONTROL 관계 추가] 대화 상자가 나타납니다. 이 대화 상자에서 관계 필드 구성에 필요한 매개 변수를 설정할 수 있습니다. Real-Time CDP B2C 사용자의 경우 **전용**&#x200B;에서 원본 스키마와 참조 스키마 간의 일대일 관계를 설정할 수 있습니다.

>[!NOTE]
>
>Real-Time CDP B2B edition에 액세스할 수 있는 경우 캔버스의 오른쪽 레일 컨트롤을 사용하여 관계 필드를 정의하고 [동일한 대화 상자](./relationship-b2b.md#relationship-field)를 사용하여 다대일 관계를 만들 수 있습니다.

![관계 추가 대화 상자](../images/tutorials/relationship/add-relationship-dialog.png)

**[!UICONTROL 참조 스키마]**&#x200B;에 대한 드롭다운을 사용하고 관계에 대한 참조 스키마를 선택합니다(이 예제에서는 &quot;[!DNL Hotels]&quot;).

>[!NOTE]
>
>기본 ID가 포함된 스키마만 참조 스키마 드롭다운 메뉴에 포함됩니다. 이 안전 조치는 아직 제대로 구성되지 않은 스키마와의 관계를 실수로 생성하는 것을 방지합니다.

참조 스키마의 ID 네임스페이스(이 경우 &quot;[!DNL Hotel ID]&quot;)는 **[!UICONTROL 참조 ID 네임스페이스]** 아래에 자동으로 채워집니다. 완료되면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![관계 매개 변수가 구성되어 있고 적용 이 강조 표시된 관계 추가 대화 상자.](../images/tutorials/relationship/apply-relationship.png)

이제 `preferredHotel` 필드가 캔버스에서 관계로 강조 표시되어 참조 스키마의 이름을 표시합니다. 변경 내용을 저장하고 워크플로우를 완료하려면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

![관계 참조와 [저장]이 강조 표시된 스키마 편집기입니다.](../images/tutorials/relationship/relationship-save.png)

### 기존 관계 필드 편집 {#edit-relationship}

참조 스키마를 변경하려면 기존 관계가 있는 필드를 선택한 다음 **[!UICONTROL 필드 속성]** 사이드바에서 **[!UICONTROL 관계 편집]**&#x200B;을 선택하십시오.

![편집 관계가 강조 표시된 스키마 편집기입니다.](../images/tutorials/relationship/edit-relationship.png)

[!UICONTROL 관계 편집] 대화 상자가 나타납니다. 여기에서 [관계 필드 정의](#relationship-field)에 설명된 프로세스를 따르거나 관계를 삭제할 수 있습니다. 참조 스키마에 대한 관계를 제거하려면 **[!UICONTROL 관계 삭제]**&#x200B;를 선택하십시오.

![관계 편집 대화 상자](../images/tutorials/relationship/edit-relationship-dialog.png)

## 관계 필터링 및 검색 {#filter-and-search}

[!UICONTROL 스키마] 작업 영역의 [!UICONTROL 관계] 탭에서 스키마 내의 특정 관계를 필터링하고 검색할 수 있습니다. 이 보기를 사용하여 관계를 빠르게 찾고 관리할 수 있습니다. 필터링 옵션에 대한 자세한 지침은 [스키마 리소스 탐색](../ui/explore.md#lookup)에 대한 문서를 참조하십시오.

![스키마 작업 영역의 관계 탭입니다.](../images/tutorials/relationship-b2b/relationship-tab.png)

## 다음 단계

이 자습서에 따라 [!DNL Schema Editor]을(를) 사용하여 두 스키마 간의 일대일 관계를 만들었습니다. API를 사용하여 관계를 정의하는 방법에 대한 단계는 [스키마 레지스트리 API를 사용하여 관계 정의](relationship-api.md)에 대한 자습서를 참조하십시오.
