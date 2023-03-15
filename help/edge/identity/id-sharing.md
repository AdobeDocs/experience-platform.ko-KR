---
title: 모바일-웹 및 도메인 간 ID 공유
description: 모바일에서 웹 속성으로, 그리고 도메인 간에 방문자 ID를 유지하는 방법에 대해 알아봅니다
keywords: ID;모바일;ID;공유;도메인;교차 도메인;SDK;플랫폼;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 모바일-웹 및 도메인 간 ID 공유

## 개요

Adobe Experience Platform Web SDK는 방문자 ID 공유 기능을 지원하여 고객이 모바일 앱과 모바일 웹 콘텐츠 간에 그리고 도메인 간에 보다 정확하게 개인화된 경험을 제공할 수 있습니다.

## 사용 사례 {#use-cases}

### 모바일 앱과 모바일 웹 사이트 간에 일관된 개인화 제공

의류 회사는 고객의 관심사를 기반으로 고객의 경험을 개인화하고 WebViews도 로드하는 모바일 애플리케이션에서 개인화를 정확하게 유지하고자 합니다. 모바일-웹 ID 공유 기능을 사용하면 를 전달하여 앱과 모바일 웹 콘텐츠에서 동일한 방문자 식별자를 사용하여 고객에게 가장 정확한 오퍼가 표시되도록 할 수 있습니다. [!DNL ECID] 모바일 웹 URL에 연결합니다.

### 도메인 간에 일관된 개인화 제공

여러 온라인 스토어를 보유한 소매업체는 고객의 관심사를 기반으로 도메인 간에 쇼핑객 경험을 개인화하려고 합니다. 소매업체는 Web SDK 도메인 간 ID 공유 기능을 사용하여 모든 도메인에서 고객의 관심사를 기반으로 정확한 오퍼를 제공할 수 있습니다.

### 방문자 활동 보고 기능 향상

기술 소매업체는 방문자가 모바일 애플리케이션에서 모바일 웹 사이트 또는 다른 도메인으로 이동하는 시기에 대한 정보를 사용하여 방문자 활동 보고를 개선하려고 합니다. 마케팅 팀은 웹 SDK 도메인 간 ID 공유 기능을 사용하여 웹 속성에서 방문자를 정확하게 추적하고 활동 보고서를 생성할 수 있습니다.

## 전제 조건 {#prerequisites}

모바일-웹 및 도메인 간 ID 공유를 사용하려면 다음을 사용해야 합니다. [!DNL Web SDK] 버전 2.11.0 이상

