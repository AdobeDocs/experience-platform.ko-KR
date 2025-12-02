---
title: setConsent
description: 각 페이지에서 사용자의 동의 환경 설정을 추적하는 데 사용됩니다.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 3%

---


# `setConsent`

`setConsent` 명령은 웹 SDK에 데이터를 보내야 하는지(옵트인), 데이터를 버려야 하는지(옵트아웃), [`defaultConsent`](configure/defaultconsent.md)을(를) 사용해야 하는지(동의 알 수 없음) 알려줍니다.

웹 SDK은 다음 표준을 지원합니다.

* **[Adobe 표준](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: 1.0 및 2.0 표준이 모두 지원됩니다.
* **[IAB 투명도 및 동의 프레임워크](/help/landing/governance-privacy-security/consent/iab/overview.md)**: 이 표준을 사용하는 경우, 구현이 올바르게 구성된 경우 방문자의 실시간 고객 프로필이 동의 정보로 업데이트됩니다.
   1. XDM 개인 프로필 스키마에 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/profile/iab.md)이(가) 포함되어 있습니다.
   1. 경험 이벤트 스키마에 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/event/iab.md)이(가) 있습니다.
   1. 이벤트 [XDM 개체](sendevent/xdm.md)에 IAB 동의 정보를 포함합니다. 웹 SDK은 이벤트 데이터를 전송할 때 동의 정보를 자동으로 포함하지 않습니다.

이 명령을 사용하면 웹 SDK은 쿠키에 사용자의 환경 설정을 기록합니다. 다음에 사용자가 브라우저에 웹 사이트를 로드할 때 SDK은 이러한 지속적인 환경 설정을 검색하여 이벤트를 Adobe에 보낼 수 있는지 확인합니다.

Adobe은 모든 동의 대화 상자 환경 설정을 Web SDK 동의와 별도로 저장할 것을 권장합니다. 웹 SDK은 동의를 검색하는 방법을 제공하지 않습니다. 사용자 환경 설정이 SDK과 계속 동기화되도록 하려면 페이지를 로드할 때마다 `setConsent` 명령을 호출할 수 있습니다. 웹 SDK은 동의를 변경할 때만 서버 호출을 수행합니다.

## ID 동기화 고려 사항 {#identity-considerations}

`setConsent` 명령은 장치 수준에서 작동하므로 ID 맵의 `ECID`만 사용합니다. `setConsent` 명령에서는 ID 맵의 다른 ID를 고려하지 않습니다.

## `defaultConsent`과(와) 함께 `setConsent` 사용 {#using-consent}

웹 SDK은 두 개의 상호 보완적인 동의 구성 명령을 제공합니다.

* [`defaultConsent`](configure/defaultconsent.md): 이 명령은 Web SDK을 사용하는 Adobe 고객의 동의 환경 설정을 캡처하기 위한 것입니다.
* [`setConsent`](setconsent.md): 이 명령은 사이트 방문자의 동의 환경 설정을 캡처하기 위한 것입니다.

이러한 설정을 함께 사용하면 구성된 값에 따라 데이터 수집 및 쿠키 설정 결과가 달라질 수 있습니다.

동의 설정을 기반으로 데이터 수집이 발생하는 시점과 쿠키가 설정되는 시점을 이해하려면 아래 표를 참조하십시오.

| `defaultConsent` | `setConsent` | 데이터 수집 발생 | 웹 SDK 브라우저 쿠키 설정 |
|---------|----------|---------|---------|
| `in` | `in` | 예 | 예 |
| `in` | `out` | 아니요 | 예 |
| `in` | 설정되지 않음 | 예 | 예 |
| `pending` | `in` | 예 | 예 |
| `pending` | `out` | 아니요 | 예 |
| `pending` | 설정되지 않음 | 아니요 | 아니요 |
| `out` | `in` | 예 | 예 |
| `out` | `out` | 아니요 | 예 |
| `out` | 설정되지 않음 | 아니요 | 아니요 |

다음 쿠키는 동의 구성이 허용하면 설정됩니다.

