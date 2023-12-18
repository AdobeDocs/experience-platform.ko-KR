---
title: 반환 항목 데이터 유형
description: 반환 항목 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL 항목 반환] 데이터 유형

[!UICONTROL 항목 반환] 는 표준 경험 데이터 모델(XDM) 데이터 유형으로서, 구매한 항목에 대한 반환 프로세스와 관련된 필수 세부 정보를 캡처합니다.

![반환 항목 데이터 형식의 다이어그램입니다.](../images/data-types/return-item.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL 반환 상태] | `returnStatus` | 문자열 | 반환된 항목의 상태(예: 보류 중 또는 승인됨)입니다. |
| [!UICONTROL 반환 이유] | `returnReason` | 문자열 | 항목에 대해 반환을 요청한 이유입니다. |
| [!UICONTROL 반환 항목 조건] | `returnItemCondition` | 문자열 | 반환이 요청되는 항목의 상태입니다. |
| [!UICONTROL 반환 해결] | `returnResolution` | 문자열 | 원하는 해결 방법 또는 반품 결과(예: 환불 또는 교환). |
| [!UICONTROL 반품 수량 요청] | `returnQuantityRequested` | 정수 | 구매자가 반품을 요청한 항목의 수량입니다. |
| [!UICONTROL 승인된 반품 수량] | `returnQuantityAuthorized` | 정수 | 반품이 승인된 품목의 수량입니다. |
| [!UICONTROL 반품 입고 수량] | `returnQuantityReceived` | 정수 | 받은 반품된 항목의 수량입니다. |
| [!UICONTROL 반품 수량 승인됨] | `returnQuantityApproved` | 정수 | 반품이 완전히 완료되고 승인된 항목의 수량입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
