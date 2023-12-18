---
title: 프로필 파트너 보강(샘플) 필드 그룹
description: 프로필 파트너 보강(샘플) 스키마 필드 그룹에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 13%

---


# [!UICONTROL 프로필 파트너 보강(샘플)] 스키마 필드 그룹

[!UICONTROL 프로필 파트너 보강(샘플)] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md). 이 필드 그룹을 사용하여 고객 프로필에 파트너 중심 보강과 관련된 추가 데이터를 제공합니다.

![의 다이어그램 [!UICONTROL 프로필 파트너 보강(샘플)] 필드 그룹입니다.](../../images/field-groups/profile-partner-enrichment-sample.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 문자열 | 세대 내 연령 범위. |
| [!UICONTROL 의류 액세서리] | `apparelAccessories` | 문자열 | 의류 및 액세서리 데이터. |
| [!UICONTROL 자전거 타기] | `bicycling` | 문자열 | 자전거 관련 정보. |
| [!UICONTROL 케이블Tv] | `cableTv` | 문자열 | 케이블 TV 관련 정보. |
| [!UICONTROL 가정학] | `domestics` | 문자열 | 국내 관련 데이터. |
| [!UICONTROL 전자 제품] | `electronics` | 문자열 | 전자 제품 관련 정보. |
| [!UICONTROL 식음료] | `foodAndBeverage` | 문자열 | 음식 및 음료 데이터. |
| [!UICONTROL 신발] | `footwear` | 문자열 | 신발 관련 정보. |
| [!UICONTROL 건강 식품] | `healthFoods` | 문자열 | 건강 식품 데이터. |
| [!UICONTROL 하이킹] | `hiking` | 문자열 | 하이킹 관련 정보. |
| [!UICONTROL householdId] | `householdId` | 문자열 | 가정의 고유 ID. |
| [!UICONTROL individualId] | `individualId` | 문자열 | 개인의 고유 ID입니다. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 문자열 | 카드 소유자 정보를 유추했습니다. |
| [!UICONTROL investPremiumCardholder] | `inferredPremiumCardholder` | 문자열 | 프리미엄 카드 소지자 세부 정보 유추. |
| [!UICONTROL match수준 플래그] | `matchLevelFlag` | 문자열 | 일치 수준 플래그 데이터. |
| [!UICONTROL 구매자 평가] | `buyerRating` | 문자열 | 구매자 등급 정보. |
| [!UICONTROL DonorRating] | `donorRating` | 문자열 | 기증자 평가 세부 정보. |
| [!UICONTROL 투자 등급] | `investmentRating` | 문자열 | 투자 등급 데이터. |
| [!UICONTROL 응답기 평가] | `responderRating` | 문자열 | 응답자 등급 정보. |
| [!UICONTROL 소비 속도] | `spendingVelocity` | 문자열 | 지출 속도 세부 정보. |
| [!UICONTROL 지출 규모] | `spendingVolume` | 문자열 | 지출 규모 정보. |
| [!UICONTROL recordId] | `recordId` | 문자열 | 고유 레코드 식별자. |
| [!UICONTROL residenceId] | `residenceId` | 문자열 | 거주자에 대한 고유 ID. |
| [!UICONTROL 항해] | `sailing` | 문자열 | 항해 관련 데이터. |
| [!UICONTROL seasonalHolidayProducts] | `seasonalHolidayProducts` | 문자열 | 계절별 휴일 제품 정보. |
| [!UICONTROL 스키] | `skiing` | 문자열 | 스키 관련 데이터. |
| [!UICONTROL 테니스] | `tennis` | 문자열 | 테니스 관련 정보. |
| [!UICONTROL tvShopper] | `tvShoppers` | 문자열 | TV 쇼핑객 정보. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) 공용 XDM 저장소에서
