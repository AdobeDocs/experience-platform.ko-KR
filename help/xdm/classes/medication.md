---
title: 약물 분류
description: Experience Data Model(XDM)의 약물 클래스에 대해 알아봅니다.
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL 약물] 클래스

XDM(Experience Data Model)에서 [!UICONTROL Medicine] 클래스는 의학적 치료에 사용되는 물질, 특히 약이나 약물을 정의하는 최소 속성 집합을 캡처합니다.

![클래스 구조](../images/classes/medication.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `medicationId` | [!UICONTROL 문자열] | 약물에 대한 고유 식별자. |
| `medicationName` | [!UICONTROL 문자열] | 약물의 이름입니다. |

{style="table-layout:auto"}

[[!UICONTROL 의료 서비스 ] 필드 그룹](../field-groups/medication/healthcare-medication.md)을 사용하여 클래스를 확장하여 해당 약이나 약물에 대한 자세한 내용을 설명할 수 있습니다.
