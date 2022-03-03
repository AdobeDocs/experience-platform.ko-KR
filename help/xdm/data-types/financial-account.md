---
title: 재무 계정 데이터 유형
description: 이 문서에서는 Financial Account XDM 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 8%

---

# [!UICONTROL 금융 계정] 데이터 유형

[!UICONTROL 금융 계정] 은 유형, 소유자 및 현재 잔액을 포함하여 금융 계정의 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/financial-account.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 통화]](./currency.md) | 계정의 현재 잔액. |
| `financialAccountId` | [!UICONTROL 문자열] | 계정에 대한 고유 ID입니다. |
| `financialAccountName` | [!UICONTROL 문자열] | 계정에 지정된 이름입니다. |
| `financialAccountType` | [!UICONTROL 문자열] | 당좌 예금, 저축, 퇴직과 같은 금융 계좌의 유형입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
