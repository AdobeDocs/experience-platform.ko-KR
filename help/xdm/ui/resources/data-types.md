---
keywords: Experience Platform;홈;인기 주제;ui;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;스키마;만들기;데이터 유형;데이터 유형;
solution: Experience Platform
title: UI를 사용하여 데이터 유형 만들기 및 편집
type: Tutorial
description: Experience Platform 사용자 인터페이스에서 데이터 유형을 만들고 편집하는 방법을 알아봅니다.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 4214339c4a661c6bca2cd571919ae205dcb47da1
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 5%

---

# UI를 사용하여 데이터 유형 만들기 및 편집 {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="표준 또는 사용자 정의 데이터 유형 필터"
>abstract="사용 가능한 데이터 유형의 목록은 클래스의 생성 방법에 따라 사전에 필터링됩니다. 표준과 사용자 정의 옵션 중에서 선택하려면 라디오 버튼을 선택하십시오. 표준 옵션은 Adobe에서 생성한 엔티티를 표시하며 사용자 정의 옵션은 내 조직 내에서 생성된 엔티티를 표시합니다. 데이터 유형의 생성 및 편집에 대한 자세한 내용은 설명서를 참조하시기 바랍니다."

XDM(Experience Data Model)에서 데이터 유형은 여러 하위 필드를 포함하는 재사용 가능한 필드입니다. 다중 필드 구조를 일관되게 사용할 수 있다는 점에서 스키마 필드 그룹과 유사하지만, 데이터 유형은 스키마 구조의 모든 위치에 포함될 수 있는 반면 필드 그룹은 루트 수준에서만 추가할 수 있으므로 보다 유연합니다.

Adobe Experience Platform은 광범위한 일반적인 경험 관리 사용 사례를 다루는 데 사용할 수 있는 많은 표준 데이터 유형을 제공합니다. 하지만 고유한 비즈니스 요구 사항을 충족하기 위해 고유한 사용자 지정 데이터 유형을 정의할 수도 있습니다.

이 자습서에서는 Platform 사용자 인터페이스에서 사용자 지정 데이터 유형을 만들고 편집하는 단계를 다룹니다.

## 전제 조건

이 안내서에서는 XDM 시스템에 대한 작업 이해가 필요합니다. 다음을 참조하십시오. [XDM 개요](../../home.md) Experience Platform 에코시스템 내에서 XDM의 역할 소개 및 [스키마 컴포지션 기본 사항](../../schema/composition.md) 데이터 유형이 XDM 스키마에 기여하는 방식에 대한 설명.

이 안내서에서는 필요하지 않지만, [UI에서 스키마 작성](../../tutorials/create-schema-ui.md) 의 다양한 기능에 익숙해지려면 [!DNL Schema Editor].

## 를 엽니다. [!DNL Schema Editor] 데이터 형식용 {#data-type}

Platform UI에서 를 선택합니다. **[!UICONTROL 스키마]** 을(를) 왼쪽 탐색에서 [!UICONTROL 스키마] 작업 영역을 선택한 다음 **[!UICONTROL 데이터 유형]** 탭. 사용 가능한 데이터 유형 목록이 표시됩니다. 데이터 유형 목록은 작성 방법에 따라 자동으로 필터링됩니다. 기본 설정은 Adobe에 의해 정의된 데이터 유형을 표시합니다. 목록을 필터링하여 조직에서 만든 목록을 표시할 수도 있습니다.

![다음 [!UICONTROL 스키마] 작업 공간 [!UICONTROL 스키마] 왼쪽 탐색 및 [!UICONTROL 데이터 유형] 강조 표시됨.](../../images/ui/resources/data-types/data-types-tab.png)

여기에서 다음 옵션을 사용할 수 있습니다.

