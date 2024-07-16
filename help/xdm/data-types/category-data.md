---
title: 범주 데이터 데이터 유형
description: 카테고리 데이터 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: f8d52f2d-5fb0-4999-8b31-ddc14225b0ab
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 9%

---

# [!UICONTROL 범주 데이터] 데이터 형식

[!UICONTROL 카테고리 데이터]은(는) 제품 카테고리와 관련된 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다.

![Category 데이터 형식의 다이어그램입니다.](../images/data-types/category-data.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-----------------|--------------------|-----------|------------------------------------------|
| [!UICONTROL 범주 식별자] | `categoryID` | 문자열 | 제품 범주에 대한 식별자. |
| [!UICONTROL 범주 이름] | `categoryName` | 문자열 | 제품 범주의 이름입니다. |
| [!UICONTROL 범주 경로] | `categoryPath` | 문자열 | 제품 범주의 경로. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/categorydata.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/categorydata.schema.json)
