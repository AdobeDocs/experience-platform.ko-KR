---
product: experience-platform
audience: user
user-guide-title: XDM(경험 데이터 모델) 시스템 도움말
breadcrumb-title: Data Model (XDM) 안내서
user-guide-description: XDM(경험 데이터 모델) 클래스와 mixin을 사용하여 경험 데이터를 표준화합니다.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 21%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM 시스템 개요](home.md)
* 스키마 {#schema}
   * [스키마 컴포지션의 기본 사항](schema/composition.md)
   * [XDM 필드 유형 제한](schema/field-constraints.md)
   * [XDM 필드 사전](schema/field-dictionary.md)
   * 스키마 사용 사례 {#use-cases}
      * [개인정보 보호 동의 혼합](schema/privacy-consent.md)
* 클래스 {#classes}
   * [XDM 개별 프로필](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* 믹신 {#mixins}
   * 프로필 혼합 {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [프로필 개인 정보](./mixins/profile/person-details.md)
      * [프로필 개인 정보](./mixins/profile/personal-details.md)
      * [프로필 세분화](./mixins/profile/segmentation.md)
      * [프로필 작업 세부 사항](./mixins/profile/work-details.md)
   * 이벤트 믹싱 {#event}
      * [ExperienceEvent EndUserIDs](./mixins/event/enduserids.md)
      * [ExperienceEvent 환경 세부 사항](./mixins/event/environment-details.md)
* 데이터 유형 {#data-types}
   * [비콘](./data-types/beacon.md)
   * [브라우저 세부 사항](./data-types/browser-details.md)
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
   * [시작하기](api/getting-started.md)
   * [리소스 목록](api/list-resources.md)
   * [리소스 찾기](api/look-up-resource.md)
   * [리소스 업데이트](api/update-resource.md)
   * [리소스 바꾸기](api/replace-resource.md)
   * [리소스 삭제](api/delete-resource.md)
   * [클래스 만들기](api/create-class.md)
   * [혼합 만들기](api/create-mixin.md)
   * [데이터 유형 만들기](api/create-data-type.md)
   * [스키마 만들기](api/create-schema.md)
   * [노조](api/unions.md)
   * [설명자](api/descriptors.md)
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