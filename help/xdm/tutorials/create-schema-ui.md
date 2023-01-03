---
keywords: Experience Platform;홈;인기 항목;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 편집기;스키마 편집기;스키마;스키마;스키마;스키마;스키마;스키마 만들기
solution: Experience Platform
title: 스키마 편집기를 사용하여 스키마 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 튜토리얼에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# 를 사용하여 스키마 만들기 [!DNL Schema Editor]

Adobe Experience Platform 사용자 인터페이스를 통해 사용자를 만들고 관리할 수 있습니다 [!DNL Experience Data Model] (XDM) 스키마는 [!DNL Schema Editor]. 이 자습서에서는 [!DNL Schema Editor].

>[!NOTE]
>
>데모 목적으로 이 자습서의 단계에는 고객 충성도 프로그램의 구성원을 설명하는 예제 스키마를 만드는 작업이 포함됩니다. 이러한 단계를 사용하여 고유한 목적으로 다른 스키마를 생성할 수 있지만, 먼저 예제 스키마 만들기 와 함께 수행하여 의 기능을 학습하는 것이 좋습니다 [!DNL Schema Editor].

를 사용하여 스키마를 작성하려는 경우 [!DNL Schema Registry] API를 대신, 를 참조하여 시작하십시오. [[!DNL Schema Registry] 개발자 안내서](../api/getting-started.md) 자습서를 시작하기 전에 [api를 사용하여 스키마 만들기](create-schema-api.md).

## 시작하기

이 자습서에서는 스키마 만들기와 관련된 Adobe Experience Platform의 다양한 측면을 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 개념에 대한 설명서를 검토하십시오.

* [[!DNL Experience Data Model (XDM)]](../home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../schema/composition.md): 클래스, 스키마 필드 그룹, 데이터 유형 및 개별 필드를 포함한 XDM 스키마 및 해당 빌딩 블록에 대한 개요입니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 를 엽니다. [!UICONTROL 스키마] 작업 영역 {#browse}

다음 [!UICONTROL 스키마] 작업 영역 [!DNL Platform] UI는 [!DNL Schema Library]를 사용하면 조직에서 사용할 수 있는 스키마를 관리할 수 있습니다. 작업 공간에는 다음과 같은 작업도 포함됩니다 [!DNL Schema Editor]는 이 자습서 전체에서 스키마를 작성할 수 있는 캔버스입니다.

로그인한 후 [!DNL Experience Platform], 선택 **[!UICONTROL 스키마]** 왼쪽 탐색에서 를 클릭하여 **[!UICONTROL 스키마]** 작업 공간. 다음 **[!UICONTROL 찾아보기]** 탭에는 스키마 목록(표시)이 표시됩니다 [!DNL Schema Library])을 클릭하여 보거나 사용자 지정할 수 있습니다. 이 목록에는 스키마의 기반이 되는 이름, 유형, 클래스 및 동작(레코드 또는 시계열)과 스키마가 마지막으로 수정된 날짜 및 시간이 포함됩니다.

다음 안내서를 참조하십시오. [UI에서 기존 XDM 리소스 탐색](../ui/explore.md) 추가 정보.

## 스키마 만들기 및 이름 지정 {#create}

