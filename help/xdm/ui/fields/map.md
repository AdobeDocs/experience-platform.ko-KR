---
title: UI에서 맵 필드 정의
description: Experience Platform 사용자 인터페이스에서 맵 필드를 정의하는 방법을 알아봅니다.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# UI에서 맵 필드 정의

Adobe Experience Platform을 사용하면 사용자 지정 XDM(경험 데이터 모델) 클래스, 스키마 필드 그룹 및 데이터 유형의 구조를 완전히 사용자 지정할 수 있습니다.

스키마 편집기에서 맵 필드를 정의하여 유연하고 동적인 데이터 구조를 모델링하거나 키-값 쌍의 컬렉션을 저장할 수도 있습니다.

Experience Platform UI(사용자 인터페이스)에서 새 필드를 정의할 때 **[!UICONTROL Type]** 드롭다운을 사용하고 목록에서 &quot;**[!UICONTROL 맵]**&quot;을(를) 선택하십시오.

![유형 드롭다운과 맵 값이 강조 표시된 스키마 편집기.](../../images/ui/fields/special/map.png)

[!UICONTROL 맵 값 형식] 속성이 나타납니다. 이 값은 [!UICONTROL 맵] 데이터 형식에 필요합니다. 맵에 사용할 수 있는 값은 [!UICONTROL 문자열] 및 [!UICONTROL 정수]입니다. 사용 가능한 옵션 드롭다운 목록에서 값을 선택합니다.

![[!UICONTROL 맵 값 형식] 드롭다운이 강조 표시된 스키마 편집기.](../../images/ui/fields/special/map-value-type.png)

하위 필드를 구성한 후에는 필드 그룹에 지정해야 합니다. **[!UICONTROL 필드 그룹]** 드롭다운 메뉴 또는 검색 필드를 사용하고 **[!UICONTROL 적용]**&#x200B;을(를) 선택하십시오. 동일한 프로세스를 사용하여 계속해서 개체에 필드를 추가하거나 **[!UICONTROL 저장]**&#x200B;을 선택하여 설정을 확인할 수 있습니다.

![필드 그룹 선택 및 설정이 적용된 기록입니다.](../../images/ui/fields/special/assign-to-field-group.gif)

## 사용 제한 사항 {#restrictions}

XDM에서는 이 데이터 유형의 사용에 대해 다음과 같은 제한 사항을 적용합니다.

* 맵 형식은 `object` 형식이어야 합니다.
* 맵 유형에는 속성이 정의되지 않아야 합니다(즉, &quot;빈&quot; 개체를 정의함).
* 맵 유형에는 맵 내에 배치할 수 있는 값을 설명하는 `additionalProperties.type` 필드(`string` 또는 `integer`)가 포함되어야 합니다.
* 다중 엔티티 세그먼테이션은 맵 키를 기준으로만 정의할 수 있으며 값을 기준으로 정의할 수는 없습니다.
* 계정 대상자에 대해서는 맵이 지원되지 않습니다.

맵 유형 필드는 다음과 같은 성능 단점이 있으므로 반드시 필요한 경우에만 사용해야 합니다.

* 1억 개의 레코드에 대해 [Adobe Experience Platform 쿼리 서비스](../../../query-service/home.md)의 응답 시간이 3초에서 10초로 감소합니다.
* 맵의 키가 16개 미만이어야 합니다. 그렇지 않으면 더 이상 성능이 저하될 수 있습니다.

>[!NOTE]
>
>Experience Platform UI는 맵 유형 필드의 키를 추출하는 방법에 제한이 있습니다. 개체 유형 필드는 확장할 수 있지만 맵은 대신 단일 필드로 표시됩니다. 문자열 또는 정수 데이터 형식이 아닌 스키마 레지스트리 API를 통해 만들어진 맵 필드는 &quot;[!UICONTROL Complex]&quot; 데이터 형식으로 표시됩니다.

## 다음 단계

이제 이 문서를 읽고 Experience Platform UI에서 맵 필드를 정의할 수 있습니다. 클래스와 필드 그룹만 사용하여 스키마에 필드를 추가할 수 있습니다. UI에서 이러한 리소스를 관리하는 방법에 대한 자세한 내용은 [클래스](../resources/classes.md) 및 [필드 그룹](../resources/field-groups.md) 만들기 및 편집에 대한 안내서를 참조하세요.

[!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md)를 참조하십시오.
