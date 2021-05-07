---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마;필드 디자인;필드 그룹;최종 사용자;id;end-user;ids
solution: Experience Platform
title: 최종 사용자 ID 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 최종 사용자 ID 세부 정보 스키마 필드 그룹의 개요를 제공합니다.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)의 문서를 참조하십시오.

[!UICONTROL End User ID Details] 는 여러 Adobe 응용 프로그램에서  [[!DNL XDM ExperienceEvent] 개인](../../classes/individual-profile.md) ID 정보를 설명하는 데 사용되는 클래스의 표준 스키마 필드 그룹입니다. 필드 그룹은 루트 레벨 `endUserIDs` 객체를 제공하며 이 객체에는 데이터가 인제스트될 때 값이 자동으로 업데이트되는 읽기 전용 `_experience` 필드가 포함됩니다.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `aacustomid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud에 대한 사용자 지정 최종 사용자 ID. |
| `aaid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud의 최종 사용자 ID. |
| `acid` | [ID](../../data-types/identity.md) | Adobe Campaign의 최종 사용자 ID. |
| `adcloud` | [ID](../../data-types/identity.md) | Adobe Advertising Cloud의 최종 사용자 ID. |
| `emailid` | [ID](../../data-types/identity.md) | 이메일 주소 ID. |
| `mcid` | [ID](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [ID](../../data-types/identity.md) | 전화 번호 ID. |
| `tntid` | [ID](../../data-types/identity.md) | Adobe Target의 최종 사용자 ID. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
