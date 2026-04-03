---
title: defaultConsent
description: 웹 속성에 대한 기본 동의 수집 방법을 설정합니다.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# `defaultConsent`

`defaultConsent` 속성은 [`setConsent`](../setconsent.md) 명령을 호출하기 전에 데이터 수집 동의를 처리하는 방법을 결정합니다. 이 속성은 데이터를 수집하기 전에 동의가 필요한 영역에 거주하는 개인의 데이터를 실수로 수집하지 않으려는 경우 유용합니다.

방문자가 GDPR(일반 데이터 보호 규정)의 적용을 받지 않는 경우 기본 동의를 `in`(으)로 설정할 수 있습니다. GDPR 관할권 내의 방문자는 기본 동의를 `pending`(으)로 설정할 수 있습니다. CMP(동의 관리 플랫폼)가 고객의 지역을 감지하고 `gdprApplies` 플래그를 IAB TCF 2.0에 제공할 수 있습니다. 이 플래그는 기본 동의를 설정하는 데 사용할 수 있습니다.

`defaultConsent` 명령을 실행할 때 `configure` 문자열 속성을 원하는 동의 수준으로 설정하십시오. 이 속성은 대/소문자를 구분하며 `"in"`, `"out"` 및 `"pending"` 세 가지 값만 지원합니다. 다른 값을 사용하려고 하면 라이브러리에서 오류가 발생합니다. `configure` 명령에 설정되지 않은 경우 기본값은 **`in`**&#x200B;입니다.

>[!IMPORTANT]
>
>페이지 로드 사이에 `defaultConsent` 값이 유지되지 않습니다. `configure` 명령을 호출할 때마다 원하는 기본 동의를 설정해야 합니다. 반대로 방문자의 해결된 동의([`setConsent`](../setconsent.md)을 통해 설정됨)는 쿠키에 유지되고 후속 페이지 로드 시 자동으로 적용됩니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: 사용자가 옵트아웃할 때까지 데이터 수집이 정상적으로 작동합니다.
* **`out`**: 사용자가 옵트인할 때까지 데이터가 영구적으로 삭제됩니다.
* **`pending`**: 사용자가 [`setConsent`](../setconsent.md) 명령을 사용하여 옵트인할 때까지 데이터가 로컬에 저장됩니다.

>[!NOTE]
>
>Adobe은 Adobe 기능 및 제품 오퍼링에 해당하는 보다 강력한 목적 또는 카테고리 세트를 구축할 계획이지만 현재 구현은 옵트인에 대한 양자택일의 접근 방식입니다. 이 제한은 웹 SDK에만 적용되며 다른 Adobe JavaScript 라이브러리에는 적용되지 않습니다.

## `defaultConsent`과(와) 함께 `setConsent` 사용 {#using-consent}

`defaultConsent`과(와) `setConsent`을(를) 함께 사용하면 구성된 값에 따라 다른 데이터 수집, 쿠키 설정 및 ID 결과를 생성합니다. 전체 상호 작용 테이블을 보려면 [데이터 수집에서 동의 및 ID](/help/collection/identity/consent.md#how-consent-affects-identity)를 참조하십시오.

## `gdprApplies`을(를) 기반으로 기본 동의 설정 중

일부 CMP에서는 GDPR(일반 데이터 보호 규정)이 고객에게 적용되는지 여부를 확인하는 기능을 제공합니다. GDPR이 적용되지 않는 고객에 대한 동의를 얻으려면 TCF API 호출에 `gdprApplies` 플래그를 사용할 수 있습니다. 예:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

위의 코드 블록에서 `configure` 명령은 TCF API에서 `tcData`을(를) 가져온 후에 호출됩니다. `gdprApplies`이(가) true이면 기본 동의가 `pending`(으)로 설정됩니다. `gdprApplies`이(가) false이면 기본 동의가 `in`(으)로 설정됩니다. 구성을 사용하여 `alloyConfiguration` 변수를 채우십시오.

## 웹 SDK 태그 확장을 사용한 기본 동의

태그를 사용하여 이러한 작업을 수행하는 방법에 대해 알아보려면 웹 SDK 태그 확장 설명서에서 [동의 설정](/help/tags/extensions/client/web-sdk/configure/consent.md)을 참조하십시오.
