---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 도움말
breadcrumb-title: Web SDK 안내서
user-guide-description: Edge 네트워크를 통해 Experience Cloud 서비스와 상호 작용할 수 있습니다.
feature: Web SDK
source-git-commit: f96c0a3b75239681f53ffec6184af64394e37a84
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 29%

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
* 신원 {#identity}
   * [개요](identity/overview.md)
   * [자사 디바이스 ID](identity/first-party-device-ids.md)
   * [모바일-웹 및 도메인 간 ID 공유](identity/id-sharing.md)
* 데이터 수집 {#data-collection}
   * [자동으로 수집된 정보](data-collection/automatic-information.md)
   * [링크 추적](data-collection/track-links.md)
   * [상거래, 제품 및 주문 데이터 수집](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Platform Web SDK로 Adobe Analytics 사용](data-collection/adobe-analytics/analytics-overview.md)
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
      * [at.js 라이브러리와 Web SDK 비교](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * A4T(Analytics for Target) 로깅 {#a4t}
         * [개요](personalization/adobe-target/analytics-logging/overview.md)
         * [클라이언트측 로깅](personalization/adobe-target/analytics-logging/client-side.md)
         * [서버측 로깅](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [개요](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [개요](personalization/ajo/overview.md)
      * [단일 페이지 애플리케이션 구현](personalization/ajo/web-spa-implementation.md)
* 동의 {#consent}
   * [동의 지원](consent/supporting-consent.md)
   * IAB 투명성 및 동의 프레임워크 2.0 {#iab-tcf}
      * [개요](consent/iab-tcf/overview.md)
      * [태그와 통합](consent/iab-tcf/with-launch.md)
      * [태그 없이 통합](consent/iab-tcf/without-launch.md)
* [Web SDK 태그 확장](web-sdk-tag-extension-overview.md)
* [릴리스 정보](release-notes.md)
* [자주 묻는 질문](web-sdk-faq.md)
* [리소스](resources.md)
