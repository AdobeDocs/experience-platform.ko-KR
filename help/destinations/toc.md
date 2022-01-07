---
audience: user
user-guide-title: 대상 안내서
user-guide-description: 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화합니다.
description: 이 문서에서는 Adobe Experience Platform 대상의 목차 목록을 설명합니다
feature: Destinations
source-git-commit: 54da385fa3e275137164423a0bec71445b0242e4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 9%

---


# 대상 {#destinations}

* [대상 개요](./home.md)
* [대상 유형 및 카테고리](./destination-types.md)
* API 자습서 {#api}
   * [Flow Service API를 사용하여 스트리밍 대상에 연결하고 데이터를 활성화합니다](./api/streaming-destinations.md)
   * [이메일 마케팅 대상에 연결하고 Flow Service API를 사용하여 데이터를 활성화합니다](./api/email-marketing.md)
   * [(베타) 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상에 활성화합니다](./api/ad-hoc-activation-api.md)
   * [대상 계정 삭제](./api/delete-destination-account.md)
   * [대상 데이터 흐름 삭제](./api/delete-destination-dataflow.md)
* UI 안내서 {#ui}
   * [대상 작업 공간](./ui/destinations-workspace.md)
   * [새 대상 연결 만들기](./ui/connect-destination.md)
   * 대상에 대상 데이터 활성화{#activate}
      * [활성화 개요](./ui/activation-overview.md)
      * [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](./ui/activate-segment-streaming-destinations.md)
      * [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](./ui/activate-streaming-profile-destinations.md)
      * [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](./ui/activate-batch-profile-destinations.md)
      * [프로필 요청 대상에 대상 데이터 활성화(베타)](./ui/activate-profile-request-destinations.md)
   * [대상 세부 사항 보기](./ui/destination-details-page.md)
   * [대상 계정 업데이트](./ui/update-accounts.md)
   * [활성화 흐름 편집](./ui/edit-activation.md)
   * [대상 삭제](./ui/delete-destinations.md)
   * [데이터 흐름 모니터링](./ui/monitor-dataflows.md)
* 대상 카탈로그 {#catalog}
   * [대상 카탈로그 개요](./catalog/overview.md)
   * Adobe 대상{#adobe}
      * [Adobe 대상 개요](./catalog/adobe/overview.md)
      * [Marketo Engage 연결](./catalog/adobe/marketo-engage.md)
      * [Experience Platform 세그먼트 공유](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * 광고 대상{#advertising}
      * [광고 대상 개요](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud 확장](./catalog/advertising/adobe-advertising-cloud.md)
      * [Win Advertiser 변환 태그 확장](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Master Tag 확장](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads Universal Event Tracking (UET) 확장](./catalog/advertising/bing-ads.md)
      * [분기 확장](./catalog/advertising/branch.md)
      * [DoubleClick Floodlight(베타) 확장](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook 픽셀 확장](./catalog/advertising/facebook-pixel.md)
      * [Flashtalk OneTag 확장](./catalog/advertising/flashtalking.md)
      * [Google 광고 연결](./catalog/advertising/google-ads-destination.md)
      * [Google 광고 확장](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager 연결](./catalog/advertising/google-ad-manager.md)
      * [Google Customer Match 연결](./catalog/advertising/google-customer-match.md)
      * [Google 디스플레이 및 비디오 360 연결](./catalog/advertising/google-dv360.md)
      * [Google 태그 확장](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag 확장](./catalog/advertising/linkedin.md)
      * [Microsoft Bing 연결](./catalog/advertising/bing.md)
      * [Pinterest 전환 추적 확장](./catalog/advertising/pinterest-extension.md)
      * [Pinterest 고객 목록 연결](./catalog/advertising/pinterest.md)
      * [무역센터 연결](./catalog/advertising/tradedesk.md)
      * [Twitter 범용 웹 사이트 태그 확장](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX 연결](./catalog/advertising/datax.md)
   * Analytics 대상 {#analytics}
      * [Analytics 대상 개요](./catalog/analytics/overview.md)
      * [Adform 웹 사이트 추적 확장](./catalog/analytics/adform.md)
      * [Adobe Analytics 확장](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics for Audio 및 Video 확장](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale 확장](./catalog/analytics/clicktale.md)
      * [콘텐츠 사각형 확장](./catalog/analytics/contentsquare.md)
      * [Decibel 확장](./catalog/analytics/decibel.md)
      * [Demandbase 확장](./catalog/analytics/demandbase.md)
      * [DialogTech 확장](./catalog/analytics/dialogtech.md)
      * [Google 글로벌 사이트 태그 확장](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics 확장](./catalog/analytics/google-universal-analytics.md)
      * [JW 플레이어 분석(베타) 확장](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK 확장](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA 처리기 확장](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS 플레이어 핸들러 확장](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics 확장](./catalog/analytics/parsely.md)
      * [Quantum 지표 확장](./catalog/analytics/quantum-metric.md)
      * [SessionCam 확장](./catalog/analytics/sessioncam.md)
      * [TMMData 확장](./catalog/analytics/tmmdata.md)
      * [다음 전환 추적 확장](./catalog/analytics/yext.md)
   * 클라우드 스토리지 대상 {#cloud-storage}
      * [클라우드 스토리지 대상 개요](./catalog/cloud-storage/overview.md)
      * [(베타) Amazon Kinesis 연결](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3 연결](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob 연결](./catalog/cloud-storage/azure-blob.md)
      * [(베타) Azure 이벤트 허브 연결](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP 연결](./catalog/cloud-storage/sftp.md)
      * [IP 주소 허용 목록](./catalog/cloud-storage/ip-address-allow-list.md)
   * 데이터 관리 플랫폼 대상 {#data-management}
      * [DMP(데이터 관리 플랫폼) 대상 개요](./catalog/data-management/overview.md)
      * [Audience Manager DIL 확장](./catalog/data-management/aam-dil-extension.md)
   * 이메일 대상 {#email}
      * [Bizible 확장](./catalog/email/bizible.md)
      * [Marketo 확장](./catalog/email/marketo.md)
      * [Marketo Munchkin 확장 프로그램](./catalog/email/marketo-munchkin.md)
      * [페블포스트 연장](./catalog/email/pebblepost.md)
   * 이메일 마케팅 대상 {#email-marketing}
      * [이메일 마케팅 대상 개요](./catalog/email-marketing/overview.md)
      * [Adobe Campaign 연결](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle Eloqua 연결](./catalog/email-marketing/oracle-eloqua.md)
      * [Responsys 연결 oracle](./catalog/email-marketing/oracle-responsys.md)
      * [Salesforce Marketing Cloud 연결](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * 태그 확장 {#launch-extensions}
      * [태그 확장 개요](./catalog/launch-extensions/overview.md)
   * 모바일 참여 대상 {#mobile-engagement}
      * [모바일 참여 대상 개요](./catalog/mobile-engagement/overview.md)
      * [Airship 속성 연결](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship 태그 연결](./catalog/mobile-engagement/airship-tags.md)
      * [연결 브레이즈](./catalog/mobile-engagement/braze.md)
   * 개인화 대상 {#personalization}
      * [개인화 대상 개요](./catalog/personalization/overview.md)
      * [Adobe Target 연결(베타)](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target 확장](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2 확장](./catalog/personalization/adobe-target-v2.md)
      * [Beemray 확장](./catalog/personalization/beemray.md)
      * [사용자 지정 개인화 연결(베타)](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence 확장](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 서비스 확장](./catalog/personalization/adobe-ecid.md)
      * [Gainsight 확장](./catalog/personalization/gainsight.md)
      * [KickFire 확장](./catalog/personalization/kickfire.md)
      * [Marketo 웹 개인화 확장](./catalog/personalization/marketo-web-personalization.md)
   * 소셜 대상{#social}
      * [소셜 대상 개요](./catalog/social/overview.md)
      * [Livefyre 확장 Adobe](./catalog/social/adobe-livefyre.md)
      * [Facebook 연결](./catalog/social/facebook.md)
      * [linkedIn Matched Audiences 연결](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] 연결](./catalog/social/twitter.md)
   * 스트리밍 대상 {#streaming}
      * [ (베타) HTTP API 연결](./catalog/streaming/http-destination.md)
   * 설문 조사 대상 {#survey}
      * [설문 조사 대상 개요](./catalog/survey/overview.md)
      * [Foresee 확장 대상](./catalog/survey/foresee.md)
      * [InMoment 확장](./catalog/survey/inmoment.md)
      * [Qualtrics 웹 사이트 피드백 확장](./catalog/survey/qualtrics.md)
      * [Question Pro Intercept 설문 조사 확장](./catalog/survey/web-intercept-surveys.md)
   * 고객 대상의 음성 {#voice}
      * [고객 대상 음성 개요](./catalog/voice/overview.md)
      * [디지털 피드백 확장 확인](./catalog/voice/confirmit-digital-feedback.md)
      * [호출 태그 확장](./catalog/voice/invoca.md)
      * [메달리아 확장](./catalog/voice/medallia.md)
      * [대화 URL 받은 편지함 확장](./catalog/voice/talkurl.md)
* 대상 SDK {#destination-sdk}
   * [개요](./destination-sdk/overview.md)
   * [통합 사전 요구 사항](./destination-sdk/integration-prerequisites.md)
   * [시작하기](./destination-sdk/getting-started.md)
   * Destination SDK 기능 {#functionality}
      * [구성 옵션](./destination-sdk/configuration-options.md)
      * [대상 구성](./destination-sdk/destination-configuration.md)
      * [서버 및 템플릿 사양](./destination-sdk/server-and-template-configuration.md)
      * [메시지 포맷](./destination-sdk/message-format.md)
      * [대상 메타데이터 관리](./destination-sdk/audience-metadata-management.md)
      * 인증 {#authentication}
         * [인증 구성](./destination-sdk/authentication-configuration.md)
         * [OAuth 2 인증](./destination-sdk/oauth2-authentication.md)
      * 개발자 도구 {#developer-tools}
         * [메시지 변환 템플릿 만들기 및 테스트](./destination-sdk/create-template.md)
         * [대상 구성 테스트](./destination-sdk/test-destination.md)
   * API 작업 {#api}
      * [Destination SDK(대상 작성) API 참조](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [대상 끝점 API 작업](./destination-sdk/destination-configuration-api.md)
      * [대상 서버 끝점 API 작업](./destination-sdk/destination-server-api.md)
      * [대상 메타데이터 끝점 API 작업](./destination-sdk/audience-metadata-api.md)
      * [자격 증명 끝점 API 작업](./destination-sdk/credentials-configuration-api.md)
      * [게시 끝점 API 작업](./destination-sdk/destination-publish-api.md)
      * 개발자 도구 참조 {#developer-tools-reference}
         * [샘플 템플릿 API 작업 가져오기](./destination-sdk/sample-template-api.md)
         * [템플릿 API 작업 렌더링](./destination-sdk/render-template-api.md)
         * [대상 테스트 API 작업](./destination-sdk/destination-testing-api.md)
         * [샘플 프로필 생성 API 작업](./destination-sdk/sample-profile-generation-api.md)
   * 안내서 {#guides}
      * [Destination SDK을 사용하여 스트리밍 대상 구성](./destination-sdk/configure-destination-instructions.md)
      * [Destination SDK에서 작성된 대상을 검토하도록 제출](./destination-sdk/submit-destination.md)
   * 대상을 문서화합니다. {#document-destination}
      * [Adobe Experience Platform에서 대상 문서화](./destination-sdk/docs-framework/documentation-instructions.md)
      * [GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [설명서 셀프 서비스 템플릿](./destination-sdk/docs-framework/self-service-template.md)
* [자주 묻는 질문](./destinations-faq.md)
* [플랫폼 릴리스 노트](https://www.adobe.com/go/platform-release-notes-en)
