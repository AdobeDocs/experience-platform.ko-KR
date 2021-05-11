---
keywords: Experience Platform;홈;인기 항목;UI;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;탐색;클래스;필드 그룹;데이터 유형;스키마
solution: Experience Platform
title: UI에서 XDM 리소스 살펴보기
description: Experience Platform 사용자 인터페이스에서 기존 스키마, 클래스, 스키마 필드 그룹 및 데이터 유형을 탐색하는 방법을 알아봅니다.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: ddf66ab277e5882afe7ffbdd87ee5df958c3e7b0
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# UI에서 XDM 리소스 살펴보기

Adobe Experience Platform에서 모든 XDM(경험 데이터 모델) 리소스는 Adobe에서 제공하는 표준 리소스와 조직에서 정의한 사용자 지정 리소스를 포함하여 [!DNL Schema Library]에 저장됩니다. Experience Platform UI에서는 [!DNL Schema Library]에서 기존 스키마, 클래스, 스키마 필드 그룹 또는 데이터 유형의 구조와 필드를 볼 수 있습니다. 이 기능은 UI가 이러한 XDM 리소스에서 제공하는 각 필드의 예상 데이터 유형 및 사용 사례에 대한 정보를 제공하므로 데이터 수집에 대한 계획 및 준비를 할 때 특히 유용합니다.

이 자습서에서는 Experience Platform UI에서 기존 스키마, 클래스, 필드 그룹 및 데이터 유형을 탐색하는 단계를 설명합니다.

## XDM 리소스 {#lookup} 조회

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL Schemas]**&#x200B;을 선택합니다. [!UICONTROL Schemas] 작업 영역에는 **[!UICONTROL Browse]** 탭과 **[!UICONTROL Classes]**, **[!UICONTROL Field groups]** 및 **[!UICONTROL Data types]**&#x200B;을(를) 자세히 살펴보기 위한 추가 전용 탭이 포함되어 있으므로 조직의 모든 기존 XDM 리소스를 검색할 수 있습니다.

![](../images/ui/explore/tabs.png)

[!UICONTROL Browse] 탭에서 필터 아이콘(![필터 아이콘 이미지](../images/ui/explore/icon.png))을 사용하여 왼쪽 레일에 컨트롤을 표시하여 나열된 결과를 좁힐 수 있습니다.

예를 들어 Adobe에서 제공하는 표준 데이터 유형만 표시하도록 목록을 필터링하려면 각각 **[!UICONTROL Type]** 및 **[!UICONTROL Owner]** 섹션 아래에서 **[!UICONTROL Datatype]** 및 **[!UICONTROL Adobe]**&#x200B;을 선택합니다.

**[!UICONTROL Included in Profile]** 토글을 사용하면 결과를 필터링하여 [실시간 고객 프로필](../../profile/home.md)에서 사용할 수 있도록 활성화된 스키마에서 사용된 리소스만 표시할 수 있습니다.

![](../images/ui/explore/filter.png)

검색 막대를 사용하여 검색 결과의 범위를 더 좁힐 수도 있습니다. 검색어를 검색할 때 상위 항목은 이름이 검색 쿼리와 일치하는 리소스를 나타냅니다. 이 항목 아래의 **[!UICONTROL Standard Fields]** 아래에 쿼리와 일치하는 필드를 포함하는 리소스가 나열됩니다. 따라서 사전에 리소스의 이름을 알지 않아도 포함된 데이터 유형을 기준으로 XDM 리소스를 검색할 수 있습니다.

![](../images/ui/explore/search.png)

검색 결과에 표시된 리소스는 제목과 일치하여 먼저 정렬한 다음 설명별로 정렬됩니다. 이러한 카테고리 중 하나에서 일치하는 단어가 더 많을수록 리소스가 목록에 더 많이 나타납니다.

>[!NOTE]
>
>표준 XDM 리소스의 경우 검색 기능은 `xdm` 네임스페이스를 포함하는 개별 필드만 반환합니다. 다른 네임스페이스(예: 테넌트 ID)에 있는 필드는 사용자 지정 리소스에 포함된 경우에만 반환됩니다.

탐색할 리소스를 찾은 경우 목록에서 해당 이름을 선택하여 캔버스에서 해당 구조를 봅니다.

## 캔버스에서 XDM 리소스 탐색 {#explore}

리소스를 선택하면 해당 구조가 캔버스에서 열립니다.

![](../images/ui/explore/canvas.png)

