---
title: XDM 비즈니스 사용자 세부 사항 스키마 필드 그룹
description: XDM 비즈니스 사용자 세부 사항 스키마 필드 그룹에 대해 알아봅니다.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# [!UICONTROL XDM 비즈니스 사용자 세부 정보] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 사용자 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) B2B(Business-to-Business) 기업의 컨텍스트에서 개별 개인에 대한 정보를 캡처합니다.

![](../../images/field-groups/business-person-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `b2b` | 오브젝트 | 사용자에 대한 B2B 관련 세부 정보를 캡처하는 객체입니다. |
| `b2b.accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 사용자와 관련된 비즈니스 계정용 복합 식별자. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 잠재 고객 전환 시 연계된 연락처에 대한 복합 식별자. |
| `b2b.personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인 또는 프로필 조각에 대한 복합 식별자. |
| `b2b.accountID` | 문자열 | 해당 사용자와 연계된 비즈니스 계정에 대한 고유 ID. |
| `b2b.blockedCause` | 문자열 | 개인이 차단되는 경우 이 속성은 그 이유를 제공합니다. |
| `b2b.convertedContactID` | 문자열 | 잠재 고객 전환 완료 시 연락처 ID. |
| `b2b.convertedDate` | DateTime | 잠재 고객 전환 완료 시 전환일. |
| `b2b.isBlocked` | 부울 | 개인의 차단 여부를 보여 줍니다. |
| `b2b.isConverted` | 부울 | 잠재 고객 전환 여부를 나타냅니다. |
| `b2b.isMarketingSuspended` | 부울 | 사용자에 대한 마케팅이 일시 중단되었는지 여부를 나타냅니다. |
| `b2b.marketingSuspendedCause` | 문자열 | 사용자에 대해 마케팅이 일시 중단된 경우 이 속성은 그 이유를 제공합니다. |
| `b2b.personGroupID` | 문자열 | 개인용 그룹 식별자. |
| `b2b.personScore` | 이중 | CRM 시스템에서 생성된 개인용 스코어. |
| `b2b.personSource` | 문자열 | 개인 정보를 받은 소스. |
| `b2b.personStatus` | 문자열 | 개인의 현재 마케팅 또는 판매 상태. |
| `b2b.personType` | 문자열 | B2B 개인 유형. |
| `extSourceSystemAudit` | [외부 소스 시스템 감사 속성](../../data-types/external-source-system-audit-attributes.md) | 비즈니스 사용자 관계가 외부 소스 시스템에서 생성되는 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `extendedWorkDetails` | 오브젝트 | 사용자에 대한 추가 작업 관련 세부 정보를 캡처합니다. |
| `extendedWorkDetails.assistantDetails` | 오브젝트 | 개인 어시스턴트와 관련된 다음 속성을 캡처합니다. <ul><li>`name`: ([개인 이름](../../data-types/person-name.md)) 어시스턴트의 전체 이름.</li><li>`phone`: ([전화 번호](../../data-types/phone-number.md)) 비서 전화번호.</li></ul> |
| `extendedWorkDetails.departments` | 문자열 배열 | 개인이 근무하는 부서 이름 목록. |
| `extendedWorkDetails.jobTitle` | 문자열 | 개인의 직함입니다. |
| `extendedWorkDetails.photoUrl` | 문자열 | 개인 사진 URL. |
| `extendedWorkDetails.reportsToID` | 문자열 | 해당 사용자의 보고 관리자에 대한 식별자. |
| `faxPhone` | [전화 번호](../../data-types/phone-number.md) | 개인의 팩스 번호입니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 사용자의 집 주소입니다. |
| `homePhone` | [전화 번호](../../data-types/phone-number.md) | 개인 집 전화번호. |
| `mobilePhone` | [전화 번호](../../data-types/phone-number.md) | 개인 휴대폰 번호. |
| `otherAddress` | [우편 주소](../../data-types/postal-address.md) | 개인용 대체 주소. |
| `otherPhone` | [전화 번호](../../data-types/phone-number.md) | 개인용 대체 전화번호. |
| `person` | [개인](../../data-types/person.md) | 개인 작업자, 연락처 또는 소유자입니다. |
| `personalEmail` | [이메일 주소](../../data-types/email-address.md) | 개인의 개인 이메일 주소입니다. |
| `workAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 회사 주소입니다. |
| `workEmail` | [이메일 주소](../../data-types/email-address.md) | 개인의 회사 이메일 주소입니다. |
| `workPhone` | [전화 번호](../../data-types/phone-number.md) | 개인 회사 전화번호. |
| `identityMap` | 맵 | 사용자에 대한 이름 공간 ID 세트가 포함된 맵 필드. 이 필드는 ID 데이터가 수집될 때 시스템에 의해 자동으로 업데이트됩니다. 이 필드를 적절하게 사용하려면 [실시간 고객 프로필](../../../profile/home.md)를 사용하여 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />에서 ID 맵에 대한 섹션을 참조하십시오. [스키마 컴포지션 기본 사항](../../schema/composition.md#identityMap) 사용 사례에 대한 자세한 내용을 보려면 여기를 클릭하십시오. |
| `isDeleted` | 부울 | 이 사용자가 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>사용 시 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md), Marketo에서 삭제된 모든 레코드는 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드가 데이터 레이크에 계속 남아 있을 수 있습니다. 설정별 `isDeleted` 끝 `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `organizations` | 문자열 배열 | 개인이 근무하는 조직 이름 목록. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
