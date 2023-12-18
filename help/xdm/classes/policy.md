---
title: 정책 클래스
description: XDM(경험 데이터 모델)의 정책 클래스에 대해 알아봅니다.
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 4%

---

# [!UICONTROL 정책] 클래스

XDM(경험 데이터 모델)에서 [!UICONTROL 정책] 클래스는 보험 증서를 정의하는 최소 속성 세트를 캡처합니다.

![](../images/classes/policy.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `assignedBeneficiary` | 배열 [[!UICONTROL 개인]](../data-types/person.md) 데이터 유형 | 정책에 할당된 수취인(또는 수취인)을 캡처합니다. |
| `benefitAmount` | [[!UICONTROL 통화]](../data-types/currency.md) | 약관에 따라 지급할 금액. |
| `location` | [[!UICONTROL 우편 주소]](../data-types/postal-address.md) | 보험 증서가 발급된 위치입니다. |
| `owner` | [!UICONTROL 오브젝트] | 정책 소유자의 프로필 정보를 캡처합니다. |
| `owner.faxPhone` | [[!UICONTROL 전화 번호]](../data-types/phone-number.md) | 소유자의 팩스 번호입니다. |
| `owner.homeAddress` | [[!UICONTROL 우편 주소]](../data-types/postal-address.md) | 소유자의 집 주소입니다. |
| `owner.homePhone` | [[!UICONTROL 전화 번호]](../data-types/phone-number.md) | 집주인의 집 전화번호. |
| `owner.mobilePhone` | [[!UICONTROL 전화 번호]](../data-types/phone-number.md) | 소유자의 휴대폰 번호입니다. |
| `owner.personalEmail` | [[!UICONTROL 이메일 주소]](../data-types/email-address.md) | 소유자의 개인 이메일 주소입니다. |
| `ID` | [!UICONTROL 문자열] | 보험 증서에 대한 식별자. |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터 수집 중에 명시적 값을 제공하지 않습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `endDate` | [!UICONTROL DateTime] | 보험 적용이 종료되는(또는 종료되는) 날짜. |
| `hasAssignedBeneficiary` | [!UICONTROL 부울] | 정책에 수취인이 할당되었는지 여부를 나타냅니다. |
| `name` | [!UICONTROL 문자열] | 보험 증서의 이름. |
| `startDate` | [!UICONTROL DateTime] | 보험 적용이 시작되는(또는 시작되는) 날짜. |
| `type` | [!UICONTROL 문자열] | 집, 자동차, 임차인 또는 보트 등 보험 증권 유형. |

{style="table-layout:auto"}
