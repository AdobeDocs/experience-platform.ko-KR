---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스키마 편집기를 사용하여 스키마 만들기
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '3376'
ht-degree: 0%

---


# Create a schema using the [!DNL Schema Editor]

이 [!DNL Schema Registry] 는 Adobe Experience Platform의 모든 리소스를 보고 관리할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다 [!DNL Schema Library]. 이 [!DNL Schema Library] 에는 Adobe, Experience Platform 파트너, 애플리케이션을 사용하는 공급업체 등이 제공하는 리소스 및 사용자가 정의하고 저장하는 리소스가 포함되어 [!DNL Schema Registry]있습니다.

이 자습서에서는 내에서 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다 [!DNL Experience Platform]. 스키마 레지스트리 API를 사용하여 스키마를 작성하려는 경우 API를 사용하여 스키마를 [만드는 자습서를 시도하기 전에 스키마 레지스트리 개발자 가이드](../api/getting-started.md) 를 읽어 보십시오 [](create-schema-api.md).

이 자습서에는 스키마를 [구성하는 데 사용할 수 있는 새 클래스를](#create-new-class) 정의하는 단계도 포함되어 있습니다.

## 시작하기

이 자습서에서는 스키마 편집기 사용과 관련된 Adobe Experience Platform의 다양한 측면을 파악해야 합니다. 이 자습서를 시작하기 전에 다음 개념을 살펴보십시오.

* [!DNL Experience Data Model (XDM)](../home.md): Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [스키마 컴포지션의 기본 사항](../schema/composition.md): 클래스, 믹싱, 데이터 유형 및 필드를 비롯한 XDM 스키마 및 구성 요소에 대한 개요입니다.
* [!DNL Real-time Customer Profile](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이 튜토리얼을 사용하려면 액세스 권한이 있어야 합니다 [!DNL Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.

## 스키마 작업 공간에서 기존 스키마 찾아보기 {#browse}

스키마 작업 공간 [!DNL Experience Platform] 은 새 스키마 [!DNL Schema Library]를 작성하고 사용 가능한 모든 스키마를 보고 관리할 수 있도록 시각화를 제공합니다. 작업 영역에는 이 자습서 전체에서 스키마를 작성할 캔버스인 스키마 편집기도 포함되어 있습니다.

로그인한 [!DNL Experience Platform]후 왼쪽 탐색 **[!UICONTROL 에서 스키마]** 를 클릭하면 스키마 작업 영역으로 이동합니다. 사용 가능한 모든 스키마를 보고 관리 및 사용자 정의할 수 있는 스키마 목록( [!DNL Schema Library]스키마 표현)이 표시됩니다. 이 목록에는 스키마의 기반이 되는 이름, 유형, 클래스 및 동작(레코드 또는 시간 시리즈)과 스키마를 마지막으로 수정한 날짜 및 시간이 포함됩니다.

클래스, 믹싱 및 데이터 형식을 포함하여 레지스트리의 모든 리소스에 대한 필터링 기능을 사용하려면 검색 막대 옆에 있는 필터 아이콘을 클릭합니다.

![스키마 라이브러리 보기](../images/tutorials/create-schema/schemas_filter.png)

## 스키마 만들기 및 이름 지정 {#create}

스키마 작성을 시작하려면 스키마 작업 영역의 오른쪽 **[!UICONTROL 위]** 모서리에서 스키마 만들기를 클릭합니다.

![스키마 만들기 단추](../images/tutorials/create-schema/create_schema_button.png)

스키마 *편집기가* 나타납니다. 스키마를 작성할 캔버스입니다. 편집기에 도착하면 사용자 지정을 시작할 수 있도록 캔버스의 *구조* 섹션에 있는 &quot;제목 없는 스키마&quot;가 자동으로 생성됩니다.

![스키마 편집기](../images/tutorials/create-schema/schema_editor.png)

편집기 오른쪽에는 *스키마 속성이* 있는데, 여기서 표시 이름 **** 필드를 사용하여 스키마의 이름을 제공할 수 있습니다. 이름을 입력했으면 캔버스가 스키마의 새 이름을 반영하도록 업데이트됩니다.

![스키마 캔버스](../images/tutorials/create-schema/name_schema.png)

스키마의 이름을 결정할 때 고려해야 할 몇 가지 중요한 사항이 있습니다.

* 나중에 라이브러리에서 스키마를 쉽게 찾을 수 있도록 스키마 이름은 짧고 설명이어야 합니다.
* 스키마 이름은 고유해야 합니다. 이는 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다. 예를 들어, 조직에서 서로 다른 브랜드에 대한 별도의 로열티 프로그램을 보유하고 있는 경우 나중에 정의할 수 있는 다른 충성도 관련 스키마와 쉽게 구별할 수 있도록 스키마 &quot;브랜드 a 충성도 구성원&quot;을 지정하는 것이 좋습니다.
* 선택적으로 설명 필드를 사용하여 스키마에 대한 추가 정보를 제공할 **[!UICONTROL 수]** 있습니다.

이 자습서는 충성도 프로그램의 구성원과 관련된 데이터를 인제스트하는 스키마를 구성하므로 스키마의 이름은 &quot;충성도 구성원&quot;입니다.

## 클래스 지정 {#class}

편집기의 왼쪽에 *컴포지션* 섹션이 있습니다. 현재 두 개의 하위 섹션이 포함되어 있습니다. *[!UICONTROL 스키마]* 및 *[!UICONTROL 클래스]*.

이제 스키마에 이름이 있으므로 스키마를 구현할 클래스를 할당할 때입니다. 클래스 **[!UICONTROL 옆에]** 있는 할당을 *[!UICONTROL 클릭합니다]*.

![](../images/tutorials/create-schema/assign_class_button.png)

[클래스 *[!UICONTROL 할당]* ] 대화 상자가 나타납니다. 이 창에는 조직에서 정의한 모든 클래스(소유자가 &quot;고객&quot;임)와 Adobe에서 정의한 표준 클래스 등 사용 가능한 모든 클래스 목록이 표시됩니다.

클래스 이름을 클릭하여 클래스에 대한 설명을 표시합니다. 클래스 구조 미리 **[!UICONTROL 보기를 선택하여]** 클래스와 연관된 필드 및 메타데이터를 볼 수도 있습니다.

이 자습서에서는 [!DNL XDM Individual Profile] 클래스를 사용합니다. 클래스 옆의 라디오 단추를 클릭하여 선택한 다음 [클래스 **[!UICONTROL 할당]을 클릭합니다]**.

![클래스 지정 대화 상자](../images/tutorials/create-schema/assign_class.png)

캔버스가 다시 나타납니다. 이제 *[!UICONTROL 클래스]* 섹션에는 선택한 클래스([!DNL XDM Individual Profile])가 포함되어 있으며 [!DNL XDM Individual Profile] 이제 클래스 *[!UICONTROL 가 기여한 필드가 구조]* 섹션 내에표시됩니다.

![XDM 개별 프로필 클래스 할당](../images/tutorials/create-schema/class_assigned_structure.png)

필드가 &quot;fieldName&quot; 형식으로 표시됩니다. | 데이터 유형&quot;을 참조하십시오. UI에서 스키마 필드를 정의하는 단계는 이 자습서의 후반부에서 제공됩니다.

>[!NOTE]
>
>스키마를 저장하기 전에 초기 작성 프로세스 중에 어느 시점에서나 스키마 [클래스를](#change-class) 변경할 수 있지만, 이 작업은 매우 신중하게 수행해야 합니다. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스 및 추가한 모든 필드가 재설정됩니다.

## 혼합 추가 {#mixin}

클래스가 지정되었으므로 *구성* 섹션에는 세 번째 하위 섹션이 포함됩니다. *[!UICONTROL 믹싱]*.

이제 혼합을 추가하여 스키마에 필드를 추가할 수 있습니다. 혼합이란 특정 개념을 설명하는 하나 이상의 들판으로 이루어진 그룹입니다. 이 자습서에서는 혼합을 사용하여 충성도 프로그램의 구성원을 설명하고 이름, 생일, 전화 번호, 주소 등과 같은 주요 정보를 캡처합니다.

믹스를 추가하려면 [믹싱] 하위 섹션 **에서 [추가** ] *를* 클릭합니다.

![](../images/tutorials/create-schema/add_mixin_button.png)

[ *[!UICONTROL 혼합 추가]* ] 대화 상자가 나타납니다. 혼합은 특정 클래스와 함께 사용하기 위한 것이기 때문에 혼합 목록은 선택한 클래스(이 경우 [!DNL XDM Individual Profile] 클래스)와 호환되는 조합만 표시합니다.

혼합 옆에 있는 라디오 단추를 선택하면 [혼합 구조 미리 보기] 옵션이 **[!UICONTROL 제공됩니다]**. &quot;프로필 인물 세부 사항&quot; 믹싱을 선택한 다음 [믹신 **[!UICONTROL 추가]를 클릭합니다]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

스키마 캔버스가 다시 나타납니다. 이제 *[!UICONTROL 믹싱]* 섹션에는 &quot;[!UICONTROL 프로필]인물 세부 사항 *[!UICONTROL &quot; 믹싱이 표시되고]* 구조섹션에는 믹싱에 의해 기고한 필드가 포함됩니다.

![](../images/tutorials/create-schema/person_details_structure.png)

이 혼합은 데이터 유형이 &quot;Person&quot;인 최상위 수준 이름 아래의 여러 필드에 기여합니다. 이 필드 그룹은 이름, 생년월일, 성별 등 개인에 대한 정보를 설명합니다.

>[!NOTE]
>
>필드는 필드의 데이터 유형뿐만 아니라 &quot;데이터 유형&quot;(공통 개념을 나타내는 필드 그룹)과 같은 스칼라 유형(문자열, 정수, 배열 또는 날짜 등)을 사용할 수 있습니다 [!DNL Schema Registry].

&quot;[!UICONTROL 이름]&quot; 필드에는 &quot;[!UICONTROL 사람 이름]&quot;의 데이터 유형이 있습니다. 이것은 일반적인 개념도 설명하며 이름, 성 및 전체 이름과 같은 이름 관련 하위 필드가 포함되어 있음을 의미합니다.

캔버스 내의 다른 필드를 클릭하면 스키마 구조에 기여하는 추가 필드를 볼 수 있습니다.

## 다른 믹신 추가 {#mixin-2}

이제 동일한 단계를 반복하여 다른 믹스를 추가할 수 있습니다. 이번에 [믹신 *[!UICONTROL 추가]* ] 대화 상자를 볼 때 &quot;[!UICONTROL 프로필 개인 정보]&quot; 믹신이 회색으로 표시되었고 그 옆에 있는 라디오 단추를 선택할 수 없습니다. 이렇게 하면 현재 스키마에 이미 포함되어 있는 믹스를 실수로 복제할 수 없습니다.

이제 [혼합[!DNL Profile Personal Details" mixin] 추가] 대화 상자에서 &quot; *[!UICONTROL 를 추가할 수]* 있습니다.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

캔버스가 추가되면 다시 나타납니다. &quot;[!UICONTROL 프로필 개인 세부 사항]&quot;은 이제 *[!UICONTROL 컴포지션]* 섹션 *[!UICONTROL 에 있는 Mixins 아래에]* 나열되며, 홈 주소, 휴대폰 등을 위한 필드가 **&#x200B;구조Vertising 아래에 추가되었습니다.

&quot;[!UICONTROL 이름]&quot; 필드와 유사하게 방금 추가한 필드는 다중 필드 개념을 나타냅니다. 예를 들어, &quot;[!UICONTROL homeAddress]&quot;의 데이터 유형이 &quot;[!UICONTROL Address]&quot;이고 &quot;[!UICONTROL mobilePhone][!UICONTROL &quot;은 &quot;Phone Number]&quot;의 데이터 유형을갖습니다. 이러한 각 필드를 클릭하여 확장하고 데이터 유형에 포함된 추가 필드를 볼 수 있습니다.

![](../images/tutorials/create-schema/personal_details_structure.png)

## 새로운 믹싱 정의 {#define-mixin}

&quot;[!UICONTROL 충성도 멤버]&quot; 스키마는 충성도 프로그램 멤버와 관련된 데이터를 캡처하기 위한 것으로 특정 충성도 관련 필드가 필요합니다. 필요한 필드가 포함된 표준 믹스인(mixins)이 없으므로 새 믹스인을 정의해야 합니다.

이 때 [혼합 *[!UICONTROL 추가]* ] 대화 상자를 열 때 [새 **[!UICONTROL 혼합 만들기]를 선택합니다]**. 그러면 혼합에 대한 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL 설명]** 을제공하라는 메시지가 표시됩니다.

![](../images/tutorials/create-schema/mixin_create_new.png)

클래스 이름과 마찬가지로 혼합기 이름은 짧고 단순해야 스키마에 어떤 내용이 기여할 것인지 설명합니다. 이 두 가지 모두 고유하므로 이름을 다시 사용할 수 없으므로 해당 이름이 충분한지 확인해야 합니다.

이 튜토리얼의 경우 새로운 믹스의 이름을 &quot;[!UICONTROL 충성도 세부 정보&quot;로 지정합니다].

스키마 **[!UICONTROL 편집기로 돌아가려면]** 믹신 추가를 클릭합니다. 이제 캔버스 왼쪽[!UICONTROL 의]믹싱 아래에 &quot; *[!UICONTROL 충성도 세부 정보]* &quot;가 표시되어야 하지만 아직 여기에 연결된 필드가 없으므로 *[!UICONTROL 구조]*&#x200B;아래에 새 필드가 나타나지 않습니다.

## 믹스에 필드 추가 {#mixin-fields}

이제 &quot;[!UICONTROL 충성도 세부 정보]&quot; 조합을 만들었으므로 혼합이 스키마에 기여할 필드를 정의할 때입니다.

시작하려면 [혼합] 섹션에서 *[!UICONTROL 믹신 이름을]* 클릭합니다. 이렇게 하면 [ *[!UICONTROL 혼합 속성]* ]이 편집기의 오른쪽에 나타나고 [ **[!UICONTROL 구조]** ] 아래의 스키마 이름 옆에 [필드 *[!UICONTROL 추가] 단추가]*&#x200B;나타납니다.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

&quot; **[!UICONTROL 충성도 멤버]** &quot; 옆에 있는 필드추가를 클릭하여 구조에 새 노드를 만듭니다. 이 노드(이 예에서 &quot;_tenantId&quot;라고 함)는 IMS 조직의 테넌트 ID 앞에 밑줄이 있는 것을 나타냅니다. 테넌트 ID가 존재하면 추가할 필드가 조직의 네임스페이스에 포함되어 있음을 나타냅니다.

즉, 추가하려는 필드는 조직에 고유하며 IMS 조직에서만 액세스할 수 있는 특정 영역 [!DNL Schema Registry] 에 저장됩니다. 정의한 필드는 항상 네임스페이스에 추가되어야 다른 표준 클래스, 혼합, 데이터 형식 및 필드의 이름과 충돌하지 않습니다.

해당 네임스페이스 노드 안은 &quot;[!UICONTROL 새 필드&quot;입니다]. 이것은 &quot;[!UICONTROL 충성도 세부 사항]&quot; 혼합의 시작이다.

![](../images/tutorials/create-schema/new_field_loyalty.png)

편집기의 오른쪽에 *[!UICONTROL 필드 속성]* 을 사용하면 우선 충성도 관련 필드를[!UICONTROL 유지하는 데 사용할 &quot;개체]&quot; 유형이 있는 &quot;[!UICONTROL 충성도]&quot; 필드를 만들어 보십시오. 완료되면 적용을 **[!UICONTROL 클릭합니다]**.

![](../images/tutorials/create-schema/loyalty_object.png)

변경 사항이 적용되고 새로 만든 &quot;[!UICONTROL 충성도]&quot; 개체가 나타납니다. 개체 옆에 있는 **[!UICONTROL 필드]** 추가를 클릭하여 충성도 관련 필드를 추가합니다. &quot;새 필드&quot;가 나타나고 *[!UICONTROL 필드 속성]* 섹션이 캔버스 오른쪽에 표시됩니다.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

각 필드에는 다음 정보가 필요합니다.

* **[!UICONTROL 필드 이름]:**낙타라고 적힌 들판 이름. 예: 충성도 수준
* **[!UICONTROL 표시 이름]:**제목 케이스에 기록된 필드의 이름입니다. 예: 충성도 수준
* **[!UICONTROL 유형]:**필드의 데이터 유형입니다. 여기에는 기본 스칼라 형식과 에 정의된 모든 데이터 유형이 포함됩니다[!DNL Schema Registry]. 예: 문자열, 정수, 부울, 사람, 주소, 전화 번호 등
* **[!UICONTROL 설명]:**문장의 경우 필드에 대한 선택적 설명을 포함해야 합니다. (최대 200자)

충성도 개체의 첫 번째 필드는 &quot;[!UICONTROL loymentId&quot;라는 문자열이 됩니다]. 새 필드의 유형을 &quot;[!UICONTROL 문자열]&quot;으로 설정할 때, 기본 값 *[!UICONTROL , 기본 형식, CumulationsFormat, CumulationsMaximum Length를 포함하여]* 여러 옵션을 적용하기 위한 여러 가지 옵션 **[!UICONTROL 으로 채워진 필드 속성]******&#x200B;창이 됩니다 ****.

![](../images/tutorials/create-schema/string_constraints.png)

선택한 데이터 유형에 따라 다른 제한 옵션을 사용할 수 있습니다. &quot;[!UICONTROL loymentId]&quot;는 이메일 주소이므로[!UICONTROL 형식]드롭다운 메뉴에서 &quot; **[!UICONTROL 이메일]** &quot;을선택합니다. 적용을 **[!UICONTROL 선택하여]** 변경 사항을 적용합니다.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## 혼합할 필드 추가 {#mixin-fields-2}

이제 &quot;[!UICONTROL loymentId]&quot; 필드를 추가했으므로 추가 필드를 추가하여 다음과 같은 충성도 관련 정보를 수집할 수 있습니다.

* 포인트(정수)
* 멤버 유효 기간(날짜)

충성도 개체에서 필드 **[!UICONTROL 추가를]** 클릭하고 필요한 정보를 입력하여 각 필드가 추가됩니다.

완료되면 충성도 오브젝트에 다음과 같은 필드가 포함됩니다. 충성도 ID, 포인트 및 이후의 멤버.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## 혼합에 &#39;enum&#39; 필드 추가 {#enum}

스키마 편집기에서 필드를 정의할 때 필드에 포함할 수 있는 데이터에 대한 추가 제한을 제공하기 위해 기본 필드 유형에 적용할 수 있는 몇 가지 추가 옵션이 있습니다.

이 필드의 예는 &quot;[!UICONTROL 충성도 수준]&quot; 필드이며, 이 필드는 값이 가능한 네 가지 옵션 중 하나만 될 수 있습니다. 이 필드를 스키마에 추가하려면 &quot; **[!UICONTROL 충성도]** &quot; 개체 옆에 있는 필드[!UICONTROL 추가를 클릭하고]필드 속성 *[!UICONTROL 아래에 필요한 필드를]*&#x200B;채웁니다.

유형 ****&#x200B;의 경우 &quot;문자열&quot;을 **[!UICONTROL 선택하면]** Array **[!UICONTROL , Enum]**&#x200B;및 IdentityCompetitan에 대한 추가 확인란이 **[!UICONTROL 나타납니다]**.

열거형 **[!UICONTROL 확인란을]** 선택하여 아래의 열거형 값 *[!UICONTROL 섹션을]* 엽니다. 여기에서 허용 가능한 각 충성도 수준에 대해 **[!UICONTROL 값]** (camelCase) 및 **[!UICONTROL 레이블]** (제목 케이스의 경우 독자가 친근한 이름 선택 사항)을 입력할 수 있습니다.

모든 필드 속성을 완료하면 **[!UICONTROL 적용을]** 클릭하면 &quot;[!UICONTROL 충성도]수준&quot; 필드가 &quot;충성도&quot; 개체에 추가됩니다.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

사용 가능한 추가 제한에 대한 자세한 내용:

* **[!UICONTROL 필수]:**데이터 수집에 필드가 필수임을 나타냅니다. 이 필드를 포함하지 않는 이 스키마를 기반으로 데이터 세트에 업로드한 데이터는 수집 시 실패합니다.
* **[!UICONTROL 어레이]:**필드에 데이터 유형이 지정된 값 배열을 포함함을 나타냅니다. 예를 들어 &quot;문자열&quot;의 데이터 유형을 선택하고 &quot;배열&quot; 확인란을 선택하면 필드에 문자열 배열이 포함됩니다.
* **[!UICONTROL 열거형]:**이 필드에 가능한 값의 열거형 목록의 값 중 하나가 포함되어야 함을 나타냅니다.
* **[!UICONTROL ID]:**이 필드가 ID 필드임을 나타냅니다. ID 필드에 대한 자세한 내용은 이 자습서[후반부에서 제공됩니다](#identity-field).

## 다중 필드 개체를 데이터 형식으로 변환 {#datatype}

몇 개의 로열티별 필드를 추가한 후 &quot;[!UICONTROL 충성도]&quot; 개체에는 다른 스키마에서 유용할 수 있는 일반적인 데이터 구조가 포함됩니다.

다중 필드 구조가 다시 사용될 수 있고 다른 곳에서 동일한 데이터 구조를 사용할 수 있는 유연성을 갖추고자 할 때 스키마 편집기를 사용하면 해당 구조를 데이터 유형으로 변환할 수 있습니다.

데이터 유형을 사용하면 여러 필드 구조를 일관되게 사용할 수 있으며 스키마 내의 어느 곳에서나 사용할 수 있으므로 혼합보다 더 유연하게 사용할 수 있습니다. 이렇게 하려면 믹싱의 필드 **[!UICONTROL 유형]** 을 레지스트리에 정의된 데이터 유형의 필드에 설정합니다.

&quot;[!UICONTROL 충성도]&quot; 개체를 데이터 유형으로 변환하려면 *[!UICONTROL 구조]* 아래의 &quot;충성도 **[!UICONTROL &quot; 필드를 클릭하고]** 필드 속성 *[!UICONTROL 에서 편집기의 오른쪽 오른쪽에 있는 새 데이터 유형으로]*&#x200B;변환을 선택합니다. &quot;데이터 유형으로 변환된[!UICONTROL 개체&quot;를 확인하는 작은 녹색 팝업이 나타납니다].

이제 *[!UICONTROL 구조]*&#x200B;아래[!UICONTROL 를 보면 &quot;]충성도[!UICONTROL &quot; 필드에 데이터 유형이 있고 필드 옆에는 더 이상 개별 필드가 아니라 다중 필드 구조의 일부임을 나타내는 작은 잠금]아이콘이 있음을 확인할 수 있습니다.

향후 스키마에서, 이제 &quot; **[!UICONTROL 충성도]** &quot;의[!UICONTROL 유형]필드를 할당하고, 자동으로 충성도 수준, 포인트, 이후의 멤버 및 충성도 ID 필드를 포함할 수 있습니다.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## 스키마 필드를 ID 필드로 설정 {#identity-field}

스키마는 데이터를 인제스트하는 데 사용되며, 이 데이터 [!DNL Experience Platform]는 궁극적으로 개인을 식별하고 여러 소스에서 나오는 정보를 통합하는 데 사용됩니다. 이 프로세스에 도움이 되도록 키 필드를 &quot;[!UICONTROL ID]&quot; 필드로 표시할 수 있습니다.

[!DNL Experience Platform] 의 ID 확인란을 사용하여 ID 필드를 쉽게 **[!UICONTROL 나타낼]** 수 [!DNL Schema Editor]있습니다.

예를 들어 동일한 &quot;수준&quot;에 속하는 로열티 프로그램의 회원 수가 수천 명에 달할 수 있지만, 로열티 프로그램의 각 멤버에는 고유한 &quot;loyaltyId&quot;가 있습니다(이 경우 개별 멤버의 이메일 주소). &quot;loyaltyId&quot;가 각 구성원의 고유 식별자이므로 ID 필드에 적합한 후보가 되는 반면 &quot;level&quot;은 아닙니다.

편집기의 *[!UICONTROL 구조]* 섹션에서 만든 &quot;[!UICONTROL 로열티]ID **[!UICONTROL &quot; 필드를 클릭하면 필드 속성 아래에]** ID *[!UICONTROL 확인란이]*&#x200B;나타납니다. 확인란을 선택하면 **[!UICONTROL 기본 ID로 설정할 수 있는 옵션이 표시됩니다]**. 그 상자도 확인해 보세요.

다음으로 ID **[!UICONTROL 네임스페이스를 제공해야 합니다]**. 미리 정의된 네임스페이스는 여러 가지가 있지만 &quot;[!UICONTROL loyaltyId]&quot;가 구성원의 이메일 주소이므로 드롭다운 목록에서 &quot;이메일&quot;을 선택합니다. 이제 적용 **[!UICONTROL 을]** 클릭하여 &quot;[!UICONTROL loymentId]&quot; 필드의 업데이트를 확인할 수 있습니다.

이제 &quot;[!UICONTROL loymentId]&quot; 필드로 인제스트된 모든 데이터는 해당 개인을 식별하고 해당 고객의 단일 뷰를 연결하는 데 사용됩니다.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>스키마 필드가 기본 ID로 설정되면 나중에 스키마의 다른 필드를 기본 필드로 설정하려고 하면 오류 메시지가 표시됩니다. 각 스키마에는 기본 ID 필드가 하나만 포함될 수 있습니다.

ID 작업에 대한 자세한 내용은 설명서를 [!DNL Identity Service](../../identity-service/home.md) 참조하십시오.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## 스키마를 [!DNL Real-time Customer Profile] {#profile}

스키마 편집기에서는 스키마를 사용할 수 있도록 하는 기능을 제공합니다 [!DNL Real-time Customer Profile](../../profile/home.md). [!DNL Profile] 고객 속성에 대한 견고한 360° 프로필과 고객이 모든 시스템과 통합된 모든 상호 작용에 대해 타임스탬프가 지정된 계정을 구축하여 각 개별 고객의 전체 상황을 파악할 수 있습니다 [!DNL Experience Platform].

스키마는 함께 사용할 수 있도록 [!DNL Real-time Customer Profile]하려면 기본 ID가 정의되어 있어야 합니다. 주 ID를 먼저 정의하지 않고 스키마를 활성화하려고 하면 &quot;기본 ID 누락&quot; 오류 메시지가 표시됩니다.

![](../images/tutorials/create-schema/missing_primary_identity.png)

편집기에서 사용할 &quot;충성도 멤버&quot; 스키마를 활성화하려면 먼저 편집기의 구조 [!DNL Profile]섹션에서 &quot;충성도 *멤버&quot;를* 클릭합니다.

편집기 오른쪽의 스키마 속성 *에서*&#x200B;표시 이름, 설명 및 유형을 포함한 스키마에 대한 정보가 표시됩니다. 이 정보 외에 프로필 표시/숨기기 단추도 **[!UICONTROL 있습니다]**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

[ **[!UICONTROL 프로필]** ]을 클릭하면 스키마를 활성화할지 여부를 묻는 팝업 창이 나타납니다 [!DNL Profile].

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>스키마를 사용하도록 설정하고 저장한 후에는 [!DNL Real-time Customer Profile] 비활성화할 수 없습니다.

## 다음 단계 및 추가 리소스

이제 &quot;[!UICONTROL 충성도 멤버]&quot; 스키마 작성을 마쳤으므로 편집기의 *구조* 섹션에서 전체 스키마를 볼 수 있습니다. 저장 **[!UICONTROL 을]** 클릭하면 [!DNL Schema Library]스키마가 저장되고 여기에서 액세스할 수 [!DNL Schema Registry]있습니다.

이제 새 스키마를 사용하여 데이터를 인제스트할 수 있습니다 [!DNL Platform]. 스키마를 사용하여 데이터를 인제스트하면 추가 변경만 가능합니다. 스키마 버전 관리에 대한 자세한 내용은 [스키마](../schema/composition.md) 구성의 기본 사항을 참조하십시오.

&quot;[!UICONTROL 충성도 멤버]&quot; 스키마는 [!DNL Schema Registry] API를 사용하여 보고 관리할 수도 있습니다. API로 작업을 시작하려면 먼저 스키마 레지스트리 API [개발자 안내서를 읽어 봅니다](../api/getting-started.md).

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

다음 비디오에서는 [!DNL Platform] UI에서 간단한 스키마를 만드는 방법을 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

다음 비디오에서는 혼합기 및 수업 사용에 대한 이해를 높이기 위해 제작되었습니다.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 부록

다음 정보는 스키마 편집기 자습서에 보충 사항입니다.

### Create a new class {#create-new-class}

[!DNL Experience Platform] 조직에 고유한 클래스를 기반으로 스키마를 정의할 수 있는 유연성을 제공합니다.

스키마 편집기의 *[!UICONTROL 클래스]* 섹션 **[!UICONTROL 에서 할당을]** 클릭하여 *[!UICONTROL 클래스]* 할당 대화상자를 엽니다. 대화 상자에서 새 클래스 **[!UICONTROL 만들기를 선택합니다&#x200B;]**.

그런 다음 새 클래스에 **[!UICONTROL 표시 이름]** (클래스에 대해 짧고 설명적이며 고유하며 사용자에게 친숙한 이름) **[!UICONTROL , 설명]**, 그리고 **[!UICONTROL 동작(&quot;RecordRecord]** &quot; 또는 &quot;TimeSeries&quot;라고[!UICONTROL 정의되는 데이터에 대해]Display Name[!UICONTROL (&quot;]RecordOr &quot;TimeSeries&quot;라고)을 지정할 수 있습니다.

![새 클래스 세부 사항](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>조직에서 정의한 클래스를 구현하는 스키마를 빌드할 때는 mixins를 호환되는 클래스에서만 사용할 수 있다는 점을 참고하십시오. 정의한 클래스는 새로 만들어지므로 [혼합 *추가] 대화 상자에 호환되는 믹스가* 없습니다. 대신 [새 혼합 **[!UICONTROL 만들기]를 선택하고 해당]** 클래스에 사용할 믹신을 정의해야 합니다. 다음에 새 클래스를 구현하는 스키마를 작성할 때 정의한 혼합이 나열되고 사용할 수 있습니다.

### 스키마 클래스 변경 {#change-class}

초기 스키마 작성 프로세스 중에 언제든지 스키마를 저장하기 전에 스키마를 기반으로 하는 클래스를 변경할 수 있습니다.

>[!WARNING]
>
>수업을 변경하기 전에 주의하세요. 믹스는 특정 클래스와 호환되므로 클래스를 변경하면 캔버스가 재설정되고 해당 점에 추가한 모든 필드가 제거됩니다.

클래스를 변경하려면 편집기의 **[!UICONTROL 컴포지션]** 섹션에서 ** 클래스 *[!UICONTROL 옆에 있는]* 할당을클릭합니다.

클래스 *[!UICONTROL 할당]* 대화 상자가 열리면 사용 가능한 목록에서 새 클래스를 선택할 수 있습니다. 클래스 **[!UICONTROL 할당을]** 클릭하면 새 클래스를 할당할지 여부를 확인하는 새 대화 상자가 열립니다.

![클래스 변경](../images/tutorials/create-schema/assign_new_class_warning.png)

클래스 변경을 확인하면 캔버스가 재설정되고 모든 컴포지션 진행 상태가 손실됩니다.