---
title: 환불 항목 데이터 유형
description: 환불 항목 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL 환불 항목] 데이터 형식

[!UICONTROL 환불 항목]은(는) 주문과 연계된 환불과 관련된 정보를 캡처하는 것을 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다.

![환불 항목 데이터 형식의 다이어그램입니다.](../images/data-types/refund-item.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL 거래 ID] | `transactionID` | 문자열 | 해당 환불 항목에 대한 고유 거래 식별자. |
| [!UICONTROL 환불 금액] | `refundAmount` | 번호 | 환불 금액. |
| [!UICONTROL 환불 사유] | `refundReason` | 문자열 | 환불 사유. |
| [!UICONTROL 환불 결제 유형] | `refundPaymentType` | 문자열 | 해당 주문에 대한 결제 방법. 사용자 지정 값이 허용됩니다. |
| [!UICONTROL 통화 코드] | `currencyCode` | 문자열 | 이 환불 항목에 사용되는 ISO 4217 통화 코드. 예: &#39;USD&#39;, &#39;EUR&#39;. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
