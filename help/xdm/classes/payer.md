---
title: 지급자 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 Player 클래스에 대한 개요를 제공합니다.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---

# [!UICONTROL 지급인] 클래스

XDM(Experience Data Model)에서 [!UICONTROL 지급인] 분류는 보험 회사와 관련된 데이터를 수집하는 지급자 기업을 정의하는 최소 속성 세트를 캡처합니다(예: 건강 보험).

![클래스 구조](../images/classes/payer.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터의 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템이 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원할 경우 여전히 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `payerId` | [!UICONTROL 문자열] | 지급자에 대한 고유 식별자입니다. |
| `payerName` | [!UICONTROL 문자열] | 지급인의 이름입니다. |

{style=&quot;table-layout:auto&quot;}
