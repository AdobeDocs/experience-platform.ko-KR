---
title: 모바일-투-웹 및 도메인 간 ID 공유
description: 모바일, 웹 속성 및 도메인 간에 방문자 ID를 유지하는 방법을 알아봅니다
keywords: ID;모바일;id;공유;도메인;도메인 간;sdk;플랫폼;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 모바일-투-웹 및 도메인 간 ID 공유

## 개요

Adobe Experience Platform Web SDK는 고객이 모바일 앱과 모바일 웹 콘텐츠 간, 도메인 간에 보다 정확하게 개인화된 경험을 제공할 수 있도록 해주는 방문자 ID 공유 기능을 지원합니다.

## 사용 사례 {#use-cases}

### 모바일 앱과 모바일 웹 사이트 간 일관된 개인화 제공

의류 회사는 고객의 관심사에 따라 고객의 경험을 개인화하고 WebViews도 로드하는 모바일 애플리케이션에서 개인화를 정확하게 유지하려고 합니다. 모바일-웹 ID 공유 기능을 사용하면 앱 및 모바일 웹 컨텐츠에서 동일한 방문자 식별자를 사용하여 고객에게 가장 정확한 오퍼가 표시되도록 할 수 있습니다 [!DNL ECID] 모바일 웹 URL로 마이그레이션 하는 경우를 설명합니다.

### 도메인 간에 일관된 개인화 제공

여러 온라인 스토어를 사용하는 소매업체는 고객 관심 사항을 기반으로 도메인 전반에서 구매자 경험을 개인화하려고 합니다. 소매업체는 웹 SDK 도메인 간 ID 공유 기능을 사용하여 모든 도메인에서 고객의 관심사에 따라 정확한 오퍼를 제공할 수 있습니다.

### 방문자 활동 보고 개선

기술 소매업체는 방문자가 모바일 애플리케이션에서 모바일 웹 사이트로 또는 다른 도메인으로 이동하는 시기에 대한 정보로 방문자 활동 보고를 개선하려고 합니다. 웹 SDK 도메인 간 ID 공유 기능을 사용하여 마케팅 팀은 웹 속성에서 방문자를 정확하게 추적하고 활동 보고서를 생성할 수 있습니다.

## 전제 조건 {#prerequisites}

모바일-to-web 및 도메인 간 ID 공유를 사용하려면 다음을 사용해야 합니다 [!DNL Web SDK] 버전 2.11.0 이상.

