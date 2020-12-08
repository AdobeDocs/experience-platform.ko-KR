---
product: experience-platform
audience: user
user-guide-title: XDM(경험 데이터 모델) 시스템 도움말
breadcrumb-title: Data Model (XDM) 안내서
user-guide-description: XDM(경험 데이터 모델) 클래스와 mixin을 사용하여 경험 데이터를 표준화합니다.
translation-type: tm+mt
source-git-commit: 1a4dd167ecd4f4f61ffe26af786b355e4561b30d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 23%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM 시스템 개요](home.md)
* 스키마 {#schema}
   * [스키마 컴포지션의 기본 사항](schema/composition.md)
   * [데이터 모델링을 위한 모범 사례](schema/best-practices.md)
   * [XDM 필드 유형 제한](schema/field-constraints.md)
   * [XDM 필드 사전](schema/field-dictionary.md)
   * 스키마 사용 사례 {#use-cases}
      * [동의 및 기본 설정 데이터 유형](schema/privacy-consent.md)
* 클래스 {#classes}
   * [XDM 개별 프로필](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* 믹신 {#mixins}
   * 프로필 혼합 {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [인구 통계 세부 사항](./mixins/profile/person-details.md)
      * [개인 연락처 세부 정보](./mixins/profile/personal-details.md)
      * [세그먼트 멤버십 세부 정보](./mixins/profile/segmentation.md)
      * [작업 연락처 세부 정보](./mixins/profile/work-details.md)
   * 이벤트 믹싱 {#event}
      * [최종 사용자 ID 세부 정보](./mixins/event/enduserids.md)
      * [환경 세부 사항](./mixins/event/environment-details.md)
   * [Mixin 이름 업데이트](./mixins/name-updates.md)
* 데이터 유형 {#data-types}
   * [비콘](./data-types/beacon.md)
   * [브라우저 세부 사항](./data-types/browser-details.md)
   * [동의 및 기본 설정](./data-types/consents.md)
   * [장치](./data-types/device.md)
   * [이메일 주소](./data-types/email-address.md)
   * [환경](./data-types/environment.md)
   * [지역](./data-types/geo.md)
   * [지역 원](./data-types/geo-circle.md)
   * [지역 좌표](./data-types/geo-coordinates.md)
   * [지역 상호 작용 세부 사항](./data-types/geo-interaction-details.md)
   * [지역 모양](./data-types/geo-shape.md)
   * [ID](./data-types/identity.md)
   * [사람 이름](./data-types/person-name.md)
   * [전화번호](./data-types/phone-number.md)
   * [컨텍스트 배치](./data-types/place-context.md)
   * [POI 세부 정보](./data-types/poi-details.md)
   * [POI 상호 작용](./data-types/poi-interaction.md)
   * [우편 주소](./data-types/postal-address.md)
* 스키마 레지스트리 API {#api}
   * [개요](api/overview.md)
   * [시작하기](api/getting-started.md)
   * [스키마](api/schemas.md)
   * [클래스](api/classes.md)
   * [믹신](api/mixins.md)
   * [데이터 유형](api/data-types.md)
   * [설명자](api/descriptors.md)
   * [노조](api/unions.md)
   * [임시 스키마](api/ad-hoc.md)
   * [부록](api/appendix.md)
* 자습서 {#tutorials}
   * [스키마(API) 만들기](tutorials/create-schema-api.md)
   * [스키마 만들기(UI)](tutorials/create-schema-ui.md)
   * [두 스키마(API) 간의 관계 정의](tutorials/relationship-api.md)
   * [두 스키마 간의 관계 정의(UI)](tutorials/relationship-ui.md)
   * [임시 스키마(API) 만들기](tutorials/ad-hoc.md)
* [문제 해결 가이드](troubleshooting-guide.md)
* [API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [플랫폼 릴리스 정보](https://www.adobe.com/go/platform-release-notes-en)