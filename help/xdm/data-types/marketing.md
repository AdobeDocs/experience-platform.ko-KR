---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;장치;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 마케팅 데이터 유형
description: 이 문서에서는 마케팅 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---

# [!UICONTROL 마케팅] 데이터 유형

[!UICONTROL 마케팅] 는 특정 터치 포인트로 활성 상태인 마케팅 활동을 설명하는 표준 XDM 데이터 유형입니다.

![](../images/data-types/marketing.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignGroup` | 문자열 | 캠페인 그룹의 이름입니다(여러 개의 캠페인을 다음과 같이 그룹화하는 경우) `50%_DISCOUNT`). |
| `campaignName` | 문자열 | 마케팅 캠페인의 이름(예: ) `50%_DISCOUNT_USA` 또는 `50%_DISCOUNT_ASIA`. |
| `trackingCode` | 문자열 | 이벤트가 연결된 마케팅 캠페인을 식별하는 데 사용할 수 있는 추적 코드입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
