---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 캠페인 마케팅 세부 사항 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 캠페인 마케팅 세부 사항 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# [!UICONTROL Campaign Marketing ] Details스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL 캠페인 마케팅 ] 세부 사항은 캠페인 그룹, 이름 및 추적 코드와 같은 마케팅 캠페인 정보를 설명하는 데 사용되는  [[!DNL XDM ExperienceEvent] 클래스 ](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/campaign-marketing-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `marketing` | [마케팅](../../data-types/marketing.md) | 캠페인 그룹, 이름 및 추적 코드와 같은 마케팅 캠페인 정보를 설명하는 개체입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.schema.json)
