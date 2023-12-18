---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 채널 세부 정보 스키마 필드 그룹
description: 채널 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# [!UICONTROL 채널 세부 사항] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 다음에 대한 문서 보기: [필드 그룹 이름 업데이트](../name-updates.md) 추가 정보.

[!UICONTROL 채널 세부 사항] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)ID, 채널 유형, 미디어 유형 및 위치 유형 등 채널 정보를 설명하는 데 사용됩니다.

![](../../images/field-groups/channel-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `channel` | [경험 채널](../../data-types/experience-channel.md) | 제품 반품, 보증 등록 및 장바구니/주문 프로세스를 설명하는 객체입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
