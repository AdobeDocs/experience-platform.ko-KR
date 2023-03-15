---
title: 카드 작업 스키마 필드 그룹
description: 이 문서에서는 카드 작업 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 6%

---

# [!UICONTROL 카드 작업] 스키마 필드 그룹

[!UICONTROL 카드 작업] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `personalFinances.cardActions` 카드 유형, 활성화 상태 및 잠금 상태 등 카드 작업에 대한 세부 정보를 캡처하는 스키마에 대한 필드입니다.

![](../../images/field-groups/card-actions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `cardActivated` | 정수 | 카드가 정상적으로 활성화되면 추적합니다. |
| `cardActivationStart` | 정수 | 카드 활성화 프로세스가 시작되면 추적합니다. |
| `cardCancelled` | 정수 | 카드가 취소되면 추적합니다. |
| `cardControlsLocked` | 정수 | 카드의 컨트롤이 잠기면 추적합니다. |
| `cardControlsUnlocked` | 정수 | 카드 제어 기능이 잠금 해제되면 추적합니다. |
| `cardID` | 문자열 | 활성화 중인 카드용 식별자. 이 값은 카드 번호와 다를 수 있습니다. |
| `cardLocked` | 정수 | 카드가 차단되면 추적합니다. |
| `cardOrderNew` | 정수 | 카드가 요청되면 추적합니다. |
| `cardOrderType` | 문자열 | 카드 주문 이벤트와 연계된 카드 주문 유형. |
| `cardType` | 문자열 | 카드 유형. |
| `cardUnlocked` | 정수 | 카드가 잠금 해제되면 추적합니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
