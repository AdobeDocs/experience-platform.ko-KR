---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;상거래;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 상거래 데이터 유형
description: 이 문서에서는 XDM(Commerce Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 상거래] 데이터 유형

[!UICONTROL 상거래] 는 구매 및 판매 활동과 관련된 레코드를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `order` | [[!UICONTROL 주문]](./order.md) | 하나 이상의 제품에 대한 주문 내역에 대해 설명합니다. |
| `cartAbandons` | [[!UICONTROL 측정]](./measure.md) | 사용자가 제품 목록을 더 이상 액세스할 수 없거나 구매할 수 없는 것으로 식별한 경우를 설명하는 데 사용됩니다. |
| `checkouts` | [[!UICONTROL 측정]](./measure.md) | 제품 목록 체크아웃 프로세스 중의 작업입니다. 체크아웃 프로세스에 여러 단계가 있는 경우 두 개 이상의 체크아웃 이벤트가 있을 수 있습니다. 여러 단계가 있는 경우 이벤트 시간 정보와 참조된 페이지 또는 경험을 사용하여 순서대로 표시되는 단계 및 개별 이벤트를 식별합니다. |
| `inStorePurchase` | [[!UICONTROL 측정]](./measure.md) | Analytics 사용을 위한 매장 내 구매와 관련된 값을 설명합니다. |
| `productListAdds` | [[!UICONTROL 측정]](./measure.md) | 장바구니에 추가되는 제품과 같이 제품 목록에 제품 추가. |
| `productListOpens` | [[!UICONTROL 측정]](./measure.md) | 만들어지는 장바구니와 같은 새 제품 목록의 초기화. |
| `productListRemovals` | [[!UICONTROL 측정]](./measure.md) | 장바구니에서 제거되는 제품과 같은 제품 목록에서 제품 항목을 제거 또는 제거합니다. |
| `productListReopens` | [[!UICONTROL 측정]](./measure.md) | 이전에 중단되었던 제품 목록에서 사용자가 다시 활성화했습니다. |
| `productListViews` | [[!UICONTROL 측정]](./measure.md) | 제품 목록 보기가 발생한 시기를 설명합니다. |
| `productViews` | [[!UICONTROL 측정]](./measure.md) | 개별 제품에 대한 보기가 발생한 시기를 설명합니다. |
| `purchases` | [[!UICONTROL 측정]](./measure.md) | 주문이 수락된 시기를 추적하는 데 사용됩니다. 구매 이벤트는 상거래 전환에서 유일한 필수 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `saveForLaters` | [[!UICONTROL 측정]](./measure.md) | 제품 목록은 나중에 사용할 수 있도록 저장됩니다(예: 위시리스트). |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