- [새 데이터 유형 만들기](#create)
- [데이터 유형 필터링](#filter)
- [편집할 기존 데이터 유형 선택](#edit)

### 새 데이터 유형 만들기 {#create}

다음에서 **[!UICONTROL 데이터 유형]** 탭, 선택 **[!UICONTROL 데이터 유형 만들기]**.

![다음 [!UICONTROL 스키마] 작업 영역 [!UICONTROL 데이터 유형] 탭 [!UICONTROL 데이터 유형 만들기] 강조 표시됨.](../../images/ui/resources/data-types/create.png)

다음 [!DNL Schema Editor] 이 나타나고 캔버스에 새 데이터 유형의 현재 구조가 표시됩니다. 편집기의 오른쪽에서 데이터 유형에 대한 표시 이름과 설명(선택 사항)을 제공할 수 있습니다. 데이터 유형을 스키마에 추가할 때 데이터 유형을 식별하는 방법이므로 데이터 유형에 고유하고 간결한 이름을 제공해야 합니다.

이 자습서에서는 레스토랑 속성을 설명하는 데이터 형식을 만들어 데이터 형식에 &quot;Restaurant&quot;이라는 표시 이름을 지정합니다.

![](../../images/ui/resources/data-types/data-type-properties.png)

여기에서 다음으로 건너뛸 수 있습니다. [다음 섹션](#add-fields) 을 클릭하여 필드를 새 데이터 형식에 추가합니다.

### 데이터 유형 필터링 {#filter}

사용 가능한 데이터 유형의 목록은 클래스의 생성 방법에 따라 사전에 필터링됩니다. 라디오 단추를 선택하여 다음 중 하나를 선택합니다. [!UICONTROL 표준] 및 [!UICONTROL 사용자 정의] 옵션. 다음 [!UICONTROL 표준] 옵션은 Adobe 및 [!UICONTROL 사용자 정의] 옵션은 조직 내에서 생성된 엔티티를 표시합니다.

![다음 [!UICONTROL 데이터 유형] 의 탭 [!UICONTROL 스키마] 작업 공간 [!UICONTROL 표준] 및 [!UICONTROL 사용자 정의] 강조 표시됨.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### 기존 데이터 유형 편집 {#edit}

>[!NOTE]
>
>실시간 고객 프로필에서 사용할 수 있도록 설정된 스키마에서 기존 데이터 유형을 사용하면 그 이후에 해당 데이터 유형에 대해 비파괴인 변경만 수행할 수 있습니다. 다음을 참조하십시오. [스키마 진화 규칙](../../schema/composition.md#evolution) 추가 정보.

조직에서 정의한 사용자 정의 데이터 유형만 편집할 수 있습니다. 선택 **[!UICONTROL 사용자 정의]** 조직에서 소유한 사용자 지정 데이터 유형만 표시합니다.

목록에서 편집할 데이터 유형을 선택하여 오른쪽 레일을 열고 데이터 유형의 세부 정보를 표시합니다. 세부 정보 패널에서 샘플 파일을 다운로드하거나, JSON 구조를 복사하거나, 데이터 유형을 패키지에 추가할 수도 있습니다.

오른쪽 레일에서 데이터 유형의 이름을 선택하여 [!DNL Schema Editor].

![다음 [!UICONTROL 데이터 유형] 의 탭 [!UICONTROL 스키마] 작업 영역, 데이터 유형 포함, [!UICONTROL 사용자 정의] 및 데이터 유형 [!UICONTROL 이름] 강조 표시됨.](../../images/ui/resources/data-types/edit.png)

## 데이터 유형에 필드 추가 {#add-fields}

데이터 형식에 필드를 추가하려면 **더하기(+)** (캔버스에서 루트 레벨 필드 옆에 있는 아이콘) 아래에 새 필드가 나타나고 오른쪽 레일이 업데이트되어 새 필드에 대한 컨트롤이 표시됩니다.

![](../../images/ui/resources/data-types/new-field.png)

오른쪽 레일의 컨트롤을 사용하여 새 필드의 세부 정보를 구성합니다. 다음 안내서를 참조하십시오 [UI의 필드 정의](../fields/overview.md#define) 를 사용하여 필드를 구성하고 데이터 유형에 추가하는 방법에 대한 구체적인 단계를 살펴보십시오.

Restaurant 데이터 형식에는 레스토랑 이름을 나타내는 문자열 필드가 필요합니다. 따라서 [!UICONTROL 필드 이름] 은 &quot;name&quot;으로 설정되고 [!UICONTROL 유형] 이(가) &quot;(으)로 설정됨[!UICONTROL 문자열]&quot;. 선택 **[!UICONTROL 적용]** 를 눌러 필드에 변경 사항을 적용합니다.

![](../../images/ui/resources/data-types/name-field.png)

필요에 따라 데이터 유형에 필드를 계속 추가합니다. 예제 Restaurant 데이터 유형에는 이제 브랜드, 좌석 용량 및 공간에 대한 추가 필드가 있습니다.

![](../../images/ui/resources/data-types/more-fields.png)

기본 필드 외에도 사용자 지정 데이터 유형 내에 추가 데이터 유형을 중첩할 수도 있습니다. 예를 들어 Restaurant 데이터 형식에는 속성의 실제 주소를 나타내는 필드가 필요합니다. 이 시나리오에서는 표준 데이터 유형 &quot;&quot;에 할당된 새 &quot;주소&quot; 필드를 추가할 수 있습니다.[!UICONTROL 우편 주소]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

이는 데이터를 설명하는 측면에서 데이터 유형이 얼마나 유연한 지를 보여 줍니다. 데이터 유형은 추가 데이터 유형을 포함할 수 있는 데이터 유형이기도 한 필드를 사용할 수 있습니다. 이를 통해 XDM 스키마 전체에서 일반적인 데이터 패턴을 추상화하고 재사용할 수 있으므로 복잡한 데이터 구조를 더 쉽게 나타낼 수 있습니다.

데이터 유형에 필드 추가를 완료했으면 을 선택합니다. **[!UICONTROL 저장]** 변경 사항을 저장하고 데이터 형식을 [!DNL Schema Library].

## 스키마에 데이터 유형 추가

데이터 유형을 만든 후에는 스키마에서 사용을 시작할 수 있습니다. XDM 스키마는 클래스와 0개 이상의 필드 그룹으로 구성되므로 데이터 유형에서 제공하는 필드를 스키마에 직접 추가할 수 없습니다. 대신 클래스 또는 필드 그룹에 포함되어야 합니다.

관련 단계를 따라 시작하십시오. [클래스에 필드 추가](./classes.md#add-fields) 또는 [필드 그룹에 필드 추가](./field-groups.md#add-fields). 또는 다음을 시작할 수 있습니다 [스키마에 직접 필드 추가](./schemas.md#add-individual-fields) 상위 클래스 또는 필드 그룹을 선택합니다. 다음을 선택할 때 **[!UICONTROL 유형]** 새 필드의 드롭다운 메뉴에서 데이터 유형 이름을 선택합니다.

## 다중 필드 개체를 데이터 형식으로 변환 {#convert}

에 여러 하위 필드가 있는 개체 유형 필드를 만들 때 [!DNL Schema Editor], 다른 클래스나 필드 그룹에서 동일한 필드 구조를 사용할 수 있도록 해당 필드를 데이터 형식으로 변환할 수 있습니다.

개체 유형 필드를 데이터 유형으로 변환하려면 캔버스에서 필드를 선택합니다. 필드를 변환하기 전에 **[!UICONTROL 표시 이름]** 는 데이터 유형의 이름이 되므로 개체가 포함할 데이터를 설명합니다. 필드를 변환할 준비가 되면 다음을 선택합니다. **[!UICONTROL 새 데이터 유형으로 전환]** 오른쪽 레일에서.

![](../../images/ui/resources/data-types/convert-object.png)

캔버스는 &quot;&quot;에서 필드의 데이터 유형을 업데이트합니다.[!UICONTROL 오브젝트]&quot;새 데이터 유형. 이제 필드에서 이 데이터 유형을 선택하여 다른 클래스와 필드 그룹에서 이 구조를 재사용할 수 있습니다. **[!UICONTROL 유형]** 드롭다운(새 필드 정의 시)

![](../../images/ui/resources/data-types/converted.png)

## 다음 단계

이 안내서에서는 Platform UI를 사용하여 데이터 유형을 만들고 편집하는 방법을 다룹니다. 의 기능에 대한 자세한 내용 [!UICONTROL 스키마] 작업 영역에서 다음을 참조하십시오 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md).

을(를) 사용하여 데이터 유형을 관리하는 방법을 알아보려면 [!DNL Schema Registry] API에서 다음을 참조하십시오. [data types endpoint 안내서](../../api/data-types.md).
