---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 웹 정보 데이터 유형
description: 이 문서에서는 웹 정보 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL 웹 정보] 데이터 유형

[!UICONTROL 웹 정보] 는 페이지 내 상호 작용과 관련된 웹 페이지, 레퍼러 및/또는 링크를 포함하여 World Wide Web 채널과 관련된 Experience 이벤트를 통해 기록된 정보를 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

![](../images/data-types/web-information.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL 웹 상호 작용]](./web-interaction.md) | 상호 작용에 해당하는 웹 링크 또는 URL에 대한 세부 사항을 설명합니다. |
| `webPageDetails` | [[!UICONTROL 웹 페이지 세부 사항]](./webpage-details.md) | 웹 상호 작용이 발생한 웹 페이지에 대한 세부 사항을 설명합니다. |
| `webReferrer` | [!UICONTROL 오브젝트] | 현재 웹 상호 작용이 기록되기 바로 전에 방문자가 도달한 URL인 웹 상호 작용의 레퍼러를 설명합니다. 다음 하위 속성을 포함합니다. <ul><li>`URL`: 레퍼러 URL입니다.</li><li>`type`: 레퍼러 유형입니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
