---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: ExperienceEvent EndUserIDs mixin
topic: overview
description: 이 문서에서는 ExperienceEvent EndUserIDs mixin에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# [!UICONTROL ExperienceEvent EndUserIDs] mixin

[!UICONTROL ExperienceEvent EndUserIDs] 는 여러 Adobe 응용 프로그램에서 [[!DNL XDM ExperienceEvent] 개인의 ID 정보를 설명하는 데 사용되는 클래스](../../classes/individual-profile.md)표준 믹스인입니다. 이 혼합은 데이터 인제스트 시 값이 자동으로 업데이트되는 읽기 전용 `endUserIDs` `_experience` 필드가 포함된 루트 레벨 개체를 제공합니다.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `aacustomid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud의 사용자 지정 최종 사용자 ID. |
| `aaid` | [ID](../../data-types/identity.md) | Adobe Analytics Cloud의 최종 사용자 ID. |
| `acid` | [ID](../../data-types/identity.md) | Adobe Campaign의 최종 사용자 ID. |
| `adcloud` | [ID](../../data-types/identity.md) | Adobe Advertising Cloud의 최종 사용자 ID. |
| `emailid` | [ID](../../data-types/identity.md) | 이메일 주소 ID. |
| `mcid` | [ID](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [ID](../../data-types/identity.md) | 전화 번호 ID. |
| `tntid` | [ID](../../data-types/identity.md) | Adobe Target의 최종 사용자 ID. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
