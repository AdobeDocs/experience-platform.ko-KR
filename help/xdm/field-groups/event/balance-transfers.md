---
title: 잔액 전송 스키마 필드 그룹
description: 잔고 이체 스키마 필드 그룹에 대해 알아봅니다.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL 잔고 이체] 스키마 필드 그룹

[!UICONTROL 잔고 이체] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `personalFinances.balanceTransfers` 계정 간 재무 잔고 이체에 대한 세부 정보를 캡처하는 스키마에 대한 객체입니다.

![](../../images/field-groups/balance-transfers.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 잔액이 이체되는 금융 계정을 설명합니다. |
| `accountTo` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 잔액이 이체되는 금융 계정을 설명합니다. |
| `transaction` | [[!UICONTROL 거래]](../../data-types/transaction.md) | 잔액 이체와 연관된 금융 거래에 대해 설명합니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
