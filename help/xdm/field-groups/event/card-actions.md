---
title: 카드 작업 스키마 필드 그룹
description: 이 문서에서는 카드 작업 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 8%

---

# [!UICONTROL 카드 작업] 스키마 필드 그룹

[!UICONTROL 카드 작업] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `personalFinances.cardActions` 카드 유형, 활성화 상태 및 잠금 상태와 같은 카드 작업에 대한 세부 사항을 캡처하는 스키마에 대한 필드입니다.

![](../../images/field-groups/card-actions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `cardActivated` | 정수 | 카드가 성공적으로 활성화되었을 때를 추적합니다. |
| `cardActivationStart` | 정수 | 카드 활성화 프로세스가 시작된 시기를 추적합니다. |
| `cardCancelled` | 정수 | 카드가 취소된 시기를 추적합니다. |
| `cardControlsLocked` | 정수 | 카드의 컨트롤이 잠긴 시점을 추적합니다. |
| `cardControlsUnlocked` | 정수 | 카드의 컨트롤 잠금이 해제된 시기를 추적합니다. |
| `cardID` | 문자열 | 활성화 중인 카드의 식별자입니다. 이 값은 카드 번호와 다를 수 있습니다. |
| `cardLocked` | 정수 | 카드가 잠긴 시점을 추적합니다. |
| `cardOrderNew` | 정수 | 카드를 요청한 시기를 추적합니다. |
| `cardOrderType` | 문자열 | 카드 주문 이벤트와 연관된 카드 주문 유형입니다. |
| `cardType` | 문자열 | 카드 유형입니다. |
| `cardUnlocked` | 정수 | 카드의 잠금이 해제된 시기를 추적합니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