| 이름 | 최대 나이 | 설명 |
|---|---|---|
| **`AMCV_###@AdobeOrg`** | 34128000(395일) | [`idMigrationEnabled`](configure/idmigrationenabled.md)이(가) 활성화된 경우 표시됩니다. 사이트의 일부 부분이 여전히 `visitor.js`을(를) 사용하고 있는 동안 Web SDK으로 전환할 때 도움이 됩니다. |
| **`Demdex cookie`** | 15552000(180일) | ID 동기화가 활성화된 경우 표시됩니다. Audience Manager은 이 쿠키를 설정하여 사이트 방문자에게 고유 ID를 할당합니다. demdex 쿠키는 Audience Manger 가 방문자 식별, ID 동기화, 세그먼테이션, 모델링, 보고 등과 같은 기본 기능을 수행하는 데 도움이 됩니다. |
| **`kndctr_orgid_cluster`** | 1800(30분) | 현재 사용자의 요청을 처리하는 Edge Network 영역을 저장합니다. Edge Network이 요청을 올바른 영역으로 라우팅할 수 있도록 이 영역은 URL 경로에 사용됩니다. 사용자가 다른 IP 주소 또는 다른 세션에 연결하는 경우 요청이 다시 가장 가까운 영역으로 라우팅됩니다. |
| **`kndct_orgid_identity`** | 34128000(395일) | ECID 및 ECID와 관련된 기타 정보를 저장합니다. |
| **`kndctr_orgid_consent`** | 15552000(180일) | 웹 사이트에 대한 사용자 동의 환경 설정을 저장합니다. |
| **`s_ecid`** | 63115200(2년) | Experience Cloud ID([!DNL ECID]) 또는 MID의 복사본을 포함합니다. MID는 `s_ecid=MCMID\|<ECID>` 구문 뒤에 오는 키-값 쌍에 저장됩니다. |

웹 SDK의 구성된 인스턴스를 호출할 때 `setConsent` 명령을 실행합니다. 이 명령에 다음 개체를 포함할 수 있습니다.

* **`consent[]`**: `consent` 개체의 배열입니다. 동의 개체는 선택하는 표준 및 버전에 따라 다른 형식으로 지정됩니다. 동의 표준에 따라 각 동의 오브젝트의 예는 아래 탭을 참조하십시오.
* **`identityMap`**: ECID 생성 방법과 연결된 ID 동의 정보를 제어하는 개체입니다. Adobe에서는 `setConsent`과 같은 다른 명령보다 먼저 [`sendEvent`](sendevent/overview.md)을(를) 실행할 때 이 개체를 포함할 것을 권장합니다.
* **`edgeConfigOverrides`**: [데이터스트림 구성 재정의](configure/edgeconfigoverrides.md)를 포함하는 개체입니다.

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 standard `consent` 개체

Adobe Experience Platform으로 데이터를 전송하는 경우 프로필 스키마에 개인 정보 스키마 필드 그룹을 포함하게 됩니다. Adobe 2.0 표준에 대한 자세한 내용은 [Adobe Experience Platform의 거버넌스, 개인 정보 및 보안](/help/landing/governance-privacy-security/overview.md)을 참조하십시오. `consents` 프로필 필드 그룹의 [!UICONTROL Consents and Preferences] 필드 스키마에 해당하는 아래 값 개체 내에 데이터를 추가할 수 있습니다.

* **`standard`**: 선택한 동의 표준입니다. Adobe 2.0 표준에 대해 이 속성을 `"Adobe"`(으)로 설정합니다.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. Adobe 2.0 표준에 대해 이 속성을 `"2.0"`(으)로 설정합니다.
* **`value`**: 동의 값이 포함된 개체입니다.
   * **`value.collect.val`**: 동의 값입니다. 사용자가 옵트인할 때는 `"y"`(으)로 설정하고 사용자가 옵트아웃할 때는 `"n"`(으)로 설정합니다.
   * **`value.metadata.time`**: 사용자가 동의 설정을 마지막으로 업데이트한 타임스탬프.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0 표준 `consent` 개체

IAB(Interactive Advertising Bureau Europe) TCF(Transparency and Consent Framework) 표준을 통해 제공된 사용자 동의 환경 설정을 기록하려면 아래와 같이 동의 문자열을 설정합니다.

