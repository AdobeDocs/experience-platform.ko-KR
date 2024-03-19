---
title: UI에서 맵 필드 정의
description: Experience Platform 사용자 인터페이스에서 맵 필드를 정의하는 방법을 알아봅니다.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# UI에서 맵 필드 정의

Adobe Experience Platform을 사용하면 사용자 지정 XDM(경험 데이터 모델) 클래스, 스키마 필드 그룹 및 데이터 유형의 구조를 완전히 사용자 지정할 수 있습니다.

스키마 편집기에서 맵 필드를 정의하여 유연하고 동적인 데이터 구조를 모델링하거나 키-값 쌍의 컬렉션을 저장할 수도 있습니다. 맵 데이터 구조를 사용하면 고유 식별자를 기반으로 정보를 구성하고 액세스하는 곳에서 효율적이고 빠른 조회, 삽입 및 삭제를 수행할 수 있습니다.

Platform UI(사용자 인터페이스)에서 새 필드를 정의할 때 **[!UICONTROL 유형]** 드롭다운을 클릭하고 &quot;**[!UICONTROL 맵]**&#x200B;목록에 있는 &quot;.

![유형 드롭다운 및 맵 값이 강조 표시된 스키마 편집기.](../../images/ui/fields/special/map.png)

A [!UICONTROL 맵 값 유형] 속성이 나타납니다. 이 값은 다음 경우에 필요합니다. [!UICONTROL 맵] 데이터 유형. 맵에 사용할 수 있는 값은 다음과 같습니다 [!UICONTROL 문자열] 및 [!UICONTROL 정수]. 사용 가능한 옵션 드롭다운 목록에서 값을 선택합니다.

![를 사용하는 스키마 편집기 [!UICONTROL 맵 값 유형] 드롭다운이 강조 표시됩니다.](../../images/ui/fields/special/map-value-type.png)

하위 필드를 구성한 후에는 필드 그룹에 지정해야 합니다. 사용 **[!UICONTROL 필드 그룹]** 드롭다운 메뉴 또는 검색 필드를 선택한 다음 **[!UICONTROL 적용]**. 동일한 프로세스를 사용하여 객체에 필드를 계속 추가하거나 다음을 선택할 수 있습니다 **[!UICONTROL 저장]** 설정을 확인합니다.

![필드 그룹 선택 사항 및 적용 중인 설정의 기록입니다.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>Platform UI는 맵 유형 필드의 키를 추출하는 방법에 제한이 있습니다. 개체 유형 필드는 확장할 수 있지만 맵은 대신 단일 필드로 표시됩니다. 문자열 또는 정수 데이터 유형이 아닌 스키마 레지스트리 API를 통해 생성된 맵 필드는 &quot;로 표시됩니다.[!UICONTROL 복합]&quot;데이터 유형.

## 다음 단계

이제 이 문서를 읽고 Platform UI에서 맵 필드를 정의할 수 있습니다. 클래스와 필드 그룹만 사용하여 스키마에 필드를 추가할 수 있습니다. UI에서 이러한 리소스를 관리하는 방법에 대한 자세한 내용은 만들기 및 편집에 대한 안내서를 참조하십시오. [클래스](../resources/classes.md) 및 [필드 그룹](../resources/field-groups.md).

의 기능에 대한 자세한 내용 [!UICONTROL 스키마] 작업 영역에서 다음을 참조하십시오 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md).
