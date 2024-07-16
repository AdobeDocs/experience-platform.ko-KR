---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;통화;
solution: Experience Platform
title: 통화 데이터 유형
description: 통화 XDM 데이터 유형에 대해 알아봅니다.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# [!UICONTROL 통화] 데이터 형식

[!UICONTROL 통화]은(는) 통화 유형 및 변환 날짜를 포함하여 통화량을 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/currency.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `amount` | 더블 | `currencyCode`에 정의된 통화량입니다. |
| `conversionDate` | 날짜/시간 | 통화 전환이 이루어진 시간의 타임스탬프입니다. |
| `currencyCode` | 문자열 | `amount`이(가) 나타내는 통화 유형을 나타내는 ISO 4217 코드입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
