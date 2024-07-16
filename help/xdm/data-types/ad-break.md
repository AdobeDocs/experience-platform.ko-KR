---
title: 광고 브레이크 데이터 유형
description: 광고 브레이크 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 21%

---

# [!UICONTROL 광고 브레이크] 데이터 형식

[!UICONTROL 광고 브레이크]는 시간 지정 광고가 시간 지정 미디어에 삽입되는 방법을 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다.

![데이터 형식 구조](../images/data-types/ad-break.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_dc.title` | 문자열 | 광고 브레이크에 대한 알기 쉬운 이름. |
| `_id` | 문자열 | 광고 브레이크에 대한 고유 식별자. |
| `offset` | 정수 | 기본 콘텐츠 시작 시 중간 광고 오프셋(시간: 초). |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
