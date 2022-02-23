---
title: 키 값 쌍 데이터 유형
description: 이 문서에서는 XDM(키 값 쌍 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL 키 값 쌍] 데이터 유형

[!UICONTROL 키 값 쌍] 는 일반 키-값 쌍의 세부 사항을 캡처하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 이 데이터 유형은 [[!UICONTROL Adobe Analytics Experience Event Full Extension] 필드 그룹](../field-groups/event/analytics-full-extension.md) 목록 변수의 배열 항목을 설명하는 데 사용됩니다.

![키 값 쌍 구조](../images/data-types/key-value-pair.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `key` | 문자열 | 일반 변수 또는 값에 대한 키(이름)입니다. |
| `value` | 문자열 | 변수의 값입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
