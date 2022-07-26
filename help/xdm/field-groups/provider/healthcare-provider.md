---
title: 의료 기관 스키마 필드 그룹
description: 이 문서에서는 Healthcare Provider 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# [!UICONTROL 의료 기관] 스키마 필드 그룹

[!UICONTROL 의료 기관] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL 공급자] 클래스](../../classes/provider.md). 단일 객체 유형 필드를 제공합니다 `healthcareProvider` 이 단체는 보건진료 서비스를 제공할 수 있는 허가를 받은 개인 건강 전문가 또는 건강 시설 조직과 관련된 속성을 캡처합니다.

![](../../images/field-groups/healthcare-provider.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `addressDetails` | 개체 배열 | 공급자의 주소 세부 정보를 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`address`: ([[!UICONTROL 우편 주소]](../../data-types/postal-address.md)): 공급자의 우편 주소입니다.</li><li>`addressType`: (문자열) 공급자가 서비스를 제공하는 위치를 나타내는 주소 유형입니다.</li></ul> |
| `emailAddress` | [[!UICONTROL 이메일 주소]](../../data-types/email-address.md) | 공급자의 전자 메일 주소입니다. |
| `fax` | [[!UICONTROL 전화번호]](../../data-types/phone-number.md) | 공급자의 팩스 번호입니다. |
| `phoneNumber` | [[!UICONTROL 전화번호]](../../data-types/phone-number.md) | 공급자의 전화 번호입니다. |
| `qualifications` | 개체 배열 | 관리 서비스와 관련된 인증, 라이센스 또는 교육을 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`issuer`: ([[!UICONTROL 계정 세부 사항]](../../data-types/account-details.md)): 자격을 규율하고 발급하는 기관입니다.</li><li>`activePeriod`: (정수) 자격이 유효한 연도입니다.</li><li>`code`: (문자열) 자격을 코딩한 표현입니다.</li></ul> |
| `classification` | 문자열 | 클래스 또는 카테고리(예: 환자 지원, 비환자 지원 등)를 기반으로 한 서비스 공급자 분류 |
| `isActive` | 부울 | 공급자가 활성 상태인지 여부를 나타냅니다. |
| `languages` | 문자열 배열 | 공급자가 작업을 수행하는 언어 목록입니다. |
| `practiceGroupName` | 문자열 | 서비스 공급자의 연습 그룹 이름입니다. |
| `practiceGroupType` | 문자열 | 서비스 공급자에 대한 연습 그룹 유형입니다. |
| `practiceType` | 문자열 | 서비스 공급자에 대한 연습 유형입니다. |
| `specialties` | 문자열 배열 | 이 공급자가 제공하는 특별 서비스 목록입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
