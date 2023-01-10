---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;결제 항목;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지급 품목 데이터 유형
description: 이 문서에서는 XDM(결제 항목 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---

# [!UICONTROL 결제 항목] 데이터 유형

[!UICONTROL 결제 항목] 는 지급 유형, 금액 및 관련 통화를 정의하는 주문과 연관된 지급을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드입니다. 모든 인스턴스는 정규 표현식을 준수해야 합니다 `^[A-Z]{3}$`. 예: `USD` 및 `EUR`. |
| `paymentAmount` | 이중 | 지급 값입니다. |
| `paymentType` | 문자열 | 이 주문에 대한 결제 방법입니다. 허용되는 열거형 값은 다음과 같습니다. <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 문자열 | 이 지급 품목에 대한 고유 거래 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
