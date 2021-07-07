---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;필드 디자인;필드 그룹;필드 그룹;최종 사용자;최종 사용자;id;
solution: Experience Platform
title: 최종 사용자 ID 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 최종 사용자 ID 세부 사항 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL 최종 사용자 ID 세부 ] 정보스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL 최종 사용자 ID ] 여러 Adobe 애플리케이션에서 개인의 ID 정보를 설명하는 데 사용되는  [[!DNL XDM ExperienceEvent] 클래스 ](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹을 자세히 설명합니다. 필드 그룹은 루트 수준 `endUserIDs` 개체를 제공하며, 이 개체는 데이터가 수집될 때 값이 자동으로 업데이트되는 읽기 전용 `_experience` 필드를 포함합니다.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `aacustomid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud에 대한 사용자 지정 최종 사용자 ID. |
| `aaid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud의 최종 사용자 ID입니다. |
| `acid` | [ID](../../data-types/identity.md) | Adobe Campaign의 최종 사용자 ID입니다. |
| `adcloud` | [ID](../../data-types/identity.md) | Adobe Advertising Cloud의 최종 사용자 ID입니다. |
| `emailid` | [ID](../../data-types/identity.md) | 이메일 주소 ID. |
| `mcid` | [ID](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [ID](../../data-types/identity.md) | 전화 번호 ID. |
| `tntid` | [ID](../../data-types/identity.md) | Adobe Target의 최종 사용자 ID입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