하위 속성을 포함하는 모든 객체 유형 필드는 처음 캔버스에 표시될 때 기본적으로 축소됩니다. 필드의 하위 속성을 표시하려면 해당 이름 옆에 있는 아이콘을 선택합니다.

![](../images/ui/explore/field-expand.png)

### 시스템 생성 필드 {#system-fields}

일부 필드 이름에는 `_repo` 및 `_id` 등의 밑줄이 추가됩니다. 데이터가 인제스트될 때 시스템에서 자동으로 생성하고 할당할 필드의 자리 표시자를 나타냅니다.

따라서 이러한 필드의 대부분은 플랫폼에 인제스트할 때 데이터 구조에서 제외되어야 합니다. 이 규칙의 주요 예외는 [`_{TENANT_ID}` 필드](../api/getting-started.md#know-your-tenant_id)입니다. 이 필드는 조직 아래에 만들어진 모든 XDM 필드를 지정해야 합니다.

### 데이터 유형 {#data-types}

캔버스에 표시된 각 필드에 대해 해당 데이터 유형이 이름 옆에 표시되어 필드가 수집해야 하는 데이터 유형을 한눈에 나타냅니다.

![](../images/ui/explore/data-types.png)

대괄호(`[]`)가 추가되는 모든 데이터 유형은 해당 특정 데이터 유형의 배열을 나타냅니다. 예를 들어 **[!UICONTROL String]\[]**&#x200B;의 데이터 유형은 필드에 문자열 값 배열이 필요함을 나타냅니다. **[!UICONTROL Payment Item]\[]**&#x200B;의 데이터 유형은 [!UICONTROL Payment Item] 데이터 유형을 준수하는 개체의 배열을 나타냅니다.

배열 필드가 객체 유형을 기반으로 하는 경우 캔버스에서 해당 아이콘을 선택하여 각 배열 항목에 대해 필요한 속성을 표시할 수 있습니다.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

캔버스의 필드 이름을 선택하면 오른쪽 레일이 업데이트되어 **[!UICONTROL Field properties]** 아래에 해당 필드에 대한 세부 정보가 표시됩니다. 여기에는 필드의 의도된 사용 사례 설명, 기본값, 패턴, 형식, 필드 필수 여부 등이 포함될 수 있습니다.

![](../images/ui/explore/field-properties.png)

검사하려는 필드가 열거형 필드이면 오른쪽 레일에 필드가 받을 허용 가능한 값도 표시됩니다.

![](../images/ui/explore/enum-field.png)

### ID 필드 {#identity}

ID 필드를 포함하는 스키마를 검사할 때 이러한 필드는 스키마에 해당 필드를 제공하는 클래스 또는 필드 그룹 아래의 왼쪽 레일에 나열됩니다. 왼쪽 레일에서 ID 필드 이름을 선택하여 깊이 중첩에 상관없이 캔버스의 필드를 표시합니다.

ID 필드는 지문 아이콘(![지문 아이콘 이미지](../images/ui/explore/identity-symbol.png))으로 캔버스에서 강조 표시됩니다. ID 필드의 이름을 선택하면 [identity namespace](../../identity-service/namespaces.md) 및 해당 필드가 스키마의 기본 ID인지 여부와 같은 추가 정보를 볼 수 있습니다.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>ID 필드 및 다운스트림 플랫폼 서비스와의 관계에 대한 자세한 내용은 [ID 필드 정의](./fields/identity.md)에 대한 안내서를 참조하십시오.

### 관계 필드 {#relationship}

관계 필드를 포함하는 스키마를 검사하는 경우 필드가 **[!UICONTROL Relationships]** 아래의 왼쪽 레일에 나열됩니다. 왼쪽 레일에서 관계 필드 이름을 선택하여 깊이 중첩에 상관없이 캔버스에 필드를 표시합니다.

관계 필드도 캔버스에서 고유하게 강조 표시되어 필드가 참조하는 대상 스키마의 이름을 표시합니다. 관계 필드의 이름을 선택하는 경우 오른쪽 레일에서 대상 스키마의 기본 ID의 ID 네임스페이스를 볼 수 있습니다.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>XDM 스키마에서 관계 사용에 대한 자세한 내용은 [UI](../tutorials/relationship-ui.md)에서 관계 만들기에 대한 자습서를 참조하십시오.

## 다음 단계

이 문서에서는 Experience Platform UI에서 기존 XDM 리소스를 탐색하는 방법을 다룹니다. [!UICONTROL Schemas] 작업 영역과 [!DNL Schema Editor]의 다른 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](./overview.md)를 참조하십시오.
