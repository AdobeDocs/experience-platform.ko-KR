---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 스키마 편집기를 사용하여 스키마 만들기
topic: tutorials
description: 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
translation-type: tm+mt
source-git-commit: f0d3aad649fa550443db0fc5168c848ae85fb459
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 0%

---


# Create a schema using the [!DNL Schema Editor]

Adobe Experience Platform 사용자 인터페이스를 사용하면 XDM(Interactive Visual Canvas) [!DNL Experience Data Model] 을 XDM(Schemas)이라고 하는 인터랙티브한 시각적 캔버스에서 스키마를 만들고 관리할 수 [!DNL Schema Editor]있습니다. 이 자습서에서는 스키마를 사용하는 방법을 설명합니다 [!DNL Schema Editor].

>[!NOTE]
>
>데모용으로 이 자습서의 단계에는 고객 충성도 프로그램 구성원을 설명하는 예제 스키마를 만드는 작업이 포함됩니다. 이러한 단계를 사용하여 자신만의 목적에 따라 다른 스키마를 생성할 수 있지만, 먼저 예제 스키마를 만들어 해당 기능을 배우는 것이 좋습니다 [!DNL Schema Editor].

대신 [!DNL Schema Registry] API를 사용하여 스키마를 작성하려는 경우 API를 사용하여 스키마를 [[!DNL Schema Registry] 만드는 자습서를 시도하기 전에 개발자 가이드](../api/getting-started.md) 읽기 [를 시작하십시오](create-schema-api.md).

## 시작하기

이 자습서에서는 스키마 만들기와 관련된 Adobe Experience Platform의 다양한 측면을 파악해야 합니다. 이 자습서를 시작하기 전에 다음 개념을 살펴보십시오.