Edge Network 모바일 구현의 경우 이 기능은 [에지 네트워크의 ID](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 확장 프로그램: 버전 1.1.0(iOS 및 Android)부터 시작합니다.

이 기능은 [!DNL VisitorAPI.js] 버전 1.7.0 이상

## 모바일-웹 ID 공유 {#mobile-to-web}

를 사용하십시오 `getUrlVariables` 의 API [에지 네트워크의 ID](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 확장을 사용하여 식별자를 쿼리 매개 변수로 검색하고 열 때 URL에 첨부합니다 [!DNL webViews].

웹 SDK에서 을 수락하려면 추가 구성이 필요하지 않습니다 `ECID` 쿼리 문자열의 값.

쿼리 문자열 매개 변수는 다음을 포함합니다.

* `MCID`: Experience Cloud ID(`ECID`)
* `MCORGID`: Experience Cloud `orgID` 와 일치해야 함 `orgID` 구성 [!DNL Web SDK].
* `TS`: 5분 이상이어야 하는 타임스탬프 매개 변수입니다.


모바일-웹 ID 공유에서는 를 사용합니다 `adobe_mc` 매개 변수. 이 `adobe_mc` 매개 변수가 있고 유효하며 `ECID` 쿼리 문자열에서 Edge Network에 수행된 첫 번째 요청의 id 맵에 자동으로 추가됩니다. 모든 후속 에지 네트워크 상호 작용은 `ECID`.

모바일 앱에서 WebView로 방문자 ID를 전달하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오. [webViews 처리](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 도메인 간 ID 공유 {#cross-domain-sharing}

도메인 간 ID 공유의 경우 웹 SDK 버전 2.11.0에 대한 지원을 추가합니다 `appendIdentityToUrl` 명령. 이 명령을 사용하면 `adobe_mc` 쿼리 문자열 매개 변수가 포함된 랜딩 페이지 URL이 있는지 확인합니다.

명령은 하나의 속성이 있는 개체를 허용합니다. `url`를 반환하고 속성이 있는 개체를 반환합니다 `url`.

이 명령은 동의 업데이트를 기다리지 않습니다. 동의를 제공하지 않은 경우 URL은 변경되지 않고 반환됩니다.

다음과 같은 경우 `ECID` 이 제공되지 않았습니다. `/acquire` 끝점을 호출하여 를 생성합니다. `ECID`.

다음은 고객이 웹 사이트에서 도메인 간 ID 공유를 구현하는 방법의 예입니다.

이 코드는 페이지의 모든 클릭 수에 대한 이벤트 리스너를 추가하고, 클릭이 일치하는 도메인에 대한 링크에 있는 경우(이 경우 `adobe.com` 또는 `behance.com`)에서 를 클릭하여 ID를 URL에 추가하고 사용자를 리디렉션합니다.

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

## 태그 확장 사용 {#tags-extension}

를 사용하는 것과 비슷합니다 [!DNL Web SDK]에 필요한 추가 구성이 없습니다. [!DNL Tags] 확장 을 사용하십시오.

태그 확장을 통해 모바일-투-웹 및 도메인 간 ID 공유를 사용하려면 태그 확장 버전 2.12.0 이상을 사용해야 합니다.

현재 페이지의 ID를 다른 도메인으로 공유하려면에서 사용할 수 있는 새로운 작업이 있습니다. [!DNL Web SDK] [!DNL Tags] 확장. 이 작업은 **[!UICONTROL 코어 - 클릭]** 이벤트 유형 및 값 비교 조건입니다.

설명된 단계를 수행합니다 [여기](../../tags/ui/managing-resources/rules.md) 다음 구성으로 규칙을 만들려면:

* [!UICONTROL 이벤트 구성]:
   * **[!UICONTROL 확장: 핵심]**
   * **[!UICONTROL 이벤트 유형: 클릭]**
   * 선택 **[!UICONTROL 사용자가 > 특정 요소를 클릭할 때]**
   * 에 을 입력합니다. **[!UICONTROL 선택기]**: `a[href]`. 이 이벤트는 앵커 태그를 클릭할 때마다 `href` 속성을 사용합니다.

      ![위에 설명된 설정으로 이벤트 구성을 보여주는 UI 이미지](assets/id-sharing-event-configuration.png)

* [!UICONTROL 조건 구성]
   * **[!UICONTROL 논리 유형]**: [!UICONTROL 일반]
   * **[!UICONTROL 확장]**: [!UICONTROL 코어]
   * **[!UICONTROL 조건 유형]**: [!UICONTROL 값 비교]
   * **[!UICONTROL 왼쪽 피연산자]**: [!UICONTROL `%this.hostname%`]. 에서 작동하는 특수 데이터 요소입니다 [!UICONTROL 코어 - 클릭] 이벤트 및 가 클릭한 링크의 호스트 이름으로 확인됩니다.
   * **[!UICONTROL 연산자]**: [!UICONTROL RegEx와 일치]
   * **[!UICONTROL 오른쪽 피연산자]**: ID를 공유할 도메인과 일치하는 정규 표현식을 입력합니다. 예를 들어, 로 끝나는 호스트 이름과 링크를 일치시키려면 `adobe.com` 또는 `behance.com`를 채우기 위한 규칙은 다음 정규 표현식을 사용합니다. `behance.com$|adobe.com$`. 연결된 페이지에는 [!DNL Web SDK] 또는 [!DNL Visitor ID] ID를 수락하기 위해 설치되었습니다.

      ![위에 설명된 설정으로 조건 구성을 보여주는 UI 이미지](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 작업 구성]
   * **[!UICONTROL 확장]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL 작업 유형]**: [!UICONTROL ID를 사용하여 리디렉션]
   * **[!UICONTROL 인스턴스]**: 인스턴스를 선택합니다. 대부분의 경우 구성된 인스턴스는 하나만 있습니다. 인스턴스가 여러 개인 경우 공유할 ID가 있는 인스턴스를 선택합니다.

      ![위에 설명된 설정으로 작업 구성을 보여주는 UI 이미지](assets/id-sharing-action-configuration.png)

다음 **[!UICONTROL ID를 사용하여 리디렉션]** 작업이 있으면 브라우저가 링크로 이동하지 못합니다. 그런 다음 `appendIdentityToUrl` 메서드 [!DNL Web SDK] 인스턴스.

마지막으로 사용자를 로 리디렉션합니다 [!DNL URL] 사용 `adobe_mc` 쿼리 문자열 매개 변수가 추가되었습니다.
