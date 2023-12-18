---
title: 장바구니 데이터 유형
description: 장바구니 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL 장바구니] 데이터 유형

[!UICONTROL 장바구니] 는 장바구니와 관련된 속성을 제공하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 이 데이터 유형을 사용하여 판매자가 할당한 고유 식별자를 캡처합니다(`Cart ID`) 및 소스(`Cart Source`) 하나 이상의 제품이 장바구니에 추가된 위치입니다.

![의 다이어그램 [!UICONTROL 장바구니] 데이터 유형.](../images/data-types/cart.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 장바구니 ID] | `cartID` | 문자열 | 판매자가 장바구니에 할당한 고유 식별자. |
| [!UICONTROL 장바구니 소스] | `cartSource` | 문자열 | 하나 이상의 제품이 장바구니에 추가된 위치입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
