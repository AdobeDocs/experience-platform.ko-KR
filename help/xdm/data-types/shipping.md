---
title: 배송 데이터 유형
description: XDM(Shipping Experience Data Model) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL 배송] 데이터 유형

[!UICONTROL 배송] 는 하나 이상의 제품 배송과 관련된 세부 정보를 제공하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 물류 명세와 주문한 상품의 배송에 관한 사항이 포함되어 있습니다.


![의 다이어그램 [!UICONTROL 배송] 데이터 유형.](../images/data-types/shipping.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL 배송 방법] | `shippingMethod` | 문자열 | 고객이 선택한 배송 방법. |
| [!UICONTROL 배송 금액] | `shippingAmount` | 숫자 | 고객이 배송비로 지불해야 했던 금액. |
| [!UICONTROL 통화 코드] | `currencyCode` | 문자열 | 제품 가격 설정에 사용되는 ISO 4217 알파벳 통화 코드. |
| [!UICONTROL 배송 대상] | `shippingDestination` | 문자열 | 사용자가 지정한 배송처 대상(예: 홈, 스토어 등)입니다. |
| [!UICONTROL 출하 일자] | `shipDate` | 문자열 | 주문에서 하나 이상의 품목이 배송된 날짜. |
| [!UICONTROL 배송 주소] | `address` | [[!UICONTROL 주소]](./address.md) | 배송 주소입니다. |
| [!UICONTROL 추적 번호] | `trackingNumber` | 숫자 | 운송 회사가 제공한 추적 번호입니다. |
| [!UICONTROL 추적 URL] | `trackingURL` | 문자열 | 주문 항목의 배송 상태를 추적할 URL입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
