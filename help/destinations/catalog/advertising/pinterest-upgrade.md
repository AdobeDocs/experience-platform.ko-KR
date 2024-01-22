---
title: 새 API로 pinterest 대상 마이그레이션. 고객 조치가 필요합니다.
description: Pinterest은 현재 Real-Time CDP의 Pinterest 대상에서 사용 중인 v4 advertiser API를 더 이상 사용하지 않습니다. pinterest 캠페인을 중단하지 않고 새 API로 원활하게 전환하기 위해 작업 항목을 이해합니다.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Pinterest 대상을 새 API로 업그레이드합니다. 2024년 1월 18일까지 고객 조치 필요.

>[!IMPORTANT]
>
>이 페이지의 고객 작업 항목은 조직이 새로운 날짜인 2023년 11월 16일 이전에 데이터를 Pinterest으로 내보내도록 데이터 흐름을 설정한 경우 적용됩니다 **[!UICONTROL Pinterest]** 최신 Pinterest API를 사용하는 대상이 대상 카탈로그에 추가되었습니다.

## 현재 상황

Pinterest은 에서 사용하던 v4 advertiser API를 더 이상 사용하지 않습니다. [Pinterest 대상](/help/destinations/catalog/advertising/pinterest.md) Real-Time CDP. Adobe이 대상을 업데이트하여 사용 [v5 광고주 API](https://developers.pinterest.com/docs/getting-started/migration/). pinterest 캠페인을 중단하지 않고 새 API로 원활하게 전환하기 위해 작업 항목을 이해하려면 이 페이지를 참조하십시오.

## 나에게 알림을 보내는 이유

pinterest에 대한 대상을 활성화할 수 있는 활성 데이터 흐름이 있는 것으로 조직에 확인되었습니다.

## 계획이 뭐야?

Adobe은 Pinterest API v5를 활용하고 새 연결에서 기존 데이터 흐름을 유지하는 새로운 Pinterest 대상 카드를 발표했습니다.

## 활성화된 대상이 계속 작동하도록 하려면 어떤 작업을 수행해야 합니까?

예. 2024년 1월 18일 이전에 Real-Time CDP에서 Pinterest 광고주 계정을 사용하여 새 Pinterest 대상을 인증해야 합니다. 자세한 지침은 아래에 나와 있습니다.

### pinterest 재인증 {#reauthenticate}

1. 다음으로 이동 **[!UICONTROL 대상 > 계정]** 화면의 필터를 사용하여 Pinterest 대상만 필터링합니다.
   ![pinterest 계정만 필터링](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 다음에서 **Pinterest** 대상, 세 점 기호 ... 를 선택한 다음 를 선택합니다. **[!UICONTROL 세부 정보 편집]**.
   ![세부 정보 편집 선택](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 선택 **[!UICONTROL OAuth에 다시 연결]** pinterest 계정에 로그인합니다.
   ![다시 연결 OAuth 선택](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 아래 섹션의 작업 항목으로 이동

### 새 대상에 대한 흐름 활성화 {#disable-old-enable-new-flows}

그런 다음 새 항목에 대한 데이터 흐름을 활성화해야 합니다  **[!UICONTROL Pinterest]** 카드.

1. 다음으로 이동 **[!UICONTROL 대상 > 찾아보기]** 화면의 필터를 사용하여 **[!UICONTROL Pinterest]** 대상만.
   ![찾아보기 탭에서만 Pinterest 데이터 흐름 필터링](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 에 대한 하이퍼링크가 연결된 연결 이름(위의 스크린샷 예에서 로열티 캠페인)을 선택합니다. **[!UICONTROL Pinterest]** 대상 및 전환 **[!UICONTROL 사용]** 전환 대상 **날짜**.
   ![새 연결에 대해 켜기/끄기, 이전 연결에 대해 끄기](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## 높은 수준의 타임라인을 공유할 수 있습니까?

예, 아래를 참조하십시오.

**2023년 11월 16일까지**: 새 대상이 준비되었으며 Pinterest이 이전 v4 API에 대한 지원을 중단할 때까지 카탈로그에 Pinterest 카드 2개가 나란히 표시되어야 합니다. 현재 Pinterest 카드에 대한 기존 데이터 흐름이 모두 새 대상에 복사됩니다.

![이전 및 새로운 Pinterest 대상 나란히](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**2023년 12월 15일까지**: <span class="preview">고객 작업 1</span>. 새 카드가 Pinterest에 연결되도록 Pinterest에 다시 인증해야 합니다. 에서 전체 지침 보기 [이 섹션](#reauthenticate).

<span class="preview">고객 작업 2</span>.그런 다음 새 카드에서 데이터 흐름을 활성화해야 합니다. 에서 전체 지침 보기 [이 섹션](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**2024년 1월 18일 이후**: <span class="preview">Pinterest이 V4 광고주 API에 대한 액세스를 해제했습니다. 새 대상으로 업그레이드하지 않은 모든 Real-Time CDP 고객은 이제 Pinterest 대상으로의 데이터 흐름이 실패했음을 알게 됩니다. [pinterest 재인증](#reauthenticate) 및 [데이터 흐름 활성화](#disable-old-enable-new-flows) 캠페인을 Pinterest으로 다시 시작하기 위해 업그레이드된 대상으로 설정합니다.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
