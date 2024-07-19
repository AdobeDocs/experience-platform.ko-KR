---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Real-Time Customer Data Platform 안내서
user-guide-description: 여러 엔터프라이즈 소스에서 알려진 데이터와 익명의 데이터를 결합하여 고객 프로필을 생성하고, 이들 프로필에서 대상자를 생성하며, 이들 대상자를 서드파티 대상으로 활성화할 수 있습니다.
role: Admin
source-git-commit: 9327cf8545caa306acd8077d089041d50a30e556
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 67%

---


# Real-Time Customer Data Platform 도움말 {#rtcdp}

* [Real-Time CDP 설명서](home.md)
* 시작 {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Real-Time CDP 개요](overview.md)
      * [Real-Time CDP 시작하기](get-started.md)
      * [홈 페이지](home-page-dashboards.md)
   * Real-Time CDP B2B 에디션 {#rtcdpb2b-intro}
      * [Real-Time CDP B2B 에디션 개요](b2b-overview.md)
      * [예제 사용 사례](./b2b-use-case.md)
      * [전체 튜토리얼](./b2b-tutorial.md)
      * [Real-Time CDP B2B 에디션 가드레일](b2b-guardrails.md)
* Audience Manager 및 Real-Time CDP {#evolution}
   * [Audience Manager의 발전](aam-to-rtcdp.md)
* 계정 프로필 {#account}
   * [계정 프로필 개요](accounts/account-profile-overview.md)
   * [계정 프로필 UI 안내서](accounts/account-profile-ui-guide.md)
* 관리 {#admin}
   * [관리 개요](administration/admin-overview.md)
* 대상 및 세분화 {#segmentation}
   * [세분화 개요](segmentation/segmentation-overview.md)
   * [세그먼트 빌더 안내서](segmentation/segment-builder-guide.md)
   * [Real-Time CDP B2B 에디션의 세분화](segmentation/b2b.md)
   * [고객 AI](segmentation/customer-ai.md)
* 데이터 세트 {#datasets}
   * [데이터 세트](datasets/dataset.md)
   * [Platform의 데이터 품질](datasets/data-quality.md)
* 대상 {#destinations}
   * [대상 개요](destinations/overview.md)
   * [Real-Time CDP B2B 에디션의 대상](destinations/b2b.md)
* 보호 기능 {#guardrails}
   * [Real-Time CDP 보호 개요](guardrails/overview.md)
   * [데이터 수집을 위한 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html){target="_blank"}
   * [[!DNL Edge Network Server API]에 대한 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html){target="_blank"}
   * [데이터 및 세분화에 대한 보호 [!DNL Real-Time Customer Profile] 보호](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko){target="_blank"}
   * [데이터 [!DNL Identity Service] 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html){target="_blank"}
   * [다음에 대한 보호 기능 [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html){target="_blank"}
   * [대상을 통한 데이터 활성화를 위한 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html){target="_blank"}
* ID {#identity}
   * [ID 및 ID 네임스페이스](profile/identities-overview.md)
* 병합 정책 {#merge-policies}
   * [병합 정책 개요](profile/merge-policies.md)
* 개인정보 보호 및 데이터 거버넌스 {#privacy}
   * [개인정보 보호 개요](privacy/privacy-overview.md)
   * [데이터 거버넌스 개요](privacy/data-governance-overview.md)
* 프로필 {#profile}
   * [프로필 개요](profile/profile-overview.md)
   * [프로필 찾아보기](profile/profile-browse.md)
* Real-Time CDP B2B 에디션 AI/ML 서비스 {#b2b-cdp-ai-ml}
   * [관련 계정](b2b-ai-ml-services/related-accounts.md)
   * [계정 일치로 이어짐](b2b-ai-ml-services/lead-to-account-matching.md)
   * 예측 리드 및 계정 점수 {#predictive-lead-and-account-scoring-intro}
      * [예측 리드 및 계정 점수 개요](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [예측 리드 및 계정 점수 관리](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* 스키마 {#schemas}
   * [스키마 개요](schemas/overview.md)
   * [Real-Time CDP B2B 에디션의 스키마](schemas/b2b.md)
* 소스 {#sources}
   * [소스 개요](sources/sources-overview.md)
   * [Real-Time CDP B2B 에디션의 소스](sources/b2b.md)
* 사용 사례 {#use-cases}
   * [샘플 사용 사례 개요](/help/rtcdp/use-case-guides/overview.md)
   * 고객 확보 {#customer-acquisition}
      * [서드파티 쿠키에 의존하지 않고 새 고객 참여 및 확보](/help/rtcdp/partner-data/prospecting.md)
      * [파트너 지원 방문자 인식을 사용하여 알 수 없는 방문자에 대한 온사이트 경험 개인화](/help/rtcdp/partner-data/onsite-personalization.md)
      * [인증되지 않은 사용자에 대한 오프사이트 재타겟팅](./partner-data/offsite-retargeting.md)
   * 프로필 보강 {#profile-enrichment}
      * [파트너가 제공한 속성으로 자사 프로필 보완](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * 개인화된 통찰력 및 참여 {#personalization-insights-engagement}
      * [일회성 고객 가치를 라이프타임 가치로 향상](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [지능적으로 고객의 재참여 유도](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [지능적으로 고객 참여를 다시 유도하십시오. Luma 예](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Experience Platform 릴리스 정보](https://experienceleague.adobe.com/ko/docs/experience-platform/release-notes/latest)
* [Experience Platform 용어](https://www.adobe.com/go/platform-glossary-kr)
