---
keywords: Experience Platform;홈;인기 항목;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;만들기;데이터 유형;데이터 유형;데이터 유형;데이터 유형
solution: Experience Platform
title: UI를 사용하여 데이터 유형 만들기 및 편집
topic-legacy: tutorial
type: Tutorial
description: Experience Platform 사용자 인터페이스에서 데이터 유형을 만들고 편집하는 방법을 알아봅니다.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# UI를 사용하여 데이터 유형 만들기 및 편집

XDM(Experience Data Model)에서 데이터 유형은 기본 리터럴 필드와 같은 방식으로 클래스 또는 믹싱에서 참조 유형 필드로 사용되며, 데이터 유형이 여러 하위 필드를 정의할 수 있다는 점에서 중요한 차이가 있습니다. 여러 필드 구조를 일관되게 사용할 수 있다는 점에서 믹싱과 유사하지만 데이터 유형은 스키마 구조의 어느 부분이든지 포함할 수 있지만 루트 수준에서만 혼합을 추가할 수 있으므로 보다 유연합니다.

Adobe Experience Platform은 다양한 일반적인 경험 관리 사용 사례를 처리하는 데 사용할 수 있는 다양한 표준 데이터 유형을 제공합니다. 그러나 고유한 비즈니스 요구 사항을 충족하기 위해 고유한 사용자 지정 데이터 유형을 정의할 수도 있습니다.

이 자습서에서는 플랫폼 사용자 인터페이스에서 사용자 지정 데이터 유형을 만들고 편집하는 단계를 설명합니다.

## 전제 조건

이 가이드를 사용하려면 XDM 시스템에 대한 작업 이해가 필요합니다. Experience Platform 에코시스템 내의 XDM 역할에 대한 소개를 보려면 [XDM 개요](../../home.md) 및 데이터 유형이 XDM 스키마에 기여하는 방법에 대한 스키마 구성](../../schema/composition.md)의 기본을 참조하십시오.[

이 안내서는 필요하지 않지만 [!DNL Schema Editor]의 다양한 기능에 익숙해지려면 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성의 자습서를 따르는 것이 좋습니다.

## 데이터 유형에 대해 [!DNL Schema Editor] 열기

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL Schemas]**&#x200B;을 선택하여 [!UICONTROL Schemas] 작업 영역을 연 다음 **[!UICONTROL Data types]** 탭을 선택합니다. Adobe에 정의된 데이터 유형과 조직에서 만든 데이터 유형 목록이 표시됩니다.

![](../../images/ui/resources/data-types/data-types-tab.png)

여기서 두 가지 옵션이 있습니다.

