---
product: experience-platform
audience: user
user-guide-title: XDM(경험 데이터 모델) 시스템 도움말
breadcrumb-title: Experience Data Model(XDM) 안내서
user-guide-description: XDM(경험 데이터 모델) 클래스와 믹스인을 사용하여 경험 데이터를 표준화합니다.
feature: 스키마
translation-type: tm+mt
source-git-commit: 4a67bcbd2a1458ae47ba64fe2647da442fdf4695
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 24%

---


# 경험 데이터 모델(XDM) 시스템 {#xdm}

* [XDM 시스템 개요](home.md)
* 스키마 {#schema}
   * [스키마 컴포지션의 기본 사항](schema/composition.md)
   * [데이터 모델링을 위한 모범 사례](schema/best-practices.md)
   * [XDM 필드 유형 제약 조건](schema/field-constraints.md)
   * [XDM 필드 사전](schema/field-dictionary.md)
* 클래스 {#classes}
   * [XDM 개별 프로필](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [세그먼트 정의](./classes/segment-definition.md)
* 믹싱 {#mixins}
   * 프로필 혼합 {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [인구 통계 세부 사항](./mixins/profile/person-details.md)
      * [개인 연락처 세부 사항](./mixins/profile/personal-details.md)
      * [세그먼트 멤버십 세부 사항](./mixins/profile/segmentation.md)
      * [작업 연락처 세부 사항](./mixins/profile/work-details.md)
   * 이벤트 믹싱 {#event}
      * [최종 사용자 ID 세부 사항](./mixins/event/enduserids.md)
      * [환경 세부 사항](./mixins/event/environment-details.md)
   * [Mixin 이름 업데이트](./mixins/name-updates.md)
* 데이터 유형 {#data-types}
   * [애플리케이션](./data-types/application.md)
   * [비콘](./data-types/beacon.md)
   * [브라우저 세부 사항](./data-types/browser-details.md)
   * [Commerce](./data-types/commerce.md)
   * [동의 및 기본 설정](./data-types/consents.md)
   * [장치](./data-types/device.md)
   * [이메일 주소](./data-types/email-address.md)
   * [환경](./data-types/environment.md)
   * [지역](./data-types/geo.md)
   * [지역 서클](./data-types/geo-circle.md)
   * [지역 좌표](./data-types/geo-coordinates.md)
   * [지역 상호 작용 세부 사항](./data-types/geo-interaction-details.md)
   * [지역 모양](./data-types/geo-shape.md)
   * [ID](./data-types/identity.md)
   * [측정](./data-types/measure.md)
   * [주문](./data-types/order.md)
   * [결제 항목](./data-types/payment-item.md)
   * [사람](./data-types/person.md)
   * [사람 이름](./data-types/person-name.md)
   * [전화번호](./data-types/phone-number.md)
   * [컨텍스트 배치](./data-types/place-context.md)
   * [POI 세부 정보](./data-types/poi-details.md)
   * [POI 상호 작용](./data-types/poi-interaction.md)
   * [우편 주소](./data-types/postal-address.md)
   * [검색](./data-types/search.md)
   * [구독](./data-types/subscription.md)
   * [웹 상호 작용](./data-types/web-interactions.md)
   * [웹 페이지 세부 사항](./data-types/webpage-details.md)
* [!UICONTROL Schemas] UI {#ui}
   * [개요](./ui/overview.md)
   * [XDM 리소스 살펴보기](./ui/explore.md)
   * 리소스 {#resources} 만들기 및 편집
      * [스키마](./ui/resources/schemas.md)
      * [클래스](./ui/resources/classes.md)
      * [혼합](./ui/resources/mixins.md)
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
   * [혼합](api/mixins.md)
   * [데이터 유형](api/data-types.md)
   * [설명자](api/descriptors.md)
   * [조합](api/unions.md)
   * [내보내기/가져오기](api/export-import.md)
   * [샘플 데이터](api/sample-data.md)
   * [감사 로그](api/audit-log.md)
   * [임시 스키마](api/ad-hoc.md)
   * [부록](api/appendix.md)
* 튜토리얼 {#tutorials}
   * [스키마 만들기(UI)](tutorials/create-schema-ui.md)
   * [스키마 만들기(API)](tutorials/create-schema-api.md)
   * [두 스키마 간의 관계 정의(UI)](tutorials/relationship-ui.md)
   * [두 스키마(API) 간의 관계 정의](tutorials/relationship-api.md)
   * [임시 스키마 만들기(API)](tutorials/ad-hoc.md)
* [문제 해결 가이드](troubleshooting-guide.md)
* [API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [플랫폼 릴리스 정보](https://www.adobe.com/go/platform-release-notes-en)