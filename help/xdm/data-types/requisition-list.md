---
title: 구매요청 목록 데이터 유형
description: 구매요청 목록 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 5%

---

# [!UICONTROL 구매요청 목록] 데이터 유형

[!UICONTROL 구매요청 목록] 는 조달 또는 구매를 위해 선별된 항목 컬렉션을 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 사용 [!UICONTROL 구매요청 목록] 구매요청 목록을 식별하고 설명하는 데이터 유형.

![의 다이어그램 [!UICONTROL 구매요청 목록] 데이터 유형.](../images/data-types/requisition-list.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL 구매요청 목록 ID] | `ID` | 문자열 | 구매요청 목록의 고유 식별자. |
| [!UICONTROL 구매요청 목록명] | `name` | 문자열 | 고객이 지정한 구매요청 목록의 이름. |
| [!UICONTROL 구매요청 목록 설명] | `description` | 문자열 | 고객이 지정한 구매요청 목록에 대한 설명. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
