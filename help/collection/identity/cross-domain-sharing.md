---
title: 도메인 간 ID 공유
description: 개인화 및 보고를 개선하기 위해 조직이 소유한 도메인 간에 ID 연속성을 유지합니다.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 도메인 간 ID 공유

방문자가 조직이 소유하는 도메인 간에 이동할 때 각 도메인은 기본적으로 자체 방문자 ID를 유지합니다. 명시적인 핸드오프가 없으면 도메인 중 하나를 클릭하여 다른 도메인으로 이동하는 방문자는 대상 사이트에서 새로운 알 수 없는 사람으로 취급됩니다. 이 유형의 구현 조각 보고는 물론 개인화를 다시 시작합니다.

도메인 간 ID 공유는 방문자가 링크를 클릭하거나 리디렉션될 때 대상 URL에 `adobe_mc` 쿼리 문자열 매개 변수를 추가하여 이 문제를 해결합니다. 이 매개 변수에는 방문자의 [ECID(Experience Cloud ID)](./overview.md), 조직 ID 및 타임스탬프가 포함됩니다. 대상 페이지가 유효한 `adobe_mc` 매개 변수와 함께 로드되면 웹 SDK이 자동으로 대상 페이지를 읽고 첫 번째 Edge Network 요청에 전달된 ID를 적용하므로 두 도메인이 동일한 방문자를 공유합니다. `adobe_mc` 매개 변수는 5분 후에 만료되므로 리디렉션 후 대상 페이지를 즉시 로드해야 합니다.

이 사용 사례에서는 다른 도메인의 웹 사이트 간 ID 공유를 다룹니다. 모바일 앱에서 WebView 또는 모바일 웹 페이지로 ID를 전달하려면 대신 [모바일에서 웹으로 ID 공유](./mobile-to-web.md)를 사용하십시오.

## 전제 조건

시작하기 전에 구현이 다음 요구 사항을 충족하는지 확인하십시오.

* **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) 버전 **2.11.0 이상** 또는 Web SDK 태그 확장이 원본 및 대상 도메인 모두에 설치되어 있습니다.
* **일치하는 구성**: 모든 참여 도메인은 웹 SDK을 구성할 때 동일한 [`orgId`](../js/commands/configure/orgid.md)을(를) 사용합니다.
* **URL 컨트롤**: 코드가 도메인 간 링크 또는 리디렉션을 제어하여 쿼리 문자열 매개 변수를 대상 URL에 추가할 수 있습니다.

## 도메인 간 공유 구현

도메인 간 핸드오프에서 소스 역할을 하는 모든 도메인에 대해 ID 공유를 구성해야 합니다. 방문자가 두 도메인 간 양방향 탐색이 가능한 경우 두 도메인을 소스로 구성합니다.

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

[`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) 명령을 사용하여 `adobe_mc` 매개 변수를 아웃바운드 링크에 추가합니다. 다음 예제에서는 앵커 요소의 클릭을 수신하고 원하는 도메인을 가리키는 링크에 ID를 추가합니다.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB 웹 SDK 태그 확장]

[**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) 작업을 사용하여 `adobe_mc` 매개 변수를 아웃바운드 링크에 추가합니다. 다음 조건을 사용하여 규칙을 만들어 원하는 동작을 수행할 수 있습니다.

1. **이벤트**: 확장을 **[!UICONTROL Core]**(으)로 설정하고 이벤트 유형을 **[!UICONTROL Click]**(으)로 설정합니다. **[!UICONTROL Elements matching the CSS selector]**&#x200B;에서 `a[href]`을(를) 입력하십시오.
2. **조건**: 확장을 **[!UICONTROL Core]**(으)로 설정하고 조건 유형을 **[!UICONTROL Value Comparison]**(으)로 설정합니다. 대상 도메인(예: **[!UICONTROL Left Operand]**)과 일치하는 정규 표현식으로 `%this.hostname%`을(를) **[!UICONTROL Operator]**(으)로, **[!UICONTROL Matches Regex]**&#x200B;을(를) **[!UICONTROL Right Operand]**(으)로, `example\.com$|example\.org$`을(를) 설정합니다.
3. **Action**: 확장을 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 작업 유형을 **[!UICONTROL Redirect with identity]**(으)로 설정합니다.

>[!ENDTABS]

## 대상 도메인에서 ID 수신

대상 도메인에는 추가 코드가 필요하지 않습니다. 웹 SDK이 페이지에 있고 URL에 유효한 `adobe_mc` 매개 변수가 포함되어 있으면 SDK은 자동으로 ECID를 추출하여 첫 번째 Edge Network 요청 시 방문자의 ID 맵에 적용합니다.

대상 도메인이 다음 조건을 충족하는지 확인합니다.

* Web SDK 또는 Web SDK 태그 확장이 설치되어 있으며 원본 도메인과 동일한 [`orgId`](../js/commands/configure/orgid.md)(으)로 구성되어 있습니다. 동일한 `orgId`을(를) 공유하는 한 도메인 간에 JavaScript 라이브러리 및 Web SDK 태그 확장을 서로 교환하여 사용할 수 있습니다.
* **매개 변수가 만료되기 전에 리디렉션 후** 5분`adobe_mc` 내에 페이지가 로드되어 첫 번째 Edge Network 요청을 보냅니다.
