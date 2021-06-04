---
keywords: Experience Platform;홈;인기 항목;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;생성;데이터 유형;데이터 유형;
solution: Experience Platform
title: UI를 사용하여 데이터 유형 만들기 및 편집
topic-legacy: tutorial
type: Tutorial
description: Experience Platform 사용자 인터페이스에서 데이터 유형을 만들고 편집하는 방법을 알아봅니다.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: bcacf2ebe99c3e397cfd5ceaf418a51bec74e659
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# UI를 사용하여 데이터 유형 만들기 및 편집

XDM(Experience Data Model)에서 여러 하위 필드를 포함하는 데이터 유형 재사용 가능한 필드입니다. 는 의 스키마 필드 그룹과 유사하지만, 여러 필드 구조를 일관되게 사용할 수 있다는 점에서 데이터 유형은 스키마 구조의 어느 곳에서든 포함할 수 있지만 필드 그룹은 루트 수준에서만 추가할 수 있으므로 보다 유연합니다.

Adobe Experience Platform에서는 다양한 일반적인 경험 관리 사용 사례를 다루는 데 사용할 수 있는 다양한 표준 데이터 유형을 제공합니다. 그러나 고유한 비즈니스 요구 사항을 충족하기 위해 고유한 사용자 지정 데이터 유형을 정의할 수도 있습니다.

이 자습서에서는 Platform 사용자 인터페이스에서 사용자 지정 데이터 유형을 만들고 편집하는 단계를 설명합니다.

## 전제 조건

