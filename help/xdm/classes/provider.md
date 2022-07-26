---
title: 공급자 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 공급자 클래스에 대한 개요를 제공합니다.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL 공급자] 클래스

XDM(Experience Data Model)에서 [!UICONTROL 공급자] 클래스는 공급자 사업자(의료 기관 또는 보험 제공자)를 정의하는 최소 속성 집합을 캡처합니다.

![클래스 구조](../images/classes/provider.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 개인 이름]](../data-types/person-name.md) | 공급자의 이름입니다. |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터의 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템이 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원할 경우 여전히 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `providerId` | [!UICONTROL 문자열] | 공급자에 대한 고유 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

클래스는 [[!UICONTROL 의료 기관] 필드 그룹](../field-groups/provider/healthcare-provider.md) 의료 기관에 대한 자세한 내용을 설명하는 데 사용됩니다.
