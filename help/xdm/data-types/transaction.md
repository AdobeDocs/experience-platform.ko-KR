---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;트랜잭션;데이터 유형;데이터 유형;데이터 유형;
title: 거래 데이터 유형
description: 이 문서에서는 XDM(트랜잭션 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  Transactiondata 유형

 트랜잭션은 통화 거래의 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

![트랜잭션 구조](../images/data-types/transaction.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 통화]](./currency.md) | 거래의 일부로 교환된 통화 금액을 설명합니다. |
| `transactionDate` | [!UICONTROL DateTime] | 트랜잭션이 발생한 시간의 타임스탬프입니다. |
| `transactionId` | [!UICONTROL 문자열] | 거래의 고유 식별자입니다. |
| `transactionType` | [!UICONTROL 문자열] | 방문자가 사용하는 트랜잭션 유형입니다. |

{style=&quot;table-layout:auto&quot;}
