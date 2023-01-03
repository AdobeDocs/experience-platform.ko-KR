---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;경험 이벤트;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;iab;tcf;동의;
solution: Experience Platform
title: 이벤트 스키마에 대한 IAB TCF 2.0 동의 필드 그룹
topic-legacy: overview
description: 이 문서에서는 XDM ExperienceEvent 클래스에 대한 IAB TCF 2.0 동의 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0 동의] 이벤트 스키마에 대한 필드 그룹

>[!IMPORTANT]
>
>이 문서에서는 [!UICONTROL IAB TCF 2.0 동의] xdm ExperienceEvent 클래스의 스키마 필드 그룹입니다. 이 필드 그룹은 시간에 따른 동의 변경 이벤트를 추적하려는 경우에만 사용해야 합니다.
>
>이벤트 데이터에 기록된 동의 값은 자동 적용 워크플로우에서 적용되지 않습니다. 자동 적용을 수행하려면 동의 값을 XDM 개별 프로필 클래스에 수집하여 실시간 고객 프로필에 대해 활성화해야 합니다.
>
>XDM 개별 프로필 클래스에 대한 필드 그룹에 대해서는 다음을 참조하십시오 [문서](../profile/iab.md) 을 가리키도록 업데이트하는 것이 좋습니다.

[!UICONTROL IAB TCF 2.0 동의] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md) 시간에 따른 동의 변경 패턴을 추적하기 위해 타임스탬프가 지정된 시리즈 IAB 동의 문자열을 캡처하는 데 사용됩니다.

![](../../images/field-groups/iab-event.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `consentStrings` | 배열 [동의 문자열](../../data-types/consent-string.md) | 이벤트와 연관된 동의 문자열 값의 배열입니다. |

{style=&quot;table-layout:auto&quot;}

다음 안내서를 참조하십시오. [플랫폼에서 IAB TCF 2.0 지원](../../../landing/governance-privacy-security/consent/iab/overview.md) 을 참조하십시오. 필드 그룹 자체에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
