---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 마케팅 데이터 유형
description: 이 문서에서는 마케팅 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 3%

---

# [!UICONTROL 마케팅] 데이터 유형

[!UICONTROL 마케팅] 는 특정 접점으로 활성화되는 마케팅 활동을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/marketing.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignGroup` | 문자열 | 캠페인 그룹의 이름(여러 캠페인이 다음과 같이 함께 그룹화된 경우) `50%_DISCOUNT`). |
| `campaignName` | 문자열 | 다음과 같은 마케팅 캠페인의 이름 `50%_DISCOUNT_USA` 또는 `50%_DISCOUNT_ASIA`. |
| `trackingCode` | 문자열 | 이벤트와 연계된 마케팅 캠페인을 식별하는 데 사용할 수 있는 추적 코드입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
