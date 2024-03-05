---
title: defaultConsent
description: 기본 동의 수집 방법을 설정합니다.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

다음 `defaultConsent` 속성은 를 호출하기 전에 데이터 수집 동의를 처리하는 방법을 결정합니다. [`setConsent`](../setconsent.md) 명령입니다. 이 속성은 데이터를 수집하기 전에 동의가 필요한 영역에 거주하는 개인의 데이터를 실수로 수집하지 않으려는 경우 유용합니다.

이 속성은 다음 세 가지 값을 허용합니다.

* **위치**: 사용자가 옵트아웃할 때까지 데이터 수집은 정상적으로 진행됩니다.
* **출력**: 사용자가 옵트인할 때까지 데이터가 영구적으로 삭제됩니다.
* **보류 중**: 사용자가 를 사용하여 옵트인할 때까지 데이터가 로컬에 저장됩니다. [`setConsent`](../setconsent.md) 명령입니다. 페이지 로드 간에는 데이터가 지속되지 않습니다.

방문자가 GDPR(일반 데이터 보호 규정)의 관할이 아닌 경우 기본 동의를 로 설정할 수 있습니다. `in`. GDPR 관할권 내의 방문자는 기본 동의를 로 설정할 수 있습니다. `pending`. CMP(동의 관리 플랫폼)가 고객의 지역을 감지하고 플래그를 제공할 수 있습니다 `gdprApplies` IAB TCF 2.0으로 이 플래그는 기본 동의를 설정하는 데 사용할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 기본 동의 설정

아래에서 원하는 라디오 버튼을 선택합니다. **[!UICONTROL 기본 동의]** 조건 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 개인 정보 보호] 섹션을 선택한 다음 원하는 섹션을 선택합니다 **[!UICONTROL 기본 동의]**.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 기본 동의 설정

설정 `defaultConsent` 문자열 속성을 원하는 동의 수준으로 `configure` 명령입니다. 이 속성은 대/소문자를 구분하며 다음 세 가지 값만 지원합니다. `"in"`, `"out"`, 및 `"pending"`. 다른 값을 사용하려고 하면 라이브러리에서 오류가 발생합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
