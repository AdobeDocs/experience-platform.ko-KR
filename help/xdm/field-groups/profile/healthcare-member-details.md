---
title: 의료 멤버 세부 정보 스키마 필드 그룹
description: 의료 멤버 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 3%

---

# [!UICONTROL 의료 멤버 세부 정보] 스키마 필드 그룹

[!UICONTROL 의료 구성원 세부 정보]는 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)에 대한 표준 스키마 필드 그룹으로, 연락처 정보, 주치의 및 플랜 정보와 같은 의료 서비스 또는 진료를 받거나 받을 사람의 세부 정보를 캡처합니다.

![필드 그룹 구조](../../images/field-groups/healthcare-member-details/structure.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 개인 청구 주소. |
| `faxPhone` | [[!UICONTROL 전화 번호]](../../data-types/phone-number.md) | 개인의 팩스 번호입니다. |
| `homeAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 사용자의 집 주소입니다. |
| `homePhone` | [[!UICONTROL 전화 번호]](../../data-types/phone-number.md) | 개인 집 전화번호. |
| `mailingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 해당 사용자의 우편 주소. |
| `memberDetails` | 오브젝트 | 개인의 의료 관련 속성 및 관계에 대한 자세한 정보를 포함하는 객체입니다. 개체 구조에 대한 자세한 내용은 아래 [하위 섹션](#memberDetails)을 참조하세요. |
| `mobilePhone` | [[!UICONTROL 전화 번호]](../../data-types/phone-number.md) | 개인 휴대폰 번호. |
| `person` | [[!UICONTROL 사용자]](../../data-types/person.md) | 개인 의료 서비스 멤버십과 관련된 개인 작업자, 연락처 또는 소유자입니다. |
| `personalEmail` | [[!UICONTROL 전자 메일 주소]](../../data-types/email-address.md) | 개인의 개인 이메일 주소입니다. |
| `shippingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 개인의 배송 주소입니다. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails`은(는) 개인의 의료 관련 특성 및 관계에 대한 자세한 정보를 포함하는 개체입니다. `memberDetails`의 구조는 아래에 설명되어 있습니다.

![memberDetails 구조](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `emergencyContact` | 오브젝트 | 사용자에 대한 다음 긴급 연락처 세부 정보를 캡처합니다. <ul><li>`fullName`: (문자열) 긴급 연락처의 전체 이름입니다.</li><li>`phone`: (문자열) 긴급 연락처의 전화 번호입니다.</li><li>`relationshipToMember`: (문자열) 비상 연락처와 사용자의 관계입니다.</li></ul> |
| `medications` | 오브젝트 배열 | 환자와 관련된 현재 및 과거 약물에 대한 세부 정보를 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`refillLocation`: ([[!UICONTROL 우편 주소]](../../data-types/postal-address.md)) 약물의 리필 위치입니다.</li><li>`ID`: (문자열) 약물 ID입니다.</li><li>`isCurrent`: (부울) 의약품이 현재인지 또는 과거인지를 나타냅니다.</li><li>`numberOfRefills`: (정수) 이 약물 공급자가 처방한 리필 횟수입니다.</li><li>`startDate`: (DateTime) 환자가 약물을 복용하기 시작한 날짜입니다.</li></ul> |
| `multipleBirth` | 오브젝트 | 여러 출산과 관련된 세부 정보 캡처: <ul><li>`isMultipleBirth`: (부울) 환자가 여러 번 출산했는지 여부를 나타냅니다.</li><li>`multipleBirthNumber`: (정수) `isMultipleBirth`이(가) true인 경우 태어난 아기 수입니다.</li></ul> |
| `plans` | 오브젝트 배열 | 환자와 관련된 현재 및 과거 의료 계획의 세부 정보를 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`coverageEndDate`: (DateTime) 플랜 적용이 종료되는 날짜입니다.</li><li>`coverageStartDate`: (DateTime) 플랜 적용이 시작되는 날짜입니다.</li><li>`isActive`: (부울) 플랜이 활성 상태인지 여부를 나타냅니다.</li><li>`planId`: (문자열) 계획 ID입니다.</li></ul> |
| `primaryCarePhysicians` | 오브젝트 배열 | 사용자와 연관된 1차 진료 의사의 세부 정보를 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`endDate`: (DateTime) 주치의가 환자 치료를 종료한 날짜입니다.</li><li>`fullname`: (문자열) 의사의 전체 이름입니다.</li><li>`providerId`: (문자열) 의사의 고유 식별자입니다.</li><li>`startDate`: (DateTime) PCP(주치의)가 환자 관리를 시작한 날짜입니다.</li></ul> |
| `specialists` | 오브젝트 배열 | 사용자와 관련된 의료 전문가의 세부 정보를 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`fullname`: (문자열) 전문가의 전체 이름입니다.</li><li>`providerId`: (문자열) 전문가의 고유 식별자입니다.</li><li>`specialty`: (문자열) 공급자의 전문 분야입니다(마취과, 비뇨기과, 방사선과, 피부과 등).</li></ul> |
| `beneficiaryRelationship` | 문자열 | 부양가족(예: 본인, 배우자, 자녀 등)인 경우 의료 서비스 구성원에 대한 수혜자 관계. |
| `billingAccountID` | 문자열 | 개인 청구 계정에 대한 고유 식별자. |
| `dateAgeCollected` | 날짜/시간 | 개인의 나이를 수집한 날짜. |
| `deceasedDate` | 날짜/시간 | 사망한 경우 사망한 날짜. |
| `isDeceased` | 부울 | 개인의 사망 여부를 나타냅니다. |
| `isDependent` | 부울 | 개인이 부양가족인지 여부를 나타냅니다. |
| `nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 표시되는 개인 및 해당 주 간의 법적 관계. |
| `preferredAvailability` | 문자열 | 개인이 선호하는 약속 요일 및 시간 가용성. |
| `primaryMemberID` | 문자열 | 개인이 피부양자인 경우 주 구독자에 대한 고유 식별자. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

이 필드 그룹을 사용하여 일반적인 [의료 업계 사용 사례](../../schema/industries/healthcare.md)를 제공하는 방법에 대한 자세한 내용은 업계 스키마 설명서를 참조하세요.
