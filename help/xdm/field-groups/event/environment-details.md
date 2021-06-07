---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;환경;환경 세부 사항;
solution: Experience Platform
title: 환경 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 ExperienceEvent 환경 세부 사항 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---


# [!UICONTROL 환경 ] 세부 정보스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL 환경 ] 세부 사항은  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 장치 세부 사항, 브라우저 정보, 현지 시간 및 기타 지역 정보와 같은 경험 이벤트와 관련된 환경 세부 사항을 캡처하는 데 사용되는 클래스에 대한 표준 스키마 필드 그룹을 나타냅니다.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [장치](../../data-types/device.md) | 일반적으로 쿠키로 세션 간에 추적할 수 있는 식별된 장치, 애플리케이션 또는 장치 브라우저 인스턴스에 대해 설명합니다. |
| `environment` | [환경](../../data-types/environment.md) | 이벤트 관찰의 상황 컨텍스트에 대한 정보, 특히 네트워크 또는 소프트웨어 버전과 같은 임시 정보를 자세히 설명합니다. |
| `placeContext` | [컨텍스트 배치](../../data-types/place-context.md) | 이벤트 관찰과 관련된 임시 상황을 설명합니다. 예를 들면 날씨, 현지 시간, 트래픽, 요일, 작업일과 휴일 및 근무 시간과 같은 로케일 관련 정보가 있습니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
