---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 스키마 편집기를 사용하여 스키마 만들기
topic: tutorial
type: Tutorial
description: 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
translation-type: tm+mt
source-git-commit: 26c3aa3b21c2d9850f29816d57ddf2da953d6b10
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 0%

---


# 스키마 만들기 [!DNL Schema Editor]

Adobe Experience Platform 사용자 인터페이스를 사용하면 XDM(Interactive Visual Canvas)을 통해 XDM( [!DNL Experience Data Model] Schemas) 스키마를 만들고 관리할 수 [!DNL Schema Editor]있습니다. 이 자습서에서는 을 사용하여 스키마를 만드는 방법을 설명합니다 [!DNL Schema Editor].

>[!NOTE]
>
>데모용으로 이 자습서의 단계에는 고객 충성도 프로그램의 구성원을 설명하는 예제 스키마를 만드는 작업이 포함됩니다. 이러한 단계를 사용하여 고유한 목적으로 다른 스키마를 만들 수 있지만, 먼저 예제 스키마 만들기와 함께 예제 스키마를 만들어 해당 기능을 배우는 것이 좋습니다 [!DNL Schema Editor].

대신 [!DNL Schema Registry] API를 사용하여 스키마를 작성하려는 경우 API를 사용하여 스키마 [[!DNL Schema Registry] 를 만드는 방법에 대한 자습서를 시도하기 전에](../api/getting-started.md) 개발자 가이드 [읽기](create-schema-api.md)를 시작합니다.

## 시작하기

이 자습서에서는 스키마 만들기와 관련된 Adobe Experience Platform의 다양한 측면을 파악해야 합니다. 이 자습서를 시작하기 전에 다음 개념에 대한 설명서를 검토하십시오.

