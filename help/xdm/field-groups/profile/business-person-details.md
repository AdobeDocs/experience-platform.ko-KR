---
title: XDM 비즈니스 개인 세부 정보 스키마 필드 그룹
description: 이 문서에서는 XDM 비즈니스 개인 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 6%

---

# [!UICONTROL XDM 비즈니스 개인 세부 정보] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 개인 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 는 B2B(Business-to-Business) 기업의 컨텍스트에서 개인의 정보를 캡처합니다.

![](../../images/field-groups/business-person-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `b2b` | 오브젝트 | 사람에 대한 B2B 특정 세부 정보를 캡처하는 객체입니다. |
| `b2b.accountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인 관련 비즈니스 계정에 대한 복합 식별자입니다. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 리드가 변환된 경우 연결된 연락처에 대한 복합 식별자입니다. |
| `b2b.personKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인 또는 프로필 조각에 대한 복합 식별자입니다. |
| `b2b.accountID` | 문자열 | 이 개인이 연결된 비즈니스 계정에 대한 고유 ID입니다. |
| `b2b.blockedCause` | 문자열 | 사람이 차단되면 이 속성은 그 이유를 제공합니다. |
| `b2b.convertedContactID` | 문자열 | 리드가 성공적으로 변환된 경우 연락처 ID입니다. |
| `b2b.convertedDate` | DateTime | 리드가 성공적으로 변환된 경우 전환 날짜입니다. |
| `b2b.isBlocked` | 부울 | 개인이 차단되었는지 여부를 나타냅니다. |
| `b2b.isConverted` | 부울 | 리드가 변환되었는지 여부를 나타냅니다. |
| `b2b.isMarketingSuspended` | 부울 | 개인이 마케팅을 일시 중단할지 여부를 나타냅니다. |
| `b2b.marketingSuspendedCause` | 문자열 | 개인에 대해 마케팅이 일시 중지된 경우 이 속성은 그 이유를 제공합니다. |
| `b2b.personGroupID` | 문자열 | 개인의 그룹 식별자입니다. |
| `b2b.personScore` | 이중 | CRM 시스템에서 사용자에 대해 생성된 점수입니다. |
| `b2b.personSource` | 문자열 | 개인 정보를 받은 원본입니다. |
| `b2b.personStatus` | 문자열 | 개인의 현재 마케팅 또는 판매 상태입니다. |
| `b2b.personType` | 문자열 | B2B 사람의 유형입니다. |
| `extSourceSystemAudit` | [외부 소스 시스템 감사 속성](../../data-types/external-source-system-audit-attributes.md) | 업무 담당자 관계가 외부 소스 시스템에서 생성된 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `extendedWorkDetails` | 오브젝트 | 사람에 대한 추가 작업 관련 세부 정보를 캡처합니다. |
| `extendedWorkDetails.assistantDetails` | 오브젝트 | 개인 도우미와 관련된 다음 속성을 캡처합니다. <ul><li>`name`: ([개인 이름](../../data-types/person-name.md)) 도우미의 전체 이름입니다.</li><li>`phone`: ([전화 번호](../../data-types/phone-number.md)) 조수의 전화 번호입니다.</li></ul> |
| `extendedWorkDetails.departments` | 문자열 배열 | 개인이 근무하는 부서 이름 목록. |
| `extendedWorkDetails.jobTitle` | 문자열 | 개인의 직함입니다. |
| `extendedWorkDetails.photoUrl` | 문자열 | 사진 URL입니다. |
| `extendedWorkDetails.reportsToID` | 문자열 | 개인의 보고 관리자에 대한 식별자입니다. |
| `faxPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 팩스 전화번호입니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 집 주소입니다. |
| `homePhone` | [전화번호](../../data-types/phone-number.md) | 그 사람의 집 전화 번호입니다. |
| `mobilePhone` | [전화번호](../../data-types/phone-number.md) | 개인의 휴대폰 번호입니다. |
| `otherAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 대체 주소입니다. |
| `otherPhone` | [전화번호](../../data-types/phone-number.md) | 그 사람의 대체 전화 번호입니다. |
| `person` | [사람](../../data-types/person.md) | 개별 배우, 연락처 또는 소유자입니다. |
| `personalEmail` | [이메일 주소](../../data-types/email-address.md) | 개인의 개인 이메일 주소입니다. |
| `workAddress` | [우편 주소](../../data-types/postal-address.md) | 사람의 회사 주소입니다. |
| `workEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 회사 전자 메일 주소입니다. |
| `workPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 직장 전화 번호입니다. |
| `identityMap` | 맵 | 개인의 지정된 ID 세트가 포함된 맵 필드입니다. ID 데이터를 수집할 때 시스템에서 이 필드를 자동으로 업데이트합니다. 에 이 필드를 적절히 활용하려면 [실시간 고객 프로필](../../../profile/home.md)에서는 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />의 ID 맵에 대한 섹션을 참조하십시오. [스키마 구성 기본 사항](../../schema/composition.md#identityMap) 를 참조하십시오. |
| `isDeleted` | 부울 | 이 사람이 Marketo Engage에서 삭제되었는지 여부를 나타냅니다.<br><br>를 사용할 때 [Marketo 소스 커넥터](../../../sources/connectors/adobe-applications/marketo/marketo.md)를 입력하면 Marketo에서 삭제된 모든 레코드가 실시간 고객 프로필에 자동으로 반영됩니다. 그러나 이러한 프로필과 관련된 레코드는 여전히 Data Lake에서 유지됩니다. 설정 `isDeleted` to `true`, 필드를 사용하여 데이터 레이크를 쿼리할 때 소스에서 삭제된 레코드를 필터링할 수 있습니다. |
| `organizations` | 문자열 배열 | 개인이 근무하는 조직명 목록입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
