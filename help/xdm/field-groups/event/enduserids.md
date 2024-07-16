---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;enduserids;최종 사용자;최종 사용자;id;
solution: Experience Platform
title: 최종 사용자 ID 세부 정보 스키마 필드 그룹
description: 최종 사용자 ID 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 14%

---


# [!UICONTROL 최종 사용자 ID 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 대한 문서를 참조하십시오.

[!UICONTROL 최종 사용자 ID 세부 정보]은(는) [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)의 표준 스키마 필드 그룹으로, 여러 Adobe 응용 프로그램에서 개인의 ID 정보를 설명하는 데 사용됩니다. 필드 그룹은 루트 수준 `endUserIDs` 개체를 제공합니다. 이 개체에는 데이터가 수집될 때 값이 자동으로 업데이트되는 읽기 전용 `_experience` 필드가 포함되어 있습니다.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `aacustomid` | [신원](../../data-types/identity.md) | Adobe Analytics Cloud에 대한 사용자 지정 최종 사용자 ID. |
| `aaid` | [신원](../../data-types/identity.md) | Adobe Analytics Cloud의 최종 사용자 ID. |
| `acid` | [신원](../../data-types/identity.md) | Adobe Campaign의 최종 사용자 ID. |
| `adcloud` | [신원](../../data-types/identity.md) | Adobe Advertising Cloud의 최종 사용자 ID. |
| `emailid` | [신원](../../data-types/identity.md) | 이메일 주소 ID. |
| `mcid` | [신원](../../data-types/identity.md) | Adobe Marketing Cloud ID(MCID). MCID는 이제 ECID(Experience Cloud ID)로 알려져 있습니다. |
| `phonenumberid` | [신원](../../data-types/identity.md) | 전화번호 ID. |
| `tntid` | [신원](../../data-types/identity.md) | Adobe Target의 최종 사용자 ID. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
