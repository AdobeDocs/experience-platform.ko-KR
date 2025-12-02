---
title: 타사 쿠키 사용
description: 서드파티 쿠키를 사용하여 방문자를 식별할 수 있습니다.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

`thirdPartyCookiesEnabled` 속성은 웹 SDK이 서드파티 컨텍스트에서 쿠키를 설정하는지 여부를 결정하는 부울입니다. 이 옵션을 활성화하면 조직이 소유하는 하위 도메인 또는 도메인 간 방문자를 식별하려는 경우 유용합니다. 그러나 많은 최신 브라우저는 서드파티 쿠키의 설정 및 만료를 제한합니다. 방문자의 브라우저가 서드파티 쿠키를 지원하지 않는 경우에는 이 속성은 아무 작업도 수행하지 않습니다.

`thirdPartyCookiesEnabled` 속성은 [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) 호출 시 [`getIdentity`](../getidentity.md)을(를) 요청할 수 있는지 여부도 제어합니다.

이 옵션이 활성화되면 웹 SDK은 Adobe Audience Manager을 사용하여 방문자를 식별합니다. 이 옵션이 비활성화되면 Audience Manager 호출이 비활성화됩니다. 자세한 내용은 Audience Manager 사용 안내서의 [Demdex 도메인에 대한 호출 이해](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=ko-KR)를 참조하십시오.

`thirdPartyCookiesEnabled` 명령을 실행할 때 `configure` 부울을 설정합니다. 웹 SDK을 구성할 때 이 속성을 생략하면 기본적으로 `true`이(가) 됩니다. 웹 SDK에서 방문자를 식별하는 데 Audience Manager을 사용하지 않도록 하려면 이 값을 `false`(으)로 설정하십시오.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## 웹 SDK 태그 확장을 사용하여 서드파티 쿠키 활성화

이 설정은 [ID 구성 설정](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
