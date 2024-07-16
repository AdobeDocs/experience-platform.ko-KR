---
title: 예금 세부 정보 스키마 필드 그룹
description: 예금 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL 예금 세부 정보] 스키마 필드 그룹

[!UICONTROL 예금 세부 정보]은(는) [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)의 표준 스키마 필드 그룹입니다. 필드 그룹은 스키마에 재무 예금에 대한 세부 정보를 캡처하는 단일 `personalFinances.deposits` 필드를 제공합니다.

![](../../images/field-groups/deposit-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `account` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 예금과 연계된 금융 계정을 설명합니다. |
| `transaction` | [[!UICONTROL 트랜잭션]](../../data-types/transaction.md) | 예금과 연계된 금융 거래에 대해 설명합니다. |
| `mobileDeposit` | [!UICONTROL 부울] | 모바일 플랫폼을 통해 예금이 수행되었는지 여부를 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json)를 참조하세요.