이 안내서에서는 XDM 시스템을 작업해야 합니다. Experience Platform 에코시스템 내에서 XDM의 역할에 대한 소개는 [XDM 개요](../../home.md) 를 참조하고, 데이터 유형이 XDM 스키마에 기여하는 방법은 스키마 구성](../../schema/composition.md)의 기본 사항을 참조하십시오.[

이 안내서에는 필요하지 않지만 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성을 위한 튜토리얼도 따라 [!DNL Schema Editor]의 다양한 기능에 익숙해지는 것이 좋습니다.

## 데이터 형식에 대해 [!DNL Schema Editor] 열기

Platform UI의 왼쪽 탐색 영역에서 **[!UICONTROL 스키마]**&#x200B;를 선택하여 [!UICONTROL 스키마] 작업 공간을 연 다음 **[!UICONTROL 데이터 유형]** 탭을 선택합니다. Adobe에 의해 정의된 데이터 유형과 조직에서 만든 데이터 유형을 포함하여 사용 가능한 데이터 유형 목록이 표시됩니다.

![](../../images/ui/resources/data-types/data-types-tab.png)

여기에서 두 가지 옵션을 사용할 수 있습니다.

- [새 데이터 유형 만들기](#create)
- [편집할 기존 데이터 유형을 선택합니다](#edit)

### 새 데이터 유형 만들기 {#create}

**[!UICONTROL 데이터 유형]** 탭에서 **[!UICONTROL 데이터 유형 만들기]**&#x200B;를 선택합니다.

![](../../images/ui/resources/data-types/create.png)

캔버스에서 새 데이터 유형의 현재 구조를 보여주는 [!DNL Schema Editor] 이 나타납니다. 편집기 오른쪽에서는 데이터 유형에 대한 표시 이름 및 선택적 설명을 제공할 수 있습니다. 스키마에 추가할 때 식별되는 방식으로 데이터 유형에 대해 고유하고 간결한 이름을 제공해야 합니다.

이 자습서에서는 레스토랑 속성을 설명하는 데이터 형식을 만들므로 데이터 형식에 &quot;Restaurant&quot;의 표시 이름이 지정됩니다.

![](../../images/ui/resources/data-types/data-type-properties.png)

여기에서 [다음 섹션](#add-fields)으로 건너뛰고 새 데이터 유형에 필드 추가를 시작할 수 있습니다.

### 기존 데이터 유형 편집

>[!NOTE]
>
>실시간 고객 프로필에서 사용할 수 있도록 활성화된 스키마에 기존 데이터 유형이 사용되면 이후 해당 데이터 유형에 비파괴만 변경할 수 있습니다. 자세한 내용은 스키마 진화 규칙](../../schema/composition.md#evolution)을 참조하십시오.[

조직에서 정의한 사용자 정의 데이터 유형만 편집할 수 있습니다. 표시된 목록의 범위를 좁히려면 필터 아이콘(![필터 아이콘](../../images/ui/resources/data-types/filter.png))을 선택하여 [!UICONTROL 소유자]를 기반으로 필터링을 위한 컨트롤을 표시합니다. 조직이 소유한 사용자 지정 데이터 유형만 표시하려면 **[!UICONTROL 고객]**&#x200B;을 선택합니다.

목록에서 편집할 데이터 유형을 선택하여 오른쪽 레일을 열고 데이터 유형의 세부 사항을 표시합니다. 오른쪽 레일에서 데이터 유형의 이름을 선택하여 [!DNL Schema Editor]에서 해당 구조를 엽니다.

![](../../images/ui/resources/data-types/edit.png)

## 데이터 형식 {#add-fields}에 필드를 추가합니다.

데이터 유형에 필드 추가를 시작하려면 캔버스에서 루트 수준 필드 옆에 있는 **더하기(+)** 아이콘을 선택합니다. 새 필드가 아래에 표시되고 오른쪽 레일이 업데이트되어 새 필드에 대한 컨트롤을 표시합니다.

![](../../images/ui/resources/data-types/new-field.png)

오른쪽 레일의 컨트롤을 사용하여 새 필드의 세부 사항을 구성합니다. 데이터 유형에 필드를 구성하고 추가하는 방법에 대한 특정 단계는 UI](../fields/overview.md#define)에서 필드 정의 의 안내서를 참조하십시오.[

레스토랑 데이터 유형에는 레스토랑 이름을 나타내는 문자열 필드가 필요합니다. 따라서 [!UICONTROL 필드 이름]은 &quot;name&quot;으로 설정되고 [!UICONTROL 유형]은 &quot;[!UICONTROL 문자열]&quot;로 설정됩니다. **[!UICONTROL 적용]**&#x200B;을 선택하여 필드에 변경 사항을 적용합니다.

![](../../images/ui/resources/data-types/name-field.png)

필요에 따라 데이터 유형에 필드를 계속 추가합니다. 예제 Restaurant 데이터 유형에는 브랜드, 좌석 용량 및 바닥 공간에 대한 추가 필드가 있습니다.

![](../../images/ui/resources/data-types/more-fields.png)

기본 필드 외에도 사용자 지정 데이터 유형에 추가 데이터 유형을 중첩할 수 있습니다. 예를 들어 Restaurant 데이터 유형에는 속성의 실제 주소를 나타내는 필드가 필요합니다. 이 시나리오에서는 표준 데이터 유형 &quot;[!UICONTROL 우편 주소]&quot;가 지정된 새 &quot;주소&quot; 필드를 추가할 수 있습니다.

![](../../images/ui/resources/data-types/address-field.png)

이는 데이터를 설명하는 측면에서 데이터 유형이 얼마나 유연한지를 보여줍니다.데이터 유형에는 추가적인 데이터 유형을 포함할 수 있는 데이터 형식인 필드를 사용할 수 있습니다. 이를 통해 XDM 스키마 전체에서 일반적인 데이터 패턴을 추상화하고 재사용할 수 있으므로 복잡한 데이터 구조를 보다 쉽게 나타낼 수 있습니다.

데이터 유형에 필드 추가를 완료했으면 **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 사항을 저장하고 데이터 유형을 [!DNL Schema Library]에 추가합니다.

## 클래스 또는 필드 그룹에 데이터 형식 추가

데이터 유형을 만들면 스키마에서 사용할 수 있습니다. XDM 스키마는 클래스와 0개 이상의 필드 그룹으로 구성되므로 데이터 형식에서 제공하는 필드를 직접 스키마에 추가할 수 없습니다. 대신 클래스 또는 필드 그룹에 포함해야 합니다.

[필드를 클래스](./classes.md#add-fields) 또는 [필드 그룹에 추가하는 것과 관련된 단계에 따라 시작하십시오.](./field-groups.md#add-fields) 새 필드에 대해 **[!UICONTROL 유형]**&#x200B;을 선택하는 경우 드롭다운 메뉴에서 데이터 유형의 이름을 선택합니다.

## 다중 필드 개체를 데이터 형식으로 변환 {#convert}

[!DNL Schema Editor]에서 여러 하위 필드가 있는 객체 유형 필드를 만들면 해당 필드를 데이터 유형으로 변환하여 다른 클래스 또는 필드 그룹에서 동일한 필드 구조를 사용할 수 있습니다.

객체 유형 필드를 데이터 유형으로 변환하려면 캔버스에서 필드를 선택합니다. 필드를 변환하기 전에 **[!UICONTROL 표시 이름]**&#x200B;이 데이터 유형의 이름이 되므로 개체가 포함할 데이터를 설명하는지 확인하십시오. 필드를 변환할 준비가 되면 오른쪽 레일에서 **[!UICONTROL 새 데이터 유형으로 변환]**&#x200B;을 선택합니다.

![](../../images/ui/resources/data-types/convert-object.png)

캔버스는 필드의 데이터 유형을 &quot;[!UICONTROL Object]&quot;에서 새 데이터 형식으로 업데이트합니다. 하위 필드 옆에는 작은 잠금 아이콘도 있어서 더 이상 개별 필드가 아니라 다중 필드 데이터 유형의 일부임을 나타냅니다. 이제 새 필드를 정의할 때 **[!UICONTROL 유형]** 드롭다운에서 이 데이터 유형을 선택하여 다른 클래스 및 필드 그룹에서 이 구조를 다시 사용할 수 있습니다.

![](../../images/ui/resources/data-types/converted.png)

## 다음 단계

이 안내서에서는 플랫폼 UI를 사용하여 데이터 유형을 만들고 편집하는 방법에 대해 설명합니다. [!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 공간 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 데이터 유형을 관리하는 방법에 대해 알려면 [데이터 유형 엔드포인트 가이드](../../api/data-types.md)를 참조하십시오.
