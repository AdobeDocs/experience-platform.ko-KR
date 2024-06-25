---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;순서;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 주문 데이터 유형
description: XDM(Order Experience Data Model) 데이터 유형에 대해 알아봅니다.
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL 주문] 데이터 유형

[!UICONTROL 주문] 는 제품 목록에 배치된 순서를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

![의 다이어그램 [!UICONTROL 주문] 데이터 유형.](../images/data-types/order.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| 구매 ID | `purchaseID` | 문자열 | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. 판매자가 ID를 정의하므로 ID가 고유하다고 보장할 수 없습니다. |
| 구매 주문 번호 | `purchaseOrderNumber` | 문자열 | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |
| 결제 목록 | `payments` | 배열 [[!UICONTROL 결제 항목]](./payment-item.md) | 해당 주문에 대한 결제 목록. 지불은 다음에 자세히 설명되어 있습니다 [!UICONTROL 결제 항목] 사양. |
| 환불 목록 | `refunds` | 배열 [[!UICONTROL 환불 항목]](./refund-item.md) | 해당 주문에 대한 환불 목록. 환불은 다음에 자세히 설명되어 있습니다. [!UICONTROL 환불 항목] 사양. |
| 반환 정보 | `returns` | [[!UICONTROL 반환 정보]](./return.md) | RMA(반품 상품 승인)가 발행되었습니다. 반환은 다음에 자세히 설명되어 있습니다. [!UICONTROL 반환 정보] 사양. |
| 통화 | `currencyCode` | 문자열 | 주문 합계에 사용되는 ISO 4217 통화 코드. 예를 들면 다음과 같습니다 `USD` 및 `EUR`. 모든 인스턴스는 패턴과 일치해야 합니다 `^[A-Z]{3}$`. |
| 세액 | `taxAmount` | 숫자 | 최종 지급의 일부로 구매자가 지불한 세액. |
| 할인 금액 | `discountAmount` | 숫자 | 정가와 특별가의 차액은 개별 상품이 아닌 전체 주문에 적용됩니다. |
| 전체 가격 | `priceTotal` | 숫자 | 할인 및 세금이 모두 적용된 이후 해당 주문의 전체 가격. |
| 주문 유형 | `orderType` | 문자열 | 완료된 주문 유형. 가능한 값은 다음과 같습니다 `checkout` 및 `instant_purchase`. |
| 마지막으로 업데이트한 날짜 | `lastUpdatedDate` | 문자열 | 상거래 시스템에서 특정 주문 레코드가 마지막으로 업데이트되는 시간. 형식: 날짜-시간. |
| 생성일 | `createdDate` | 문자열 | 상거래 시스템에서 새 주문이 생성된 시간/날짜. 형식: 날짜-시간. |
| 취소 일자 | `cancelDate` | 문자열 | 구매자가 주문 취소를 시작한 날짜/시간입니다. 형식: 날짜-시간. |
| 총 환불 금액 | `refundTotal` | 숫자 | 모든 환불 항목과 할인 후 등 주문에 대한 이 환불에 제공된 총 금액. 이(가) 적용되었습니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
