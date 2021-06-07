---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 마케팅 데이터 유형
topic-legacy: overview
description: 이 문서에서는 마케팅 XDM 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 3%

---


#  마케팅 데이터 유형

 마케팅은 특정 터치 포인트로 활성 상태인 마케팅 활동을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/marketing.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignGroup` | 문자열 | 캠페인 그룹의 이름입니다(여러 캠페인을 `50%_DISCOUNT` 과 같이 함께 그룹화하는 경우). |
| `campaignName` | 문자열 | `50%_DISCOUNT_USA` 또는 `50%_DISCOUNT_ASIA` 과 같은 마케팅 캠페인의 이름입니다. |
| `trackingCode` | 문자열 | 이벤트가 연결된 마케팅 캠페인을 식별하는 데 사용할 수 있는 추적 코드입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
