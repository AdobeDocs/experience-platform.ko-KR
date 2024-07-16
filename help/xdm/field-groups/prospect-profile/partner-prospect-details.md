---
title: Partner Prospect Details(샘플) 필드 그룹
description: Partner Prospect Details (Sample) 필드 그룹 (XDM) 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL 파트너 잠재 고객 세부 정보(샘플)] 필드 그룹

[!UICONTROL 파트너 잠재 고객 세부 정보(샘플)]은(는) [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)에 대한 표준 스키마 필드 그룹입니다. [!UICONTROL Partner Prospect Details(샘플)]은(는) Prospect의 프로필과 관련된 다양한 세부 정보에 대한 샘플 프레임워크를 제공합니다. 이 프레임워크를 통해 다양한 잠재 고객 관련 정보를 구성하고 관리하는 프로세스를 간소화할 수 있습니다.

이 필드 그룹은 [개별 잠재 고객 프로필 클래스](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html)를 파트너의 컨텍스트에서 확장합니다.

![[!UICONTROL 파트너 잠재 고객 세부 정보(샘플)] 필드 그룹의 다이어그램입니다.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 문자열 | 세대 내 연령 범위. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | 문자열 | 의류/액세서리에 대한 선호도 또는 참여. |
| [!UICONTROL 자전거 타기] | `bicycling` | 문자열 | 자전거 타기에 대한 관심 또는 참여. |
| [!UICONTROL cableTv] | `cableTv` | 문자열 | 케이블 TV와의 관계를 나타냅니다. |
| [!UICONTROL 국내] | `domestics` | 문자열 | 국내 활동의 환경 설정 또는 참여 |
| [!UICONTROL 전자 제품] | `electronics` | 문자열 | 전자 장치에 대한 관심 또는 참여. |
| [!UICONTROL 음식 및 음료] | `foodAndBeverage` | 문자열 | 음식/음료에 대한 선호도 또는 관여. |
| [!UICONTROL 신발] | `footwear` | 문자열 | 신발에 대한 관심 또는 관여. |
| [!UICONTROL 건강식품] | `healthFoods` | 문자열 | 건강 식품에 대한 선호도 또는 참여. |
| [!UICONTROL 하이킹] | `hiking` | 문자열 | 하이킹 활동에 대한 관심 또는 참여 |
| [!UICONTROL householdId] | `householdId` | 문자열 | 세대에 대한 고유 식별자. |
| [!UICONTROL 개별 ID] | `individualId` | 문자열 | 개인에 대한 고유 식별자. |
| [!UICONTROL referredCardHolder] | `inferredCardHolder` | 문자열 | 카드 소지자가 된다는 추론. |
| [!UICONTROL referredPremiumCardholder] | `inferredPremiumCardholder]` | 문자열 | 프리미엄 카드 소지자라는 추론. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 문자열 | 일치 수준의 지표. |
| [!UICONTROL 구매자 평가] | `buyerRating` | 문자열 | 구매 행동과 관련된 등급입니다. |
| [!UICONTROL DonorRating] | `donorRating` | 문자열 | 기증자 행동과 관련된 등급. |
| [!UICONTROL 투자 평가] | `investmentRating` | 문자열 | 투자 행위와 관련된 등급입니다. |
| [!UICONTROL 응답기 평가] | `responderRating` | 문자열 | 응답자 동작과 관련된 등급입니다. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | 문자열 | 지출 속도 또는 비율. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | 문자열 | 지출액 또는 양. |
| [!UICONTROL recordId] | `recordId` | 문자열 | 레코드에 대한 고유 식별자. |
| [!UICONTROL residenceId] | `residenceId` | 문자열 | 거주지에 대한 고유 식별자. |
| [!UICONTROL 항해] | `sailing` | 문자열 | 항해 활동에 대한 관심 또는 개입을 나타냅니다. |
| [!UICONTROL seasonalHolidayProducts] | `seasonalHolidayProducts` | 문자열 | 휴일 제품에 대한 환경 설정 또는 관여를 나타냅니다. |
| [!UICONTROL 스키] | `skiing` | 문자열 | 스키 활동에 대한 관심 또는 개입을 나타냅니다. |
| [!UICONTROL 테니스] | `tennis` | 문자열 | 테니스 활동에 대한 관심 또는 개입을 나타냅니다. |
| [!UICONTROL tvShoppers] | `tvShoppers` | 문자열 | TV 쇼핑에 참여했음을 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소의 [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json)을(를) 참조하십시오.
