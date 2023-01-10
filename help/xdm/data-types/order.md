---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;순서;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 주문 데이터 유형
description: 이 문서에서는 XDM(주문 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---

# [!UICONTROL 주문] 데이터 유형

[!UICONTROL 주문] 는 제품 목록에 대해 배치된 순서를 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/order.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `payments` | 배열 [[!UICONTROL 결제 항목]](./payment-item.md) | 이 주문에 대한 지급 목록입니다. |
| `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드입니다. 모든 인스턴스는 정규 표현식을 준수해야 합니다 `^[A-Z]{3}$`. 예: `USD` 및 `EUR`. |
| `priceTotal` | 이중 | 모든 할인과 세금이 적용된 후 이 주문의 총 가격. |
| `purchaseID` | 문자열 | 이 구매 또는 계약에 대해 판매자가 할당한 고유 식별자입니다. 판매자에 의해 정의되므로 ID가 고유하다는 보장이 없습니다. |
| `purchaseOrderNumber` | 문자열 | 이 구매 또는 계약에 대해 구매자가 할당한 고유 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
