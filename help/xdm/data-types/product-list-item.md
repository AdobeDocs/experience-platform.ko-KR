---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;주소;xdm:주소;데이터 유형;데이터 유형;
solution: Experience Platform
title: 제품 목록 항목 데이터 유형
description: 이 문서에서는 제품 목록 항목 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 4%

---

# [!UICONTROL 제품 목록 항목] 데이터 유형

[!UICONTROL 제품 목록 항목] 는 특정 시점에 특정 옵션, 가격 및 사용 컨텍스트가 있는 고객이 선택한 제품을 설명하는 표준 XDM 데이터 유형입니다.

이 데이터 유형에 캡처된 값은 제품 레코드와 다를 수 있습니다. 예를 들어, 제품 레코드에는 모든 고객에 대해 일관된 제품 정보 시스템의 세부 사항이 포함되어 있습니다. 이 경우 제품 목록 항목이 구매 시 고객에게 제공되는 실제 가격을 가지며, 이는 판매 캠페인이나 계절별 가격 때문에 달라질 수 있습니다.

![](../images/data-types/product-list-item.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `selectedOptions` | 개체 배열 | 구성 가능한 제품에 대해 선택한 사용자 지정 옵션을 포함합니다. 각 목록 항목은 다음 속성을 갖는 객체입니다.<ul><li>`attribute`: 구성 가능한 속성의 이름입니다.</li><li>`value`: 속성 값입니다.</li></ul> |
| `SKU` | [!UICONTROL 문자열] | 공급업체에서 정의한 제품의 고유 식별자인 SKU(Stock Keeping Unit). |
| `_id` | [!UICONTROL 문자열] | 이 제품 항목에 대한 라인 항목 식별자입니다. 제품 자체는 `product`. |
| `currencyCode` | [!UICONTROL 문자열] | 다음 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 제품 가격책정에 사용되는 알파벳 통화 코드. |
| `discountAmount` | [!UICONTROL 이중] | 제품이 할인된 경우, 이는 일반 가격과 제품에 대한 특별 가격 간의 차이를 나타냅니다. |
| `name` | [!UICONTROL 문자열] | 이 제품 보기에 대해 사용자에게 표시되는 제품의 표시 이름입니다. |
| `priceTotal` | [!UICONTROL 이중] | 제품 라인 항목의 총 가격. |
| `product` | [!UICONTROL 문자열] (URI) | URI `$id` 제품 자체를 캡처하는 XDM 스키마 입니다. |
| `productAddMethod` | [!UICONTROL 문자열] | 방문자가 목록에 제품 항목을 추가하는 데 사용한 방법입니다. |
| `productImageUrl` | [!UICONTROL 문자열] | 제품의 기본 이미지에 대한 URL입니다. |
| `quantity` | [!UICONTROL 정수] | 고객이 제품을 필요로 한다고 표시한 단위 수입니다. |
| `unitOfMeasureCode` | [!UICONTROL 문자열] | 표준 [측정 단위 코드](https://ucum.org/ucum) 관련 `quantity` 속성을 사용합니다. |

{style=&quot;table-layout:auto&quot;}

우편 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
