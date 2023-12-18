---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;poi;상호 작용;관심 영역;관심 영역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 관심 영역 인터랙션 데이터 유형
description: 관심 영역 인터랙션 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL 관심 영역 인터랙션] 데이터 유형

[!UICONTROL 관심 영역 인터랙션] 는 모바일 장치가 범위 내에 있을 때 모바일 애플리케이션에 ID 정보를 전달하는 무선 장치를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 관심 영역 세부 정보]](./poi-details.md) | 이벤트를 발생시킨 POI에 대한 세부 정보를 설명합니다. |
| `poiEntries` | 오브젝트 | 사용자가 POI를 입력한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`: 측정값에 대한 고유 식별자.</li><li>`value`: 측정값의 수량 값입니다.</li></ul> |
| `poiExits` | 오브젝트 | 사용자가 POI를 종료한 횟수를 설명합니다. 다음 두 가지 속성을 포함합니다. <ul><li>`id`: 측정값에 대한 고유 식별자.</li><li>`value`: 측정값의 수량 값입니다.</li></ul> |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
