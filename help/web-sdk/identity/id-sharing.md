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

의류 회사는 고객의 관심사를 기반으로 고객의 경험을 개인화하고 WebViews도 로드하는 모바일 애플리케이션에서 개인화를 정확하게 유지하고자 합니다. 모바일-웹 ID 공유 기능을 사용하면 를 전달하여 앱과 모바일 웹 콘텐츠에서 동일한 방문자 식별자를 사용하여 고객에게 가장 정확한 오퍼가 표시되도록 할 수 있습니다. [!DNL ECID] 모바일 웹 URL에 연결합니다.

### 도메인 간에 일관된 개인화 제공

여러 온라인 스토어를 보유한 소매업체는 고객의 관심사를 기반으로 도메인 간에 쇼핑객 경험을 개인화하려고 합니다. 소매업체는 Web SDK 도메인 간 ID 공유 기능을 사용하여 모든 도메인에서 고객의 관심사를 기반으로 정확한 오퍼를 제공할 수 있습니다.

### 방문자 활동 보고 기능 향상

기술 소매업체는 방문자가 모바일 애플리케이션에서 모바일 웹 사이트 또는 다른 도메인으로 이동하는 시기에 대한 정보를 사용하여 방문자 활동 보고를 개선하려고 합니다. 마케팅 팀은 웹 SDK 도메인 간 ID 공유 기능을 사용하여 웹 속성에서 방문자를 정확하게 추적하고 활동 보고서를 생성할 수 있습니다.

## 전제 조건 {#prerequisites}

모바일-웹 및 도메인 간 ID 공유를 사용하려면 다음을 사용해야 합니다. [!DNL Web SDK] 버전 2.11.0 이상

Edge Network 모바일 구현의 경우 이 기능은 [Edge Network용 ID](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 확장 프로그램은 버전 1.1.0부터 시작됩니다(iOS 및 Android).

이 기능은 와 호환됩니다. [!DNL VisitorAPI.js] 버전 1.7.0 이상

## Mobile-to-web ID 공유 {#mobile-to-web}

사용 `getUrlVariables` 의 API [Edge Network용 ID](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) 식별자를 쿼리 매개 변수로 검색하고 열 때 URL에 첨부하는 확장명 [!DNL webViews].

웹 SDK가 동의하는 데 추가 구성이 필요하지 않습니다. `ECID` 쿼리 문자열의 값입니다.

쿼리 문자열 매개 변수에는 다음이 포함됩니다.

* `MCID`: Experience Cloud ID(`ECID`)
* `MCORGID`: EXPERIENCE CLOUD `orgID` 다음 항목과 일치해야 합니다. `orgID` 에서 구성됨 [!DNL Web SDK].
* `TS`: 5분을 초과할 수 없는 타임스탬프 매개 변수입니다.


Mobile-to-web ID 공유는 `adobe_mc` 매개 변수. 다음의 경우 `adobe_mc` 매개 변수가 있고 유효합니다. `ECID` 쿼리 문자열에서 Edge Network에 대한 첫 번째 요청의 id 맵에 자동으로 추가됩니다. 이후의 모든 에지 네트워크 상호 작용에서는 `ECID`.

모바일 앱에서 WebView로 방문자 ID를 전달하는 방법에 대한 자세한 내용은 [WebView 처리](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 도메인 간 ID 공유 구현 {#cross-domain-sharing}

다음을 참조하십시오. [`appendIdentityToUrl`](../commands/appendidentitytourl.md) 웹 SDK 태그 확장 및 웹 SDK JavaScript 라이브러리를 모두 사용하는 구현 지침에 대한 명령입니다.
