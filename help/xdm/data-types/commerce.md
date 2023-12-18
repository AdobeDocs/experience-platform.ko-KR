---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;상거래;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 상거래 데이터 유형
description: Commerce Experience Data Model(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL 상거래] 데이터 유형

[!UICONTROL 상거래] 는 구매 및 판매와 관련된 레코드를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

![의 다이어그램 [!UICONTROL 상거래] 데이터 유형.](../images/data-types/commerce.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL 주문] | `order` | [[!UICONTROL 주문]](./order.md) | 하나 이상의 제품에 대한 주문 내역에 대해 설명합니다. |
| [!UICONTROL 프로모션 ID] | `promotionID` | [!UICONTROL 문자열] | 주문된 주문에 대한 프로모션 식별자(있는 경우). |
| [!UICONTROL 장바구니 포기] | `cartAbandons` | [[!UICONTROL 측정]](./measure.md) | 사용자가 제품 목록을 더 이상 액세스할 수 없거나 구매할 수 없는 것으로 식별하는 시기를 설명합니다. |
| [!UICONTROL 체크아웃] | `checkouts` | [[!UICONTROL 측정]](./measure.md) | 제품 목록 체크아웃 프로세스 중의 작업입니다. 체크아웃 프로세스에 여러 단계가 있는 경우 두 개 이상의 체크아웃 이벤트가 있을 수 있습니다. 여러 단계가 있는 경우 이벤트 시간 정보와 참조된 페이지 또는 경험을 사용하여 순서대로 표시되는 단계 및 개별 이벤트를 식별합니다. |
| [!UICONTROL 제품 목록(장바구니) 추가] | `productListAdds` | [[!UICONTROL 측정]](./measure.md) | 장바구니에 추가되는 제품과 같이 제품 목록에 제품 추가. |
| [!UICONTROL 제품 목록(장바구니) 오픈 수] | `productListOpens` | [[!UICONTROL 측정]](./measure.md) | 만들어지는 장바구니와 같은 새 제품 목록의 초기화. |
| [!UICONTROL 제품 목록(장바구니) 제거] | `productListRemovals` | [[!UICONTROL 측정]](./measure.md) | 장바구니에서 제거되는 제품과 같은 제품 목록에서 제품 항목을 제거 또는 제거합니다. |
| [!UICONTROL 제품 목록(장바구니) 재오픈 수] | `productListReopens` | [[!UICONTROL 측정]](./measure.md) | 이전에 중단되었던 제품 목록에서 사용자가 다시 활성화했습니다. |
| [!UICONTROL 제품 목록(장바구니) 보기] | `productListViews` | [[!UICONTROL 측정]](./measure.md) | 제품 목록 조회수가 발생한 시점을 설명합니다.제품 목록 조회수가 발생한 시점을 설명합니다. |
| [!UICONTROL 제품 보기] | `productViews` | [[!UICONTROL 측정]](./measure.md) | 개별 제품에 대한 보기가 발생한 시기를 설명합니다. |
| [!UICONTROL 구매] | `purchases` | [[!UICONTROL 측정]](./measure.md) | 주문이 수락된 시기를 추적하는 데 사용됩니다. 구매 이벤트는 상거래 전환에서 유일한 필수 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| [!UICONTROL 나중을 위해 저장] | `saveForLaters` | [[!UICONTROL 측정]](./measure.md) | 위시리스트와 같이 나중에 사용할 수 있도록 제품 목록을 저장하는 경우를 설명합니다. |
| [!UICONTROL 스토어에서 구매] | `inStorePurchase` | [[!UICONTROL 측정]](./measure.md) | &#39;inStore&#39; 구매를 나타냅니다. 이 정보는 분석 용도로 저장됩니다. |
| [!UICONTROL 장바구니] | `cart` | [[!UICONTROL 장바구니]](./cart.md) | 하나 이상의 제품이 포함된 장바구니의 속성입니다. |
| [!UICONTROL 배송] | `shipping` | [[!UICONTROL 배송]](./shipping.md) | 하나 이상의 제품에 대한 배송 세부 정보. |
| [!UICONTROL 과금] | `billing` | [[!UICONTROL 과금]](#billing) | 하나 이상의 지불에 대한 청구 세부 정보. |
| [!UICONTROL 즉시 구매] | `instantPurchase` | [[!UICONTROL 측정]](./measure.md) | 제품을 즉시 구매하여 장바구니 또는 체크아웃을 건너뛸 가능성이 있는 경우를 설명합니다. |
| [!UICONTROL 구매요청 목록 열람수] | `requisitionListOpens` | [[!UICONTROL 측정]](./measure.md) | 새 구매요청 목록의 초기화를 나타냅니다. |
| [!UICONTROL 구매요청 목록 삭제] | `requisitionListDeletes` | [[!UICONTROL 측정]](./measure.md) | 구매요청 목록 제거를 나타냅니다. |
| [!UICONTROL 구매요청 목록 추가] | `requisitionListAdds` | [[!UICONTROL 측정]](./measure.md) | 구매요청 목록에 제품을 추가함을 나타냅니다. |
| [!UICONTROL 구매요청 목록 제거] | `requisitionListRemovals` | [[!UICONTROL 측정]](./measure.md) | 구매요청 제품 목록에서 제품이 제거되었음을 나타냅니다. |
| [!UICONTROL 요청 목록] | `requisitionList` | [[!UICONTROL 요구 사항 목록]](./requisition-list.md) | 고객이 생성한 구매요청 목록의 속성. |
| [!UICONTROL 범위] | `commerceScope` | [[!UICONTROL commercescope]](./commerce-scope.md) | 이벤트가 발생한 위치의 상거래 범위 식별자(스토어 보기, 스토어, 웹 사이트 등). |

{style="table-layout:auto"}

## [!UICONTROL 과금] 데이터 유형 {#billing}

[!UICONTROL 과금] 는 청구 세부 정보에 대한 정보가 포함된 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 특히, 청구 주소에 중점을 둡니다.

![과금 데이터 유형 다이어그램.](../images/data-types/billing.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL 청구 주소] | `address` | [[!UICONTROL 우편 주소]](./postal-address.md) | 청구 주소. |

{style="table-layout:auto"}

에 대한 자세한 내용은 [!UICONTROL 상거래] 데이터 유형은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
