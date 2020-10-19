---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: ExperienceEvent 환경 세부 정보 혼합
topic: overview
description: 이 문서에서는 ExperienceEvent 환경 세부 사항 혼합에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# [!UICONTROL ExperienceEvent 환경 세부 정보] 혼합

[!UICONTROL ExperienceEvent 환경 세부 사항] 은 장치 세부 사항, 브라우저 정보, 현지 시간 및 기타 지역 정보와 같은 경험 이벤트와 관련된 환경 세부 사항을 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스에 대한 표준 혼합입니다](../../classes/individual-profile.md) .

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [장치](../../data-types/device.md) | 일반적으로 쿠키로 세션 간에 추적할 수 있는 식별된 장치, 응용 프로그램 또는 장치 브라우저 인스턴스에 대해 설명합니다. |
| `environment` | [환경](../../data-types/environment.md) | 특히 네트워크 또는 소프트웨어 버전과 같은 임시 정보를 자세히 설명하는 이벤트 참조의 상황에 대한 정보를 설명합니다. |
| `placeContext` | [컨텍스트 배치](../../data-types/place-context.md) | 이벤트 관찰과 관련된 일시적인 상황을 설명합니다. 예로는 날씨, 현지 시간, 트래픽, 요일, 근무일 및 근무 시간과 같은 로케일별 정보가 있습니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
