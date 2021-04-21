---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;순서;데이터 유형;데이터 유형;데이터 유형;data-type;
solution: Experience Platform
title: 주문 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM(Order Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# [!UICONTROL Order] 데이터 유형

[!UICONTROL Order] 는 제품 목록에 대한 순서를 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/order.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `payments` | [[!UICONTROL Payment Items]](./payment-item.md) 배열 | 이 주문에 대한 결제 목록. |
| `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드. 모든 인스턴스는 일반 표현식 `^[A-Z]{3}$`을(를) 준수해야 합니다. 예: `USD` 및 `EUR`. |
| `priceTotal` | 이중 | 모든 할인 및 세금이 적용된 후 이 주문의 총 가격. |
| `purchaseID` | 문자열 | 이 구매 또는 계약에 대해 판매자가 지정한 고유 식별자. 판매자에 의해 정의되므로 ID가 고유하다는 보장이 없습니다. |
| `purchaseOrderNumber` | 문자열 | 구매자가 이 구매 또는 계약에 대해 지정한 고유 식별자. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
