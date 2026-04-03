---
title: 모바일 앱에서 모바일 웹/WebViews로 ID 공유
description: 모바일 앱의 ID를 모바일 웹 콘텐츠 또는 WebView에 전달하여 웹 컨텍스트에서 보고 및 개인화를 계속할 수 있습니다.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 모바일 앱에서 모바일 웹/WebViews로 ID 공유

방문자가 모바일 앱에서 WebView 또는 모바일 웹 페이지로 이동하면 앱 및 웹 컨텍스트는 각각 고유한 ID를 유지합니다. 명시적인 전달 없이 웹 경험은 방문자를 새로운 알 수 없는 사람으로 취급하여 보고를 단편화하고 개인화를 다시 시작합니다.

Mobile-to-web ID 공유는 [ 쿼리 문자열 매개 변수를 통해 방문자의 ](./overview.md)ECID(Experience Cloud ID)`adobe_mc`를 모바일 앱에서 웹 대상으로 전달하여 이 문제를 해결합니다. 매개 변수에는 ECID, Experience Cloud 조직 ID 및 타임스탬프가 전달됩니다. 웹 대상이 유효한 `adobe_mc` 매개 변수와 함께 로드되면 웹 SDK이 자동으로 이 대상을 읽고 첫 번째 Edge Network 요청에 전달된 ID를 적용하므로 두 컨텍스트가 동일한 방문자를 공유합니다.

조직에서 제어하는 WebView 또는 모바일 웹 페이지를 모바일 앱에서 열고 앱 활동 및 웹 활동을 동일한 방문자에게 연결된 상태로 유지하려는 경우 이 패턴을 사용합니다. 다른 도메인의 웹 사이트 간 ID 연속성이 목표라면 대신 [도메인 간 공유](cross-domain-sharing.md)를 사용하십시오.

## 전제 조건

시작하기 전에 구현이 다음 요구 사항을 충족하는지 확인하십시오.

* **모바일 앱**: Edge Network용 ID [ID](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) 확장 버전 **1.1.0 이상**&#x200B;이(가) 있는 Adobe Experience Platform Mobile SDK(iOS 및 Android).
* **웹 대상**: [Web SDK](/help/collection/js/js-overview.md) 버전 **2.11.0 이상** 또는 Web SDK 태그 확장.
* **URL 컨트롤**: 이 코드는 쿼리 문자열 매개 변수를 추가할 수 있도록 앱이 WebView 또는 브라우저에 전달하는 URL을 제어합니다.
* **일치하는 구성**: 동일한 Experience Cloud 조직 ID가 모바일 및 웹 구현에 모두 구성되어 있습니다.

## 모바일 앱에서 ID 검색 {#retrieve-identity}

Edge Network용 ID 확장의 [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) API를 사용하여 방문자의 ID를 쿼리 문자열로 검색합니다. 그런 다음 WebView 또는 브라우저를 열기 전에 해당 문자열을 URL에 추가할 수 있습니다.

반환된 문자열에는 다음 URL로 인코딩된 매개 변수가 포함되어 있습니다.

| 매개변수 | 설명 |
| --- | --- |
| `MCID` | Experience Cloud ID(ECID). |
| `MCORGID` | Experience Cloud 조직 ID입니다. 이 매개 변수는 대상 페이지의 웹 SDK에 구성된 조직과 일치해야 합니다. |
| `TS` | 타임스탬프. 대상이 **5분** 내에 이 값을 받아야 하거나 핸드오프가 거부됩니다. |

다음 코드 예는 모바일 앱에서 핸드오프의 모습을 보여 줍니다.

>[!BEGINTABS]

>[!TAB Swift(iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin(Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## 웹 측에서 ID 수신 {#receive-identity}

웹 대상에는 추가 코드가 필요하지 않습니다. 웹 SDK이 페이지에 있고 URL에 유효한 `adobe_mc` 매개 변수가 포함되어 있으면 SDK은 자동으로 ECID를 추출하여 첫 번째 Edge Network 요청 시 방문자의 ID 맵에 적용합니다.

웹 대상이 웹 SDK 태그 확장을 사용하며 ID를 유지하는 동안 방문자를 다른 페이지로 리디렉션해야 하는 경우 [ID로 리디렉션](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) 액션을 사용하여 `adobe_mc` 매개 변수를 다음 페이지로 전달합니다.

>[!NOTE]
>
>`adobe_mc` 매개 변수는 **5분** 후에 만료됩니다. URL이 열린 후 웹 대상이 로드되어 첫 번째 Edge Network 요청을 즉시 전송하는지 확인하십시오.
