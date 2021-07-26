---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;통화;
solution: Experience Platform
title: 통화 데이터 유형
topic-legacy: overview
description: 이 문서에서는 통화 XDM 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 5%

---

#  현재 데이터 유형

 통화는 통화 유형 및 전환 날짜를 포함하여 통화 금액을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/currency.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `amount` | 이중 | 디스플레이에서 나타낼 수 있는 색상 수입니다. |
| `conversionDate` | DateTime | 디스플레이에서 나타낼 수 있는 색상 수입니다. |
| `currencyCode` | 문자열 | 디스플레이에서 나타낼 수 있는 색상 수입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)