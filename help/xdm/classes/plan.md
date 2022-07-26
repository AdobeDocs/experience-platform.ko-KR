---
title: 계획 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 계획 클래스에 대한 개요를 제공합니다.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL 계획] 클래스

XDM(Experience Data Model)에서 [!UICONTROL 계획] 분류는 건강 계획이나 보험 계획과 같은 계획을 정의하는 최소 속성 세트를 캡처합니다.

![클래스 구조](../images/classes/plan.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터의 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템이 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원할 경우 여전히 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `planId` | [!UICONTROL 문자열] | 계획에 대한 고유 식별자입니다. |
| `planName` | [!UICONTROL 문자열] | 계획의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

클래스는 [[!UICONTROL 의료 계획 세부 정보] 필드 그룹](../field-groups/plan/healthcare-plan-details.md) 건강 보험 계획에 대한 더 자세한 내용을 설명하다.
