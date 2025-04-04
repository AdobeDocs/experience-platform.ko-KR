---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;iab;tcf;동의;
solution: Experience Platform
title: 프로필 스키마에 대한 IAB TCF 2.0 동의 필드 그룹
description: XDM 개인 프로필 클래스에 대한 IAB TCF 2.0 동의 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# 프로필 스키마에 대한 [!UICONTROL IAB TCF 2.0 동의] 필드 그룹

>[!NOTE]
>
>이 문서에서는 XDM 개별 프로필 클래스에 대한 [!UICONTROL IAB TCF 2.0 동의] 스키마 필드 그룹을 다룹니다. XDM ExperienceEvent 클래스의 필드 그룹은 대신 다음 [문서](../event/iab.md)을(를) 참조하십시오.

[!UICONTROL IAB TCF 2.0 동의]은(는) 타임스탬프가 지정된 시리즈 IAB 동의 문자열을 캡처하여 시간에 따른 동의 변경 패턴을 추적하는 데 사용되는 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)에 대한 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/iab-profile.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `identityPrivacyInfo` | 맵 | 고객의 개별 ID 값을 다른 TCF 동의 문자열과 연결하는 맵 유형 개체입니다. 이 객체의 구조에 대한 예가 아래에 나와 있습니다. |

{style="table-layout:auto"}

다음 JSON은 `identityPrivacyInfo` 맵의 구조를 보여 줍니다.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

예제에서 볼 수 있듯이 `xdm:identityPrivacyInfo`의 각 루트 수준 키는 Identity Service에서 인식하는 ID 네임스페이스에 해당합니다. 또한 각 네임스페이스 속성에는 키가 해당 네임스페이스에 대한 고객의 해당 ID 값과 일치하는 하위 속성이 하나 이상 있어야 합니다. 이 예에서 고객은 `13782522493631189`의 Experience Cloud ID(`ECID`) 값으로 식별됩니다.

>[!NOTE]
>
>위의 예에서는 단일 네임스페이스/값 쌍을 사용하여 고객의 ID를 나타내지만 다른 네임스페이스에 대해 키를 추가할 수 있으며 각 네임스페이스에는 여러 개의 ID 값이 있을 수 있으며 각 ID 값에는 고유한 TCF 동의 환경 설정이 있습니다.

각 ID 값에 대해 ID에 대한 TCF 동의 값을 제공하는 `identityIABConsent` 속성을 제공해야 합니다. 이 속성의 값은 [[!UICONTROL 동의 문자열] 데이터 형식](../../data-types/consent-string.md)을 준수해야 합니다.

이 필드 그룹의 사용 사례에 대한 자세한 내용은 Experience Platform의 [IAB TCF 2.0 지원](../../../landing/governance-privacy-security/consent/iab/overview.md)에 대한 안내서를 참조하십시오. 필드 그룹 자체에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
