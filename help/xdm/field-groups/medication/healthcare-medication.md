---
title: 의료 치료 스키마 필드 그룹
description: 이 문서에서는 의료 약제 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 6%

---

# [!UICONTROL 의료용 약물] 스키마 필드 그룹

[!UICONTROL 의료용 약물] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL 약물] 클래스](../../classes/medication.md). 단일 객체 유형 필드를 제공합니다 `medication` 브랜드 이름, 로트 번호 및 수량과 같은 상세내역을 캡처합니다.

![](../../images/field-groups/healthcare-medication.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ingredients` | 개체 배열 | 약물에 들어 있는 재료를 나열합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`isActive`: (부울) 이 성분이 이 약물에 여전히 활성 상태인지 여부를 나타냅니다.</li><li>`name`: (문자열) 재료 이름입니다.</li><li>`quantity`: (문자열) 약제에 함유된 성분의 수량</li></ul> |
| `brandName` | 문자열 | 그 약의 상표명. |
| `codes` | 문자열 배열 | 이 약물을 식별하는 코드 목록입니다. |
| `dosageUnitNumber` | 이중 | 약물의 제단위번호. |
| `dosageUnitOfMeasurement` | 문자열 | 제제번호의 측정단위 |
| `expiryDate` | DateTime | 약물의 만료 날짜. |
| `genericName` | 문자열 | 약물의 일반 이름. |
| `lotNumber` | 문자열 | 약품 배치에 대한 고유 식별자입니다. |
| `manufacturerName` | 문자열 | 약품 제조업자의 이름입니다. |
| `quantity` | 이중 | 패키지 안에 있는 약물의 양. |
| `status` | 문자열 | 약물/약물 투여 시 활성 여부를 나타내는 일반적인 상태. |
| `volume` | 이중 | 약물의 양. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
