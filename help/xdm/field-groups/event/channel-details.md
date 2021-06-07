---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 채널 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 채널 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---


# [!UICONTROL 채널 ] 세부 정보스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL 채널 ] 세부 정보는 ID,  [[!DNL XDM ExperienceEvent] 채널 유형, 미디어 유형 및 위치 유형과 같은 채널 정보를 설명하는 데 사용되는 ](../../classes/experienceevent.md) 클래스의 표준 스키마 필드 그룹을 나타냅니다.

![](../../images/field-groups/channel-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `channel` | [경험 채널](../../data-types/experience-channel.md) | 제품 반품, 보증 등록 및 장바구니/주문 프로세스를 설명하는 객체입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.schema.json)
