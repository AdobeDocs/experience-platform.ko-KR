---
audience: user
solution: Data Collection
user-guide-title: 데이터 수집
breadcrumb-title: 데이터 수집
user-guide-description: Adobe Experience Platform으로 데이터를 전송하는 방법에 대해 알아봅니다.
feature: Data Collection
role: Developer
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 30%

---


# 데이터 수집 {#collection}

+ [개요](home.md)
+ [권한](permissions.md)
+ BrightScript {#brightscript}
   + [BrightScript 개요](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [웹 SDK JavaScript 개요](js/js-overview.md)
   + [릴리스 정보](js/release-notes.md)
   + 설치 {#install}
      + [설치 개요](js/install/overview.md)
      + [기본 코드](js/install/base-code.md)
      + [라이브러리](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [사용자 지정 빌드](js/install/create-custom-build.md)
   + 명령 {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [propositions 적용](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + 구성 {#configure}
         + [개요](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [클릭콜렉션활성화됨](js/commands/configure/clickcollectionenabled.md)
         + [컨텍스트](js/commands/configure/context.md)
         + [대화](js/commands/configure/conversation.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnable](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehidingStyle](js/commands/configure/prehidingstyle.md)
         + [푸시 알림](js/commands/configure/pushnotifications.md)
         + [스트리밍 미디어](js/commands/configure/streamingmedia.md)
         + [target마이그레이션 활성화됨](js/commands/configure/targetmigrationenabled.md)
         + [타사 쿠키 사용](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [개요](js/commands/sendevent/overview.md)
         + [데이터](js/commands/sendevent/data.md)
         + [documentUnload](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [개인화](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [set디버그](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [명령 응답](js/commands/command-responses.md)
   + [후크 모니터링](js/monitoring-hooks.md)
   + [FAQ](js/faq.md)
+ 태그 클라이언트측 JavaScript {#tags}
   + [개요](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [회사](tags/company.md)
   + [컨테이너(_C)](tags/container.md)
   + [쿠키](tags/cookie.md)
   + [환경에만 해당되는 결과를 반환합니다](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [모니터(_M)](tags/monitors.md)
   + [set디버그](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [추적](tags/track.md)
+ 사용 사례 {#use-cases}
   + [개요](use-cases/overview.md)
   + [클라이언트 힌트](use-cases/client-hints.md)
   + [클라이언트 상태](use-cases/client-state.md)
   + [상거래 데이터 수집](use-cases/collect-commerce-data.md)
   + [CSP 구성](use-cases/configuring-a-csp.md)
   + [디버깅](use-cases/debugging.md)
   + [이벤트 중복 제거](use-cases/event-duplication.md)
   + ID {#identity}
      + [개요](use-cases/identity/id-overview.md)
      + [자사 디바이스 ID](use-cases/identity/first-party-device-ids.md)
      + [ID 공유](use-cases/identity/id-sharing.md)
   + [여러 SDK 인스턴스](use-cases/multiple-instances.md)
   + 개인화 {#personalization}
      + [개요](use-cases/personalization/pers-overview.md)
      + [자동으로 DOM 작업 렌더링](use-cases/personalization/render-auto-pers-content.md)
      + [HTML 오퍼 렌더링](use-cases/personalization/render-html-offers.md)
      + [수동으로 제안 렌더링](use-cases/personalization/render-manual-propositions.md)
      + [플리커 관리](use-cases/personalization/manage-flicker.md)
      + [이벤트 표시](use-cases/personalization/display-events.md)
      + [상위 및 하위 페이지 이벤트](use-cases/personalization/top-bottom-page-events.md)
