---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;필드 디자인;필드 그룹;필드 그룹;최종 사용자;최종 사용자;id;
solution: Experience Platform
title: 최종 사용자 ID 세부 정보 스키마 필드 그룹
description: 이 문서에서는 최종 사용자 ID 세부 사항 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---


# [!UICONTROL 최종 사용자 ID 세부 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 최종 사용자 ID 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)여러 Adobe 애플리케이션에서 개인의 id 정보를 설명하는 데 사용됩니다. 필드 그룹은 루트 수준을 제공합니다 `endUserIDs` 개체(그 자체가 읽기 전용 포함) `_experience` 데이터가 수집될 때 값이 자동으로 업데이트되는 필드입니다.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `aacustomid` | [신원](../../data-types/identity.md) | Adobe Analytics Cloud에 대한 사용자 지정 최종 사용자 ID. |
| `aaid` | [신원](../../data-types/identity.md) | Adobe Analytics Cloud의 최종 사용자 ID입니다. |
| `acid` | [신원](../../data-types/identity.md) | Adobe Campaign의 최종 사용자 ID입니다. |
| `adcloud` | [신원](../../data-types/identity.md) | Adobe Advertising Cloud의 최종 사용자 ID입니다. |
| `emailid` | [신원](../../data-types/identity.md) | 이메일 주소 ID. |
| `mcid` | [신원](../../data-types/identity.md) | Adobe Marketing Cloud ID(MCID). 이제 MCID를 ECID(Experience Cloud ID)라고 합니다. |
| `phonenumberid` | [신원](../../data-types/identity.md) | 전화 번호 ID. |
| `tntid` | [신원](../../data-types/identity.md) | Adobe Target의 최종 사용자 ID입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