스키마 작성을 시작하려면 다음을 선택합니다 **[!UICONTROL 스키마 만들기]** 의 오른쪽 상단 모서리에서 **[!UICONTROL 스키마]** 작업 공간. 드롭다운 메뉴가 나타나고 핵심 클래스 중에서 선택할 수 있는 옵션이 제공됩니다 [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent]. 이러한 클래스가 사용자의 목적에 맞지 않는 경우 **[!UICONTROL 찾아보기]** 사용 가능한 다른 클래스 또는 [새 클래스 만들기](#create-new-class).

이 자습서를 사용하려면 을(를) 선택합니다. **[!UICONTROL XDM 개별 프로필]**.

![](../images/tutorials/create-schema/create_schema_button.png)

스키마를 기반으로 하기 위해 표준 XDM 클래스를 선택했으므로, **[!UICONTROL 필드 그룹 추가]** 스키마에 필드 추가를 즉시 시작할 수 있는 대화 상자가 나타납니다. 현재, 을(를) 선택합니다. **[!UICONTROL 취소]** 을 클릭하여 대화 상자를 종료합니다.

![](../images/tutorials/create-schema/cancel-field-group.png)

다음 [!DNL Schema Editor] 이 나타납니다. 스키마를 작성할 캔버스입니다. 제목 없는 스키마는 **[!UICONTROL 구조]** 편집기에 도착할 때 캔버스의 섹션 및 해당 클래스를 기반으로 한 모든 스키마에 포함된 표준 필드가 표시됩니다. 스키마에 대해 지정된 클래스도 아래에 나열됩니다 **[!UICONTROL 클래스]** in **[!UICONTROL 조성물]** 섹션을 참조하십시오.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>다음을 수행할 수 있습니다 [스키마 클래스 변경](#change-class) 스키마가 저장되기 전에 초기 구성 프로세스 중에 언제든지 이 작업을 수행해야 합니다. 필드 그룹은 특정 클래스와 호환되기 때문에 클래스를 변경하면 캔버스 및 추가한 필드가 재설정됩니다.

편집기 오른쪽의 필드를 사용하여 스키마에 대한 표시 이름과 선택적 설명을 제공합니다. 이름을 입력하면 새 스키마 이름을 반영하도록 캔버스가 업데이트됩니다.

![](../images/tutorials/create-schema/name_schema.png)

스키마 이름을 결정할 때 고려해야 할 몇 가지 중요한 고려 사항이 있습니다.

* 나중에 스키마를 쉽게 찾을 수 있도록 스키마 이름은 짧고 설명적이어야 합니다.
* 스키마 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다. 예를 들어, 조직에 다양한 브랜드에 대한 별도의 충성도 프로그램이 있는 경우 나중에 정의할 수 있는 다른 충성도 관련 스키마와 쉽게 구별하도록 하려면 스키마 &quot;Brand A 충성도 멤버&quot;를 지정하는 것이 좋습니다.
* 스키마 설명을 사용하여 스키마와 관련된 추가 컨텍스트 정보를 제공할 수도 있습니다.

이 자습서에서는 충성도 프로그램 멤버와 관련된 데이터를 수집하는 스키마를 사용하므로 스키마의 이름을 &quot;충성도 멤버&quot;로 지정합니다.

## 필드 그룹 추가 {#field-group}

이제 필드 그룹을 추가하여 스키마에 필드를 추가할 수 있습니다. 필드 그룹은 특정 개념을 설명하는 데 함께 사용되는 하나 이상의 필드 그룹입니다. 이 자습서에서는 필드 그룹을 사용하여 충성도 프로그램의 구성원을 설명하고 이름, 생일, 전화 번호, 주소 등의 주요 정보를 캡처합니다.

필드 그룹을 추가하려면 **[!UICONTROL 추가]** 에서 **[!UICONTROL 필드 그룹]** 하위 섹션.

![](../images/tutorials/create-schema/add-field-group-button.png)

사용 가능한 필드 그룹 목록을 표시하는 새 대화 상자가 나타납니다. 각 필드 그룹은 특정 클래스에서만 사용할 수 있으므로 대화 상자에는 선택한 클래스와 호환되는 필드 그룹(이 경우 [!DNL XDM Individual Profile] 클래스). 표준 XDM 클래스를 사용하는 경우 필드 그룹 목록이 사용 인기도에 따라 지능적으로 정렬됩니다.

![](../images/tutorials/create-schema/field-group-popularity.png)

목록에서 필드 그룹을 선택하면 오른쪽 레일에 필드 그룹이 표시됩니다. 원하는 경우 여러 필드 그룹을 선택하고, 각 필드 그룹을 오른쪽 레일의 목록에 추가한 후에 확인하면 됩니다. 또한 현재 선택한 필드 그룹의 오른쪽에 아이콘이 표시되어 제공된 필드의 구조를 미리 볼 수 있습니다.

![](../images/tutorials/create-schema/preview-field-group-button.png)

필드 그룹을 미리 볼 때 오른쪽 레일에 필드 그룹의 스키마에 대한 자세한 설명이 제공됩니다. 제공된 캔버스에서 필드 그룹의 필드를 탐색할 수도 있습니다. 다른 필드를 선택하면 오른쪽 레일이 업데이트되어 해당 필드에 대한 세부 사항이 표시됩니다. 선택 **[!UICONTROL 뒤로]** 미리 보기를 완료하여 필드 그룹 선택 대화 상자로 돌아갑니다.

![](../images/tutorials/create-schema/preview-field-group.png)

이 자습서에서 **[!UICONTROL 인구 통계 세부 정보]** 필드 그룹을 선택한 다음 **[!UICONTROL 필드 그룹 추가]**.

![](../images/tutorials/create-schema/demographic-details.png)

스키마 캔버스가 다시 나타납니다. 다음 **[!UICONTROL 필드 그룹]** 이제 섹션에 &quot;&quot;[!UICONTROL 인구 통계 세부 정보]&quot; 및 **[!UICONTROL 구조]** 섹션에는 필드 그룹에서 제공하는 필드가 포함되어 있습니다. 필드 그룹의 이름을 **[!UICONTROL 필드 그룹]** 캔버스 내에서 제공하는 특정 필드를 강조 표시하는 섹션을 참조하십시오.

![](../images/tutorials/create-schema/demographic-details-structure.png)

이 필드 그룹은 최상위 수준 이름 아래에 여러 필드에 기여합니다 `person` 데이터 유형 &quot; 사용[!UICONTROL 개인]&quot;. 이 필드 그룹은 이름, 생년월일 및 성별을 포함한 개인에 대한 정보를 설명합니다.

>[!NOTE]
>
>필드에서는 스칼라 유형(예: 문자열, 정수, 배열 또는 날짜)과 [!DNL Schema Registry].

다음 사항에 주의하십시오. `name` 필드에 &quot;[!UICONTROL 개인 이름]&quot;은(는) 일반적인 개념을 설명하고 이름, 성, 호칭 제목 및 접미사와 같은 이름 관련 하위 필드를 포함함을 의미합니다.

캔버스 내에서 다른 필드를 선택하여 스키마 구조에 기여하는 추가 필드를 표시합니다.

## 다른 필드 그룹 추가 {#field-group-2}

이제 동일한 단계를 반복하여 다른 필드 그룹을 추가할 수 있습니다. 를 볼 때 **[!UICONTROL 필드 그룹 추가]** 이 대화 상자에서 &quot;[!UICONTROL 인구 통계 세부 정보]&quot; 필드 그룹이 회색으로 표시되어 있고 그 옆에 있는 확인란을 선택할 수 없습니다. 따라서 현재 스키마에 이미 포함시킨 필드 그룹을 실수로 복제할 수 없습니다.

이 자습서에서 &quot;[!DNL Personal Contact Details]&quot; 필드 그룹을 선택한 다음 **[!UICONTROL 필드 그룹 추가]** 를 추가하여 스키마에 추가합니다.

![](../images/tutorials/create-schema/personal-contact-details.png)

추가한 후에는 캔버스가 다시 나타납니다. &quot;[!UICONTROL 개인 연락처 세부 정보]&quot;이(가) 이제 다음에 나열됩니다. **[!UICONTROL 필드 그룹]** 에서 **[!UICONTROL 조성물]** 섹션에 home address, mobile phone 등의 필드를 추가했습니다. **[!UICONTROL 구조]**.

와 비슷합니다 `name` 필드에서 방금 추가한 필드는 다중 필드 개념을 나타냅니다. 예, `homeAddress` 에는 &quot;의 데이터 유형이 있습니다.[!UICONTROL 우편 주소]&quot; 및 `mobilePhone` 에는 &quot;의 데이터 유형이 있습니다.[!UICONTROL 전화 번호]&quot;. 이러한 각 필드를 선택하여 확장하고 데이터 유형에 포함된 추가 필드를 볼 수 있습니다.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## 사용자 지정 필드 그룹 정의 {#define-field-group}

&quot;[!UICONTROL 충성도 멤버]스키마는 충성도 프로그램의 멤버와 관련된 데이터를 캡처하기 위한 것으로, 따라서 몇 가지 특정 충성도 관련 필드가 필요합니다.

표준이 있습니다 [!UICONTROL 충성도 세부 사항] 스키마에 추가하여 충성도 프로그램과 관련된 공통 필드를 캡처할 수 있는 필드 그룹입니다. 표준 필드 그룹을 사용하여 스키마에서 캡처된 개념을 나타내는 것이 좋지만 표준 충성도 필드 그룹의 구조가 특정 충성도 프로그램에 대한 모든 관련 데이터를 캡처하지 못할 수 있습니다. 이 시나리오에서는 대신 이러한 필드를 캡처할 새 사용자 지정 필드 그룹을 정의하도록 선택할 수 있습니다.

를 엽니다. **[!UICONTROL 필드 그룹 추가]** 대화 상자를 다시 사용하지만 이번에는 **[!UICONTROL 새 필드 그룹 만들기]** 꼭대기 근처에요 그런 다음 필드 그룹에 대한 표시 이름과 설명을 제공해야 합니다.

![](../images/tutorials/create-schema/create-new-field-group.png)

클래스 이름과 마찬가지로 필드 그룹 이름은 필드 그룹이 스키마에 기여하는 것을 설명하는 짧고 간단해야 합니다. 이러한 매개 변수도 고유하므로 이름을 다시 사용할 수 없으므로 고유한지 확인해야 합니다.

이 자습서에서 새 필드 그룹의 이름을 &quot;충성도 세부 사항&quot;으로 지정합니다.

선택 **[!UICONTROL 필드 그룹 추가]** 로 돌아가기 [!DNL Schema Editor]. &quot;[!UICONTROL 충성도 세부 사항]이제 다음에 표시됩니다. **[!UICONTROL 필드 그룹]** 캔버스 왼쪽에 있지만 연결된 필드가 없으므로 아래에 새 필드가 표시되지 않습니다 **[!UICONTROL 구조]**.

## 필드 그룹에 필드 추가 {#field-group-fields}

충성도 세부 사항 필드 그룹을 만들었으므로 이제 필드 그룹이 스키마에 기여할 필드를 정의해야 합니다.

시작하려면, **[!UICONTROL 필드 그룹]** 섹션을 참조하십시오. 이렇게 하면 필드 그룹의 속성이 편집기의 오른쪽에 표시되고 **더하기(+)** 아래의 스키마 이름 옆에 아이콘 표시 **[!UICONTROL 구조]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

을(를) 선택합니다 **더하기(+)** 아이콘 옆에 있는 &quot;[!DNL Loyalty Members]&quot;를 눌러 구조에 새 노드를 생성합니다. 이 노드( `_tenantId` 이 예에서) 는 IMS 조직의 테넌트 ID를 나타내며 앞에 밑줄이 표시됩니다. 테넌트 ID가 있는지 여부는 추가하고 있는 필드가 조직의 네임스페이스에 포함되어 있음을 나타냅니다.

즉, 추가하려는 필드는 조직에 고유하며 [!DNL Schema Registry] ( 조직에만 액세스할 수 있는 특정 영역 ) 정의한 필드는 다른 표준 클래스, 필드 그룹, 데이터 유형 및 필드에서 이름이 있는 충돌을 방지하기 위해 항상 테넌트 네임스페이스에 추가해야 합니다.

해당 네임스페이스 노드 안에는 &quot;[!UICONTROL 새 필드]&quot;. &quot;[!UICONTROL 충성도 세부 사항]&quot; 필드 그룹&quot;을 입력합니다.

![](../images/tutorials/create-schema/new_field_loyalty.png)

편집기 오른쪽의 컨트롤을 사용하여 먼저 `loyalty` &quot; 유형이 있는 필드[!UICONTROL 개체]충성도 관련 필드를 유지하는 데 사용됩니다. 완료되면 을 선택합니다 **[!UICONTROL 적용]**.

![](../images/tutorials/create-schema/loyalty_object.png)

변경 사항이 적용되고 새로 만든 `loyalty` 개체가 나타납니다. 을(를) 선택합니다 **더하기(+)** 아이콘 옆에 추가 충성도 관련 필드를 추가합니다. A &quot;[!UICONTROL 새 필드]&quot; 이 나타나고 **[!UICONTROL 필드 속성]** 캔버스 오른쪽에 섹션이 보입니다.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

각 필드에는 다음 정보가 필요합니다.

* **[!UICONTROL 필드 이름]:** 낙타케이스로 쓰여진 들판의 이름입니다. 예: 충성도 수준
* **[!UICONTROL 표시 이름]:** 제목 사례에 기록된 필드의 이름입니다. 예: 충성도 수준
* **[!UICONTROL 유형]:** 필드의 데이터 유형입니다. 여기에는 기본 스칼라 유형과 [!DNL Schema Registry]. 예: [!UICONTROL 문자열], [!UICONTROL 정수], [!UICONTROL 부울], [!UICONTROL 개인], [!UICONTROL 주소], [!UICONTROL 전화 번호]등
* **[!UICONTROL 설명]:** 필드에 대한 선택적 설명은 문장 대소문자를 구분하고 최대 200자를 포함해야 합니다.

에 대한 첫 번째 필드 `Loyalty` 객체는 `loyaltyId`. 새 필드의 유형을 &quot;[!UICONTROL 문자열]&quot;, **[!UICONTROL 필드 속성]** 단면에는 기본값, 형식 및 최대 길이를 포함하여 구속을 적용하는 여러 옵션이 채워집니다.

![](../images/tutorials/create-schema/string_constraints.png)

선택한 데이터 유형에 따라 다른 제한 옵션을 사용할 수 있습니다. 이후 `loyaltyId` 은(는) 이메일 주소입니다. &quot;[!UICONTROL 이메일]&quot; **[!UICONTROL 형식]** 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다. 선택 **[!UICONTROL 적용]** 변경 사항을 적용하려면

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 필드 그룹에 필드 추가 {#field-group-fields-2}

이제 를 추가했으므로 `loyaltyId` 필드에서 추가 필드를 추가하여 다음과 같은 충성도 관련 정보를 캡처할 수 있습니다.

* 포인트(정수)
* 이후 멤버(날짜)

각 필드를 스키마에 추가하려면 **더하기(+)** 아이콘 옆에 있는 를 클릭합니다. `loyalty` 개체를 입력하고 필요한 정보를 입력합니다.

완료되면 충성도 개체에는 충성도 ID, 포인트 및 멤버-이후의 필드가 포함됩니다.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 필드 그룹에 열거형 필드 추가 {#enum}

에서 필드를 정의할 때 [!DNL Schema Editor], 필드에 포함할 수 있는 데이터에 대한 추가 제한 사항을 제공하기 위해 기본 필드 유형에 적용할 수 있는 몇 가지 추가 옵션이 있습니다. 이러한 제약 조건에 대한 사용 사례는 다음 표에 설명되어 있습니다.

| 제한 | 설명 |
| --- | --- |
| [!UICONTROL 필수 여부] | 필드가 데이터 처리에 필수임을 나타냅니다. 이 필드를 포함하지 않는 이 스키마를 기반으로 데이터 세트에 업로드된 모든 데이터는 수집 시 실패합니다. |
| [!UICONTROL 어레이] | 필드에 각각 데이터 유형이 지정된 값의 배열이 포함되어 있음을 나타냅니다. 예를 들어 데이터 유형이 &quot;인 필드에서 이 제약 조건 사용[!UICONTROL 문자열]&quot; 필드에 문자열 배열이 포함되도록 지정합니다. |
| [!UICONTROL 열거형] | 이 필드에는 가능한 값을 열거한 목록에서 값 중 하나가 포함되어야 함을 나타냅니다. |
| [!UICONTROL 신원] | 이 필드가 ID 필드임을 나타냅니다. ID 필드에 대한 자세한 정보가 제공됩니다 [이 자습서의 후반부](#identity-field). |
| [!UICONTROL 관계] | 스키마 관계는 결합 스키마 및 [!DNL Real-Time Customer Profile]이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다음 [!UICONTROL 관계] 제약 조건은 이 필드가 다른 클래스를 기반으로 한 스키마의 기본 ID를 참조하며 두 스키마 간의 관계를 의미합니다. 다음에서 자습서를 참조하십시오. [관계 정의](./relationship-ui.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>필수, ID 또는 관계 필드가 왼쪽 레일에 표시되므로 스키마의 복잡성에 관계없이 이러한 필드를 쉽게 찾을 수 있습니다.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

이 자습서의 경우 [!DNL "loyalty"] 스키마의 객체에는 고객의 &quot;충성도 수준&quot;을 설명하는 새로운 열거형 필드가 필요합니다. 이 경우 값은 가능한 4가지 옵션 중 하나일 수 있습니다. 이 필드를 스키마에 추가하려면 **더하기(+)** 아이콘 옆의 아이콘 `loyalty` 개체 및 **[!UICONTROL 필드 이름]** 및 **[!UICONTROL 표시 이름]**. 대상 **[!UICONTROL 유형]**, &quot; 선택[!UICONTROL 문자열]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

해당 유형을 선택한 다음 필드의 확인란을 추가로 선택합니다 **[!UICONTROL 어레이]**, **[!UICONTROL 열거형]**, 및 **[!UICONTROL ID]**.

을(를) 선택합니다 **[!UICONTROL 열거형]** 확인란을 클릭하여 열기 **[!UICONTROL 열거형 값]** 섹션을 참조하십시오. 여기에서 을 입력할 수 있습니다 **[!UICONTROL 값]** (camelCase) 및 **[!UICONTROL 레이블]** (제목 케이스의 선택적 읽기 전용 이름)을 사용할 수 있는 각 충성도 수준에 대해 설명합니다.

모든 필드 속성을 완료했으면 을 선택합니다 **[!UICONTROL 적용]** 를 추가하려면[!DNL loyaltyLevel]&quot; 필드를 `loyalty` 개체.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 다중 필드 개체를 데이터 형식으로 변환 {#datatype}

다음 `loyalty` 이제 개체에는 몇 개의 충성도 관련 필드가 포함되어 있으며, 다른 스키마에서 유용할 수 있는 일반적인 데이터 구조를 나타냅니다. 다음 [!DNL Schema Editor] 이러한 개체의 구조를 데이터 형식으로 변환하여 재사용 가능한 다중 필드 개체를 쉽게 적용할 수 있습니다.

데이터 유형을 사용하면 여러 필드 구조를 일관성 있게 사용할 수 있으며 스키마 내의 어디에서든 사용할 수 있으므로 필드 그룹보다 더 유연하게 대처할 수 있습니다. 이 작업은 필드의 **[!UICONTROL 유형]** 값에서 정의한 데이터 유형의 값 [!DNL Schema Registry].

를 변환하려면 `loyalty` 개체를 데이터 형식으로 `loyalty` 아래의 필드 **[!UICONTROL 구조]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 새 데이터 유형으로 변환]** 편집자의 오른편에 **[!UICONTROL 필드 속성]**. 객체가 성공적으로 변환되었는지 확인하는 녹색 팝오버가 나타납니다.

![](../images/tutorials/create-schema/convert-data-type.png)

이제, **[!UICONTROL 구조]**, 다음을 확인할 수 있습니다. `loyalty` 필드에 &quot;[!DNL Loyalty]&quot; 그리고 필드 옆에는 작은 잠금 아이콘이 있어서 개별 필드가 아니라 다중 필드 데이터 유형의 일부임을 나타냅니다.

![](../images/tutorials/create-schema/loyalty_data_type.png)

향후 스키마에서 필드를 &quot;[!DNL Loyalty]&quot;을 입력하면 ID, 충성도 수준, 이후의 멤버 및 포인트에 대한 필드가 자동으로 포함됩니다.

>[!NOTE]
>
>스키마 편집과 별도로 사용자 지정 데이터 유형을 만들고 편집할 수도 있습니다. 다음 안내서를 참조하십시오. [데이터 유형 만들기 및 편집](../ui/resources/data-types.md) 추가 정보.

## 스키마 필드 검색 및 필터링

이제 스키마에 기본 클래스에서 제공하는 필드 외에 여러 필드 그룹이 포함됩니다. 더 큰 스키마로 작업하는 경우 왼쪽 레일의 필드 그룹 이름 옆에 있는 확인란을 선택하여 표시된 필드를 원하는 필드 그룹에서 제공하는 필드로만 필터링할 수 있습니다.

![](../images/tutorials/create-schema/filter-by-field-group.png)

스키마에서 특정 필드를 찾고 있는 경우, 검색 창을 사용하여 표시되는 필드를 제공된 필드 그룹에 관계없이 이름별로 필터링할 수도 있습니다.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>검색 함수는 일치하는 필드를 표시할 때 선택한 필드 그룹 필터를 고려합니다. 검색 쿼리에 예상한 결과가 표시되지 않으면 관련 필드 그룹을 필터링하지 않았는지 다시 확인해야 할 수 있습니다.

## 스키마 필드를 ID 필드로 설정 {#identity-field}

스키마가 제공하는 표준 데이터 구조는 여러 소스에서 동일한 개인에게 속하는 데이터를 식별하는 데 활용할 수 있으므로 세그먼테이션, 보고, 데이터 과학 분석 등과 같은 다양한 다운스트림 사용 사례를 수행할 수 있습니다. 개별 ID를 기반으로 데이터를 결합하려면 주요 필드를 [!UICONTROL ID] 적용 가능한 스키마 내의 필드.

[!DNL Experience Platform] 를 사용하면 **[!UICONTROL ID]** 확인란 [!DNL Schema Editor]. 하지만 데이터의 특성을 기반으로 ID로 사용할 가장 적합한 필드를 결정해야 합니다.

예를 들어 동일한 &quot;충성도 수준&quot;에 속하는 충성도 프로그램 멤버가 수천 명이 있을 수 있지만 충성도 프로그램의 각 멤버에는 고유한 멤버가 있습니다 `loyaltyId` (이 인스턴스에서 개별 구성원의 이메일 주소입니다.) 사실 `loyaltyId` 는 각 구성원의 고유 식별자로 id 필드에 적합한 후보입니다. `loyaltyLevel` 은 아닙니다.

>[!IMPORTANT]
>
>아래 요약된 단계에서는 기존 스키마 필드에 ID 설명자를 추가하는 방법을 설명합니다. 스키마 자체의 구조 내에서 ID 필드를 정의하는 대신 `identityMap` ID 정보를 포함할 필드입니다.
>
>사용할 계획이라면 `identityMap`를 추가하면 스키마에 직접 추가하는 모든 기본 ID를 재정의한다는 점을 기억하십시오. 의 섹션을 참조하십시오. `identityMap` 에서 [스키마 구성 안내서 기본 사항](../schema/composition.md#identityMap) 추가 정보.

에서 **[!UICONTROL 구조]** 편집기의 섹션에서 `loyaltyId` 필드 및 **[!UICONTROL ID]** 확인란 아래에 표시됩니다. **[!UICONTROL 필드 속성]**. 상자 및 옵션을 선택하여 다음과 같이 설정합니다. **[!UICONTROL 기본 ID]** 이 나타납니다. 이 상자도 선택하십시오.

>[!NOTE]
>
>각 스키마에는 기본 ID 필드가 하나만 포함될 수 있습니다. 스키마 필드를 기본 ID로 설정하면 나중에 스키마의 다른 ID 필드를 기본 ID로 설정하려고 하면 오류 메시지가 표시됩니다.

다음으로, **[!UICONTROL ID 네임스페이스]** 드롭다운에서 사전 정의된 네임스페이스 목록에서 을 선택합니다. 이후 `loyaltyId` 고객의 이메일 주소입니다. &quot;[!UICONTROL 이메일]&quot;&quot;을 클릭합니다. 선택 **[!UICONTROL 적용]** 업데이트 내용을 확인하려면 `loyaltyId` 필드.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>표준 네임스페이스 및 해당 정의 목록을 보려면 [[!DNL Identity Service] 설명서](../../identity-service/troubleshooting-guide.md#standard-namespaces).

변경 사항을 적용한 후 `loyaltyId` 는 이제 id 필드임을 나타내는 지문 기호를 표시합니다.

![](../images/tutorials/create-schema/identity-applied.png)

이제 `loyaltyId` 필드를 사용하여 해당 개인을 식별하고 해당 고객의 단일 보기를 함께 결합합니다. 에서 ID로 작업하는 방법에 대해 자세히 알아보려면 [!DNL Experience Platform]을(를) 검토하십시오 [[!DNL Identity Service]](../../identity-service/home.md) 설명서.

## 에서 사용할 스키마 활성화 [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) 의 id 데이터 활용 [!DNL Experience Platform] 각 개별 고객에 대한 전체적인 뷰를 제공합니다. 이 서비스는 고객 특성에 대한 강력한 360° 프로필 및 [!DNL Experience Platform].

에서 사용할 수 있도록 스키마를 활성화하려면 [!DNL Real-Time Customer Profile]에는 기본 ID가 정의되어 있어야 합니다. 기본 ID를 먼저 정의하지 않고 스키마를 활성화하려고 하면 오류 메시지가 표시됩니다.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

에서 사용할 &quot;충성도 멤버&quot; 스키마를 활성화하려면 [!DNL Profile], 을 선택하여 시작합니다.[!DNL Loyalty Members]&quot; **[!UICONTROL 구조]** 편집기의 섹션.

편집기 오른쪽에는 표시 이름, 설명 및 유형을 포함한 스키마에 대한 정보가 표시됩니다. 이 정보 외에 **[!UICONTROL 프로필]** 전환 단추.

![](../images/tutorials/create-schema/profile-toggle.png)

선택 **[!UICONTROL 프로필]** 에 대한 스키마를 활성화할지 확인하는 팝업 창이 나타납니다 [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>스키마를에 사용할 수 있게 되면 [!DNL Real-Time Customer Profile] 저장되고, 비활성화될 수 없습니다.

선택 **[!UICONTROL 활성화]** 을 클릭하여 선택 사항을 확인합니다. 을(를) 선택할 수 있습니다 **[!UICONTROL 프로필]** 원할 경우 다시 전환하여 스키마를 비활성화하되, 이후에 스키마가 저장되면 [!DNL Profile] 이 활성화되어 있으면 더 이상 비활성화할 수 없습니다.

## 다음 단계 및 추가 리소스

이제 스키마 작성을 완료했으므로 캔버스에서 전체 스키마를 볼 수 있습니다. 선택 **[!UICONTROL 저장]** 스키마는 [!DNL Schema Library], 다음을 통해 액세스할 수 있음 [!DNL Schema Registry].

이제 새 스키마를 사용하여에 데이터를 수집할 수 있습니다 [!DNL Platform]. 스키마를 사용하여 데이터를 수집하면 추가 변경만 수행할 수 있습니다. 자세한 내용은 [스키마 구성 기본 사항](../schema/composition.md) 스키마 버전 관리에 대한 자세한 내용은 를 참조하십시오.

이제 다음 자습서를 따르십시오. [UI에서 스키마 관계 정의](./relationship-ui.md) 를 추가하여 &quot;충성도 멤버&quot; 스키마에 새 관계 필드를 추가합니다.

&quot;충성도 멤버&quot; 스키마는 [!DNL Schema Registry] API. API 작업을 시작하려면 먼저 [[!DNL Schema Registry API] 개발자 안내서](../api/getting-started.md).

### 비디오 리소스

>[!WARNING]
>
>다음 [!DNL Platform] 다음 비디오에 표시된 UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

다음 비디오에서는 [!DNL Platform] UI.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

다음 비디오에서는 필드 그룹 및 클래스 작업에 대한 이해를 돕기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 부록

다음 섹션에서는 [!DNL Schema Editor].

### 새 클래스 만들기 {#create-new-class}

[!DNL Experience Platform] 는 조직에 고유한 클래스를 기반으로 스키마를 정의할 수 있는 유연성을 제공합니다. 새 클래스를 만드는 방법에 대해 알아보려면 [UI에서 클래스 만들기 및 편집](../ui/resources/classes.md#create).

### 스키마 클래스 변경 {#change-class}

스키마를 저장하기 전에 초기 구성 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재지정은 매우 신중하게 수행해야 합니다. 필드 그룹은 특정 클래스와 호환되기 때문에 클래스를 변경하면 캔버스 및 추가한 필드가 재설정됩니다.

스키마 클래스를 변경하는 방법에 대한 자세한 내용은 [UI에서 스키마 관리](../ui/resources/schemas.md).
