---
title: 제품
seo-title: Adobe Experience Platform 웹 SDK를 사용한 제품 지원
description: Experience Platform 웹 SDK가 있는 제품 또는 장바구니를 가지고 있는 경우 데이터를 추가하는 방법 학습
seo-description: Experience Platform 웹 SDK가 있는 제품 또는 장바구니를 가지고 있는 경우 데이터를 추가하는 방법 학습
keywords: products;commerce;measures;measure;order;cartAbandons;checkouts;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
translation-type: tm+mt
source-git-commit: c34cd52301d812655c85d4e1bca42049204f9403
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 6%

---


# 상거래 및 제품 수집

사이트에 제품이 있는 경우 Adobe에서 가장 많은 기능을 사용하도록 설정하기 위해 전송할 수 있는 기본 집합입니다. 비록 이것이 제안이지만, 그것은 처음부터 매우 강력한 데이터 세트를 제공합니다.

이 문서에서는 ExperienceEvent [Commerce Details 믹싱을](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 사용합니다. 그 `commerce` 혼합물은 두 부분으로 나뉘어져 있다:개체 및 배열 `commerce` 을 `productListItems` 참조하십시오. 이 `commerce` 개체를 사용하면 배열에서 어떤 작업이 발생하는지 알 수 `productListItems` 있습니다.

>[!TIP]
>
>Adobe Analytics에 익숙하다면 변수 `commerce` 와 가장 밀접한 관계가 `events` 있습니다. 변수 `productListItems` 와 더 밀접한 관계가 `products` 있습니다.

## 제품과 관련된 작업

아래는 개체에서 사용할 수 `measures` 있는 `commerce` 목록입니다.

>[!TIP]
>
>측정값에는 두 개의 필드가 있습니다. `id` 및 `value`. 대부분의 경우 필드만 사용합니다(예: `value` `'value':1`). 이 `id` 필드에서는 측정값이 전송된 시간을 추적하는 데 사용할 수 있는 고유한 식별자를 설정할 수 있습니다. XDM(Measure) 설명서를 [참조하십시오](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **측정** | **권장 사항** | **설명** |
|---|---|---|
| [cartPermissions](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 선택 사항입니다 | 사용자가 장바구니에 액세스하거나 구매할 수 없습니다. |
| [체크아웃](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 매우 권장 | 사용자가 더 이상 제품을 검색하지 않지만 제품을 구입하는 중입니다. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 매우 권장 | 제품이 목록에 추가됩니다. 제품을 동시에 설정해야 `productListItems` 합니다. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 선택 사항입니다 | 새 제품 목록이 만들어집니다. (예: 새 장바구니가 만들어집니다.) |
| [productListRemoval](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 매우 권장 | 제품이 제품 목록에서 제거됩니다. |
| [productList다시 열기](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 선택 사항입니다 | 사용자가 제품 목록을 다시 활성화합니다. 이는 종종 리마케팅 캠페인에서 발생합니다. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 매우 권장 | 제품 목록이 표시됩니다. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 매우 권장 | 제품 보기가 발생했습니다. 에서 본 제품을 설정해야 합니다 `productListItems`. |
| [구매](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 매우 권장 | 주문은 수락됩니다 제품 목록이 있어야 합니다. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 선택 사항입니다 | 나중에 사용할 수 있도록 제품이 저장됩니다. |

다음은 SDK에서 이러한 설정을 설정하는 방법 `Measures` 의 예입니다.

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

또한 상거래 객체에는 호출된 주문 세부 사항을 수집하기 위한 특수 필드도 있습니다 `order`.

| **주문** | **옵션** | **권장 사항** | **설명** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 주문 합계에 대한 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화입니다. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 주문에 대한 지불 목록. 결제 [항목에는](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 다음이 포함됩니다. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 선택 사항입니다 | 이 지불 방법에 대한 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화입니다. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 매우 권장 | 지정된 통화 코드의 지급 값. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 매우 권장 | 지불 유형(예:, `credit_card``gift_card`, `paypal`). 자세한 내용은 [알려진 값](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 목록을 참조하십시오. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 선택 사항입니다 | 이 결제 트랜잭션의 고유 ID. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 매우 권장 | 모든 할인 및 세금이 적용된 후 이 주문에 대한 합계입니다. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 향상된 기능 | 이 구매에 대해 판매자가 지정하는 고유 식별자입니다. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 선택 사항입니다 | 구매자가 이 구매에 할당한 고유 식별자입니다. |

다음은 SDK에서 일반적인 구매의 예입니다.

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

제품 목록은 해당 작업과 관련된 제품을 나타냅니다. productListItems의 [목록입니다](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). 각 제품에는 선택 사항 필드가 많이 있습니다.

| **필드** | **권장 사항** | **설명** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 선택 사항입니다 | 제품의 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화입니다. 이 기능은 통화 코드가 다른 제품이 적용되는 경우에만 유용합니다. 예를 들어 장바구니에 구매하거나 추가하는 경우 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 매우 권장 | 해당되는 경우에만 설정해야 합니다. 예를 들어, 제품의 다른 변형이 가격만 다를 수 `productView` 있으므로 설정할 수 없을 수 `productListAdds`있습니다. |
| [제품](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 매우 권장 | 제품의 XDM ID. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 매우 권장 | 방문자가 목록에 제품 항목을 추가하는 데 사용한 방법입니다. 측정값을 사용하여 `productListAdds` 설정하며, 제품이 목록에 추가될 때만 사용해야 합니다. Examples include `add to cart button`, `quick add`, and `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 매우 권장 | 제품의 표시 이름 또는 읽을 수 있는 이름으로 설정됩니다. |
| [수량](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 매우 권장 | 고객이 제품이 필요하다고 표시한 판매량 설정 `productListAdds`, `productListRemoves`, `purchases`및 `saveForLaters`등을 해야 합니다. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 매우 권장 | 저장 장치. 제품의 고유 식별자입니다. |

## 예

`productView` event

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

`productView` event

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

`checkout` event

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

`purchase` event

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
