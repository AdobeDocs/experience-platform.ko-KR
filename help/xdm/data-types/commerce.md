---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;상거래;데이터 유형;데이터 유형;데이터 유형;A;
solution: Experience Platform
title: 상거래 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM(Commerce Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# [!UICONTROL Commerce] 데이터 유형

[!UICONTROL Commerce] 는 구매 및 판매 활동과 관련된 기록을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `order` | [[!UICONTROL Order]](./order.md) | 하나 이상의 제품에 대한 주문서에 대해 설명합니다. |
| `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | 사용자가 제품 목록에 더 이상 액세스할 수 없거나 구입할 수 없는 것으로 식별된 시기를 설명하는 데 사용됩니다. |
| `checkouts` | [[!UICONTROL Measure]](./measure.md) | 제품 목록의 체크아웃 프로세스 중 작업입니다. 체크아웃 프로세스에 여러 단계가 있을 경우 체크아웃 이벤트를 두 개 이상 사용할 수 있습니다. 여러 단계가 있는 경우, 이벤트 시간 정보 및 참조된 페이지 또는 경험이 순서대로 표시되는 단계와 개별 이벤트를 식별하는 데 사용됩니다. |
| `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | 분석 사용을 위해 매장 내 구입과 관련된 값을 설명합니다. |
| `productListAdds` | [[!UICONTROL Measure]](./measure.md) | 장바구니에 추가되는 제품과 같이 제품 목록에 제품을 추가하는 것입니다. |
| `productListOpens` | [[!UICONTROL Measure]](./measure.md) | 만들어지는 장바구니 같은 새 제품 목록의 초기 화면입니다. |
| `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | 장바구니에서 제거할 제품과 같이 제품 목록에서 제품 항목을 제거하거나 제거합니다. |
| `productListReopens` | [[!UICONTROL Measure]](./measure.md) | 사용자가 다시 활성화한 이전에 포기한 제품 목록. |
| `productListViews` | [[!UICONTROL Measure]](./measure.md) | 제품 목록의 보기 또는 보기가 발생한 시기를 설명합니다. |
| `productViews` | [[!UICONTROL Measure]](./measure.md) | 개별 제품의 보기 또는 보기가 발생한 시기를 설명합니다. |
| `purchases` | [[!UICONTROL Measure]](./measure.md) | 주문이 수락된 시점을 추적하는 데 사용됩니다. 구매 이벤트는 커머스 전환에서 유일한 필수 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | 제품 목록은 위시리즈와 같은 향후 사용을 위해 저장됩니다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
