---
title: appendIdentityToUrl
description: 앱, 웹 및 도메인 간에 개인화된 경험을 보다 정확하게 전달합니다.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

`appendIdentityToUrl` 명령을 사용하면 URL에 사용자 식별자를 쿼리 문자열로 추가할 수 있습니다. 이 작업을 사용하면 도메인 간에 방문자의 ID를 전달할 수 있으므로 도메인 또는 채널을 모두 포함하는 데이터 세트에 대해 방문자 수가 중복되지 않도록 합니다. 웹 SDK 버전 2.11.0 이상에서 사용할 수 있습니다.

URL에 추가되고 생성된 쿼리 문자열은 `adobe_mc`입니다. 웹 SDK에서 ECID를 찾을 수 없으면 `/acquire` 끝점을 호출하여 ECID를 생성합니다.

>[!NOTE]
>
>동의를 제공하지 않은 경우 이 메서드의 URL은 변경되지 않은 상태로 반환됩니다. 이 명령은 즉시 실행되며 동의 업데이트를 기다리지 않습니다.

URL을 매개 변수로 사용하여 `appendIdentityToUrl` 명령을 실행합니다. 이 메서드는 식별자가 추가된 URL을 쿼리 문자열로 반환합니다.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

페이지에서 받은 모든 클릭에 대한 이벤트 리스너를 추가하고 URL이 원하는 도메인과 일치하는지 확인할 수 있습니다. 이 경우 ID를 URL에 추가하고 사용자를 리디렉션합니다.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

이 명령은 [`edgeConfigOverrides`](configure/edgeconfigoverrides.md) 개체를 지원합니다.

## 응답 개체

이 명령을 사용하여 [응답을 처리](command-responses.md)할 때 응답 개체에는 ID 정보가 쿼리 문자열 매개 변수로 추가된 새 URL인 **`url`**&#x200B;이(가) 포함됩니다.

## 웹 SDK 태그 확장을 사용하여 URL에 ID 추가

이 명령과 같은 웹 SDK 태그 확장은 [ID를 사용하여 리디렉션](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) 작업입니다.
