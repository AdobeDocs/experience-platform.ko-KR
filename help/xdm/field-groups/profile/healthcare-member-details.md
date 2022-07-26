---
title: 의료 구성원 세부 정보 스키마 필드 그룹
description: 이 문서에서는 Healthcare 멤버 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 4%

---

# [!UICONTROL 의료 구성원 세부 정보] 스키마 필드 그룹

[!UICONTROL 의료 구성원 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 또한 연락처 정보, 1차 진료 의사, 계획 정보 등 의료 서비스 또는 의료 서비스를 받게 되거나 받게 될 사람의 세부 정보를 캡처합니다.

![필드 그룹 구조](../../images/field-groups/healthcare-member-details/structure.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 개인의 청구 주소입니다. |
| `faxPhone` | [[!UICONTROL 전화번호]](../../data-types/phone-number.md) | 사람의 팩스 전화번호입니다. |
| `homeAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 개인의 집 주소입니다. |
| `homePhone` | [[!UICONTROL 전화번호]](../../data-types/phone-number.md) | 그 사람의 집 전화 번호입니다. |
| `mailingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 사람의 우편 주소입니다. |
| `memberDetails` | 개체 | 개인의 의료 관련 속성 및 관계에 대한 자세한 정보를 포함하는 객체입니다. 자세한 내용은 [하위 섹션](#memberDetails) 를 참조하십시오. |
| `mobilePhone` | [[!UICONTROL 전화번호]](../../data-types/phone-number.md) | 개인의 휴대폰 번호입니다. |
| `person` | [[!UICONTROL 사람]](../../data-types/person.md) | 개인의 의료 서비스 멤버십과 관련된 개인 배우, 담당자 또는 소유자. |
| `personalEmail` | [[!UICONTROL 이메일 주소]](../../data-types/email-address.md) | 개인의 개인 이메일 주소입니다. |
| `shippingAddress` | [[!UICONTROL 우편 주소]](../../data-types/postal-address.md) | 사람의 배송 주소입니다. |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` 은 개인의 의료 관련 속성 및 관계에 대한 자세한 정보를 포함하는 객체입니다. 의 구조 `memberDetails` 은 아래에 설명되어 있습니다.

![memberDetails 구조](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `emergencyContact` | 개체 | 개인을 위한 다음과 같은 긴급 연락처 세부 정보를 캡처합니다. <ul><li>`fullName`: (문자열) 응급 연락처의 전체 이름입니다.</li><li>`phone`: (문자열) 긴급 연락처의 전화 번호입니다.</li><li>`relationshipToMember`: (문자열) 응급 연락처와 사람에 대한 관계입니다.</li></ul> |
| `medications` | 개체 배열 | 그 사람과 연관된 현재 약물과 과거 약물의 세부사항을 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`refillLocation`: ([[!UICONTROL 우편 주소]](../../data-types/postal-address.md)) 약물의 리필 위치.</li><li>`ID`: (문자열) 약제 ID.</li><li>`isCurrent`: (부울) 약물이 최신 상태인지 또는 지난 상태인지를 나타냅니다.</li><li>`numberOfRefills`: (정수) 이 약제의 제공자가 처방하는 리필의 수입니다.</li><li>`startDate`: (DateTime) 투약하기 시작한 날짜입니다.</li></ul> |
| `multipleBirth` | 개체 | 여러 출산 관련 세부 정보 캡처: <ul><li>`isMultipleBirth`: (부울) 사용자가 여러 개의 출산을 제공했는지 여부를 나타냅니다.</li><li>`multipleBirthNumber`: (정수) 다음의 경우 태어난 영아의 수입니다. `isMultipleBirth` 는 true입니다.</li></ul> |
| `plans` | 개체 배열 | 사용자와 연관된 현재 및 과거 의료 계획의 세부 사항을 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`coverageEndDate`: (일자Time) 제도 적용 범위의 종료 일자.</li><li>`coverageStartDate`: (일자Time) 제도 적용 범위가 시작되는 일자입니다.</li><li>`isActive`: (부울) 계획이 활성 상태인지 여부를 나타냅니다.</li><li>`planId`: (문자열) 계획 ID입니다.</li></ul> |
| `primaryCarePhysicians` | 개체 배열 | 개인과 연관된 1차 진료 의사의 상세내역을 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`endDate`: (DateTime) 1차 진료 의사가 개인 관리를 종료한 날짜입니다.</li><li>`fullname`: (문자열) 의사의 전체 이름입니다.</li><li>`providerId`: (문자열) 의사의 고유 식별자입니다.</li><li>`startDate`: (DateTime) 1차 진료 의사가 개인을 돌본 날짜입니다.</li></ul> |
| `specialists` | 개체 배열 | 해당 사용자와 관련된 의료 전문가의 세부 사항을 나열합니다. 각 배열 항목은 다음 세부 정보를 캡처하는 객체입니다. <ul><li>`fullname`: (문자열) 전문가의 전체 이름입니다.</li><li>`providerId`: (문자열) 전문가의 고유 식별자입니다.</li><li>`specialty`: (문자열) 공급자의 전문과목(마취과, 비뇨기과, 방사선학, 피부과 등)입니다.</li></ul> |
| `beneficiaryRelationship` | 문자열 | 개인이 부양가족인 경우 의료 구성원에 대한 수혜자 관계(예: 자기, 배우자, 1차 하위 구성요소 등). |
| `billingAccountID` | 문자열 | 개인의 청구 계정에 대한 고유 식별자입니다. |
| `dateAgeCollected` | DateTime | 개인의 연령이 수집된 날짜입니다. |
| `deceasedDate` | DateTime | 사망한 사람이 사망한 날짜입니다. |
| `isDeceased` | 부울 | 사람이 사망했는지 여부를 나타냅니다. |
| `isDependent` | 부울 | 개인이 부양가족인지 여부를 나타냅니다. |
| `nationality` | 문자열 | ISO 3166-1 Alpha-2 코드를 사용하여 표시되는 개인 및 해당 상태 간의 법적 관계. |
| `preferredAvailability` | 문자열 | 약속에 대한 개인의 선호 일자 및 시간 가용성. |
| `primaryMemberID` | 문자열 | 개인이 부양가족인 경우 기본 가입자의 고유 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

이 필드 그룹을 사용하여 공통으로 제공하는 방법에 대한 자세한 내용은 업계 스키마 설명서 를 참조하십시오 [의료 업계 활용 사례](../../schema/industries/healthcare.md).
