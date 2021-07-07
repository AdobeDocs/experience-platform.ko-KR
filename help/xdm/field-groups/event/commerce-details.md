---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 상거래 세부 사항 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 상거래 세부 사항 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL 상거래 ] 세부 정보스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL 상거래 ] 세부 사항은 제품 정보(SKU, 이름, 수량) 및 표준 장바구니 작업(주문, 체크아웃, 중단)과 같은 상거래 데이터를 설명하는 데 사용되는  [[!DNL XDM ExperienceEvent] 클래스 ](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/commerce-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | 제품 반품, 보증 등록 및 장바구니/주문 프로세스를 설명하는 객체입니다. |
| `productListItems` | [제품 목록 항목의 배열](../../data-types/product-list-item.md) | 고객이 선택한 제품을 나타내는 항목의 목록이며 특정 시점의 특정 옵션 및 가격(제품 레코드와 다를 수 있음)입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
