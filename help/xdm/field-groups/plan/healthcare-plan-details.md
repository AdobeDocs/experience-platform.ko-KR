---
title: 의료 계획 세부 정보 스키마 필드 그룹
description: 이 문서에서는 의료 계획 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# [!UICONTROL 의료 계획 세부 정보] 스키마 필드 그룹

[!UICONTROL 의료 계획 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL 계획] 클래스](../../classes/plan.md). 단일 객체 유형 필드를 제공합니다 `healthcarePlanDetails` 의료 계획과 관련된 속성을 캡처합니다.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `networkDetails` | 개체 배열 | 수혜자가 치료를 받을 수 있고 &quot;네트워크 내&quot; 비율로 보상될 공급자 네트워크의 상세내역을 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`networkID`: (문자열) 네트워크에 대한 보험자별 ID입니다.</li><li>`networkName`: (문자열) 네트워크에 대한 보험자별 이름입니다.</li></ul> |
| `affiliations` | 문자열 배열 | 계획에 속한 비즈니스 업체 목록입니다. |
| `coverageType` | 문자열 | 제도 적용 범위 유형입니다. 허용되는 값은 다음과 같습니다.<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 부울 | 계획이 활성 상태인지 여부를 나타냅니다. |
| `lastVerificationDate` | DateTime | 계획이 마지막으로 확인된 날짜입니다. |
| `payerID` | 문자열 | 지급자에 대한 고유 식별자(즉, 계획에 대한 보험 공급자). |
| `planLevel` | 문자열 | 계획 레벨을 나타냅니다. 허용되는 값은 다음과 같습니다.<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 문자열 | 계획 유형을 나타냅니다. 허용되는 값은 다음과 같습니다.<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 문자열 | 계획이 적용되는 소유자 유형입니다. 예를 들면 개인, 그룹, 조직 등이 있습니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
