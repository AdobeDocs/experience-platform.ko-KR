---
title: 제품
seo-title: Adobe Experience Platform 웹 SDK를 사용한 제품 지원
description: Experience Platform Web SDK를 사용하여 제품 또는 장바구니가 있는 경우 데이터를 추가하는 방법 학습
seo-description: Experience Platform Web SDK를 사용하여 제품 또는 장바구니가 있는 경우 데이터를 추가하는 방법 학습
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 제품

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

사이트에 제품이 있는 경우 Adobe의 기능을 최대한 활용할 수 있도록 전송하려는 기본 사항 세트입니다. 이것이 제안이지만, 그것은 처음부터 매우 강력한 데이터 세트를 제공합니다.

이 문서에서는 ExperienceEvent 상거래 [세부 사항 믹싱을](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 사용합니다. 이 `commerce` 혼합물은 두 부분으로 나뉘어져 있습니다.객체와 `commerce` 배열을 `productListItems` 지정합니다. 이 `commerce` 객체를 사용하면 `productListItems` 배열에서 수행되는 작업을 표시할 수 있습니다.

>[!Tip]
>Adobe Analytics에 익숙한 경우 `commerce` 이 `events` 변수와 가장 밀접하게 관련되어 있습니다. 이 `productListItems` 변수는 `products` 변수와 보다 밀접하게 관련되어 있습니다.

## 제품과 관련된 작업

다음은 `measures` 개체에서 사용할 수 `commerce` 있는 목록입니다.

>[!Tip]
>측정값에는 두 개의 필드가 있습니다. `id` 및 `value`Adobe 대부분의 경우 `value` 필드만 사용합니다(예: `'value':1`). 이 `id` 필드를 사용하면 측정값이 전송된 시기를 추적하는 데 사용할 수 있는 고유한 식별자를 설정할 수 있습니다. XDM 측정 설명서를 [참조하십시오](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **측정** | **권장 사항** | **설명** |
|---|---|---|
| [cartDisablement](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 선택 사항입니다 | 사용자가 장바구니에 액세스하거나 구매할 수 없습니다. |
| [체크아웃](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 매우 권장 | 사용자가 더 이상 제품을 검색하지 않지만 제품을 구입하는 중입니다. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 매우 권장 | 제품이 목록에 추가됩니다. 제품을 동시에 설정해야 `productListItems` 합니다. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 선택 사항입니다 | 새 제품 목록이 만들어집니다. (예: 새 장바구니가 만들어집니다.) |
| [productListRemoval](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 매우 권장 | 제품이 제품 목록에서 제거됩니다. |
| [productList다시 열기](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 선택 사항입니다 | 사용자가 제품 목록을 다시 활성화합니다. 이는 종종 리마케팅 캠페인에서 발생합니다. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 매우 권장 | 제품 목록이 표시됩니다. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 매우 권장 | 제품 보기가 발생했습니다. 에서 본 제품을 설정해야 합니다 `productListItems`. |
| [구매](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 매우 권장 | 주문이 접수되었습니다. 제품 목록이 있어야 합니다. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 선택 사항입니다 | 나중에 사용할 수 있도록 제품이 저장됩니다. |

다음은 SDK에서 이러한 설정을 설정하는 `Measures` 방법의 예입니다.

```javascript
alloy("event", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

또한 상거래 객체에는 호출된 주문 세부 사항을 수집하기 위한 특수 필드도 `order`있습니다.

| **주문** | **옵션** | **권장 사항** | **설명** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 주문 [합계에 대한](https://en.wikipedia.org/wiki/ISO_4217) ISO 4217 통화. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 주문에 대한 결제 목록. 지불 [항목에](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 다음이 포함됩니다. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 선택 사항입니다 | 이 [지불 방법에 대한](https://en.wikipedia.org/wiki/ISO_4217) ISO 4217 통화. |
|  | [지불 금액](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 매우 권장 | 지정된 통화 코드의 지급 값. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 매우 권장 | 지불 유형(예: `credit_card`, `gift_card`, `paypal`). 자세한 내용은 [알려진 값](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 목록을 참조하십시오. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 선택 사항입니다 | 이 결제 트랜잭션의 고유 ID. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 매우 권장 | 모든 할인 및 세금이 적용된 후 이 주문에 대한 합계입니다. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 향상된 기능 | 이 구매에 대해 판매자가 지정한 고유 식별자입니다. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 선택 사항입니다 | 구매자가 이 구매에 할당한 고유 식별자입니다. |

다음은 SDK의 일반적인 구매 사례입니다.

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```

## 제품 목록

제품 목록은 해당 작업과 관련된 제품을 나타냅니다. productListItems의 [목록입니다](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). 각 제품에는 여러 개의 선택적 필드가 있습니다.

| **필드** | **권장 사항** | **설명** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 선택 사항입니다 | 제품의 [ISO](https://en.wikipedia.org/wiki/ISO_4217) 4217 통화 이 기능은 통화 코드가 다른 제품을 사용할 수 있고 적용되는 경우에만 유용합니다. 예를 들어 장바구니에 구매하거나 추가하는 경우 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 매우 권장 | 해당되는 경우에만 설정해야 합니다. 예를 들어, 제품의 다른 `productView` 변형에 가격이 다를 수 있지만 한 번에 설정할 수 없을 수 `productListAdds`있습니다. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 매우 권장 | 제품의 XDM ID입니다. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 매우 권장 | 방문자가 목록에 제품 항목을 추가하는 데 사용한 방법입니다. 측정값으로 `productListAdds` 설정하며, 제품이 목록에 추가될 때만 사용해야 합니다. 예로는 `add to cart button`, `quick add`및 `upsell`가 있습니다. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 매우 권장 | 이것은 제품의 표시 이름 또는 읽을 수 있는 이름으로 설정됩니다. |
| [수량](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 매우 권장 | 고객이 제품을 필요로 한다고 표시한 판매량 설정 `productListAdds``productListRemoves`및 `purchases`설정 `saveForLaters`등이 필요합니다. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 매우 권장 | 저장소 보관 장치. 제품의 고유 식별자입니다. |

## 예

`productView` 이벤트에 연결된다는 점을 이용합니다

```javascript
alloy("event",{
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

`productView` 이벤트에 연결된다는 점을 이용합니다

```javascript
alloy("event",{
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

`checkout` 이벤트에 연결된다는 점을 이용합니다

```javascript
alloy("event",{
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

`purchase` 이벤트에 연결된다는 점을 이용합니다

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```
