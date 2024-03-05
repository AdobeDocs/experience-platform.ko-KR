---
title: setConsent
description: 각 페이지에서 사용자의 동의를 추적하는 데 사용됩니다.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

다음 `setConsent` 명령은 웹 SDK에 데이터를 전송하거나(옵트인), 데이터를 삭제하거나(옵트아웃), [`defaultConsent`](configure/defaultconsent.md) (동의 알 수 없음).

웹 SDK는 다음 표준을 지원합니다.

* **[Adobe 표준](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: 1.0 및 2.0 표준이 모두 지원됩니다.
* **[IAB 투명성 및 동의 프레임워크](/help/landing/governance-privacy-security/consent/iab/overview.md)**: 이 표준을 사용하는 경우, 구현이 올바르게 구성된 경우 방문자의 실시간 고객 프로필이 동의 정보로 업데이트됩니다.
   1. XDM 개인 프로필 스키마에는 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/profile/iab.md).
   1. 경험 이벤트 스키마에는 [IAB TCF 2.0 동의 필드 그룹](/help/xdm/field-groups/event/iab.md).
   1. 이벤트에 IAB 동의 정보를 포함합니다 [XDM 개체](sendevent/xdm.md). 웹 SDK는 이벤트 데이터를 전송할 때 동의 정보를 자동으로 포함하지 않습니다.

이 명령을 사용하면 Web SDK는 쿠키에 사용자의 환경 설정을 기록합니다. 다음에 사용자가 브라우저에 웹 사이트를 로드할 때 SDK는 이러한 지속적인 환경 설정을 검색하여 Adobe에게 이벤트를 보낼 수 있는지 확인합니다.

Adobe은 모든 동의 대화 상자 환경 설정을 웹 SDK 동의와 별도로 저장할 것을 권장합니다. 웹 SDK는 동의를 검색하는 방법을 제공하지 않습니다. 사용자 환경 설정이 SDK와 계속 동기화되도록 하려면 다음을 호출할 수 있습니다. `setConsent` 페이지를 로드할 때마다 명령을 실행합니다. Web SDK는 동의를 변경할 때만 서버 호출을 수행합니다.

## 웹 SDK 태그 확장을 사용하여 동의 설정

동의 설정은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 동의 설정]**.
1. 다음을 포함하여 오른쪽에서 원하는 필드를 설정합니다. **[!UICONTROL 표준]** 및 **[!UICONTROL 일반 동의]**.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

이 작업 내에 여러 동의 개체를 포함할 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 동의 설정

실행 `setConsent` 명령을 사용하여 웹 SDK의 구성된 인스턴스를 호출할 수 있습니다. 이 명령에 다음 개체를 포함할 수 있습니다.

* **`consent[]`**: 의 배열 `consent` 개체. 동의 개체는 선택하는 표준 및 버전에 따라 다른 형식으로 지정됩니다.
* **`identityMap`**: ECID 생성 방법과 어떤 ID 동의 정보가 연결되어 있는지 제어하는 개체입니다. Adobe 다음과 같은 경우 이 개체를 포함하는 것이 좋습니다. `setConsent` 은 과 같은 다른 명령보다 먼저 실행됩니다. [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: 다음을 포함하는 오브젝트 [데이터 스트림 구성 무시](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 표준 `consent` 오브젝트

* **`standard`**: 사용자가 선택하는 동의 표준입니다. 이 속성을 다음으로 설정 `"Adobe"` Adobe 2.0 표준용.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. 이 속성을 다음으로 설정 `"2.0"` Adobe 2.0 표준용.
* **`value`**: 동의 값을 포함하는 객체입니다.
   * **`value.collect.val`**: 동의 값입니다. 유효한 값은 다음과 같습니다. `"y"` (옵트인) 및 `"n"` (옵트아웃).
   * **`value.metadata.time`**: 사용자가 동의 값을 설정하는 타임스탬프입니다.

```js
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

### IAB TCF 2.0 표준 `consent` 오브젝트

* **`standard`**: 사용자가 선택하는 동의 표준입니다. 이 속성을 다음으로 설정 `"IAB TCF"` IAB TCF 2.0 표준의 경우.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. 이 속성을 다음으로 설정 `"2.0"` IAB TCF 2.0 표준의 경우.
* **`value`**: 동의 값을 포함하는 문자열.
* **`gdprApplies`**: GDPR이 이 동의 값에 적용되는지 여부를 결정하는 부울입니다. 기본값은 `true`입니다.
* **`gdprContainsPersonalData`**: 이 사용자와 연결된 이벤트 데이터에 개인 데이터가 포함되어 있는지 여부를 결정하는 부울입니다. 기본값은 `false`입니다.

```js
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

>[!TAB Adobe 1.0]

### Adobe 1.0 표준 `consent` 오브젝트

* **`standard`**: 사용자가 선택하는 동의 표준입니다. 이 속성을 다음으로 설정 `"Adobe"` Adobe 1.0 표준용.
* **`version`**: 동의 표준의 버전을 나타내는 문자열입니다. 이 속성을 다음으로 설정 `"1.0"` Adobe 1.0 표준용.
* **`value.general`**: 동의 값입니다. 유효한 값은 다음과 같습니다. `"in"` (옵트인) 및 `"out"` (옵트아웃).

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
