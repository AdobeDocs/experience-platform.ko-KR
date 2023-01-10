---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;통화;
solution: Experience Platform
title: 통화 데이터 유형
description: 이 문서에서는 통화 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL 통화] 데이터 유형

[!UICONTROL 통화] 는 통화 유형 및 변환 날짜를 포함하여 통화 금액을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/currency.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `amount` | 이중 | 에 정의된 통화 금액입니다. `currencyCode`. |
| `conversionDate` | DateTime | 통화 전환이 수행된 시간의 타임스탬프입니다. |
| `currencyCode` | 문자열 | 해당 통화 유형을 나타내는 ISO 4217 코드 `amount` 는 을 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
