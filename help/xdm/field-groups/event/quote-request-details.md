---
title: 견적 요청 세부 정보 스키마 필드 그룹
description: Quote Request Details 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# [!UICONTROL 견적 요청 세부 정보] 스키마 필드 그룹

[!UICONTROL 견적 요청 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `quotes` 보험 증서, 헬스케어, 제조 주문 및 첨단 기술 주문을 포함하여 다양한 유형의 견적에 대한 요청 프로세스 세부 정보를 캡처하는 스키마 객체.

![](../../images/field-groups/quote-request-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 통화]](../../data-types/currency.md) | 방문자에게 표시되는 견적의 할인 금액입니다. |
| `premium` | [[!UICONTROL 통화]](../../data-types/currency.md) | 방문자에게 표시되는 견적의 프리미엄 금액입니다. |
| `location` | [!UICONTROL 문자열] | 방문자 위치 근처의 소매점을 찾는 데 사용되는 우편 번호입니다. |
| `requestID` | [!UICONTROL 문자열] | 견적 요청에 대한 고유 식별자. |
| `selectedRetailer` | [!UICONTROL 문자열] | 견적 요청에 대해 선택된 소매업체(해당하는 경우). |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
