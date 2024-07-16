---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;주소;xdm:address;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 제품 목록 항목 데이터 유형
description: 제품 목록 항목 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 18%

---

# [!UICONTROL 제품 목록 항목] 데이터 형식

[!UICONTROL 제품 목록 항목]은(는) 특정 시점에 대한 특정 옵션, 가격 및 사용 컨텍스트와 함께 고객이 선택한 제품을 설명하는 표준 XDM 데이터 형식입니다.

이 데이터 유형에서 캡처한 값은 제품 레코드와 다를 수 있습니다. 예를 들어 제품 레코드에는 모든 고객에 대해 일관적인 제품 정보 시스템의 세부 사항이 포함되어 있습니다. 여기서 제품 목록 항목에는 구매 시 고객에게 제공되는 실제 가격이 있으며, 이는 판매 캠페인이나 계절별 가격 책정에 따라 다를 수 있습니다.

![](../images/data-types/product-list-item.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `selectedOptions` | 오브젝트 배열 | 구성 가능한 제품에 대해 선택된 사용자 지정 옵션을 포함합니다. 각 목록 항목은 다음 속성을 갖는 객체입니다.<ul><li>`attribute`: 구성 가능한 특성의 이름입니다.</li><li>`value`: 특성 값입니다.</li></ul> |
| `SKU` | [!UICONTROL 문자열] | 공급업체가 정의한 제품에 대한 고유 식별자인 SKU(Stock Keeping Unit). |
| `_id` | [!UICONTROL 문자열] | 해당 제품 항목에 대한 라인 항목 식별자. 제품 자체는 `product`을(를) 통해 식별됩니다. |
| `currencyCode` | [!UICONTROL 문자열] | 제품 가격 설정에 사용되는 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 알파벳 통화 코드입니다. |
| `discountAmount` | [!UICONTROL 이중] | 상품을 할인한 경우, 이는 상품에 대한 정가와 특별가의 차이를 나타낸다. |
| `name` | [!UICONTROL 문자열] | 해당 제품 조회를 위해 사용자에게 제시된 제품별 디스플레이 이름. |
| `priceTotal` | [!UICONTROL 이중] | 제품 라인 항목의 전체 가격. |
| `product` | [!UICONTROL 문자열](URI) | 제품 자체를 캡처하는 XDM 스키마의 URI `$id`입니다. |
| `productAddMethod` | [!UICONTROL 문자열] | 방문자가 목록에 제품 항목을 추가하는 데 사용한 메서드입니다. |
| `productImageUrl` | [!UICONTROL 문자열] | 제품의 기본 이미지에 대한 URL. |
| `quantity` | [!UICONTROL 정수] | 제품이 필요하다고 고객이 표시한 단위 수. |
| `unitOfMeasureCode` | [!UICONTROL 문자열] | `quantity` 속성과 관련된 제품에 대한 표준 [측정 단위 코드](https://ucum.org/ucum). |

{style="table-layout:auto"}

우편 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
