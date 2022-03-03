---
title: 세부 정보 스키마 필드 그룹
description: 이 문서에서는 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

---

# [!UICONTROL 예금 상세내역] 스키마 필드 그룹

[!UICONTROL 예금 상세내역] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `personalFinances.deposits` 필드를 스키마 로 설정합니다. 스키마에는 금융 예금에 대한 세부 정보가 캡처됩니다.

![](../../images/field-groups/deposit-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `account` | [[!UICONTROL 금융 계정]](../../data-types/financial-account.md) | 예금과 연관된 재무 계정을 설명합니다. |
| `transaction` | [[!UICONTROL 트랜잭션]](../../data-types/transaction.md) | 예금과 관련된 금융 거래를 설명합니다. |
| `mobileDeposit` | [!UICONTROL 부울] | 모바일 플랫폼을 통해 예금이 수행되었는지 여부를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
