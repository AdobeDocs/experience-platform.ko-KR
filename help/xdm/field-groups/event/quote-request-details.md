---
title: 견적 요청 세부 정보 스키마 필드 그룹
description: 이 문서에서는 Quote Request Details 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# [!UICONTROL 견적 요청 세부 정보] 스키마 필드 그룹

[!UICONTROL 견적 요청 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `quotes` 스키마에 대한 객체. 이 스키마에서 보험 정책, 의료, 제조 주문, 하이테크 주문 등 다양한 유형의 견적에 대한 요청 프로세스 세부 정보를 캡처합니다.

![](../../images/field-groups/quote-request-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 통화]](../../data-types/currency.md) | 방문자에게 표시되는 견적의 할인 금액입니다. |
| `premium` | [[!UICONTROL 통화]](../../data-types/currency.md) | 방문자에게 표시되는 견적에 대한 프리미엄 금액입니다. |
| `location` | [!UICONTROL 문자열] | 방문자의 위치 근처에 있는 소매점을 찾는 데 사용되는 우편 번호입니다. |
| `requestID` | [!UICONTROL 문자열] | 견적 요청에 대한 고유 식별자입니다. |
| `selectedRetailer` | [!UICONTROL 문자열] | 해당되는 경우 견적 요청에 대해 선택한 소매점입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