- [새 데이터 유형 만들기](#create)
- [편집할 기존 데이터 유형 선택](#edit)

### 새 데이터 유형 {#create} 만들기

**[!UICONTROL Data types]** 탭에서 **[!UICONTROL Create data type]**&#x200B;을 선택합니다.

![](../../images/ui/resources/data-types/create.png)

캔버스에 새 데이터 유형의 현재 구조를 보여주는 [!DNL Schema Editor]이 나타납니다. 편집기의 오른쪽에서 데이터 유형에 대한 표시 이름과 선택적 설명을 제공할 수 있습니다. 스키마에 추가할 때 식별되는 데이터 유형에 대해 고유하고 간결한 이름을 제공해야 합니다.

이 자습서에서는 레스토랑 속성을 설명하는 데이터 유형을 만들어 데이터 유형에 &quot;Restaurant&quot;이라는 표시 이름이 지정됩니다.

![](../../images/ui/resources/data-types/data-type-properties.png)

여기서 [다음 섹션](#add-fields)으로 건너뛰어 새 데이터 유형에 필드를 추가하기 시작할 수 있습니다.

### 기존 데이터 유형 편집

조직에서 정의한 사용자 지정 데이터 유형만 편집할 수 있습니다. 표시된 목록의 범위를 좁히려면 필터 아이콘(![필터 아이콘](../../images/ui/resources/data-types/filter.png))을 선택하여 [!UICONTROL Owner]를 기준으로 필터링 컨트롤을 표시합니다. 조직에서 소유한 사용자 지정 데이터 유형만 표시하려면 **[!UICONTROL Customer]**&#x200B;을 선택합니다.

목록에서 편집할 데이터 유형을 선택하여 오른쪽 레일을 열고 데이터 유형의 세부 사항을 표시합니다. 오른쪽 레일에 있는 데이터 유형의 이름을 선택하여 [!DNL Schema Editor]에서 해당 구조를 엽니다.

![](../../images/ui/resources/data-types/edit.png)

## 데이터 유형 {#add-fields}에 필드 추가

데이터 유형에 필드 추가를 시작하려면 캔버스의 루트 수준 필드 옆에 있는 **더하기(+)** 아이콘을 선택합니다. 새 필드가 아래에 나타나고 새 필드에 대한 표시 컨트롤을 표시하는 오른쪽 레일이 업데이트됩니다.

![](../../images/ui/resources/data-types/new-field.png)

오른쪽 레일의 컨트롤을 사용하여 새 필드의 세부 사항을 구성합니다. 필드를 구성하고 데이터 유형에 추가하는 방법에 대한 특정 단계는 [UI](../fields/overview.md#define)에서 필드 정의 가이드를 참조하십시오.

레스토랑 데이터 유형에는 레스토랑 이름을 나타내는 문자열 필드가 필요합니다. 이와 같이 [!UICONTROL Field name]은 &quot;name&quot;으로 설정되고 [!UICONTROL Type]은 &quot;[!UICONTROL String]&quot;로 설정됩니다. **[!UICONTROL Apply]**&#x200B;을 선택하여 필드에 변경 내용을 적용합니다.

![](../../images/ui/resources/data-types/name-field.png)

필요에 따라 데이터 유형에 필드를 계속 추가합니다. 예제 레스토랑 데이터 유형에는 이제 브랜드, 좌석 공간 및 바닥 공간에 대한 추가 필드가 있습니다.

![](../../images/ui/resources/data-types/more-fields.png)

기본 필드 외에도 사용자 지정 데이터 유형 내에 추가 데이터 유형을 중첩할 수도 있습니다. 예를 들어 Restaurant 데이터 유형에는 속성의 실제 주소를 나타내는 필드가 필요합니다. 이 시나리오에서는 표준 데이터 유형 &quot;[!UICONTROL Postal address]&quot;이 지정된 새 &quot;주소&quot; 필드를 추가할 수 있습니다.

![](../../images/ui/resources/data-types/address-field.png)

이는 데이터를 설명하는 관점에서 유연한 데이터 유형을 어떻게 활용하는지 보여줍니다.데이터 유형은 추가 데이터 유형을 포함할 수 있는 데이터 유형인 필드를 사용할 수 있습니다. 따라서 XDM 스키마 전체에서 일반적인 데이터 패턴을 추상하고 재사용할 수 있으므로 복잡한 데이터 구조를 쉽게 나타낼 수 있습니다.

데이터 유형에 필드 추가가 완료되면 **[!UICONTROL Save]**&#x200B;을 선택하여 변경 내용을 저장하고 데이터 유형을 [!DNL Schema Library]에 추가합니다.

## 클래스 또는 믹싱에 데이터 유형 추가

데이터 유형을 생성한 후 스키마에서 사용할 수 있습니다. XDM 스키마는 클래스와 0개 이상의 혼합으로 구성되므로 데이터 형식에서 제공하는 필드를 스키마에 직접 추가할 수 없습니다. 대신 교실 또는 혼합기에 포함되어야 합니다.

[클래스](./classes.md#add-fields) 또는 [믹신](./mixins.md#add-fields)에 필드를 추가하는 것과 관련된 단계를 따라 시작합니다. 새 필드에 **[!UICONTROL Type]**&#x200B;을 선택하는 경우 드롭다운 메뉴에서 데이터 유형의 이름을 선택합니다.

## 다중 필드 개체를 데이터 형식 {#convert}으로 변환

[!DNL Schema Editor]에서 여러 하위 필드가 있는 객체 유형 필드를 만들 때 해당 필드를 데이터 유형으로 변환할 수 있으므로 다른 클래스 또는 믹싱에 동일한 필드 구조를 사용할 수 있습니다.

객체 유형 필드를 데이터 유형으로 변환하려면 캔버스에서 필드를 선택합니다. 필드를 변환하기 전에 **[!UICONTROL Display name]**&#x200B;이 데이터 유형의 이름이 되므로 객체가 포함할 데이터를 설명하는지 확인합니다. 필드를 변환할 준비가 되면 오른쪽 레일에서 **[!UICONTROL Convert to new data type]**&#x200B;을 선택합니다.

![](../../images/ui/resources/data-types/convert-object.png)

캔버스는 필드의 데이터 유형을 &quot;[!UICONTROL Object]&quot;에서 새 데이터 유형으로 업데이트합니다. 하위 필드 옆에는 더 이상 개별 필드가 아니라 다중 필드 데이터 유형의 일부임을 나타내는 작은 잠금 아이콘도 있습니다. 이제 새 필드를 정의할 때 **[!UICONTROL Type]** 드롭다운에서 이 데이터 유형을 선택하여 다른 클래스 및 믹스에서 이 구조를 다시 사용할 수 있습니다.

![](../../images/ui/resources/data-types/converted.png)

## 다음 단계

이 안내서에서는 플랫폼 UI를 사용하여 데이터 유형을 만들고 편집하는 방법에 대해 설명합니다. [!UICONTROL Schemas] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](../overview.md)를 참조하십시오.

[!DNL Schema Registry] API를 사용하여 데이터 유형을 관리하는 방법에 대해 알아보려면 [데이터 유형 끝점 안내서](../../api/data-types.md)를 참조하십시오.
