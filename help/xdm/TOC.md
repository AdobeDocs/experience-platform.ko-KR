---
audience: user
user-guide-title: XDM(경험 데이터 모델) 시스템 도움말
breadcrumb-title: Experience Data Model(XDM) 안내서
user-guide-description: XDM(경험 데이터 모델) 클래스 및 스키마 필드 그룹을 사용하여 경험 데이터를 표준화합니다.
feature: Schemas
source-git-commit: 6b3a1cc4cfba5475aba781a1d0511a59e399135f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 17%

---


# XDM(경험 데이터 모델) 시스템 {#xdm}

* [XDM 시스템 개요](home.md)
* 스키마 {#schema}
   * [스키마 작성 기본 사항](schema/composition.md)
   * [데이터 모델링 우수 사례](schema/best-practices.md)
   * [XDM 필드 유형 제한](schema/field-constraints.md)
   * [XDM에서의 네임스페이스](./schema/namespaces.md)
   * [XDM 필드 사전](schema/field-dictionary.md)
   * 업계 데이터 모델 {#industries}
      * [개요](./schema/industries/overview.md)
      * [소매](./schema/industries/retail.md)
      * [금융 서비스](./schema/industries/financial.md)
      * [통신](./schema/industries/telecom.md)
      * [여행 및 숙박](./schema/industries/travel-hospitality.md)
* 클래스 {#classes}
   * [XDM 개별 프로필](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [세그먼트 정의](./classes/segment-definition.md)
* 스키마 필드 그룹 {#field-groups}
   * 프로필 필드 그룹 {#profile}
      * [인구 통계 세부 정보](./field-groups/profile/demographic-details.md)
      * [IAB TCF 2.0 동의](./field-groups/profile/iab.md)
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [충성도 세부 사항](./field-groups/profile/loyalty-details.md)
      * [개인 연락처 세부 정보](./field-groups/profile/personal-contact-details.md)
      * [동의 및 기본 설정](./field-groups/profile/consents.md)
      * [세그먼트 멤버십 세부 정보](./field-groups/profile/segmentation.md)
      * [통신 구독](./field-groups/profile/telecom-subscription.md)
      * [작업 연락처 세부 정보](./field-groups/profile/work-contact-details.md)
   * 이벤트 필드 그룹 {#event}
      * [캠페인 마케팅 세부 사항](./field-groups/event/campaign-marketing-details.md)
      * [채널 세부 사항](./field-groups/event/channel-details.md)
      * [상거래 세부 사항](./field-groups/event/commerce-details.md)
      * [장치 거래 세부 사항](./field-groups/event/device-trade-in-details.md)
      * [최종 사용자 ID 세부 정보](./field-groups/event/enduserids.md)
      * [환경 세부 사항](./field-groups/event/environment-details.md)
      * [IAB TCF 2.0 동의](./field-groups/event/iab.md)
      * [웹 세부 사항](./field-groups/event/web-details.md)
   * [필드 그룹 이름 업데이트](./field-groups/name-updates.md)
* 데이터 유형 {#data-types}
   * [애플리케이션](./data-types/application.md)
   * [비콘](./data-types/beacon.md)
   * [브라우저 세부 사항](./data-types/browser-details.md)
   * [Commerce](./data-types/commerce.md)
   * [동의 문자열](./data-types/consent-string.md)
   * [동의 및 기본 설정](./data-types/consents.md)
   * [통화](./data-types/currency.md)
   * [디바이스](./data-types/device.md)
   * [이메일 주소](./data-types/email-address.md)
   * [환경](./data-types/environment.md)
   * [경험 채널](./data-types/experience-channel.md)
   * [일반 동의 필드](./data-types/consent-field.md)
   * [일반 마케팅 기본 설정 필드](./data-types/marketing-field.md)
   * [구독이 있는 일반 마케팅 기본 설정 필드](./data-types/marketing-field-subscriptions.md)
   * [일반 개인화 기본 설정 필드](./data-types/personalization-field.md)
   * [지역](./data-types/geo.md)
   * [지역 원](./data-types/geo-circle.md)
   * [지역 좌표](./data-types/geo-coordinates.md)
   * [지역 상호 작용 세부 사항](./data-types/geo-interaction-details.md)
   * [지역 모양](./data-types/geo-shape.md)
   * [ID](./data-types/identity.md)
   * [마케팅](./data-types/marketing.md)
   * [측정](./data-types/measure.md)
   * [주문](./data-types/order.md)
   * [결제 항목](./data-types/payment-item.md)
   * [사람](./data-types/person.md)
   * [개인 이름](./data-types/person-name.md)
   * [전화번호](./data-types/phone-number.md)
   * [컨텍스트 배치](./data-types/place-context.md)
   * [POI 세부 사항](./data-types/poi-details.md)
   * [POI 상호 작용](./data-types/poi-interaction.md)
   * [우편 주소](./data-types/postal-address.md)
   * [제품 목록 항목](./data-types/product-list-item.md)
   * [검색](./data-types/search.md)
   * [구독](./data-types/subscription.md)
   * [통신 구독](./data-types/telecom-subscription.md)
   * [웹 정보](./data-types/web-information.md)
   * [웹 상호 작용](./data-types/web-interaction.md)
   * [웹 페이지 세부 사항](./data-types/webpage-details.md)
*  SchemaUI  {#ui}
   * [개요](./ui/overview.md)
   * [XDM 리소스 살펴보기](./ui/explore.md)
   * 리소스 {#resources} 만들기 및 편집
      * [스키마](./ui/resources/schemas.md)
      * [클래스](./ui/resources/classes.md)
      * [필드 그룹](./ui/resources/field-groups.md)
      * [데이터 유형](./ui/resources/data-types.md)
   * 필드 정의 {#fields}
      * [개요](./ui/fields/overview.md)
      * [필수 필드](./ui/fields/required.md)
      * [개체 필드](./ui/fields/object.md)
      * [배열 필드](./ui/fields/array.md)
      * [열거형 필드](./ui/fields/enum.md)
      * [ID 필드](./ui/fields/identity.md)
      * [관계 필드](./ui/fields/relationship.md)
   * [샘플 XDM 데이터 생성](./ui/sample.md)
   * [XDM 스키마 내보내기](./ui/export.md)
* 스키마 레지스트리 API {#api}
   * [개요](api/overview.md)
   * [시작하기](api/getting-started.md)
   * [스키마](api/schemas.md)
   * [비헤이비어](api/behaviors.md)
   * [클래스](api/classes.md)
   * [스키마 필드 그룹](api/field-groups.md)
   * [데이터 유형](api/data-types.md)
   * [설명자](api/descriptors.md)
   * [노조](api/unions.md)
   * [내보내기/가져오기](api/export-import.md)
   * [샘플 데이터](api/sample-data.md)
   * [감사 로그](api/audit-log.md)
   * [애드혹 스키마](api/ad-hoc.md)
   * [Mixin(사용되지 않음)](api/mixins.md)
   * [부록](api/appendix.md)
* 튜토리얼 {#tutorials}
   * [스키마 만들기(UI)](tutorials/create-schema-ui.md)
   * [스키마(API) 만들기](tutorials/create-schema-api.md)
   * [두 스키마(UI) 간의 관계 정의](tutorials/relationship-ui.md)
   * [두 스키마(API) 간의 관계를 정의합니다](tutorials/relationship-api.md)
   * [임시 스키마(API) 만들기](tutorials/ad-hoc.md)
* [문제 해결 안내서](troubleshooting-guide.md)
* [API 참조](https://www.adobe.io/experience-platform-apis/references/schema-registry/)
* [플랫폼 릴리스 노트](https://www.adobe.com/go/platform-release-notes-en)