---
title: 정책 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 정책 클래스에 대한 개요를 제공합니다.
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 8%

---

# [!UICONTROL 정책] 클래스

XDM(Experience Data Model)에서 [!UICONTROL 정책] 클래스는 보험 정책을 정의하는 최소 속성 집합을 캡처합니다.

![](../images/classes/policy.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `assignedBeneficiary` | 배열 [[!UICONTROL 개인]](../data-types/person.md) 데이터 유형 | 정책에 지정된 수혜자(또는 수혜자)를 캡처합니다. |
| `benefitAmount` | [[!UICONTROL 통화]](../data-types/currency.md) | 정책 조건에 따라 지불할 금액입니다. |
| `location` | [[!UICONTROL 우편 주소]](../data-types/postal-address.md) | 보험 증권 발급 위치. |
| `owner` | [!UICONTROL 개체] | 정책 소유자의 프로필 정보를 캡처합니다. |
| `owner.faxPhone` | [[!UICONTROL 전화번호]](../data-types/phone-number.md) | 소유자의 팩스 전화 번호입니다. |
| `owner.homeAddress` | [[!UICONTROL 우편 주소]](../data-types/postal-address.md) | 소유자의 집 주소입니다. |
| `owner.homePhone` | [[!UICONTROL 전화번호]](../data-types/phone-number.md) | 주인의 집 전화 번호입니다. |
| `owner.mobilePhone` | [[!UICONTROL 전화번호]](../data-types/phone-number.md) | 소유자의 휴대폰 번호입니다. |
| `owner.personalEmail` | [[!UICONTROL 이메일 주소]](../data-types/email-address.md) | 소유자의 개인 이메일 주소입니다. |
| `ID` | [!UICONTROL 문자열] | 보험 증권의 식별자입니다. |
| `_id` | [!UICONTROL 문자열] | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터의 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템이 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원할 경우 여전히 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| `endDate` | [!UICONTROL DateTime] | 보험 가입 종료(또는 종료)일 |
| `hasAssignedBeneficiary` | [!UICONTROL 부울] | 정책이 수혜자를 지정했는지 여부를 나타냅니다. |
| `name` | [!UICONTROL 문자열] | 보험 증권의 이름입니다. |
| `startDate` | [!UICONTROL DateTime] | 보험 가입 시작(또는 시작)일. |
| `type` | [!UICONTROL 문자열] | 주택, 자동차, 렌터 또는 보트와 같은 보험 정책의 유형. |

{style=&quot;table-layout:auto&quot;}
