---
title: 노출 횟수 데이터 유형
description: 이 문서에서는 노출 XDM 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  인상주의 데이터 유형

 Impressis는 마케팅 노출을 설명하는 표준 XDM 데이터 유형이며 광고, 디지털 게시물 또는 웹 페이지와 같은 컨텐츠에 대한 디지털 보기 또는 참여 수를 수량화하는 데 사용되는 지표입니다.

![](../images/data-types/impressions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ID` | 문자열 | 노출에 대한 고유 ID입니다. |
| `displays` | 정수 | 고객에게 노출 항목이 표시된 횟수입니다. |
| `selected` | 정수 | 노출 항목을 선택하거나 클릭한 횟수입니다. |
| `type` | 문자열 | 노출 유형. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
