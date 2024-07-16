---
title: 공급자 클래스
description: XDM(경험 데이터 모델)의 공급자 클래스에 대해 알아봅니다.
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL 공급자] 클래스

XDM(Experience Data Model)에서 [!UICONTROL Provider] 클래스는 공급자 비즈니스 엔터티(예: 의료 서비스 공급자 또는 보험 공급자)를 정의하는 최소 속성 집합을 캡처합니다.

![클래스 구조](../images/classes/provider.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 사용자 이름]](../data-types/person-name.md) | 공급자의 이름입니다. |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `providerId` | [!UICONTROL 문자열] | 공급자에 대한 고유 식별자. |

{style="table-layout:auto"}

의료 서비스 공급자에 대한 자세한 내용을 설명하기 위해 [[!UICONTROL 의료 서비스 공급자] 필드 그룹](../field-groups/provider/healthcare-provider.md)을 사용하여 클래스를 확장할 수 있습니다.
