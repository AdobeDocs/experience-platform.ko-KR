---
title: 의료 서비스 공급자 스키마 필드 그룹
description: 의료 공급자 스키마 필드 그룹에 대해 알아봅니다.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!UICONTROL 의료 기관] 스키마 필드 그룹

[!UICONTROL 의료 기관] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL 공급자] 클래스](../../classes/provider.md). 단일 오브젝트 유형 필드를 제공합니다 `healthcareProvider` 이는 의료 서비스 진단 및 치료 서비스를 제공하도록 라이선스를 받은 개인 의료 전문가 또는 의료 시설 조직과 관련된 속성을 캡처합니다.

![](../../images/field-groups/healthcare-provider.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `addressDetails` | 오브젝트 배열 | 공급자의 주소 세부 정보를 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`address`: ([[!UICONTROL 우편 주소]](../../data-types/postal-address.md)): 공급자의 우편 주소.</li><li>`addressType`: (문자열) 공급자가 서비스를 제공하는 위치를 나타내는 주소 유형입니다.</li></ul> |
| `emailAddress` | [[!UICONTROL 이메일 주소]](../../data-types/email-address.md) | 공급자의 이메일 주소입니다. |
| `fax` | [[!UICONTROL 전화 번호]](../../data-types/phone-number.md) | 공급자의 팩스 번호입니다. |
| `phoneNumber` | [[!UICONTROL 전화 번호]](../../data-types/phone-number.md) | 공급자의 전화번호. |
| `qualifications` | 오브젝트 배열 | 서비스 제공과 관련된 인증, 라이선스 또는 교육을 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`issuer`: ([[!UICONTROL 계정 세부 정보]](../../data-types/account-details.md)): 자격을 규제하고 발급하는 조직입니다.</li><li>`activePeriod`: (정수) 자격이 유효할 연도입니다.</li><li>`code`: (문자열) 자격의 코딩된 표현입니다.</li></ul> |
| `classification` | 문자열 | 분류 또는 범주(예: 환자 진료, 비환자 진료 등)를 기준으로 서비스 제공업체를 분류합니다. |
| `isActive` | 부울 | 공급자가 활성 상태인지 여부를 나타냅니다. |
| `languages` | 문자열 배열 | 공급자가 작업을 수행하는 언어 목록입니다. |
| `practiceGroupName` | 문자열 | 서비스 공급자의 연습 그룹 이름입니다. |
| `practiceGroupType` | 문자열 | 서비스 공급자에 대한 서비스 그룹 유형입니다. |
| `practiceType` | 문자열 | 서비스 공급자에 대한 연습 유형입니다. |
| `specialties` | 문자열 배열 | 해당 공급자가 제공하는 특별 혜택 목록. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
