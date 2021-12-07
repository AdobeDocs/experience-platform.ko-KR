---
title: Adobe Experience Platform Web SDK를 사용하여 상거래 및 제품 정보 수집
description: Adobe Experience Platform Web SDK를 사용하여 제품 또는 장바구니와 관련된 데이터를 추가하는 방법을 알아봅니다.
keywords: 제품;상거래;측정;측정값;주문;장바구니 포기;체크아웃;제품ListAdds;productListOpen;productListRemoval;productListReopenes;productListViews;productViews;구매;saveForLaters;currencyCode;payment;paymentAmount;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# 상거래 및 제품 정보 수집

사이트에 제품이 있다면 Adobe에서 가장 많은 기능을 활성화하기 위해 전송할 기본 항목 세트입니다. 비록 이것이 제안이지만, 처음부터 매우 강력한 데이터 세트를 제공합니다.

이 문서에서는 [ExperienceEvent Commerce 세부 사항](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 스키마 필드 그룹. 다음 `commerce` 필드 그룹은 다음 두 부분으로 나뉘어져 있습니다. a `commerce` 개체 및 `productListItems` 배열입니다. 다음 `commerce` 개체를 사용하면 `productListItems` 배열입니다.

>[!TIP]
>
>Adobe Analytics에 익숙하다면 `commerce` 는 `events` 변수를 채우는 방법을 설명합니다. 다음 `productListItems` 는 `products` 변수를 채우는 방법을 설명합니다.

## 제품과 관련된 작업

아래는 `measures` 에서 사용 가능 `commerce` 개체.

>[!TIP]
>
>측정값에는 두 개의 필드가 있습니다. `id` 및 `value`. 대부분의 경우 `value` 필드만(예: `'value':1`). 다음 `id` 필드에서는 측정값이 전송된 시기를 추적하는 데 사용할 수 있는 고유 식별자를 설정할 수 있습니다. 에 대한 XDM 설명서 를 참조하십시오. [측정](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **측정** | **권장 사항** | **설명** |
|---|---|---|
| [cart포기](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 선택 사항입니다 | 사용자가 장바구니에 더 이상 액세스하거나 구매할 수 없습니다. |
| [체크아웃](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 매우 권장 | 사용자가 더 이상 제품을 탐색하지 않지만 제품을 구매하는 중입니다. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 매우 권장 | 제품이 목록에 추가됩니다. 에서 제품을 설정해야 합니다. `productListItems` 동시에 |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 선택 사항입니다 | 새 제품 목록이 만들어집니다. (예를 들어 새 장바구니가 만들어집니다.) |
| [productListRemoval](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 매우 권장 | 제품이 제품 목록에서 제거됩니다. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 선택 사항입니다 | 사용자가 제품 목록을 다시 활성화합니다. 이는 리마케팅 캠페인에서 종종 발생합니다. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 매우 권장 | 제품 목록이 표시됩니다. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 매우 권장 | 제품 보기가 발생했습니다. 에서 본 제품을 반드시 설정하십시오. `productListItems`. |
| [구매](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 매우 권장 | 주문은 수락됩니다. 제품 목록이 있어야 합니다. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 선택 사항입니다 | 향후 사용할 수 있도록 제품이 저장됩니다. |

다음은 이러한 속성을 설정하는 방법의 예입니다 `Measures` 를 반환합니다.

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

상거래 객체에는 다음과 같은 주문 세부 사항을 수집하기 위한 특수 필드도 있습니다. `order`.

| **주문** | **옵션** | **권장 사항** | **설명** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 주문 합계에 대한 통화. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 주문에 대한 지급 목록입니다. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 에는 다음 항목이 포함되어 있습니다. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 선택 사항입니다 | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 이 결제 방법의 통화. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 매우 권장 | 지정된 통화 코드의 지급 값입니다. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 매우 권장 | 지급 유형(예: `credit_card`, `gift_card`, `paypal`). 다음 목록을 참조하십시오. [알려진 값](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 자세한 내용 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 선택 사항입니다 | 이 결제 거래의 고유 ID입니다. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 매우 권장 | 모든 할인과 세금이 적용된 후 이 주문에 대한 합계입니다. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 매우 권장 | 판매자가 이 구매에 대해 할당한 고유 식별자입니다. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 선택 사항입니다 | 구매자가 이 구매에 대해 할당한 고유 식별자입니다. |

다음은 SDK의 일반적인 구매의 예입니다.

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

## 제품 목록

제품 목록은 해당 작업과 관련된 제품을 나타냅니다. 목록 [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). 각 제품에는 여러 개의 선택적 필드가 있습니다.

| **필드** | **권장 사항** | **설명** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 선택 사항입니다 | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 제품에 대한 통화. 이 기능은 다른 통화 코드가 있는 제품을 사용할 수 있고 적용되는 경우에만 유용합니다. 예를 들어 장바구니에 구매하거나 추가하는 경우가 있습니다. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 매우 권장 | 해당되는 경우에만 설정해야 합니다. 예를 들어 `productView` 이벤트의 다른 변형에는 가격이 다를 수 있지만 `productListAdds` 이벤트. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 매우 권장 | 제품의 XDM ID입니다. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 매우 권장 | 방문자가 목록에 제품 항목을 추가하는 데 사용한 방법입니다. 설정 `productListAdds` 및 는 제품이 목록에 추가되는 경우에만 사용해야 합니다. 예로는 `add to cart button`, `quick add` 및 `upsell`가 있습니다. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 매우 권장 | 제품의 표시 이름 또는 사람이 읽을 수 있는 이름으로 설정됩니다. |
| [수량](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 매우 권장 | 고객이 제품을 필요로 한다고 표시한 단위 수입니다. 설정 `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`등 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 매우 권장 | 보관 장치. 제품의 고유 식별자입니다. |

## 예시

`productViews` 이벤트

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

`productListAdds` 이벤트

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

`checkouts` 이벤트

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

`order` 이벤트

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```
