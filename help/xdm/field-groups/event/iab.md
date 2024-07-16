---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;ExperienceEvent;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;iab;tcf;동의;
solution: Experience Platform
title: 이벤트 스키마에 대한 IAB TCF 2.0 동의 필드 그룹
description: XDM ExperienceEvent 클래스에 대한 IAB TCF 2.0 동의 스키마 필드 그룹에 대해 알아봅니다.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# 이벤트 스키마에 대한 [!UICONTROL IAB TCF 2.0 동의] 필드 그룹

>[!IMPORTANT]
>
>이 문서에서는 XDM ExperienceEvent 클래스의 [!UICONTROL IAB TCF 2.0 동의] 스키마 필드 그룹에 대해 설명합니다. 이 필드 그룹은 시간이 지남에 따라 동의 변경 이벤트를 추적하려는 경우에만 사용해야 합니다.
>
>이벤트 데이터에 기록된 동의 값은 자동 시행 워크플로우에서 적용되지 않습니다. 자동 시행을 수행하려면 동의 값을 XDM 개인 프로필 클래스에 수집하고 실시간 고객 프로필에 대해 활성화해야 합니다.
>
>XDM 개별 프로필 클래스를 위한 필드 그룹의 경우 대신 다음 [문서](../profile/iab.md)를 참조하십시오.

[!UICONTROL IAB TCF 2.0 동의]은(는) 타임스탬프가 지정된 시리즈 IAB 동의 문자열을 캡처하여 시간에 따른 동의 변경 패턴을 추적하는 데 사용되는 [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/iab-event.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `consentStrings` | [동의 문자열](../../data-types/consent-string.md) 배열 | 이벤트와 연결된 동의 문자열 값의 배열입니다. |

{style="table-layout:auto"}

이 필드 그룹의 사용 사례에 대한 자세한 내용은 ](../../../landing/governance-privacy-security/consent/iab/overview.md) 플랫폼의 [IAB TCF 2.0 지원 가이드를 참조하십시오. 필드 그룹 자체에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
