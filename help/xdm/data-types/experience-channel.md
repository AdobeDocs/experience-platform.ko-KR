---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 세부 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: Experience Channel 데이터 유형
description: 이 문서에서는 경험 채널 XDM(경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# [!UICONTROL 경험 채널] 데이터 유형

[!UICONTROL 경험 채널] 는 경험 채널을 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 경험 채널은 디지털 경험이 소비되는 방식에 대한 방법 또는 경로를 나타냅니다.

경험 채널에는 여러 가지가 있으며, 각 경험 채널은 콘텐츠 전달 방법, 고객 상호 작용을 관찰하는 방법 및 데이터 수집 방법에 대한 다양한 제약 조건을 갖습니다. 채널 내에서 경험을 특정 위치에 전달할 수 있습니다. 채널에 존재하는 위치와 유형은 채널마다 다릅니다.

![](../images/data-types/experience-channel.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_id` | 문자열 | 채널을 고유하게 식별하는 ID입니다. 각 특정 경험 채널은 상수를 정의합니다 `@id`. |
| `_type` | 문자열 | 속성이 비슷한 채널에 대해 대략적인 분류 레이블을 제공합니다. |
| `contentTypes` | 문자열 배열 | 이 채널이 제공할 수 있는 콘텐츠 유형입니다. |
| `locationTypes` | 문자열 배열 | 해당 채널이 구성하고 콘텐츠를 전달할 수 있는 위치 유형(가상 공간). |
| `mediaAction` | 문자열 | 해당되는 경우 경험 이벤트 미디어 작업에 대해 설명합니다. |
| `mediaType` | 문자열 | 미디어 유형이 유료, 소유 또는 소득인지 설명합니다. |
| `metricTypes` | 문자열 배열 | 이 채널에서 수집할 수 있는 지표. |
| `mode` | 문자열 | 이 채널에서 경험이 제공되는 방식. |
| `typeAtSource` | 문자열 | 채널의 사용자 지정 이름입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
