---
title: Adobe Experience Platform Web SDK를 사용하여 상거래, 제품 및 주문 정보 수집
description: Adobe Experience Platform Web SDK를 사용하여 제품 또는 장바구니와 관련된 데이터를 추가하는 방법에 대해 알아봅니다.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# 상거래, 제품 및 주문 정보 수집

조직에서 제품 또는 서비스를 판매하는 경우 이 페이지를 해당 제품 및 서비스를 추적하는 방법에 대한 안내서로 사용할 수 있습니다.

이 페이지에서는 XDM을 사용합니다. [상거래 스키마](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) 필드 그룹입니다.

이 필드 그룹은 다음 두 가지 주요 부분으로 구성됩니다.

* 다음 `commerce` 개체. 이 개체를 사용하면 다음에 발생하는 작업을 나타낼 수 있습니다. `productListItems` 배열입니다.
* 다음 `productListItems` 배열입니다.

>[!TIP]
>
>Adobe Analytics에 익숙한 경우 `commerce` 개체에는 의 상거래 이벤트와 유사한 데이터가 포함됩니다. `events` 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다. 다음 `productListItems` 오브젝트 배열에 다음과 유사한 데이터가 포함되어 있습니다. `products` 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다.

## 다음 `commerce` 오브젝트 {#commerce-object}

이 섹션에서는 다음에서 사용할 수 있는 필드에 대해 설명합니다. `commerce` 개체.

>[!TIP]
>
>측정에는 두 개의 필드가 있습니다. `id` 및 `value`. 대부분의 경우 `value` 필드(예: `'value':1`). 다음 `id` 필드를 사용하면 측정값이 전송될 때 추적할 고유 식별자를 설정할 수 있습니다. 다음에 대한 XDM 설명서 참조: [측정](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) 추가 정보.

| 측정 | 권장 사항 | 설명 |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | 선택 사항입니다 | 사용자가 장바구니에 더 이상 액세스하거나 구매할 수 없습니다. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | 적극 권장 | 사용자가 더 이상 제품을 탐색하지 않고 제품을 구매 중입니다. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | 적극 권장 | 제품이 목록에 추가됩니다. 제품을에서 설정해야 합니다. `productListItems` 동시에. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | 선택 사항입니다 | 새 제품 목록이 만들어집니다. 예를 들어 새 장바구니가 만들어집니다. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | 적극 권장 | 제품이 제품 목록에서 제거됩니다. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | 선택 사항입니다 | 사용자가 제품 목록을 다시 활성화합니다. 이 작업은 리마케팅 캠페인에서 자주 수행됩니다. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | 적극 권장 | 제품 목록이 표시됩니다. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | 적극 권장 | 제품 보기가 발생했습니다. 에서 본 제품을 설정해야 합니다. `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | 적극 권장 | 주문이 수락됩니다. 제품 목록이 있어야 합니다. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | 선택 사항입니다 | 나중에 사용할 수 있도록 제품이 저장됩니다. |

{style="table-layout:auto"}

### `Commerce` 오브젝트 예

아래 섹션을 확장하여 의 필드를 사용하는 웹 SDK 명령의 예를 봅니다. `commerce` 개체.

+++`productViews`

기본 웹 SDK `sendEvent` 호출 설정 `productViews` 필드 대상 `1`:

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

+++

## 다음 `order` 오브젝트 {#order-object}

다음 `commerce` 객체에는 주문 세부 사항을 수집하는 전용 객체가 포함되어 있습니다. 이를 라고 합니다. `order` 개체.

이 섹션에서는 `order` 개체.

| 필드 | 옵션 | 권장 사항 | 설명 |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 주문 합계에 대한 통화. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | 주문에 대한 결제 목록. A [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) 에는 다음 항목이 포함되어 있습니다. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | 선택 사항입니다 | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 해당 결제 방법에 대한 통화. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | 적극 권장 | 지정된 통화 코드 내 결제 값. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | 적극 권장 | 결제 유형(예: `credit_card`, `gift_card`, `paypal`). 목록 보기 [알려진 값](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) 을 참조하십시오. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | 선택 사항입니다 | 해당 결제 거래에 대한 고유 ID. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | 적극 권장 | 할인 및 세금이 모두 적용된 후 이 주문에 대한 합계입니다. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | 적극 권장 | 판매자가 해당 구매에 할당한 고유 식별자. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | 선택 사항입니다 | 구매자가 해당 구매에 할당한 고유 식별자. |

### Order 객체 예

아래 섹션을 확장하여 를 사용하는 웹 SDK 명령의 예를 봅니다. `commerce` 개체.

+++`Order` 개체 예

웹 SDK `sendEvent` 호출 설정 `order` 의 여러 제품에 적용되는 개체 `productListItems` 배열:

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

+++

## 제품 목록 개체 {#product-list-object}

제품 목록은 해당 작업과 관련된 제품을 나타냅니다. 다음 중 하나입니다. [productListItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). 각 제품에는 몇 가지 옵션 필드가 있습니다.

| 필드 | 권장 사항 | 설명 |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | 선택 사항입니다 | 다음 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 제품에 대한 통화. 이 필드는 일반적으로 제품 목록에 다른 통화 코드가 있는 제품이 여러 개 있는 경우에만 적용됩니다. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | 적극 권장 | 해당되는 경우에만 이 필드를 설정하십시오. 예를 들어 를 설정하지 못할 수 있습니다 `productView` 이벤트입니다. 제품의 다양한 변형은 가격이 다를 수 있지만 `productListAdds` 이벤트. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | 적극 권장 | 제품에 대한 XDM ID. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | 적극 권장 | 방문자가 목록에 제품 항목을 추가하는 데 사용한 메서드입니다. 다음으로 설정 `productListAdds` 를 측정하고 제품이 목록에 추가되는 경우에만 사용됩니다. 예로는 `add to cart button`, `quick add` 및 `upsell`가 있습니다. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | 적극 권장 | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | 적극 권장 | 고객이 제품에 필요하다고 표시한 단위 수. 다음에 설정되어야 함: `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`등. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | 적극 권장 | 상점 유지 장치. 제품에 대한 고유 식별자입니다. |

### 제품 목록 예

아래 섹션을 확장하여 다음을 사용하는 웹 SDK 명령의 예를 봅니다. `productListItems` 개체.

+++`productListItems` 예

웹 SDK `sendEvent` 호출 설정 `productViews` 의 여러 제품용 `productListItems` 배열:

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

+++

+++`productListAdds` 예

웹 SDK `sendEvent` 호출 설정 `productListAdds` 의 여러 제품에 대한 이벤트 `productListItems` 배열:

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

+++

+++`checkouts` 예

웹 SDK `sendEvent` 호출 설정 `checkouts` 의 여러 제품에 대한 이벤트 `productListItems` 배열:

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

+++
