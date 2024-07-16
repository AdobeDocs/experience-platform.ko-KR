---
title: 장바구니 데이터 유형
description: 장바구니 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# [!UICONTROL 장바구니] 데이터 형식

[!UICONTROL 장바구니]은(는) 장바구니와 관련된 속성을 제공하는 표준 XDM(경험 데이터 모델) 데이터 형식입니다. 이 데이터 형식을 사용하여 판매자(`Cart ID`)가 할당한 고유 식별자 및 하나 이상의 제품이 장바구니에 추가된 소스(`Cart Source`)를 캡처합니다.

![[!UICONTROL Cart] 데이터 형식의 다이어그램입니다.](../images/data-types/cart.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 장바구니 ID] | `cartID` | 문자열 | 판매자가 장바구니에 할당한 고유 식별자. |
| [!UICONTROL 장바구니 Source] | `cartSource` | 문자열 | 하나 이상의 제품이 장바구니에 추가된 위치입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
