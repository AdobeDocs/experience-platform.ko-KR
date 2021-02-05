---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;포이;상호 작용;관심 영역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 관심 영역 상호 작용 데이터 유형
topic: overview
description: 이 문서에서는 관심 영역 상호 작용 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---


# [!UICONTROL 관심 영역 ] 상호 작용 데이터 유형

[!UICONTROL 관심 영역 ] 상호 작용은 모바일 장치가 범위 내에 있는 모바일 응용 프로그램에 ID 정보를 전달하는 무선 장치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 관심 영역 세부 사항]](./poi-details.md) | 이벤트를 발생시킨 POI의 세부 사항을 설명합니다. |
| `poiEntries` | 개체 | POI에 입력한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`:측정값에 대한 고유 식별자입니다.</li><li>`value`:측정값의 수량화 가능 값입니다.</li></ul> |
| `poiExits` | 개체 | 사람이 POI를 종료한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`:측정값에 대한 고유 식별자입니다.</li><li>`value`:측정값의 수량화 가능 값입니다.</li></ul> |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
