---
title: 지불인 분류
description: XDM(Experience Data Model)의 지불인 클래스에 대해 알아봅니다.
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# [!UICONTROL 지불인] 클래스

XDM(경험 데이터 모델)에서 [!UICONTROL 지불인] class는 보험 회사(예: 건강 보험)에 관련된 데이터를 수집하는 지불 사업체를 정의하는 최소 속성 세트를 캡처합니다.

![클래스 구조](../images/classes/payer.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터 수집 중에 명시적 값을 제공하지 않습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `payerId` | [!UICONTROL 문자열] | 지불자에 대한 고유 식별자. |
| `payerName` | [!UICONTROL 문자열] | 지불자의 이름. |

{style="table-layout:auto"}
