---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 상호 작용;데이터 유형;데이터 유형;
solution: Experience Platform
title: 웹 인터랙션 데이터 유형
description: 이 문서에서는 웹 인터랙션 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# [!UICONTROL 웹 인터랙션] 데이터 유형

[!UICONTROL 웹 인터랙션] 는 초기 페이지 로드가 완료된 후 웹 페이지에서 발생한 상호 작용에 대한 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 단일 페이지 웹 앱(SPA)과 같이 새 페이지 로드를 트리거하지 않는 리치 웹 애플리케이션에서 상호 작용을 기록하기 위한 것입니다.

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 측정]](./measure.md) | 웹 링크의 클릭을 추적하는 측정입니다. |
| `URL` | 문자열 | 해당 웹 인터랙션에 사용되는 실제 링크 또는 URL. |
| `name` | 문자열 | 이 웹 링크에 사용되는 표준 이름. 분류 목적으로 사용됩니다. |
| `type` | 문자열 | 링크 유형. 이 속성은 다음 열거형 값 중 하나와 같아야 합니다. <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