* [[!DNL 경험 데이터 모델(XDM)]](../home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../schema/composition.md):클래스, 믹싱, 데이터 유형 및 필드를 비롯한 XDM 스키마 및 구성 요소에 대한 개요입니다.
* [[!DNL 실시간 고객 프로필]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 스키마 작업 공간에서 기존 [!UICONTROL 스키마] 찾아보기 {#browse}

UI의 [!UICONTROL 스키마] 작업 영역에서는 [!DNL Platform] 조직에 사용할 수 있는 스키마를 [!DNL Schema Library]관리할 수 있도록 시각화를 제공합니다. 작업 영역에는 이 자습서 전체에서 스키마를 작성할 수 있는 캔버스인 캔버스도 포함되어 있습니다. [!DNL Schema Editor]

로그인한 [!DNL Experience Platform]후 왼쪽 탐색 **[!UICONTROL 에서 스키마]** 를 선택하여 스키마 작업 **[!UICONTROL 영역을]** 엽니다. [ **[!UICONTROL 찾아보기]** ] 탭에는 사용자가 보고 사용자 정의할 수 있는 스키마 목록(표시 [!DNL Schema Library])이 표시됩니다. 이 목록에는 스키마의 기반이 되는 이름, 유형, 클래스 및 동작(레코드 또는 시간 시리즈)과 스키마를 마지막으로 수정한 날짜 및 시간이 포함됩니다.

클래스, 믹싱 및 데이터 형식을 포함하여 레지스트리의 모든 리소스에 대한 필터링 기능을 사용하려면 검색 막대 옆에 있는 필터 아이콘을 선택합니다. Adobe 또는 조직의 소유물인지 여부 및 리소스가 사용 가능하게 설정되어 있는지 여부를 기준으로 필터링할 수도 있습니다 [!DNL Real-time Customer Profile].

![](../images/tutorials/create-schema/schemas_filter.png)

## 스키마 만들기 및 이름 지정 {#create}

스키마 구성을 시작하려면 스키마 작업 **[!UICONTROL 영역의 오른쪽 위]** 모서리에서 스키마 **[!UICONTROL 만들기를]** 선택합니다. 핵심 클래스 XDM 개인 프로필 [!UICONTROL 및] XDM ExperienceEvent 중 하나를 선택할 수 있는 드롭다운 메뉴가 [!UICONTROL 나타납니다]. 이러한 클래스가 귀하의 목적에 맞지 않을 경우 **[!UICONTROL 찾아보기를]** 선택하여 사용 가능한 다른 클래스 [에서](#create-new-class)선택하거나 새 클래스를만들 수도 있습니다.

이 자습서를 사용하려면 XDM **[!UICONTROL 개별 프로필을 선택합니다]**.

![](../images/tutorials/create-schema/create_schema_button.png)

가 [!DNL Schema Editor] 나타납니다. 스키마를 작성할 캔버스입니다. 스키마를 기준으로 하는 표준 XDM 클래스를 선택했으므로, 편집기에 도착할 때 제목이 없는 스키마가 해당 클래스를 기반으로 하는 모든 스키마에 포함된 표준 필드와 함께 캔버스의 **[!UICONTROL 구조]** 섹션에 자동으로 생성됩니다. 스키마에 대해 할당된 클래스는 [컴포지션] 섹션의 **[!UICONTROL 클래스]** 아래에도 **[!UICONTROL 나열됩니다]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>스키마를 저장하기 전에 초기 작성 프로세스 중에 어느 시점에서나 스키마 [클래스를](#change-class) 변경할 수 있지만, 이 작업은 매우 신중하게 수행해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

편집기의 오른쪽에 있는 필드를 사용하여 스키마에 대한 표시 이름과 선택적 설명을 제공합니다. 이름을 입력했으면 캔버스가 스키마의 새 이름을 반영하도록 업데이트됩니다.

![](../images/tutorials/create-schema/name_schema.png)

스키마의 이름을 결정할 때 고려해야 할 몇 가지 중요한 사항이 있습니다.

* 스키마 이름은 나중에 스키마를 쉽게 찾을 수 있도록 짧고 설명이어야 합니다.
* 스키마 이름은 고유해야 합니다. 이는 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다. 예를 들어, 조직에서 서로 다른 브랜드에 대한 별도의 로열티 프로그램을 보유하고 있는 경우 나중에 정의할 수 있는 다른 충성도 관련 스키마와 쉽게 구별할 수 있도록 스키마 &quot;브랜드 a 충성도 구성원&quot;을 지정하는 것이 좋습니다.
* 스키마 설명을 사용하여 스키마에 대한 추가 컨텍스트 정보를 제공할 수도 있습니다.

이 자습서는 충성도 프로그램의 구성원과 관련된 데이터를 인제스트하는 스키마를 구성하므로 스키마의 이름은 &quot;충성도 구성원&quot;입니다.

## 혼합 추가 {#mixin}

이제 혼합을 추가하여 스키마에 필드를 추가할 수 있습니다. 혼합이란 특정 개념을 설명하기 위해 흔히 함께 사용되는 하나 이상의 들판으로 이루어진 그룹입니다. 이 자습서에서는 혼합을 사용하여 충성도 프로그램의 구성원을 설명하고 이름, 생일, 전화 번호, 주소 등과 같은 주요 정보를 캡처합니다.

믹스를 추가하려면 [믹싱] 하위 **[!UICONTROL 섹션에서]** [ **[!UICONTROL 추가]** ]를선택합니다.

![](../images/tutorials/create-schema/add_mixin_button.png)

사용 가능한 믹스의 목록이 표시된 새 대화 상자가 나타납니다. 각 혼합은 특정 클래스와 함께 사용하기 위한 것이므로 대화 상자에는 선택한 클래스(이 경우 [!DNL XDM Individual Profile] 클래스)와 호환되는 혼합만 나열됩니다. 표준 XDM 클래스를 사용하는 경우 혼합 목록이 사용 인기도에 따라 지능적으로 정렬됩니다.

![](../images/tutorials/create-schema/mixin-popularity.png)

목록에서 혼합을 선택하면 오른쪽 레일에 나타납니다. 원할 경우 여러 믹스를 선택하고 확인하기 전에 오른쪽 레일의 목록에 각 믹스를 추가할 수 있습니다. 또한 현재 선택된 믹스의 오른쪽에 아이콘이 표시되어 해당 믹스에서 제공하는 필드의 구조를 미리 볼 수 있습니다.

![](../images/tutorials/create-schema/preview-mixin-button.png)

혼합을 미리 볼 때 오른쪽 레일에 믹스인의 스키마에 대한 자세한 설명이 제공됩니다. 제공된 캔버스에서 믹스의 필드를 탐색할 수도 있습니다. 다른 필드를 선택하면 오른쪽 레일이 업데이트되어 해당 필드에 대한 세부 정보가 표시됩니다. 미리 **[!UICONTROL 보기가]** 끝나면 뒤로를 선택하여 혼합 선택 대화 상자로 돌아갑니다.

![](../images/tutorials/create-schema/preview-mixin.png)

이 튜토리얼의 경우 [프로필 **[!UICONTROL 인물 세부]** 정보]를 선택한 다음 [혼합 **[!UICONTROL 추가]를 선택합니다]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

스키마 캔버스가 다시 나타납니다. 이제 **[!UICONTROL 믹싱]** 섹션에 &quot;[!UICONTROL 프로필 인물 세부]사항 **[!UICONTROL &quot;이 표시되고]** 구조섹션에는 믹싱에 의해 작성된 필드가 포함됩니다. [혼합] 섹션 아래에서 **[!UICONTROL 혼합]** 이름을 선택하여 캔버스 내에서 제공하는 특정 필드를 강조할 수 있습니다.

![](../images/tutorials/create-schema/person_details_structure.png)

이 혼합은 데이터 유형 &quot; `person` 사람[!UICONTROL &quot;과 함께 최상위 수준 이름 아래 여러 필드]에 기여합니다. 이 필드 그룹은 이름, 생년월일, 성별 등 개인에 대한 정보를 설명합니다.

>[!NOTE]
>
>필드는 필드 내에 정의된 데이터 유형(공통 개념을 나타내는 필드 그룹)은 물론 문자열, 정수, 배열 또는 날짜와 같은 스칼라 유형을 사용할 수 있습니다 [!DNL Schema Registry].

이 필드에는 &quot; `name` 전체 이름&quot;이라는 데이터 유형이 있습니다. 이것은 일반적인 개념을 설명하며 이름, 성, 관례 제목 및 접미어 같은 이름 관련 하위 필드가 포함되어 있음을 의미합니다.

캔버스 내의 다른 필드를 선택하여 스키마 구조에 기여하는 추가 필드를 표시합니다.

## 다른 믹신 추가 {#mixin-2}

이제 동일한 단계를 반복하여 다른 믹스를 추가할 수 있습니다. 이번에 믹신 **[!UICONTROL 추가]** 대화 상자를 볼 때 &quot;프로필 개인 정보&quot; 혼합이 회색으로 표시되었고 그 옆의 확인란을 선택할 수 없습니다. 이렇게 하면 현재 스키마에 이미 포함되어 있는 믹스를 실수로 복제할 수 없습니다.

이 자습서의 경우 대화 상자에서 &quot;[!DNL Profile personal details]&quot; 믹싱을 선택한 다음 **[!UICONTROL 믹신]** 추가를 선택하여 스키마에 추가합니다.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

캔버스가 추가되면 다시 나타납니다. &quot;[!UICONTROL 프로필 개인 정보]&quot;가 이제 **[!UICONTROL 컴포지션]** 섹션 **[!UICONTROL 의]** Mixins 아래에 **[!UICONTROL 나열되고, 홈 주소, 휴대폰 등의 필드가 Structure에]**&#x200B;추가되었습니다.

필드 `name` 와 마찬가지로 방금 추가한 필드는 다중 필드 개념을 나타냅니다. 예를 들어 데이터 유형 &quot; `homeAddress` 우편 주소[!UICONTROL &quot;]가 있고 데이터 유형 &quot; `mobilePhone` 전화 번호[!UICONTROL &quot;가 있습니다]. 이러한 각 필드를 선택하여 확장하고 데이터 유형에 포함된 추가 필드를 볼 수 있습니다.

![](../images/tutorials/create-schema/personal_details_structure.png)

## 새로운 믹싱 정의 {#define-mixin}

&quot;[!UICONTROL 충성도 멤버]&quot; 스키마는 충성도 프로그램 멤버와 관련된 데이터를 캡처하기 위한 것으로 특정 충성도 관련 필드가 필요합니다. 필요한 필드가 포함된 표준 혼합이 없으므로 새 혼합을 정의해야 합니다.

이 때 [혼합 **[!UICONTROL 추가]** ] 대화 상자를 열 때 [새 **[!UICONTROL 혼합 만들기]를 선택합니다]**. 그러면 혼합에 대한 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]** 을제공하라는 메시지가 표시됩니다.

![](../images/tutorials/create-schema/mixin_create_new.png)

클래스 이름과 마찬가지로 혼합기 이름은 짧고 단순해야 스키마에 어떤 내용이 기여할 것인지 설명합니다. 이 두 가지 모두 고유하므로 이름을 다시 사용할 수 없으므로 해당 이름이 충분한지 확인해야 합니다.

이 튜토리얼의 경우 새로운 믹스의 이름을 &quot;[!UICONTROL 충성도 세부 정보&quot;로 지정합니다].

[ **[!UICONTROL 혼합]** 추가]를 선택하여 로 돌아갑니다 [!DNL Schema Editor]. 이제 캔버스 왼쪽[!UICONTROL 의]믹싱 아래에 &quot; **[!UICONTROL 충성도 세부 정보]** &quot;가 표시되어야 하지만 아직 여기에 연결된 필드가 없으므로 **[!UICONTROL 구조]**&#x200B;아래에 새 필드가 나타나지 않습니다.

## 믹스에 필드 추가 {#mixin-fields}

이제 &quot;[!UICONTROL 충성도 세부 정보]&quot; 조합을 만들었으므로 혼합이 스키마에 기여할 필드를 정의할 때입니다.

시작하려면 [믹싱] 섹션에서 **[!UICONTROL 혼합 이름을]** 선택합니다. 이렇게 하면 믹스의 속성이 편집기의 오른쪽에 나타나고 [구조] 아래의 스키마 이름 옆에 [필드 **[!UICONTROL 추가]** ] 단추가 **[!UICONTROL 나타납니다]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

&quot; **[!UICONTROL Add field]** next to &quot;[!DNL Loyalty Members]to create a new node in the structure. 이 노드 `_tenantId` (이 예에서 호출됨)는 IMS 조직의 테넌트 ID 앞에 밑줄이 있는 것을 나타냅니다. 테넌트 ID가 존재하면 추가할 필드가 조직의 네임스페이스에 포함되어 있음을 나타냅니다.

즉, 추가하려는 필드는 조직에 고유하며 조직만 액세스할 수 있는 특정 영역 [!DNL Schema Registry] 에 저장됩니다. 정의한 필드는 항상 테넌트 네임스페이스에 추가되어야 다른 표준 클래스, 혼합, 데이터 유형 및 필드의 이름과 충돌하지 않습니다.

해당 네임스페이스 노드 안은 &quot;[!UICONTROL 새 필드&quot;입니다]. 이것은 &quot;[!UICONTROL 충성도 세부 사항]&quot; 혼합의 시작이다.

![](../images/tutorials/create-schema/new_field_loyalty.png)

편집기의 오른쪽에 있는 컨트롤을 사용하여 우선 충성도 관련 필드를 유지하는 데 사용할 &quot; `loyalty` 개체&quot; 형식의 필드를 만듭니다. 완료되면 적용을 **[!UICONTROL 선택합니다]**.

![](../images/tutorials/create-schema/loyalty_object.png)

변경 사항이 적용되고 새로 만든 `loyalty` 개체가 나타납니다. 개체 **[!UICONTROL 옆에 있는 필드]** 추가를 선택하여 충성도 관련 필드를 추가합니다. &quot;[!UICONTROL 새 필드]&quot;가 나타나고 **[!UICONTROL 필드 속성]** 섹션이 캔버스 오른쪽에 표시됩니다.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

각 필드에는 다음 정보가 필요합니다.

* **[!UICONTROL 필드 이름]:** 낙타라고 적힌 들판 이름. 예:충성도 수준
* **[!UICONTROL 표시 이름]:** 제목 케이스에 기록된 필드의 이름입니다. 예:충성도 수준
* **[!UICONTROL 유형]:** 필드의 데이터 유형입니다. 여기에는 기본 스칼라 형식과 에 정의된 모든 데이터 유형이 포함됩니다 [!DNL Schema Registry]. 예: [!UICONTROL 문자열]정수, [!UICONTROL 부울], [!UICONTROL 개인],주소,전화 번호, 등
* **[!UICONTROL 설명]:** 문장에 200자까지 입력할 수 있는 선택적 필드 설명이 포함되어야 합니다.

객체의 첫 번째 필드는 `Loyalty` 문자열 `loyaltyId`입니다. 새 필드의 유형을 &quot;[!UICONTROL 문자열]&quot;로 설정할 때 **[!UICONTROL 필드 속성]****[!UICONTROL 섹션은 기본 값]**, 형식 **[!UICONTROL 및 최대 길이]**&#x200B;를 포함하여 **[!UICONTROL 기본 값]**,형식 및 최대 길이 제한을 적용하기 위한 몇 가지 옵션으로 채워집니다.

![](../images/tutorials/create-schema/string_constraints.png)

선택한 데이터 유형에 따라 다른 제한 옵션을 사용할 수 있습니다. 이메일 주소 `loyaltyId` 가 되므로 형식[!UICONTROL 드롭다운 메뉴에서 &quot;]이메일 **[!UICONTROL &quot;을]** 선택합니다. 적용을 **[!UICONTROL 선택하여]** 변경 사항을 적용합니다.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 믹스에 필드 추가 {#mixin-fields-2}

이제 필드를 추가했으므로 추가 필드를 추가하여 다음과 같은 충성도 관련 정보를 캡처할 수 있습니다. `loyaltyId`

* 포인트(정수)
* 멤버-이후(날짜)

개체 필드 **[!UICONTROL 를]** 선택하고 필요한 정보를 입력하여 각 필드가 `loyalty` 추가됩니다.

완료되면 충성도 개체에는 충성도 ID, 포인트 및 멤버 등록 필드가 포함됩니다.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 혼합에 열거형 필드 추가 {#enum}

에서 필드를 정의할 때 필드 [!DNL Schema Editor]에 포함할 수 있는 데이터에 대한 추가 제한을 제공하기 위해 기본 필드 유형에 적용할 수 있는 몇 가지 추가 옵션이 있습니다. 이러한 제한 사항에 대한 사용 사례는 다음 표에 설명되어 있습니다.

| 제한 | 설명 |
| --- | --- |
| [!UICONTROL 필수 여부] | 데이터 수집에 필드가 필수임을 나타냅니다. 이 필드를 포함하지 않는 이 스키마를 기반으로 데이터 세트에 업로드한 데이터는 수집 시 실패합니다. |
| [!UICONTROL Array] | 필드에 데이터 유형이 지정된 값 배열을 포함함을 나타냅니다. 예를 들어 데이터 유형이 &quot;[!UICONTROL String]&quot;인 필드에 이 제약 조건을 사용하면 필드에 문자열 배열이 포함되도록 지정합니다. |
| [!UICONTROL 열거형] | 이 필드에 가능한 값의 열거형 목록의 값 중 하나가 포함되어야 함을 나타냅니다. |
| [!UICONTROL ID] | 이 필드가 ID 필드임을 나타냅니다. ID 필드에 대한 자세한 내용은 이 자습서 [후반부에서 제공됩니다](#identity-field). |
| [!UICONTROL 관계] | 스키마 관계는 조합 스키마 및 조합 스키마 사용을 통해 유추할 수 있지만, 이 [!DNL Real-time Customer Profile]는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 관계 [!UICONTROL 제약 조건은 이 필드가 다른 클래스를 기반으로 한 스키마의 기본 ID를 참조하고 두 스키마 간의 관계를 의미함을 나타냅니다] . 자세한 내용은 관계 [를](./relationship-ui.md) 정의하는 자습서를 참조하십시오. |

이 자습서의 경우 스키마의 [!DNL "loyalty"] 개체에는 고객의 &quot;충성도 수준&quot;을 설명하는 새 열거형 필드가 필요합니다. 여기서 값은 가능한 네 가지 옵션 중 하나만 사용할 수 있습니다. 이 필드를 스키마에 추가하려면 개체 옆에 있는 필드 **[!UICONTROL 추가]** 를 `loyalty` 선택하고 필드 이름 **[!UICONTROL 및]** 표시 이름에 필요한 필드를 **[!UICONTROL 채웁니다]**. 유형 **[!UICONTROL 에]**&#x200B;대해 &quot;[!UICONTROL 문자열]&quot;을 선택합니다.

![](../images/tutorials/create-schema/loyalty-level-type.png)

배열, 열거형 **[!UICONTROL 및]** ID에 대한 확인란을 포함하여 해당 유형을 선택한 후에 필드에 대한 추가 확인란은 **[!UICONTROL 나타납니다]******.

열거형 **[!UICONTROL 확인란을]** 선택하여 아래의 **[!UICONTROL 열거형 값]** 섹션을 엽니다. 여기에서 허용 가능한 각 충성도 수준에 대해 **[!UICONTROL 값]** (camelCase) 및 **[!UICONTROL 레이블]** (제목 케이스의 경우 독자가 친근한 이름 선택 사항)을 입력할 수 있습니다.

모든 필드 속성을 완료한 경우 **[!UICONTROL 적용을]** 선택하여[!DNL loyaltyLevel]개체에 &quot; `loyalty` &quot; 필드를추가합니다.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 다중 필드 개체를 데이터 형식으로 변환 {#datatype}

이제 개체에는 몇 개의 로열티별 필드가 포함되어 있으며 다른 스키마에서 유용할 수 있는 일반적인 데이터 구조를 나타냅니다. `loyalty` 이 도구 [!DNL Schema Editor] 를 사용하면 재사용 가능한 다중 필드 개체를 해당 개체의 구조를 데이터 형식으로 변환하여 쉽게 적용할 수 있습니다.

데이터 유형을 사용하면 여러 필드 구조를 일관되게 사용할 수 있으며 스키마 내의 어느 곳에서나 사용할 수 있으므로 혼합보다 더 유연하게 사용할 수 있습니다. 이 작업은 필드의 **[!UICONTROL 유형]** 값을 에 정의된 데이터 유형의 값으로 설정하여 [!DNL Schema Registry]수행합니다.

개체를 데이터 형식으로 변환하려면 `loyalty` 구조 `loyalty` 아래의 필드 **[!UICONTROL 를 선택한 다음]**&#x200B;필드 속성 아래에 있는 편집기의 오른쪽에 있는 새 데이터 형식으로 **[!UICONTROL 변환을]** ****&#x200B;선택합니다. 개체가 성공적으로 변환되었음을 확인하는 녹색 팝업이 나타납니다.

![](../images/tutorials/create-schema/convert-data-type.png)

이제 **[!UICONTROL 구조]**&#x200B;아래에서 `loyalty`[!DNL Loyalty]보면, 필드에 데이터 유형이 &quot;&quot;이고 필드 옆에 필드가 작은 잠금 아이콘이 있다는 것을 알 수 있습니다. 이는 필드가 더 이상 개별 필드가 아니라 다중 필드 데이터 유형의 일부임을 나타냅니다.

![](../images/tutorials/create-schema/loyalty_data_type.png)

이후 스키마에서, 이제 &quot; **[!UICONTROL 유형]** &quot;에 필드를 할당할 수 있으며 ID, 충성도 수준, 이후의 멤버 및 포인트에 대한[!DNL Loyalty]필드가 자동으로 포함됩니다.

## 스키마 필드 검색 및 필터링

이제 스키마에는 기본 클래스에서 제공하는 필드 외에 여러 개의 혼합이 포함됩니다. 큰 스키마를 사용하는 경우 왼쪽 레일의 혼합 이름 옆에 있는 확인란을 선택하여 표시되는 필드를 관심 있는 믹스에서만 제공하는 필드로 필터링할 수 있습니다.

![](../images/tutorials/create-schema/filter-by-mixin.png)

스키마에서 특정 필드를 찾는 경우 검색 막대를 사용하여 표시되는 필드를 이름에 따라 필터링할 수도 있습니다.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>검색 함수는 일치하는 필드를 표시할 때 선택한 믹신 필터를 고려합니다. 검색 쿼리가 원하는 결과를 표시하지 않는 경우 관련 혼합을 필터링하지 않고 있는지 다시 확인해야 합니다.

## 스키마 필드를 ID 필드로 설정 {#identity-field}

스키마가 제공하는 표준 데이터 구조를 활용하여 여러 소스에서 동일한 개인에 속하는 데이터를 식별할 수 있으므로 세분화, 보고, 데이터 과학 분석 등과 같은 다양한 다운스트림 사용 사례를 허용할 수 있습니다. 개별 ID를 기반으로 데이터를 똑바르게 하려면 해당 스키마 내에서 키 필드를 [!UICONTROL ID] 필드로 표시해야 합니다.

[!DNL Experience Platform] 의 ID 확인란을 사용하여 ID 필드를 쉽게 **[!UICONTROL 나타낼]** 수 [!DNL Schema Editor]있습니다. 하지만 데이터의 특성에 따라 ID로 사용할 수 있는 가장 적합한 필드를 결정해야 합니다.

예를 들어 동일한 &quot;충성도 수준&quot;에 속한 수천 명의 로열티 프로그램 멤버가 있을 수 있지만 로열티 프로그램의 각 멤버에는 고유한(이 경우 개별 멤버의 이메일 주소)이 있습니다. `loyaltyId` 각 멤버 `loyaltyId` 의 고유 식별자이기 때문에 ID 필드에 적합한 후보가 되는 반면 ID 필드는 사용할 수 `loyaltyLevel` 없습니다.

>[!IMPORTANT]
>
>아래 단계에는 기존 스키마 필드에 ID 설명자를 추가하는 방법이 나와 있습니다. 스키마 자체의 구조 내에서 ID 필드를 정의하는 대신 필드를 사용하여 ID 정보를 대신 포함할 수도 있습니다. `identityMap`
>
>사용을 계획하는 경우 스키마에 직접 추가하는 기본 ID를 `identityMap`재정의한다는 점을 명심하십시오. 자세한 내용은 스키마 구성 안내서 `identityMap` 의 [기본](../schema/composition.md#identityMap) 섹션을 참조하십시오.

편집기의 **[!UICONTROL 구조]** 섹션 `loyaltyId` 에서 필드를 선택하면 필드 속성 아래에 **[!UICONTROL ID]** 확인란이 **[!UICONTROL 나타납니다]**. 기본 ID로 설정하는 옵션과 상자를 **[!UICONTROL 선택합니다]** . 이 상자도 선택하십시오.

>[!NOTE]
>
>각 스키마에는 기본 ID 필드가 하나만 포함될 수 있습니다. 스키마 필드가 기본 ID로 설정되면 나중에 스키마의 다른 ID 필드를 기본 ID로 설정하려고 하면 오류 메시지가 표시됩니다.

그런 다음 드롭다운에서 미리 정의된 네임스페이스 **** 목록에서 Identity 네임스페이스를 제공해야 합니다. 고객의 이메일 주소 `loyaltyId` 이므로 드롭다운에서 &quot;[!UICONTROL 이메일]&quot;을 선택합니다. 적용 **[!UICONTROL 을]** 선택하여 `loyaltyId` 필드 업데이트를 확인합니다.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>표준 네임스페이스와 그 정의 목록은 [[!DNL Identity Service] 설명서를 참조하십시오](../../identity-service/troubleshooting-guide.md#standard-namespaces).

변경 사항을 적용한 후 의 아이콘은 이제 ID 필드임을 나타내는 지문 기호를 `loyaltyId` 표시합니다. 또한 왼쪽 레일의 [!DNL Loyalty Details] 혼합은 그 아래에 ID 필드를 나열하므로 스키마의 ID 필드가 어떤 혼합인지 쉽게 확인할 수 있습니다.

![](../images/tutorials/create-schema/identity-applied.png)

이제 `loyaltyId` 필드로 인제스트된 모든 데이터는 해당 고객을 식별하고 해당 고객의 한 보기를 연결하는 데 사용됩니다. ID 작업에 대한 자세한 내용 [!DNL Experience Platform]은 [[!DNL Identity Service]](../../identity-service/home.md) 설명서를 참조하십시오.

## 스키마를 [!DNL Real-time Customer Profile] {#profile}

[[!DNL 실시간 고객 프로필]](../../profile/home.md) ID 데이터 [!DNL Experience Platform] 를 활용하여 각 개별 고객을 전체적으로 파악합니다. 이 서비스는 고객 속성에 대한 360도 프로파일을 구축하고 고객과 통합된 모든 시스템에서 타임스탬프가 지정된 계정을 생성하며, [!DNL Experience Platform]

스키마는 함께 사용할 수 있도록 [!DNL Real-time Customer Profile]하려면 기본 ID가 정의되어 있어야 합니다. 주 ID를 먼저 정의하지 않고 스키마를 활성화하려고 하면 오류 메시지가 표시됩니다.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

에서 사용할 &quot;충성도 멤버&quot; 스키마를 활성화하려면 편집기의 [!DNL Profile]구조[!DNL Loyalty Members]섹션에서 &quot; **[!UICONTROL &quot;을]** 선택합니다.

편집기의 오른쪽에는 표시 이름, 설명 및 유형을 비롯한 스키마에 대한 정보가 표시됩니다. 이 정보 외에도 프로필 **[!UICONTROL 전환]** 단추가 있습니다.

![](../images/tutorials/create-schema/profile-toggle.png)

프로파일 **[!UICONTROL 을]** 선택하면 팝업 창이 나타나면서 스키마를 활성화할지 여부를 확인하는 메시지가 나타납니다 [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>스키마를 사용하도록 설정하고 저장한 후에는 [!DNL Real-time Customer Profile] 비활성화할 수 없습니다.

활성화를 **[!UICONTROL 선택하여]** 선택을 확인합니다. 원할 경우 **[!UICONTROL 프로필]** 토글을 다시 선택하여 스키마를 비활성화할 수 있지만 스키마를 활성화한 상태에서 스키마를 저장한 후에는 더 이상 비활성화할 수 [!DNL Profile] 없습니다.

## 다음 단계 및 추가 리소스

스키마 구성을 마쳤으면 캔버스에서 전체 스키마를 볼 수 있습니다. 저장 **[!UICONTROL 을]** 선택하면 스키마는 [!DNL Schema Library]에 저장되므로 사용자가 액세스할 수 [!DNL Schema Registry]있습니다.

이제 새 스키마를 사용하여 데이터를 인제스트할 수 있습니다 [!DNL Platform]. 스키마를 사용하여 데이터를 인제스트하면 추가 변경만 가능합니다. 스키마 버전 관리에 대한 자세한 내용은 [스키마](../schema/composition.md) 구성의 기본 사항을 참조하십시오.

이제 UI에서 스키마 관계 [를 정의하는 자습서에 따라 &quot;충성도](./relationship-ui.md) 멤버&quot; 스키마에 새 관계 필드를 추가할 수 있습니다.

&quot;충성도 멤버&quot; 스키마는 [!DNL Schema Registry] API를 사용하여 보고 관리할 수도 있습니다. API 작업을 시작하려면 먼저 [[!DNL Schema Registry API] 개발자 안내서를 읽어 봅니다](../api/getting-started.md).

### 비디오 리소스

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

다음 비디오에서는 [!DNL Platform] UI에서 간단한 스키마를 만드는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

다음 비디오에서는 혼합기 및 수업 사용에 대한 이해를 높이기 위해 제작되었습니다.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 부록

다음 절에서는 의 사용과 관련된 추가 정보를 제공합니다 [!DNL Schema Editor].

### Create a new class {#create-new-class}

[!DNL Experience Platform] 조직에 고유한 클래스를 기반으로 스키마를 정의할 수 있는 유연성을 제공합니다.

스키마 작업 **[!UICONTROL 공간]** 에서 ****&#x200B;스키마 **[!UICONTROL 만들기를 선택한 다음 드롭다운에서]** 찾아보기를 선택합니다.

![](../images/tutorials/create-schema/browse-classes.png)

사용 가능한 클래스 목록에서 선택할 수 있는 대화 상자가 나타납니다. 대화 상자의 맨 위에서 새 클래스 **[!UICONTROL 만들기를 선택합니다]**. 그런 다음 새 클래스에 **[!UICONTROL 표시 이름]** (클래스에 대한 짧고 설명적이며 고유하며 사용자에게 친숙한 이름) **[!UICONTROL , 설명]**, 그리고 **[!UICONTROL 행동]** (&quot;Record&quot;[!UICONTROL 또는 &quot;BehaviorTime Series&quot;라고 정의되는 데이터 스키마에 대해]Display 이름[!UICONTROL (&quot;A RecordTime SeriesA BehaviorBehaviorBehavior]&quot;)을제공할 수 있습니다.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>조직에서 정의한 클래스를 구현하는 스키마를 빌드할 때는 mixins를 호환되는 클래스에서만 사용할 수 있다는 점을 참고하십시오. 정의한 클래스는 새로 만들어지므로 [혼합 **[!UICONTROL 추가] 대화 상자에 나열된 호환 가능한 믹스가]** 없습니다. 대신 [새 믹싱 **[!UICONTROL 만들기]를]** 선택하고 해당 클래스에 사용할 믹신을 정의해야 합니다. 다음에 새 클래스를 구현하는 스키마를 작성할 때 정의한 혼합이 나열되고 사용할 수 있습니다.

### 스키마 클래스 변경 {#change-class}

스키마를 저장하기 전에 초기 작성 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재지정은 매우 신중하게 해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

클래스를 재할당하려면 캔버스의 **[!UICONTROL 왼쪽에서 [할당]** ]을 선택합니다.

![](../images/tutorials/create-schema/assign_class_button.png)

조직에서 정의한 모든 클래스(소유자가 &quot;[!UICONTROL 고객]&quot;) 및 Adobe에서 정의된 표준 클래스를 포함하여 사용 가능한 모든 클래스의 목록을 표시하는 대화 상자가 나타납니다.

목록에서 클래스를 선택하여 대화 상자의 오른쪽에 해당 설명을 표시합니다. 클래스 구조 **[!UICONTROL 미리 보기를 선택하여]** 클래스와 연관된 필드 및 메타데이터를 볼 수도 있습니다. 계속하려면 **[!UICONTROL 클래스]** 할당을 선택합니다.

![](../images/tutorials/create-schema/assign_class.png)

새 클래스를 지정할지 여부를 확인하는 새 대화 상자가 열립니다. 할당을 **[!UICONTROL 선택하여]** 확인합니다.

![](../images/tutorials/create-schema/assign-confirm.png)

클래스 변경을 확인한 후 캔버스가 재설정되고 모든 컴포지션 진행 상태가 손실됩니다.