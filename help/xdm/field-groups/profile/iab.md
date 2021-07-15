---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;스키마 디자인;필드 그룹;필드 그룹;iab;tcf;동의;
solution: Experience Platform
title: IAB TCF 2.0 동의 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 IAB TCF 2.0 동의 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---


# [!UICONTROL IAB TCF 2.0 ] 동의 스키마 필드 그룹

>[!NOTE]
>
>이 문서에서는 XDM 개별 프로필 클래스에 대한 [!UICONTROL IAB TCF 2.0 동의] 스키마 필드 그룹을 다룹니다. XDM ExperienceEvent 클래스에 대한 필드 그룹의 경우 다음 [document](../event/iab.md) 를 대신 참조하십시오.

[!UICONTROL IAB TCF 2.0] 은 시간에 따른 동의 변경 패턴을 추적하기 위해 타임스탬프가 지정된  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 시리즈 IAB 동의 문자열을 캡처하는 데 사용되는 클래스에 대한 표준 스키마 필드 그룹을 나타냅니다.

![](../../images/field-groups/iab-profile.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `identityPrivacyInfo` | 맵 | 고객의 개별 ID 값을 다른 TCF 동의 문자열로 연결하는 맵 유형 개체입니다. 이 개체의 구조에 대한 예는 아래에 나와 있습니다. |

{style=&quot;table-layout:auto&quot;}

다음 JSON에서는 `identityPrivacyInfo` 맵의 구조를 보여 줍니다.

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

예제에서 알 수 있듯이 `xdm:identityPrivacyInfo`의 각 루트 수준 키는 Identity 서비스에서 인식하는 ID 네임스페이스에 해당합니다. 따라서 각 네임스페이스 속성에는 키가 해당 네임스페이스에 대한 고객의 해당 ID 값과 일치하는 하나 이상의 하위 속성이 있어야 합니다. 이 예에서 고객은 `13782522493631189`의 Experience Cloud ID(`ECID`) 값으로 식별됩니다.

>[!NOTE]
>
>위의 예에서는 단일 네임스페이스/값 쌍을 사용하여 고객 ID를 나타내지만 다른 네임스페이스에 추가 키를 추가할 수 있으며 각 네임스페이스에는 각각 고유한 TCF 동의 환경 설정 세트가 있는 여러 ID 값이 있을 수 있습니다.

각 ID 값에 대해 ID에 대한 TCF 동의 값을 제공하는 `identityIABConsent` 속성을 제공해야 합니다. 이 속성의 값은 [[!UICONTROL 동의 문자열] 데이터 형식](../../data-types/consent-string.md)을 준수해야 합니다.

이 필드 그룹의 사용 사례에 대한 자세한 내용은 Platform](../../../landing/governance-privacy-security/consent/iab/overview.md)의 [IAB TCF 2.0 지원에 대한 안내서를 참조하십시오. 필드 그룹 자체에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
