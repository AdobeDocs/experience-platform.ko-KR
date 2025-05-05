---
title: 모바일-웹 및 도메인 간 ID 공유
description: 모바일에서 웹 속성으로, 그리고 도메인 간에 방문자 ID를 유지하는 방법에 대해 알아봅니다
keywords: ID;모바일;ID;공유;도메인;교차 도메인;SDK;플랫폼;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 모바일-웹 및 도메인 간 ID 공유

## 개요

Adobe Experience Platform Web SDK는 방문자 ID 공유 기능을 지원하여 고객이 모바일 앱과 모바일 웹 콘텐츠 간에 그리고 도메인 간에 보다 정확하게 개인화된 경험을 제공할 수 있습니다.

## 사용 사례 {#use-cases}

### 모바일 앱과 모바일 웹 사이트 간에 일관된 개인화 제공

의류 회사는 고객의 관심사를 기반으로 고객의 경험을 개인화하고 WebViews도 로드하는 모바일 애플리케이션에서 개인화를 정확하게 유지하고자 합니다. Mobile-to-Web ID 공유 기능을 사용하면 [!DNL ECID]을(를) 모바일 웹 URL에 전달하여 앱과 모바일 웹 콘텐츠에서 동일한 방문자 식별자를 사용하여 고객에게 가장 정확한 오퍼가 표시되도록 할 수 있습니다.

### 도메인 간에 일관된 개인화 제공

여러 온라인 스토어를 보유한 소매업체는 고객의 관심사를 기반으로 도메인 간에 쇼핑객 경험을 개인화하려고 합니다. 소매업체는 Web SDK 도메인 간 ID 공유 기능을 사용하여 모든 도메인에서 고객의 관심사를 기반으로 정확한 오퍼를 제공할 수 있습니다.

### 방문자 활동 보고 기능 향상

기술 소매업체는 방문자가 모바일 애플리케이션에서 모바일 웹 사이트 또는 다른 도메인으로 이동하는 시기에 대한 정보를 사용하여 방문자 활동 보고를 개선하려고 합니다. 마케팅 팀은 웹 SDK 도메인 간 ID 공유 기능을 사용하여 웹 속성에서 방문자를 정확하게 추적하고 활동 보고서를 생성할 수 있습니다.

## 전제 조건 {#prerequisites}

모바일-웹 및 도메인 간 ID 공유를 사용하려면 [!DNL Web SDK] 버전 2.11.0 이상을 사용해야 합니다.

Edge Network 모바일 구현의 경우, 이 기능은 버전 1.1.0(iOS 및 Android)부터 시작되는 [Edge Network ID](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 확장에서 지원됩니다.

이 기능은 [!DNL VisitorAPI.js] 버전 1.7.0 이상과도 호환됩니다.

## Mobile-to-web ID 공유 {#mobile-to-web}

[!DNL webViews]을(를) 열 때 [Edge Network ID](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) 확장의 `getUrlVariables` API를 사용하여 식별자를 쿼리 매개 변수로 검색하고 URL에 첨부합니다.

웹 SDK가 쿼리 문자열에서 `ECID` 값을 수락하는 데 추가 구성이 필요하지 않습니다.

쿼리 문자열 매개 변수에는 다음이 포함됩니다.

* `MCID`: Experience Cloud ID(`ECID`)
* `MCORGID`: [!DNL Web SDK]에 구성된 `orgID`과(와) 일치해야 하는 Experience Cloud `orgID`입니다.
* `TS`: 타임스탬프 매개 변수는 5분을 초과할 수 없습니다.


Mobile-to-web ID 공유에서는 `adobe_mc` 매개 변수를 사용합니다. `adobe_mc` 매개 변수가 있고 유효하면 쿼리 문자열의 `ECID`이(가) Edge Network에 수행된 첫 번째 요청에서 ID 맵에 자동으로 추가됩니다. 모든 후속 Edge Network 상호 작용에서는 해당 `ECID`을(를) 사용합니다.

모바일 앱에서 WebView로 방문자 ID를 전달하는 방법에 대한 자세한 내용은 [WebViews 처리](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html?lang=ko#implementation)에 대한 설명서를 참조하십시오.

## 도메인 간 ID 공유 구현 {#cross-domain-sharing}

Web SDK 태그 확장과 Web SDK JavaScript 라이브러리를 모두 사용하는 구현 지침은 [`appendIdentityToUrl`](../commands/appendidentitytourl.md) 명령을 참조하십시오.
