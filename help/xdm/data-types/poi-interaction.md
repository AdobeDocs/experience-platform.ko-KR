---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;poi;상호 작용;관심 영역;관심 영역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 관심 영역 인터랙션 데이터 유형
description: 관심 영역 인터랙션 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL 관심 영역 상호 작용] 데이터 형식

[!UICONTROL 관심 영역 상호 작용]은 모바일 장치가 범위 내에 있을 때 ID 정보를 모바일 응용 프로그램에 전달하는 무선 장치를 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/poi-interaction.png){width=400}

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 관심 영역 세부 정보]](./poi-details.md) | 이벤트를 발생시킨 POI에 대한 세부 정보를 설명합니다. |
| `poiEntries` | 오브젝트 | 사용자가 POI를 입력한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`: 측정값의 고유 식별자입니다.</li><li>`value`: 측정값의 수량 값입니다.</li></ul> |
| `poiExits` | 오브젝트 | 사용자가 POI를 종료한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`: 측정값의 고유 식별자입니다.</li><li>`value`: 측정값의 수량 값입니다.</li></ul> |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
