---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 세부 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 웹 정보 데이터 유형
description: 웹 정보 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL 웹 정보] 데이터 형식

[!UICONTROL 웹 정보]는 웹 페이지, 레퍼러 및/또는 페이지 내 상호 작용과 관련된 링크를 포함하여 World Wide Web 채널에 해당하는 Experience Event를 통해 기록된 정보를 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다.

![](../images/data-types/web-information.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL 웹 인터랙션]](./web-interaction.md) | 인터랙션에 해당하는 웹 링크 또는 URL에 대한 세부 정보를 설명합니다. |
| `webPageDetails` | [[!UICONTROL 웹 페이지 세부 정보]](./webpage-details.md) | 웹 인터랙션이 발생한 웹 페이지에 대한 세부 정보를 설명합니다. |
| `webReferrer` | [!UICONTROL 개체] | 웹 인터랙션의 레퍼러(현재 웹 인터랙션이 기록되기 바로 전에 방문자가 들어온 URL)에 대해 설명합니다. 다음 하위 속성을 포함합니다. <ul><li>`URL`: 레퍼러 URL.</li><li>`type`: 레퍼러 유형입니다.</li></ul> |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
