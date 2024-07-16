---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 마케팅 데이터 유형
description: 마케팅 XDM 데이터 유형에 대해 알아봅니다.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# [!UICONTROL 마케팅] 데이터 형식

[!UICONTROL 마케팅]은(는) 특정 접점으로 활성화된 마케팅 활동을 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/marketing.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignGroup` | 문자열 | 캠페인 그룹의 이름(`50%_DISCOUNT`과 같이 여러 캠페인이 함께 그룹화된 경우). |
| `campaignName` | 문자열 | 마케팅 캠페인의 이름(예: `50%_DISCOUNT_USA` 또는 `50%_DISCOUNT_ASIA`) |
| `trackingCode` | 문자열 | 이벤트와 연계된 마케팅 캠페인을 식별하는 데 사용할 수 있는 추적 코드입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