Edge Network 모바일 구현의 경우 이 기능은 [Edge Network용 ID](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 확장 프로그램은 버전 1.1.0부터 시작됩니다(iOS 및 Android).

이 기능은 와 호환됩니다. [!DNL VisitorAPI.js] 버전 1.7.0 이상

## Mobile-to-web ID 공유 {#mobile-to-web}

사용 `getUrlVariables` 의 API [Edge Network용 ID](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 식별자를 쿼리 매개 변수로 검색하고 열 때 URL에 첨부하는 확장명 [!DNL webViews].

웹 SDK가 동의하는 데 추가 구성이 필요하지 않습니다. `ECID` 쿼리 문자열의 값입니다.

쿼리 문자열 매개 변수에는 다음이 포함됩니다.

* `MCID`: Experience Cloud ID(`ECID`)
* `MCORGID`: EXPERIENCE CLOUD `orgID` 다음 항목과 일치해야 합니다. `orgID` 에서 구성됨 [!DNL Web SDK].
* `TS`: 5분을 초과할 수 없는 타임스탬프 매개 변수입니다.


Mobile-to-web ID 공유는 `adobe_mc` 매개 변수. 다음의 경우 `adobe_mc` 매개 변수가 있고 유효합니다. `ECID` 쿼리 문자열에서 Edge Network에 대한 첫 번째 요청의 id 맵에 자동으로 추가됩니다. 이후의 모든 에지 네트워크 상호 작용에서는 `ECID`.

모바일 앱에서 WebView로 방문자 ID를 전달하는 방법에 대한 자세한 내용은 [WebView 처리](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 도메인 간 ID 공유 {#cross-domain-sharing}

도메인 간 ID 공유를 위해 Web SDK 버전 2.11.0에는 `appendIdentityToUrl` 명령입니다. 이 명령을 사용하면 `adobe_mc` 쿼리 문자열 매개 변수.

명령은 하나의 속성이 있는 개체를 수락합니다. `url`속성을 가진 개체를 반환합니다. `url`.

이 명령은 동의 업데이트를 기다리지 않습니다. 동의를 제공하지 않은 경우 URL은 변경되지 않고 반환됩니다.

다음과 같은 경우 `ECID` 제공되지 않음, `/acquire` 끝점이 호출되어 다음을 생성합니다. `ECID`.

다음은 고객이 웹 사이트에서 도메인 간 ID 공유를 구현하는 방법의 예입니다.

이 코드는 페이지의 모든 클릭에 대한 이벤트 리스너를 추가하고, 해당 클릭이 일치하는 도메인에 대한 링크를 기반으로 한 경우(이 경우 `adobe.com` 또는 `behance.com`)에서 URL에 ID를 추가하고 사용자를 해당 URL로 리디렉션합니다.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Tags 확장 사용 {#tags-extension}

를 사용하는 것과 비슷합니다. [!DNL Web SDK]에 필요한 추가 구성이 없습니다. [!DNL Tags] URL을 통해 전달된 ID를 사용하는 확장입니다.

Tags 확장을 통해 모바일-웹 및 도메인 간 ID 공유를 사용하려면 Tags 확장 버전 2.12.0 이상을 사용해야 합니다.

현재 페이지에서 다른 도메인으로 ID를 공유하려면에서 새 작업을 사용할 수 있습니다. [!DNL Web SDK] [!DNL Tags] 확장명. 이 작업은 **[!UICONTROL 코어 - 클릭]** 이벤트 유형 및 값 비교 조건.

설명된 단계 수행 [여기](../../tags/ui/managing-resources/rules.md) 다음 구성으로 규칙을 만들려면:

* [!UICONTROL 이벤트 구성]:
   * **[!UICONTROL 확장: 핵심]**
   * **[!UICONTROL 이벤트 유형: 클릭]**
   * 선택 **[!UICONTROL 사용자가 > 특정 요소를 클릭할 때]**
   * 다음을 입력합니다. **[!UICONTROL 선택기]**: `a[href]`. 이 이벤트는 페이지에서 앵커 태그를 클릭할 때마다 `href` 속성.

      ![위에서 설명한 설정을 사용한 이벤트 구성을 보여 주는 UI 이미지](assets/id-sharing-event-configuration.png)

* [!UICONTROL 조건 구성]
   * **[!UICONTROL 논리 유형]**: [!UICONTROL 보통]
   * **[!UICONTROL 확장]**: [!UICONTROL 코어]
   * **[!UICONTROL 조건 유형]**: [!UICONTROL 값 비교]
   * **[!UICONTROL 왼쪽 피연산자]**: [!UICONTROL `%this.hostname%`]. 와 함께 작동하는 특수 데이터 요소입니다 [!UICONTROL 코어 - 클릭] 및 는 클릭한 링크의 호스트 이름으로 확인됩니다.
   * **[!UICONTROL 연산자]**: [!UICONTROL RegEx와 일치]
   * **[!UICONTROL 오른쪽 피연산자]**: ID를 공유할 도메인과 일치하는 정규 표현식을 입력합니다. 예를 들어 로 끝나는 호스트 이름의 링크를 일치시키려면 `adobe.com` 또는 `behance.com`, 다음 정규 표현식을 사용합니다. `behance.com$|adobe.com$`. 링크된 페이지에는 [!DNL Web SDK] 또는 [!DNL Visitor ID] id를 수락하도록 설치되었습니다.

      ![위에서 설명한 설정이 있는 조건 구성을 보여 주는 UI 이미지](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 작업 구성]
   * **[!UICONTROL 확장]**: [!UICONTROL Adobe Experience Platform 웹 SDK]
   * **[!UICONTROL 작업 유형]**: [!UICONTROL ID로 리디렉션]
   * **[!UICONTROL 인스턴스]**: 인스턴스를 선택합니다. 대부분의 경우 구성된 인스턴스는 한 개만 있습니다. 인스턴스가 여러 개 있는 경우 공유할 ID가 있는 인스턴스를 선택합니다.

      ![위에서 설명한 설정이 있는 작업 구성을 보여 주는 UI 이미지](assets/id-sharing-action-configuration.png)

다음 **[!UICONTROL ID로 리디렉션]** 작업을 수행하면 브라우저가 링크로 이동하지 못합니다. 그런 다음 를 호출합니다. `appendIdentityToUrl` 다음에 대한 메서드 [!DNL Web SDK] 인스턴스.

마지막으로 사용자를 로 리디렉션합니다. [!DNL URL] (으)로 `adobe_mc` 쿼리 문자열 매개 변수가 추가되었습니다.
