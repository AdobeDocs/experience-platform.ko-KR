---
title: 의료 서비스 플랜 세부 정보 스키마 필드 그룹
description: 의료 서비스 플랜 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL 의료 서비스 플랜 세부 정보] 스키마 필드 그룹

[!UICONTROL 의료 서비스 플랜 세부 정보]은(는) [[!UICONTROL 플랜] 클래스](../../classes/plan.md)의 표준 스키마 필드 그룹입니다. 의료 계획과 관련된 속성을 캡처하는 단일 개체 유형 필드 `healthcarePlanDetails`을(를) 제공합니다.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `networkDetails` | 오브젝트 배열 | 수혜자가 치료를 요청할 수 있는 공급자의 보험사가 정의한 네트워크에 대한 세부 정보를 나열하며 &quot;네트워크 내&quot; 요율로 보장됩니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`networkID`: (문자열) 네트워크에 대한 보험자별 ID입니다.</li><li>`networkName`: (문자열) 네트워크에 대한 보험자별 이름입니다.</li></ul> |
| `affiliations` | 문자열 배열 | 플랜과 연계된 비즈니스 엔티티 목록. |
| `coverageType` | 문자열 | 제도 수혜범위 유형. 허용되는 값은 다음과 같습니다.<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 부울 | 플랜이 활성 상태인지 여부를 나타냅니다. |
| `lastVerificationDate` | 날짜/시간 | 플랜이 마지막으로 확인된 날짜. |
| `payerID` | 문자열 | 지급자(즉, 제도에 대한 보험 공급자)에 대한 고유 식별자. |
| `planLevel` | 문자열 | 계획 레벨을 나타냅니다. 허용되는 값은 다음과 같습니다.<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 문자열 | 계획 유형을 나타냅니다. 허용되는 값은 다음과 같습니다.<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 문자열 | 플랜이 사용되는 소유자 유형입니다. 예를 들면 개인, 그룹, 조직 등이 있습니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json)를 참조하세요.
