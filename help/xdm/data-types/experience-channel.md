---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 경험 채널 데이터 유형
description: 이 문서에서는 XDM(Experience Channel Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# [!UICONTROL 경험 채널] 데이터 유형

[!UICONTROL 경험 채널] 는 경험 채널을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 경험 채널은 디지털 경험이 사용되는 방법을 나타냅니다.

컨텐츠 전달 방법, 고객 상호 작용 준수 방법 및 데이터 수집 방법에 대한 서로 다른 제한 사항이 있는 여러 경험 채널이 있습니다. 채널 내에서 경험은 특정 위치에 전달될 수 있습니다. 채널에 있는 위치의 위치 및 유형은 채널마다 다릅니다.

![](../images/data-types/experience-channel.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | 문자열 | 채널을 고유하게 식별하는 ID입니다. 각 특정 경험 채널은 상수를 정의합니다 `@id`. |
| `_type` | 문자열 | 비슷한 속성을 갖는 채널에 대해 대략적인 분류 레이블을 제공합니다. |
| `contentTypes` | 문자열 배열 | 이 채널이 전달할 수 있는 컨텐츠 유형입니다. |
| `locationTypes` | 문자열 배열 | 이 채널이 구성되며 컨텐츠를 제공할 수 있는 위치 유형(가상 위치)입니다. |
| `mediaAction` | 문자열 | 해당되는 경우 Experience Event 미디어 작업에 대해 설명합니다. |
| `mediaType` | 문자열 | 미디어 유형이 유료, 소유 또는 획득되는지 여부를 설명합니다. |
| `metricTypes` | 문자열 배열 | 이 채널에서 수집할 수 있는 지표입니다. |
| `mode` | 문자열 | 이 채널에서 경험을 전달하는 방법. |
| `typeAtSource` | 문자열 | 채널의 사용자 지정 이름입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
