---
title: 잔액 이전 스키마 필드 그룹
description: 이 문서에서는 잔액 이전 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 4%

---

# [!UICONTROL 잔액 이전] 스키마 필드 그룹

[!UICONTROL 잔액 이전] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `personalFinances.balanceTransfers` 스키마 객체입니다. 스키마에는 계정 간 재무 잔액 이전에 대한 세부 정보가 캡처됩니다.

![](../../images/field-groups/balance-transfers.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 잔액이 이전되는 재무 계정을 설명합니다. |
| `accountTo` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 잔액이 이전되는 재무 계정을 설명합니다. |
| `transaction` | [[!UICONTROL 트랜잭션]](../../data-types/transaction.md) | 잔액 이동과 관련된 금융 거래를 설명합니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
