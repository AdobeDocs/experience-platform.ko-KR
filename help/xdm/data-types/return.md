---
title: 반환 데이터 유형
description: 반환 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 6%

---

# [!UICONTROL 반환] 데이터 유형

[!UICONTROL 반환] 는 RMA(반품 승인)와 관련된 필수 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

![반환 데이터 형식의 다이어그램입니다.](../images/data-types/return.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL 반환 ID] | `returnID` | 문자열 | 해당 RMA에 대한 고유 식별자. |
| [!UICONTROL 반환 상태] | `returnStatus` | 문자열 | RMA의 현재 상태(예: 보류 중 또는 마감). |
| [!UICONTROL 주문 구매 ID] | `purchaseID` | 문자열 | RMA가 관련된 주문/구매에 대한 고유 식별자. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

