---
title: 금융 계정 데이터 유형
description: 이 문서에서는 금융 계정 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 5%

---

# [!UICONTROL 금융 계정] 데이터 유형

[!UICONTROL 금융 계정] 는 유형, 소유자 및 현재 잔액을 포함한 금융 계정의 세부 정보를 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/financial-account.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 통화]](./currency.md) | 계정의 현재 잔고. |
| `financialAccountId` | [!UICONTROL 문자열] | 계정용 고유 ID. |
| `financialAccountName` | [!UICONTROL 문자열] | 계정에 할당된 이름. |
| `financialAccountType` | [!UICONTROL 문자열] | 확인, 저축 또는 퇴직과 같은 금융 계정의 유형입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
