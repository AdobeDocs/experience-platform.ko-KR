---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;순서;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 주문 데이터 유형
description: XDM(Order Experience Data Model) 데이터 유형에 대해 알아봅니다.
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# [!UICONTROL 주문] 데이터 유형

[!UICONTROL 주문] 는 제품 목록에 배치된 순서를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

<img src="../images/data-types/order.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `payments` | 배열 [[!UICONTROL 결제 항목]](./payment-item.md) | 해당 주문에 대한 결제 목록. |
| `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드. 모든 인스턴스는 정규 표현식을 준수해야 합니다 `^[A-Z]{3}$`. 예: `USD` 및 `EUR`. |
| `priceTotal` | 이중 | 할인 및 세금이 모두 적용된 후 이 주문의 총 가격. |
| `purchaseID` | 문자열 | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. 이는 판매자에 의해 정의되므로 ID가 고유하다고 보장할 수 없습니다. |
| `purchaseOrderNumber` | 문자열 | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
