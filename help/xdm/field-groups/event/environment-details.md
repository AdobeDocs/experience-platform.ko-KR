---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;환경;환경 세부 정보;
solution: Experience Platform
title: 환경 세부 정보 스키마 필드 그룹
description: ExperienceEvent 환경 세부 사항 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 2%

---


# [!UICONTROL 환경 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 대한 문서를 참조하십시오.

[!UICONTROL 환경 세부 정보]은(는) 장치 세부 정보, 브라우저 정보, 현지 시간 및 기타 지리적 정보 등 경험 이벤트와 관련된 환경 세부 정보를 캡처하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)의 표준 스키마 필드 그룹입니다.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [장치](../../data-types/device.md) | 일반적으로 쿠키를 통해 세션에서 추적할 수 있는 식별된 디바이스, 애플리케이션 또는 디바이스 브라우저 인스턴스를 설명합니다. |
| `environment` | [환경](../../data-types/environment.md) | 이벤트 관찰 상황에 대한 정보, 특히 네트워크 또는 소프트웨어 버전 등 임시 정보에 대해 자세히 설명합니다. |
| `placeContext` | [컨텍스트 배치](../../data-types/place-context.md) | 이벤트 관찰과 관련된 일시적인 상황을 설명합니다. 예를 들면 날씨, 현지 시간, 교통, 요일, 근무일과 휴일 비교 및 근무 시간 등 로케일별 정보가 포함됩니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
