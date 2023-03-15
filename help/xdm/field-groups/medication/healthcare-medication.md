---
title: 헬스케어 의약품 스키마 필드 그룹
description: 이 문서에서는 헬스케어 의약품 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---

# [!UICONTROL 건강관리약] 스키마 필드 그룹

[!UICONTROL 건강관리약] 는 의 표준 스키마 필드 그룹입니다. [[!UICONTROL 약물] 클래스](../../classes/medication.md). 단일 오브젝트 유형 필드를 제공합니다 `medication` 브랜드 이름, 로트 번호 및 수량 등 세부 정보를 캡처합니다.

![](../../images/field-groups/healthcare-medication.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ingredients` | 오브젝트 배열 | 약물에 들어 있는 성분들을 열거합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`isActive`: (부울) 이 성분이 여전히 이 약물에 활발하게 사용되는지 여부를 나타냅니다.</li><li>`name`: (문자열) 재료의 이름입니다.</li><li>`quantity`: (문자열) 의약품에 포함된 성분의 수량입니다.</li></ul> |
| `brandName` | 문자열 | 약물의 브랜드 이름. |
| `codes` | 문자열 배열 | 이 의약품을 식별하는 코드 목록입니다. |
| `dosageUnitNumber` | 이중 | 약물의 용량 단위 번호입니다. |
| `dosageUnitOfMeasurement` | 문자열 | 복용량 번호에 대한 측정 단위. |
| `expiryDate` | DateTime | 약물의 유통기한. |
| `genericName` | 문자열 | 약물의 일반 이름. |
| `lotNumber` | 문자열 | 약물 배치에 대한 고유 식별자. |
| `manufacturerName` | 문자열 | 약품 제조업체의 이름. |
| `quantity` | 이중 | 포장 안에 들어 있는 약물의 양. |
| `status` | 문자열 | 약물/약물의 활성 여부를 나타내는 일반적인 상태. |
| `volume` | 이중 | 약물의 양. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
