---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 도움말
breadcrumb-title: Web SDK 안내서
user-guide-description: Edge 네트워크를 통해 Experience Cloud 서비스와 상호 작용할 수 있습니다.
feature: Web SDK
source-git-commit: 15a1fd71bc5f00efdd475abd3385dc6bf4737a17
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 32%

---


# Adobe Experience Platform 웹 SDK {#edge}

* [Platform Web SDK 개요](home.md)
* 기본 사항 {#fundamentals}
   * [지원되는 사용 사례](fundamentals/supported-use-cases.md)
   * [전제 조건](fundamentals/prerequisite.md)
   * [SDK 설치](fundamentals/installing-the-sdk.md)
   * [SDK 구성](fundamentals/configuring-the-sdk.md)
   * [명령 실행](fundamentals/executing-commands.md)
   * [이벤트 추적](fundamentals/tracking-events.md)
   * [디버깅](fundamentals/debugging.md)
   * [CSP 구성](fundamentals/configuring-a-csp.md)
   * [여러 속성과 상호 작용](fundamentals/interacting-with-multiple-properties.md)
   * [사용자 에이전트 클라이언트 힌트](fundamentals/user-agent-client-hints.md)
* 데이터스트림 {#datastreams}
   * [개요](./datastreams/overview.md)
   * [데이터 스트림 구성](./datastreams/configure.md)
   * [데이터 수집을 위한 데이터 준비](./datastreams/data-prep.md)
* 신원 {#identity}
   * [개요](identity/overview.md)
   * [자사 장치 ID](identity/first-party-device-ids.md)
   * [모바일-투-웹 및 도메인 간 ID 공유](identity/id-sharing.md)
* 데이터 수집 {#data-collection}
   * [자동으로 수집된 정보](data-collection/automatic-information.md)
   * [링크 추적](data-collection/track-links.md)
   * [상거래 및 제품 데이터 수집](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Platform Web SDK에서 Adobe Analytics 사용](data-collection/adobe-analytics/analytics-overview.md)
      * [Analytics 변수 매핑](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [자동으로 매핑된 변수](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Analytics에 데이터 보내기](data-collection/adobe-analytics/sending-data-to-analytics.md)
* 개인화 {#personalization}
   * [개인화된 콘텐츠 렌더링](personalization/rendering-personalization-content.md)
   * [하이브리드 구현을 통한 개인화](personalization/hybrid-personalization.md)
   * [플리커 관리](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [개요](personalization/adobe-target/target-overview.md)
      * [단일 페이지 애플리케이션 구현](personalization/adobe-target/spa-implementation.md)
      * [응답 토큰 액세스](personalization/adobe-target/accessing-response-tokens.md)
      * [mbox 타사 ID 사용](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [at.js 라이브러리를 웹 SDK와 비교](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * A4T(Target) 로깅 분석 {#a4t}
         * [개요](personalization/adobe-target/analytics-logging/overview.md)
         * [클라이언트측 로깅](personalization/adobe-target/analytics-logging/client-side.md)
         * [서버 측 로깅](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [개요](personalization/offer-decisioning/offer-decisioning-overview.md)
* 동의 {#consent}
   * [동의 지원](consent/supporting-consent.md)
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [개요](consent/iab-tcf/overview.md)
      * [태그와 통합](consent/iab-tcf/with-launch.md)
      * [태그 없이 통합](consent/iab-tcf/without-launch.md)
* 웹 SDK 태그 확장 {#extension}
   * [웹 SDK 확장](extension/web-sdk-extension-configuration.md)
   * [이벤트 유형](extension/event-types.md)
   * [작업 유형](extension/action-types.md)
   * [데이터 요소 유형](extension/data-element-types.md)
   * [ECID 액세스](extension/accessing-the-ecid.md)
   * [웹 SDK 확장 릴리스 노트](extension/web-sdk-ext-release-notes.md)
* [릴리스 정보](release-notes.md)
* [자주 묻는 질문](web-sdk-faq.md)
* [리소스](resources.md)
