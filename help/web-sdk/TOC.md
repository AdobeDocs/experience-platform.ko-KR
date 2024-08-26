---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 도움말
breadcrumb-title: Web SDK 안내서
user-guide-description: Edge 네트워크를 통해 Experience Cloud 서비스와 상호 작용할 수 있습니다.
feature: Web SDK
role: Developer
source-git-commit: 1a6d42fd1319828f5bb5d470f24ea5ee8bed4661
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 22%

---


# Adobe Experience Platform 웹 SDK {#web-sdk}

* [Web SDK 개요](home.md)
* [릴리스 정보](release-notes.md)
* 웹 SDK 설치 {#install}
   * [개요](install/overview.md)
   * [태그 확장을 사용하여 웹 SDK 설치](install/extension.md)
   * [JavaScript 라이브러리를 사용하여 웹 SDK 설치](install/library.md)
   * [NPM 패키지를 사용하여 Web SDK 설치](install/npm.md)
* 명령 {#commands}
   * {#configure} 구성
      * [개요](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [클릭콜렉션활성화됨](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [컨텍스트](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnable](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [스트리밍 미디어](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehidingStyle](commands/configure/prehidingstyle.md)
      * [target마이그레이션 활성화됨](commands/configure/targetmigrationenabled.md)
      * [타사 쿠키 사용](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [개요](commands/sendevent/overview.md)
      * [데이터](commands/sendevent/data.md)
      * [documentUnload](commands/sendevent/documentunloading.md)
      * [개인화](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [유형](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [propositions 적용](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [set디버그](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [데이터 스트림 재정의 구성](commands/datastream-overrides.md)
   * [명령 응답](commands/command-responses.md)

* ID {#identity}
   * [개요](identity/overview.md)
   * [자사 디바이스 ID](identity/first-party-device-ids.md)
   * [모바일-웹 및 도메인 간 ID 공유](identity/id-sharing.md)

* 개인화 {#personalization}
   * [디스플레이 이벤트 관리](personalization/display-events.md)
   * [개인화된 콘텐츠 렌더링](personalization/rendering-personalization-content.md)
   * [하이브리드 구현을 통한 Personalization](personalization/hybrid-personalization.md)
   * [플리커 관리](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [개요](personalization/adobe-target/target-overview.md)
      * [단일 페이지 애플리케이션 구현](personalization/adobe-target/spa-implementation.md)
      * [응답 토큰 액세스](personalization/adobe-target/accessing-response-tokens.md)
      * [mbox 타사 ID 사용](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [at.js 라이브러리와 Web SDK 비교](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * A4T(Analytics for Target) 로깅 {#a4t}
         * [개요](personalization/adobe-target/analytics-logging/overview.md)
         * [클라이언트측 로깅](personalization/adobe-target/analytics-logging/client-side.md)
         * [서버측 로깅](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer decisioning {#offer-decisioning}
      * [개요](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [개요](personalization/ajo/overview.md)
      * [단일 페이지 애플리케이션 구현](personalization/ajo/web-spa-implementation.md)
      * [Web SDK에서 웹 인앱 메시지 지원 구성](personalization/web-in-app-messaging.md)

* 동의 {#consent}
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [개요](consent/iab-tcf/overview.md)
      * [태그와 통합](consent/iab-tcf/with-tags.md)
      * [태그 없이 통합](consent/iab-tcf/without-tags.md)

* 사용 사례 {#use-cases}
   * [개요](use-cases/overview.md)
   * [웹 SDK를 사용하여 Adobe Analytics에 데이터 보내기](use-cases/adobe-analytics.md)
   * [사용자 에이전트 클라이언트 힌트](use-cases/client-hints.md)
   * [상거래 데이터 수집](use-cases/collect-commerce-data.md)
   * [CSP 구성](use-cases/configuring-a-csp.md)
   * [디버깅 메서드](use-cases/debugging.md)
   * [여러 웹 SDK 인스턴스 사용](use-cases/multiple-instances.md)
   * [상단 및 하단 페이지 이벤트 구성](use-cases/top-bottom-page-events.md)

* [자주 묻는 질문](faq.md)
* [리소스](resources.md)
