---
title: Talon.One Source 개요
description: Adobe Experience Platform의 Talon.One 소스에 대해 알아보기
badge: Beta
last-substantial-update: 2026-04-06T00:00:00Z
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: f3026e0a717c07d95f12e3aeaf380ddc1b87c712
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>[!DNL Talon.One] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../home.md#terms-and-conditions)을 참조하십시오.

[!DNL Talon.One]을(를) 사용하면 고객에 맞는 개인화된 마케팅 캠페인을 쉽게 만들고, 관리하고, 최적화할 수 있습니다. 이 강력한 플랫폼을 사용하여 할인을 실행하고, 쿠폰을 배포하고, 추천 프로그램을 시작하고, 충성도 프로그램을 설정하고, 게임화된 인센티브를 제공할 수 있습니다. 이 모든 인센티브는 대상자를 참여시키고 보상하도록 설계된 확장 가능한 하나의 시스템입니다.

Adobe Experience Platform 소스 카탈로그의 [!DNL Talon.One] 소스를 사용하여 [!DNL Talon.One] 계정에서 일괄 처리 및 스트리밍 충성도 데이터를 모두 수집할 수 있습니다.

* [Talon.One 스트리밍 이벤트](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One 일괄 처리 Source 커넥터](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>충성도 데이터는 충성도 포인트, 사용된 충성도 포인트, 현재 계층, 부여된 쿠폰, 참조 및 성과와 같은 최종 사용자의 충성도 프로그램 정보를 나타냅니다.

## 전제 조건 {#prerequisites}

[!DNL Talon.One Batch Source Connector]을(를) 인증하고 연결하려면 다음 자격 증명의 값을 제공하십시오.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 도메인 | [!DNL Talon.One] 응용 프로그램 환경과 연결된 고유한 URL입니다. 도메인을 입력할 때 프로토콜이나 경로를 포함하지 않아야 합니다. | `acmetalonone.us-east4` |
| [!DNL Talon.One] 관리 API 키 | 관리 API 키는 [!DNL Talon.One]의 관리 API에 대한 액세스를 인증하고 권한을 부여하는 데 사용되는 자격 증명입니다. 다음과 같은 작업을 처리합니다. <ul><li>쿠폰 가져오는 중</li><li>캠페인 데이터 검색 중</li><li>애플리케이션 및 엔드포인트 관리</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## 매핑 {#mapping}

고유한 `effectType` 값을 기반으로 각 효과 개체를 매핑하기 위해 데이터 준비 `array_to_map` 함수를 사용할 수 있습니다. 이렇게 하면 순서가 지정되지 않은 효과 배열을 요구 사항과 일치하는 키-값 쌍으로 쉽게 변환할 수 있습니다. 지침은 아래 예를 참조하십시오.

또한 Adobe에서 제공하는 표준화된 충성도 필드 그룹을 사용하여 충성도 프로그램 개념을 일관된 방식으로 모델링할 수도 있습니다.

>[!BEGINTABS]

>[!TAB 충성도 세부 정보]

이벤트 데이터가 아닌 레코드 속성을 캡처하여 개인의 충성도 멤버십 상태를 설명하는 데 사용되는 XDM 개인 프로필용 표준 XDM 필드 그룹입니다. 프로필 스키마에서 이 필드 그룹을 사용하여 다음을 캡처합니다.

* **회원이 프로그램에 있는 사용자**(`loyaltyID`, `program`, `status`, `tier`)
* **현재 및 라이프타임 잔액**(`points`, `lifetimePoints`, `expiredPoints` 등)
* 키 **멤버십 날짜**(`joinDate`, `upgradeDate`, `tierExpiryDate`)

>[!TAB 충성도 이벤트 세부 정보]

충성도 이벤트 세부 정보 필드 그룹은 특정 거래에서 획득하거나 상환한 포인트와 같은 이벤트 수준에서 충성도 활동을 캡처하도록 설계되었습니다. 이 필드 그룹에는 `xdm:points`, `xdm:pointsRedeemed`, `xdm:pointsAsOfDate` 및 `xdm:program` 등의 필드가 포함되어 있습니다. 경험 이벤트 스키마에서 이 이벤트 수준 필드 그룹을 사용하여 다음을 캡처합니다.

* **이벤트당 이동** 포인트(획득, 보상, 만료)
* 충성도 쿠폰 또는 추천으로 인해 발생한 **할인**
* 충성도 공급자와의 조정을 위한 **프로그램 ID** 및 거래 ID.

>[!ENDTABS]

| 소스 | 대상 |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## 다음 단계

[!DNL Talon.One] 계정을 Experience Platform에 연결하고 일괄 처리 및 스트리밍 로열티 데이터를 모두 수집하는 방법에 대해 알아보려면 다음 설명서를 참조하십시오.

* [Talon.One 스트리밍 이벤트](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One 일괄 처리 Source 커넥터](../../tutorials/ui/create/loyalty/talon-one-batch.md)
