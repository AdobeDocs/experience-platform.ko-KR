---
title: 제품 클래스
description: XDM(경험 데이터 모델)의 제품 클래스에 대해 알아봅니다.
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 8%

---

# [!UICONTROL 제품] 클래스

XDM(Experience Data Model)에서 [!UICONTROL Product] 클래스는 소매 제품을 정의하는 최소 속성 집합을 캡처합니다.

![](../images/classes/product.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productListPrice` | [통화](../data-types/currency.md) | 판매 및 할인 혜택 이전 제품의 기본 가격을 설명합니다. |
| `_id` | 문자열 | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `productDescription` | 문자열 | 제품에 대한 설명. |
| `productID` | 문자열 | 제품에 대한 고유 식별자. |
| `productLastModifiedDate` | 날짜/시간 | 업데이트를 위해 이 제품을 마지막으로 수정한 시간의 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 타임스탬프입니다. |
| `productManufacturedDate` | 날짜/시간 | 이 제품을 만든 시간의 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 타임스탬프입니다. |
| `productName` | 문자열 | 제품 이름. |
| `productRating` | 문자열 | 제품에 대한 고객 리뷰 등급. |

{style="table-layout:auto"}

## 호환 가능한 필드 그룹 {#field-groups}

Adobe은 [!UICONTROL Product] 클래스와 함께 사용할 여러 표준 필드 그룹을 제공합니다. 다음은 클래스에서 일반적으로 사용되는 몇 가지 필드 그룹 목록입니다.

* [[!UICONTROL 제품 카탈로그]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 제품 범주]](../field-groups/product/product-category.md)
