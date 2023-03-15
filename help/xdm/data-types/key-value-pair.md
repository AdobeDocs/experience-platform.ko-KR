---
title: 키 값 쌍 데이터 유형
description: 이 문서에서는 키 값 쌍 XDM(경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# [!UICONTROL 키 값 쌍] 데이터 유형

[!UICONTROL 키 값 쌍] 는 일반 키-값 쌍의 세부 사항을 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 이 데이터 형식은 [[!UICONTROL Adobe Analytics ExperienceEvent 전체 확장] 필드 그룹](../field-groups/event/analytics-full-extension.md) 목록 변수의 배열 항목을 설명합니다.

![키 값 쌍 구조](../images/data-types/key-value-pair.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `key` | 문자열 | 일반 변수 또는 값의 키(이름)입니다. |
| `value` | 문자열 | 변수의 값입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