* [[!DNL Experience Data Model (XDM)]](../home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크.
   * [스키마 컴포지션의 기본 사항](../schema/composition.md):클래스, 믹싱, 데이터 유형 및 필드를 비롯한 XDM 스키마 및 구성 요소에 대한 개요입니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 스키마 작업 [!UICONTROL 공간] 열기 {#browse}

UI의 [!UICONTROL 스키마] 작업 영역에서는 [!DNL Platform] 조직에 사용할 수 있는 스키마를 [!DNL Schema Library]관리할 수 있도록 시각화를 제공합니다. 작업 영역에는 이 자습서 [!DNL Schema Editor]를 통해 스키마를 구성할 수 있는 캔버스도 포함되어 있습니다.

로그인한 [!DNL Experience Platform]후 왼쪽 탐색 **[!UICONTROL 에서 스키마]** 를 선택하여 스키마 작업 **[!UICONTROL 영역을]** 엽니다. [ **[!UICONTROL 찾아보기]** ] 탭에는 사용자가 보고 사용자 정의할 수 있는 스키마 목록(표시 [!DNL Schema Library])이 표시됩니다. 이 목록에는 스키마 기반이 되는 이름, 유형, 클래스 및 비헤이비어(레코드 또는 시간 시리즈)와 스키마를 마지막으로 수정한 날짜 및 시간이 포함됩니다.

자세한 내용은 UI의 기존 [XDM 리소스](./explore.md) 탐색에 대한 가이드를 참조하십시오.

## 스키마 만들기 및 이름 지정 {#create}

스키마 구성을 시작하려면 스키마 작업 영역의 오른쪽 위 **[!UICONTROL 모서리에서 스키마]** 만들기를 **[!UICONTROL 선택합니다]** . 핵심 클래스 XDM 개별 프로필 [!UICONTROL 및 XDM ExperienceEvent 중 하나를 선택할 수 있는] 드롭다운 메뉴가 [!UICONTROL 나타납니다]. 이러한 클래스가 귀하의 목적에 맞지 않을 경우 [ **[!UICONTROL 찾아보기]** ]를 선택하여 사용 가능한 다른 클래스 중에서 선택하거나 새 클래스를 [만들 수도 있습니다](#create-new-class).

이 자습서를 사용하려면 XDM **[!UICONTROL 개별 프로필을 선택합니다]**.

![](../images/tutorials/create-schema/create_schema_button.png)

이 [!DNL Schema Editor] 나타납니다. 스키마를 작성할 캔버스입니다. 스키마를 기준으로 하는 표준 XDM 클래스를 선택했으므로 편집기에 도착할 때 제목이 없는 스키마는 해당 클래스를 기반으로 하는 모든 스키마에 포함된 표준 필드와 함께 **[!UICONTROL 캔버스의 구조]** 섹션에 자동으로 생성됩니다. 스키마에 대해 할당된 클래스는 컴포지션 섹션의 **[!UICONTROL 클래스]** 아래에도 **[!UICONTROL 나열됩니다]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>스키마가 저장되기 전에 초기 구성 프로세스 중에 언제든지 스키마 [클래스를](#change-class) 변경할 수 있지만 이는 매우 신중하게 수행해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

편집기의 오른쪽에 있는 필드를 사용하여 스키마에 대한 표시 이름 및 선택적 설명을 제공합니다. 이름을 입력하면 캔버스가 스키마의 새 이름을 반영하도록 업데이트됩니다.

![](../images/tutorials/create-schema/name_schema.png)

스키마 이름을 결정할 때 고려해야 할 몇 가지 중요한 사항이 있습니다.

* 나중에 스키마를 쉽게 찾을 수 있도록 스키마 이름은 짧고 설명이어야 합니다.
* 스키마 이름은 고유해야 합니다. 이는 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다. 예를 들어 조직에 다른 브랜드에 대한 별도의 로열티 프로그램이 있는 경우 나중에 정의할 수 있는 다른 로열티 관련 스키마와 쉽게 구별되도록 스키마 &quot;브랜드 a 충성도 구성원&quot;을 지정하는 것이 좋습니다.
* 스키마 설명을 사용하여 스키마에 대한 추가 컨텍스트 정보를 제공할 수도 있습니다.

이 자습서는 충성도 프로그램 구성원과 관련된 데이터를 인제스트하는 스키마를 구성하므로 스키마의 이름은 &quot;충성도 구성원&quot;입니다.

## 혼합 추가 {#mixin}

이제 믹스를 추가하여 스키마에 필드를 추가할 수 있습니다. 혼합은 특정 개념을 묘사하는 데 주로 함께 사용되는 하나 이상의 필드 그룹입니다. 이 자습서에서는 혼합을 사용하여 로열티 프로그램의 구성원을 설명하고 이름, 생일, 전화번호, 주소 등 주요 정보를 수집합니다.

믹싱을 추가하려면 [믹싱] **[!UICONTROL 하위 섹션]** 에서 [ **[!UICONTROL 추가]** ]를선택합니다.

![](../images/tutorials/create-schema/add_mixin_button.png)

사용 가능한 믹스의 목록을 표시하는 새 대화 상자가 나타납니다. 각 믹스는 특정 클래스와 함께 사용하기 위한 것이므로 대화 상자에는 선택한 클래스(이 경우 [!DNL XDM Individual Profile] 클래스)와 호환되는 믹스만 나열됩니다. 표준 XDM 클래스를 사용하는 경우 혼합 목록이 사용 인기도에 따라 지능적으로 정렬됩니다.

![](../images/tutorials/create-schema/mixin-popularity.png)

목록에서 혼합을 선택하면 오른쪽 레일에 나타납니다. 원할 경우 여러 믹스를 선택하고 확인하기 전에 오른쪽 레일의 목록에 각 믹스를 추가할 수 있습니다. 또한 현재 선택된 믹스의 오른쪽에 아이콘이 표시되어 해당 믹스에서 제공하는 필드의 구조를 미리 볼 수 있습니다.

![](../images/tutorials/create-schema/preview-mixin-button.png)

믹싱을 미리 볼 때 오른쪽 레일에 믹스의 스키마에 대한 자세한 설명이 제공됩니다. 제공된 캔버스에서 믹스의 필드를 탐색할 수도 있습니다. 다른 필드를 선택하면 오른쪽 레일이 업데이트되어 해당 필드에 대한 세부 정보가 표시됩니다. 미리 **[!UICONTROL 보기를]** 마치면 [뒤로]를 선택하여 혼합 선택 대화 상자로 돌아갑니다.

![](../images/tutorials/create-schema/preview-mixin.png)

이 자습서에서 인구 통계 **[!UICONTROL 세부]** 정보 믹싱을 선택한 다음 혼합 **[!UICONTROL 추가를 선택합니다]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

스키마 캔버스가 다시 나타납니다. 이제 **[!UICONTROL 혼합]** 섹션에 &quot;[!UICONTROL 인구 통계 세부]사항 **[!UICONTROL &quot;이 나열되고]** 구조섹션에는 믹싱에 의해 기고한 필드가 포함됩니다. [혼합] 섹션 아래에서 **[!UICONTROL 믹스의]** 이름을 선택하여 캔버스 내에서 제공하는 특정 필드를 강조할 수 있습니다.

![](../images/tutorials/create-schema/person_details_structure.png)

이 혼합은 데이터 유형이 &quot;사람&quot;인 최상위 수준 이름 아래 `person` 의 여러 필드에[!UICONTROL 기여합니다]. 이 필드 그룹은 이름, 생년월일, 성별 등 개인에 대한 정보를 설명합니다.

>[!NOTE]
>
>필드는 에 정의된 데이터 유형(일반적인 개념을 나타내는 필드 그룹)은 물론 문자열, 정수, 배열 또는 날짜와 같은 스칼라 유형을 사용할 수 있습니다 [!DNL Schema Registry].

필드에 &quot; `name` 사람 이름&quot;의 데이터 유형이 있습니다. 이것은 일반적인 개념을 설명하고 이름, 성, 관례 제목 및 접미어 등과 같은 이름 관련 하위 필드를 포함합니다.

캔버스 내의 다른 필드를 선택하여 스키마 구조에 기여하는 추가 필드를 표시합니다.

## 다른 믹싱 추가 {#mixin-2}

이제 동일한 단계를 반복하여 다른 믹싱을 추가할 수 있습니다. 이번에는 [믹서 **[!UICONTROL 추가]** ] 대화 상자를 볼 때 &quot;[!UICONTROL 인구 통계학적]정보&quot; 혼합이 회색으로 처리되었으며 그 옆에 있는 확인란을 선택할 수 없습니다. 이렇게 하면 현재 스키마에 이미 포함된 믹스를 실수로 복제할 수 없습니다.

이 자습서의 경우 대화 상자에서 &quot;[!DNL Personal Contact Details]&quot; 믹싱을 선택한 다음 **[!UICONTROL 믹싱]** 추가를 선택하여 스키마에 추가합니다.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

일단 추가되면 캔버스가 다시 나타납니다. &quot;[!UICONTROL Personal Contact Details]&quot;는 이제 **[!UICONTROL 컴포지션]****[!UICONTROL 섹션의 Mixin에]** 나열되어 있으며 Structure에 집 주소, 휴대폰 등을 위한 필드가 ****&#x200B;추가되었습니다.

필드와 `name` 유사하게, 방금 추가한 필드는 다중 필드 개념을 나타냅니다. 예를 들어, 데이터 유형 &quot; `homeAddress` 우편 주소[!UICONTROL &quot;가 있고]데이터 유형이 &quot; `mobilePhone` 전화 번호[!UICONTROL &quot;입니다]. 이러한 각 필드를 선택하여 확장하고 데이터 유형에 포함된 추가 필드를 볼 수 있습니다.

![](../images/tutorials/create-schema/personal_details_structure.png)

## 새 믹싱 정의 {#define-mixin}

&quot;[!UICONTROL 충성도 멤버]&quot; 스키마는 충성도 프로그램 멤버와 관련된 데이터를 캡처하기 위한 것으로, 따라서 특정 충성도 관련 필드가 필요합니다. 필요한 필드를 포함하는 표준 믹싱이 없으므로 새 믹싱을 정의해야 합니다.

이번에는 [혼합 추가] 대화 상자를 **[!UICONTROL 열]** 때 [새 **[!UICONTROL 혼합 만들기]를 선택합니다]**. 그러면 혼합에 대한 표시 이름과 설명을 입력하라는 메시지가 표시됩니다.

![](../images/tutorials/create-schema/mixin_create_new.png)

클래스 이름과 마찬가지로 혼합기 이름은 짧고 단순해야 스키마에 어떤 내용이 기여하는지 설명합니다. 이러한 구성 요소도 고유하므로 이름을 다시 사용할 수 없으므로 해당 이름이 적절한지 확인해야 합니다.

이 튜토리얼의 경우 새로운 믹스의 이름을 &quot;충성도 세부 사항&quot;으로 지정합니다.

[ **[!UICONTROL 혼합]** 추가]를 선택하여 로 [!DNL Schema Editor]돌아갑니다. 이제 &quot;[!UICONTROL 충성도 세부]사항 **[!UICONTROL &quot;이 캔버스 왼쪽]** 의 믹싱 **[!UICONTROL 아래에 표시되지만 아직 연결된 필드가 없으므로]**&#x200B;구조아래에 새 필드가 나타나지 않습니다.

## 믹스에 필드 추가 {#mixin-fields}

이제 &quot;충성도 세부 사항&quot; 믹싱을 만들었으므로 믹싱이 스키마에 기여할 필드를 정의할 때가 되었습니다.

먼저 [믹싱] 섹션에서 믹스인 이름을 **[!UICONTROL 선택합니다]** . 이렇게 하면 믹스의 속성이 편집기의 오른쪽에 나타나고 [구조] 아래의 스키마 이름 옆에 **더하기(+)** 아이콘이 **[!UICONTROL 나타납니다]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

&quot; **&quot; 옆에 있는 더하기(+)**[!DNL Loyalty Members]아이콘을 선택하여 구조에 새 노드를 만듭니다. 이 노드 `_tenantId` (이 예에서 호출됨)는 IMS 조직의 테넌트 ID 앞에 밑줄이 있는 것을 나타냅니다. 테넌트 ID가 존재하면 추가할 필드가 조직의 네임스페이스에 포함되어 있음을 나타냅니다.

즉, 추가하려는 필드는 조직에 고유하며 조직에서만 액세스할 수 있는 특정 영역 [!DNL Schema Registry] 의 필드에 저장됩니다. 정의한 필드는 다른 표준 클래스, 혼합, 데이터 유형 및 필드의 이름과 충돌하지 않도록 항상 테넌트 네임스페이스에 추가해야 합니다.

해당 이름 지정 노드 안은 &quot;[!UICONTROL 새 필드]&quot;입니다. 이것은 &quot;[!UICONTROL 충성도 세부 사항]&quot; 믹스의 시작이다.

![](../images/tutorials/create-schema/new_field_loyalty.png)

편집기의 오른쪽에 있는 컨트롤을 사용하여 충성도 관련 필드를 유지하는 데 사용할 `loyalty` 유형 &quot;[!UICONTROL 개체]&quot;가 있는 필드를 만듭니다. 완료되면 적용을 **[!UICONTROL 선택합니다]**.

![](../images/tutorials/create-schema/loyalty_object.png)

변경 사항이 적용되고 새로 만든 객체가 `loyalty` 나타납니다. 개체 옆에 있는 **더하기(+)** 아이콘을 선택하여 충성도 관련 필드를 더 추가합니다. &quot;[!UICONTROL 새 필드]&quot;가 나타나고 **[!UICONTROL 필드 속성]** 섹션이 캔버스의 오른쪽에 표시됩니다.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

각 필드에는 다음 정보가 필요합니다.

* **[!UICONTROL 필드 이름]:** 낙타로 쓰여진 들판 이름. 예:충성도 수준
* **[!UICONTROL 표시 이름]:** 제목 케이스에 기록된 필드의 이름입니다. 예:충성도 수준
* **[!UICONTROL 유형]:** 필드의 데이터 유형입니다. 여기에는 기본 스칼라 형식과 에 정의된 모든 데이터 유형이 포함됩니다 [!DNL Schema Registry]. 예: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person],Address, Phone 번호등.
* **[!UICONTROL 설명]:** 필드에 대한 선택적 설명은 문장에 200자 이내로 작성하여 포함해야 합니다.

객체의 첫 번째 필드 `Loyalty` 는 호출된 문자열이 됩니다 `loyaltyId`. 새 필드의 유형을 &quot;[!UICONTROL 문자열]&quot;로 설정하면 **[!UICONTROL 필드 속성]** 섹션이 기본값, 형식 및 최대 길이 등 제한을 적용하기 위한 여러 가지 옵션으로 채워집니다.

![](../images/tutorials/create-schema/string_constraints.png)

선택한 데이터 유형에 따라 다른 제한 옵션을 사용할 수 있습니다. 이메일 주소 `loyaltyId` 가 되므로 형식[!UICONTROL 드롭다운 메뉴에서 &quot;이메일]&quot;을 **[!UICONTROL 선택합니다]** . 적용 **[!UICONTROL 을]** 선택하여 변경 내용을 적용합니다.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 믹스에 필드 추가 {#mixin-fields-2}

필드를 추가했으므로 추가 필드를 추가하여 다음과 같은 충성도 관련 정보를 `loyaltyId` 캡처할 수 있습니다.

* 포인트(정수)
* 회원-이후(날짜)

스키마에 각 필드를 추가하려면 객체 옆에 있는 **더하기(+)** 아이콘을 `loyalty` 선택하고 필요한 정보를 입력합니다.

완료되면 충성도 개체에는 충성도 ID, 포인트 및 회원 이후의 필드가 포함됩니다.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 믹스에 열거형 필드 추가 {#enum}

에서 필드를 정의할 때 [!DNL Schema Editor]는 필드에 포함할 수 있는 데이터에 대한 추가 제한을 제공하기 위해 기본 필드 유형에 적용할 수 있는 몇 가지 추가 옵션이 있습니다. 이러한 제한 사항에 대한 사용 사례는 다음 표에 설명되어 있습니다.

| 제한 | 설명 |
| --- | --- |
| [!UICONTROL 필수 여부] | 필드를 데이터 수집에 필요함을 나타냅니다. 이 필드를 포함하지 않는 이 스키마를 기반으로 데이터 세트에 업로드한 모든 데이터는 수집 시 실패합니다. |
| [!UICONTROL 배열] | 필드에 데이터 유형이 지정된 값 배열을 포함함을 나타냅니다. 예를 들어 데이터 유형이 &quot;[!UICONTROL String]&quot;인 필드에 이 제약 조건을 사용하면 필드에 문자열 배열이 포함되도록 지정합니다. |
| [!UICONTROL 열거형] | 이 필드에는 가능한 값이 열거된 목록의 값 중 하나가 포함되어야 함을 나타냅니다. |
| [!UICONTROL ID] | 이 필드가 ID 필드임을 나타냅니다. ID 필드에 대한 자세한 내용은 이 자습서 [후반부에 있습니다](#identity-field). |
| [!UICONTROL 관계] | 스키마 관계는 공용 스키마 및 공용 스키마 사용을 통해 유추할 수 있지만 동일한 클래스를 공유하는 스키마에만 [!DNL Real-time Customer Profile]적용됩니다. Relationship [!UICONTROL 제약 조건은 이] 필드가 다른 클래스를 기반으로 한 스키마의 기본 ID를 참조하고 두 스키마 간의 관계를 의미함을 나타냅니다. 자세한 내용은 관계 [를](./relationship-ui.md) 정의하는 자습서를 참조하십시오. |

이 자습서의 경우 스키마 [!DNL "loyalty"] 의 객체에는 고객의 &quot;충성도 수준&quot;을 설명하는 새 열거형 필드가 필요합니다. 이 필드는 값이 가능한 4개의 옵션 중 하나만 사용할 수 있습니다. 이 필드를 스키마에 추가하려면 객체 옆에 있는 **더하기(+)** 아이콘을 `loyalty` 선택하고 **[!UICONTROL 필드 이름]** 및 **[!UICONTROL 표시 이름에 필요한 필드를]**&#x200B;채웁니다. 유형 **[!UICONTROL 에]**&#x200B;대해 &quot;[!UICONTROL 문자열]&quot;을 선택합니다.

![](../images/tutorials/create-schema/loyalty-level-type.png)

배열 확인란, 열거형 및 ID를 포함하여 해당 유형을 선택한 후에 **[!UICONTROL 필드에]**&#x200B;대한 추가 **[!UICONTROL 확인란]****[!UICONTROL 이]**&#x200B;나타납니다.

아래의 **[!UICONTROL 열거형]** 값 섹션을 열려면 **[!UICONTROL 열거형]** 확인란을 선택합니다. 여기에서 허용되는 각 충성도 수준에 대해 **[!UICONTROL 값]** (camelCase) 및 **[!UICONTROL 레이블]** (제목 케이스의 경우 독자에게 친근한 이름 선택 사항)을 입력할 수 있습니다.

모든 필드 속성을 완료한 경우 **[!UICONTROL 적용을]** 선택하여 &quot;[!DNL loyaltyLevel]&quot; 필드를 개체에 `loyalty` 추가합니다.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## 다중 필드 개체를 데이터 형식으로 변환 {#datatype}

이제 개체 `loyalty` 에 몇 개의 로열티별 필드가 있으며 다른 스키마에서 유용할 수 있는 일반적인 데이터 구조를 나타냅니다. 이 [!DNL Schema Editor] 를 사용하면 해당 개체의 구조를 데이터 유형으로 변환하여 재사용 가능한 다중 필드 개체를 쉽게 적용할 수 있습니다.

데이터 유형을 사용하면 여러 필드 구조를 일관되게 사용할 수 있으며 스키마 내의 어느 곳에서든 사용할 수 있으므로 혼합보다 더 유연하게 사용할 수 있습니다. 이 작업은 필드의 **[!UICONTROL 유형]** 값을 에 정의된 데이터 유형의 값으로 설정하여 [!DNL Schema Registry]수행합니다.

개체를 데이터 유형으로 변환하려면 `loyalty` [구조] `loyalty` 아래의 필드 **[!UICONTROL 를 선택한 다음 [필드] 속성]**&#x200B;아래에 있는 편집기의 오른쪽에 있는 새 데이터 **[!UICONTROL 유형으로]** 변환 **[!UICONTROL 을]**&#x200B;선택합니다. 개체가 성공적으로 변환되었음을 확인하는 녹색 팝업 창이 나타납니다.

![](../images/tutorials/create-schema/convert-data-type.png)

이제 **[!UICONTROL 구조]**&#x200B;아래에서 필드 `loyalty` 에 &quot;[!DNL Loyalty]&quot;의 데이터 유형이 있고 필드 옆에 작은 잠금 아이콘이 있다는 것을 확인할 수 있습니다. 이는 필드가 더 이상 개별 필드가 아니라 다중 필드 데이터 유형의 일부임을 나타냅니다.

![](../images/tutorials/create-schema/loyalty_data_type.png)

이후 스키마에서 필드를 &quot;[!DNL Loyalty]&quot; 유형으로 할당할 수 있으며 ID, 충성도 수준, 이후의 멤버 및 포인트에 대한 필드를 자동으로 포함할 수 있습니다.

>[!NOTE]
>
>사용자 정의 데이터 유형을 편집 스키마와 독립적으로 생성 및 편집할 수도 있습니다. 자세한 내용은 [데이터 유형](./create-data-type.md) 만들기 및 편집에 대한 자습서를 참조하십시오.

## 스키마 필드 검색 및 필터링

이제 스키마에는 기본 클래스에서 제공하는 필드 외에 여러 혼합이 포함됩니다. 큰 스키마를 사용하여 작업하는 경우 왼쪽 레일의 혼합 이름 옆에 있는 확인란을 선택하여 표시되는 필드를 관심 있는 믹스에서 제공하는 필드에 대해서만 필터링할 수 있습니다.

![](../images/tutorials/create-schema/filter-by-mixin.png)

스키마에서 특정 필드를 찾고 있는 경우 검색 막대를 사용하여 표시되는 필드의 믹싱과 관계없이 이름을 기준으로 필드를 필터링할 수도 있습니다.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>검색 함수는 일치하는 필드를 표시할 때 선택한 혼합 필터를 고려합니다. 검색 쿼리가 원하는 결과를 표시하지 않는 경우 관련 혼합을 필터링하지 않는지 다시 확인해야 합니다.

## 스키마 필드를 ID 필드로 설정 {#identity-field}

스키마가 제공하는 표준 데이터 구조를 활용하여 여러 소스에서 동일한 개인에 속하는 데이터를 식별할 수 있으므로 세분화, 보고, 데이터 과학 분석 등과 같은 다양한 다운스트림 사용 사례를 허용할 수 있습니다. 개별 ID를 기반으로 데이터를 스티칭하려면 해당 스키마 내에서 키 필드를 [!UICONTROL ID] 필드로 표시해야 합니다.

[!DNL Experience Platform] 의 ID 확인란을 사용하여 ID 필드를 **[!UICONTROL 쉽게]** 나타낼 수 [!DNL Schema Editor]있습니다. 그러나 데이터의 특성에 따라 ID로 사용할 가장 적합한 필드를 결정해야 합니다.

예를 들어 동일한 &quot;충성도 수준&quot;에 속하는 로열티 프로그램 회원이 수천 명에 달할 수 있지만, 로열티 프로그램의 각 멤버에는 고유한(이 경우 개별 멤버의 이메일 주소)가 있습니다. `loyaltyId` 각 멤버 `loyaltyId` 에 대한 고유 식별자이기 때문에 ID 필드에 적합한 후보가 되는 반면 ID 필드는 사용할 수 `loyaltyLevel` 없습니다.

>[!IMPORTANT]
>
>아래 설명된 단계에 ID 설명자를 기존 스키마 필드에 추가하는 방법이 나와 있습니다. 스키마 자체의 구조 내에서 ID 필드를 정의하는 대신 필드를 사용하여 ID 정보를 `identityMap` 대신 포함할 수도 있습니다.
>
>사용 계획이라면 스키마 `identityMap`에 직접 추가하는 모든 기본 ID를 재정의한다는 것을 명심하십시오. 자세한 내용은 스키마 `identityMap` 컴포지션 안내서의 [](../schema/composition.md#identityMap) 기본 사항 섹션을 참조하십시오.

편집기의 **[!UICONTROL 구조]** 섹션에서 `loyaltyId` 필드를 선택하면 필드 속성 **[!UICONTROL 아래에]** ID **[!UICONTROL 확인란이]**&#x200B;나타납니다. 확인란을 선택하고 이 ID를 기본 ID로 설정하는 **[!UICONTROL 옵션이]** 나타납니다. 이 상자도 선택하십시오.

>[!NOTE]
>
>각 스키마에는 하나의 기본 ID 필드만 포함할 수 있습니다. 스키마 필드를 기본 ID로 설정하면 나중에 스키마의 다른 ID 필드를 기본 ID로 설정하려고 하면 오류 메시지가 표시됩니다.

그런 다음 드롭다운에 **[!UICONTROL 사전 정의된 네임스페이스]** 목록에서 ID 네임스페이스를 제공해야 합니다. 고객 `loyaltyId` 의 이메일 주소이므로 드롭다운에서 &quot;[!UICONTROL 이메일]&quot;을 선택합니다. 적용 **[!UICONTROL 을]** 선택하여 필드에 대한 업데이트를 `loyaltyId` 확인합니다.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>표준 네임스페이스 및 해당 정의 목록은 설명서를 [[!DNL Identity Service] 참조하십시오](../../identity-service/troubleshooting-guide.md#standard-namespaces).

변경 사항을 적용한 후 의 아이콘은 이제 ID 필드임을 나타내는 지문 기호를 `loyaltyId` 표시합니다.

![](../images/tutorials/create-schema/identity-applied.png)

이제 필드에 수집되는 모든 데이터를 `loyaltyId` 사용하여 해당 고객을 식별하고 해당 고객의 한 보기를 결합할 수 있습니다. ID 작업에 대한 자세한 내용 [!DNL Experience Platform]은 설명서를 [[!DNL Identity Service]](../../identity-service/home.md) 참조하십시오.

## 스키마를 [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) 의 id 데이터를 활용하여 각 고객 [!DNL Experience Platform] 의 전체 상황을 파악할 수 있습니다. 이 서비스는 고객 속성에 대한 360도 프로파일을 구축하고 고객과 통합된 모든 시스템에서 타임스탬프가 지정된 계정을 만듭니다 [!DNL Experience Platform].

스키마에서 함께 사용할 수 있도록 설정하려면 기본 ID가 [!DNL Real-time Customer Profile]정의되어 있어야 합니다. 기본 ID를 먼저 정의하지 않고 스키마를 활성화하려고 하면 오류 메시지가 표시됩니다.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

&quot;충성도 멤버&quot; 스키마를 사용하여 [!DNL Profile]사용하려면 편집기의 구조 섹션에서 &quot;[!DNL Loyalty Members]&quot;를 **[!UICONTROL 선택하여]** 시작합니다.

편집기의 오른쪽에는 표시 이름, 설명 및 유형을 비롯한 스키마에 대한 정보가 표시됩니다. 이 정보 외에도 프로필 **[!UICONTROL 전환]** 단추가 있습니다.

![](../images/tutorials/create-schema/profile-toggle.png)

프로파일 **[!UICONTROL 을]** 선택하면 팝업 창이 나타나면서 스키마를 활성화할 것임을 확인하는 메시지가 [!DNL Profile]표시됩니다.

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>스키마를 활성화한 후 저장하면 [!DNL Real-time Customer Profile] 는 비활성화할 수 없습니다.

사용 **[!UICONTROL 을]** 선택하여 선택을 확인합니다. 원할 경우 **[!UICONTROL 프로필]** 토글을 다시 선택하여 스키마를 비활성화할 수 있지만 활성화된 상태에서 스키마를 저장한 후에는 [!DNL Profile] 더 이상 비활성화할 수 없습니다.

## 다음 단계 및 추가 리소스

이제 스키마 작성을 마쳤으므로 캔버스에서 전체 스키마를 볼 수 있습니다. 저장 **[!UICONTROL 을]** 선택하면 스키마는 [!DNL Schema Library]에 저장되고, 이렇게 하면 사용자가 스키마를 액세스할 수 [!DNL Schema Registry]있습니다.

이제 새 스키마를 사용하여 데이터를 인제스트할 수 있습니다 [!DNL Platform]. 스키마를 사용하여 데이터를 인제스트하면 추가 변경만 수행할 수 있습니다. 스키마 [버전 관리에 대한 자세한 내용은 스키마](../schema/composition.md) 구성 기본 사항을 참조하십시오.

이제 UI에서 스키마 관계를 [정의하는 자습서에 따라 &quot;충성도](./relationship-ui.md) 멤버&quot; 스키마에 새 관계 필드를 추가할 수 있습니다.

&quot;충성도 멤버&quot; 스키마는 [!DNL Schema Registry] API를 사용하여 보고 관리할 수도 있습니다. API 작업을 시작하려면 [[!DNL Schema Registry API] 개발자 안내서를 읽어 봅니다](../api/getting-started.md).

### 비디오 리소스

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

다음 비디오에서는 [!DNL Platform] UI에서 간단한 스키마를 만드는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

다음 비디오는 혼합기 및 클래스 작업에 대한 이해를 높이기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 부록

다음 섹션에서는 소프트웨어의 사용에 대한 추가 정보를 제공합니다 [!DNL Schema Editor].

### Create a new class {#create-new-class}

[!DNL Experience Platform] 조직에 고유한 클래스를 기반으로 스키마를 정의할 수 있는 유연성을 제공합니다.

스키마 **[!UICONTROL 작업]** 영역에서 **[!UICONTROL 스키마]****[!UICONTROL 만들기를 선택한]** 다음 드롭다운에서찾아보기를 선택합니다.

![](../images/tutorials/create-schema/browse-classes.png)

사용 가능한 클래스 목록에서 선택할 수 있는 대화 상자가 나타납니다. 대화 상자의 맨 위에서 새 클래스 **[!UICONTROL 만들기를 선택합니다]**. 그런 다음 새 클래스에 스키마가 정의하는 데이터에 대한 표시 이름(클래스의 짧고 설명적이며 고유한 이름), 설명 및 비헤이비어(&quot;[!UICONTROL 레코드]&quot; 또는 &quot;[!UICONTROL 시간 시리즈]&quot;)를 지정할 수 있습니다.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>조직에서 정의한 클래스를 구현하는 스키마를 빌드할 때는 믹스를 호환 가능한 클래스에서만 사용할 수 있습니다. 정의한 클래스는 새로 만들어지므로 [믹서 추가] 대화 상자에 **[!UICONTROL 호환되는 믹스가]** 없습니다. 대신 [새 믹싱 만들기]를 **[!UICONTROL 선택하고 해당]** 클래스에 사용할 믹싱을 정의해야 합니다. 다음에 새 클래스를 구현하는 스키마를 작성할 때 정의한 혼합이 나열되고 사용할 수 있습니다.

### 스키마 클래스 변경 {#change-class}

스키마를 저장하기 전에 초기 컴포지션 프로세스 중에 언제든지 스키마 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>스키마에 대한 클래스 재지정은 매우 주의해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

클래스를 재할당하려면 **[!UICONTROL 캔버스의]** 왼쪽에서 [할당]을 선택합니다.

![](../images/tutorials/create-schema/assign_class_button.png)

조직에서 정의한 모든 클래스(소유자가 &quot;[!UICONTROL 고객]&quot;인 경우)와 Adobe에서 정의한 표준 클래스를 포함하여 사용 가능한 모든 클래스의 목록을 표시하는 대화 상자가 나타납니다.

목록에서 클래스를 선택하여 대화 상자의 오른쪽에 해당 설명을 표시합니다. 미리 보기 클래스 구조 **[!UICONTROL 를 선택하여 클래스와]** 연결된 필드 및 메타데이터를 볼 수도 있습니다. 계속하려면 **[!UICONTROL 클래스]** 할당을 선택합니다.

![](../images/tutorials/create-schema/assign_class.png)

새 클래스를 지정할 것인지 확인하는 새 대화 상자가 열립니다. 지정할 **[!UICONTROL 지정을]** 선택합니다.

![](../images/tutorials/create-schema/assign-confirm.png)

클래스 변경을 확인한 후 캔버스가 재설정되고 모든 컴포지션 진행 상태가 손실됩니다.