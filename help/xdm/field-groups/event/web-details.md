---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 웹 세부 정보 스키마 필드 그룹
description: 이 문서에서는 웹 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---

# [!UICONTROL 웹 세부 사항] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 웹 세부 사항] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)상호 작용, 페이지 세부 사항 및 레퍼러와 같은 웹 세부 사항 이벤트에 대한 정보를 설명하는 데 사용됩니다.

![](../../images/field-groups/web-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `web` | [웹 정보](../../data-types/web-information.md) | 링크 클릭 수, 웹 페이지 세부 사항, 레퍼러 정보 및 브라우저 세부 사항을 설명합니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