이렇게 동의를 설정하면 실시간 고객 프로필이 동의 정보로 업데이트됩니다. 이를 수행하려면 프로필 XDM 스키마에 [프로필 개인 정보 보호 스키마 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)이 있어야 합니다. 이벤트를 보낼 때 IAB 동의 정보를 이벤트 XDM 개체에 수동으로 추가해야 합니다. 웹 SDK은 이벤트에 동의 정보를 자동으로 포함하지 않습니다.

이벤트에서 동의 정보를 보내려면 [!DNL Profile] 사용 [!DNL XDM ExperienceEvent] 스키마에 경험 이벤트 개인 정보 보호 필드 그룹을 추가해야 합니다. 구성 방법에 대한 단계는 데이터 집합 준비 안내서의 [ExperienceEvent 스키마 업데이트](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema)에 대한 섹션을 참조하십시오.

* **`standard`**: 선택한 동의 표준입니다. IAB TCF 2.0 표준에 대해 이 속성을 `"IAB TCF"`(으)로 설정합니다.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. IAB TCF 2.0 표준에 대해 이 속성을 `"2.0"`(으)로 설정합니다.
* **`value`**: 동의 값이 포함된 문자열입니다.
* **`gdprApplies`**: GDPR이 이 동의 값에 적용되는지 여부를 결정하는 부울입니다. 기본값은 `true`입니다.
* **`gdprContainsPersonalData`**: 이 사용자와 연결된 이벤트 데이터에 개인 데이터가 포함되어 있는지 여부를 결정하는 부울입니다. 기본값은 `false`입니다.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

IAB TCF 2.0 API는 고객이 동의를 업데이트할 때에 대한 이벤트를 제공합니다. 이 문제는 고객이 처음에 환경 설정을 지정하고 고객이 환경 설정을 업데이트할 때 발생합니다. 이벤트 수신기를 추가하여 `setConsent` 명령을 실행할 수 있습니다.

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

위의 코드 블록은 `useractioncomplete` 이벤트를 수신한 다음 동의를 설정하여 동의 문자열과 `gdprApplies` 플래그를 전달합니다. 고객에 대한 사용자 지정 ID가 있는 경우 `identityMap` 변수를 채우십시오.

>[!TAB Adobe 1.0]

### Adobe 1.0 standard `consent` 개체

* **`standard`**: 선택한 동의 표준입니다. Adobe 1.0 표준에 대해 이 속성을 `"Adobe"`(으)로 설정합니다.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. Adobe 1.0 표준에 대해 이 속성을 `"1.0"`(으)로 설정합니다.
* **`value.general`**: 동의 값입니다. 사용자가 옵트인할 때는 `"in"`(으)로 설정하고 사용자가 옵트아웃할 때는 `"out"`(으)로 설정합니다.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### 한 번의 요청으로 여러 표준 보내기 {#multiple-standards}

웹 SDK은 아래 예와 같이, 요청에 두 개 이상의 동의 개체 전송을 지원합니다.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## 동의 환경 설정 지속성 {#persistence}

`setConsent` 명령을 사용하여 사용자 환경 설정을 웹 SDK에 전달하면 SDK에서 사용자 환경 설정을 쿠키에 유지합니다. 다음 번에 사용자가 브라우저에 웹 사이트를 로드하면 웹 SDK에서 이 지속 환경 설정을 검색하여 사용하여 이벤트를 Adobe에 보낼 수 있는지 여부를 결정합니다.

현재 환경 설정으로 동의 대화 상자를 표시할 수 있도록 사용자의 환경 설정을 개별적으로 저장합니다. 웹 SDK에서 사용자 환경 설정을 검색할 방법은 없습니다. 사용자 환경 설정이 SDK과 계속 동기화되도록 하려면 페이지를 로드할 때마다 `setConsent` 명령을 호출할 수 있습니다. 웹 SDK은 기본 설정이 변경되는 경우에만 서버를 호출합니다.

## 웹 SDK 태그 확장을 사용하여 동의 설정

이 명령에 해당하는 웹 SDK 태그 확장은 [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md) 작업입니다.
