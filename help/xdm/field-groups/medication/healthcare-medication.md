---
title: 헬스케어 의약품 스키마 필드 그룹
description: 의료 서비스 약물 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL 의료 의약품] 스키마 필드 그룹

[!UICONTROL 의료 의약품]은(는) [[!UICONTROL 의약품] 클래스](../../classes/medication.md)의 표준 스키마 필드 그룹입니다. 브랜드 이름, 로트 번호 및 수량 등의 세부 정보를 캡처하는 단일 개체 유형 필드 `medication`을(를) 제공합니다.

![](../../images/field-groups/healthcare-medication.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `ingredients` | 오브젝트 배열 | 약물에 들어 있는 성분들을 열거합니다. 각 객체에는 다음 속성이 포함됩니다. <ul><li>`isActive`: (부울) 이 성분이 여전히 이 약에서 활발하게 사용되고 있는지 여부를 나타냅니다.</li><li>`name`: (문자열) 재료의 이름입니다.</li><li>`quantity`: (문자열) 의약품에 있는 성분의 수량입니다.</li></ul> |
| `brandName` | 문자열 | 약물의 브랜드 이름. |
| `codes` | 문자열 배열 | 이 의약품을 식별하는 코드 목록입니다. |
| `dosageUnitNumber` | 더블 | 약물의 용량 단위 번호입니다. |
| `dosageUnitOfMeasurement` | 문자열 | 복용량 번호에 대한 측정 단위. |
| `expiryDate` | 날짜/시간 | 약물의 유통기한. |
| `genericName` | 문자열 | 약물의 일반 이름. |
| `lotNumber` | 문자열 | 약물 배치에 대한 고유 식별자. |
| `manufacturerName` | 문자열 | 약품 제조업체의 이름. |
| `quantity` | 더블 | 포장 안에 들어 있는 약물의 양. |
| `status` | 문자열 | 약물/약물의 활성 여부를 나타내는 일반적인 상태. |
| `volume` | 더블 | 약물의 양. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json)를 참조하세요.
