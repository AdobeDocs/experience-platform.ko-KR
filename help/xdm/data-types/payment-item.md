---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지불 항목;데이터 유형;데이터 유형;data-type;data type
solution: Experience Platform
title: 지급 항목 데이터 유형
topic: overview
description: 이 문서에서는 XDM(Payment Item Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---


# [!UICONTROL 결제 ] 항목 데이터 유형

[!UICONTROL 결제 ] 항목은 지급 유형, 금액 및 관련 통화를 정의하는 주문과 연관된 지급을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드. 모든 인스턴스는 일반 표현식 `^[A-Z]{3}$`을(를) 준수해야 합니다. 예: `USD` 및 `EUR`. |
| `paymentAmount` | 이중 | 지불 값. |
| `paymentType` | 문자열 | 이 주문에 대한 지불 방법. 허용되는 열거형 값은 다음과 같습니다. <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 문자열 | 이 결제 항목에 대한 고유 거래 식별자. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)