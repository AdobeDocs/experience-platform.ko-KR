---
title: 노출 횟수 데이터 유형
description: 노출 횟수 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# [!UICONTROL 노출 횟수] 데이터 형식

[!UICONTROL 노출 수]은(는) 광고, 디지털 게시물 또는 웹 페이지와 같은 콘텐츠에 대한 디지털 보기 또는 참여 수를 정량화하는 데 사용되는 지표인 마케팅 노출 수를 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/impressions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ID` | 문자열 | 노출에 대한 고유 ID. |
| `displays` | 정수 | 고객에게 노출 항목이 표시된 횟수입니다. |
| `selected` | 정수 | 노출 항목을 선택하거나 클릭한 횟수입니다. |
| `type` | 문자열 | 노출 유형. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
