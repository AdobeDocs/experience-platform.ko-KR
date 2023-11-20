---
title: 새 API로 pinterest 대상 마이그레이션. 고객 조치가 필요합니다.
description: Pinterest은 현재 Real-Time CDP의 Pinterest 대상에서 사용 중인 v4 advertiser API를 더 이상 사용하지 않습니다. pinterest 캠페인을 중단하지 않고 새 API로 원활하게 전환하기 위해 작업 항목을 이해합니다.
hide: true
hidefromtoc: true
source-git-commit: 57097b785da3b516b5ce6670c0a376bd1d0fe479
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Pinterest 대상을 새 API로 업그레이드합니다. 2023년 12월 15일까지 고객 조치 필요

>[!IMPORTANT]
>
>이 페이지의 고객 작업 항목은 조직이 다음 날짜인 2023년 11월 16일 이전에 데이터를 Pinterest으로 내보내도록 데이터 흐름을 설정한 경우 적용됩니다. **[!UICONTROL (새로운 기능) Pinterest]** 최신 Pinterest API를 사용하는 대상이 대상 카탈로그에 추가되었습니다.

## 현재 상황

Pinterest은 현재 이 사용하는 v4 advertiser API를 더 이상 사용하지 않습니다. [Pinterest 대상](/help/destinations/catalog/advertising/pinterest.md) Real-Time CDP. Adobe이 Pinterest에서 작업 중이며 대상을 업데이트하여 사용 중 [v5 광고주 API](https://developers.pinterest.com/docs/getting-started/migration/). pinterest 캠페인을 중단하지 않고 새 API로 원활하게 전환하기 위해 작업 항목을 이해하려면 이 페이지를 참조하십시오.

## 나에게 알림을 보내는 이유

pinterest에 대한 대상을 활성화할 수 있는 활성 데이터 흐름이 있는 것으로 조직에 확인되었습니다.

## 계획이 뭐야?

Adobe은 Pinterest API v5를 활용하고 새 연결에서 기존 데이터 흐름을 유지하는 새로운 Pinterest 대상 카드를 출시합니다.

## 활성화된 대상이 계속 작동하도록 하려면 어떤 작업을 수행해야 합니까?

예. 2023년 11월 16일 이후에는 Real-Time CDP에서 Pinterest 광고주 계정을 사용하여 새 Pinterest 대상을 인증해야 합니다. 자세한 지침은 아래에 나와 있습니다.

### pinterest 재인증 {#reauthenticate}

1. 다음으로 이동 **[!UICONTROL 대상 > 계정]** 화면의 필터를 사용하여 Pinterest 대상만 필터링합니다.
   ![pinterest 계정만 필터링](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 다음에서 **(새로운 기능) Pinterest** 대상, 세 점 기호 ... 를 선택한 다음 를 선택합니다. **[!UICONTROL 세부 정보 편집]**.
   ![세부 정보 편집 선택](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 선택 **[!UICONTROL OAuth에 다시 연결]** pinterest 계정에 로그인합니다.
   ![다시 연결 OAuth 선택](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 아래 섹션의 작업 항목으로 이동

### 기존 대상에 대한 기존 흐름을 비활성화하고 새 대상에 대한 흐름을 활성화합니다. {#disable-old-enable-new-flows}

그런 다음 이전 대상 카드에 대한 기존 흐름을 수동으로 비활성화해야 합니다 **[!UICONTROL (사용 중단) Pinterest]** 새 카드에 대한 플로우 활성화 **[!UICONTROL (새로운 기능) Pinterest]**.

1. 다음으로 이동 **[!UICONTROL 대상 > 찾아보기]** 화면의 필터를 사용하여 **[!UICONTROL (새로운 기능) Pinterest]** 및 **[!UICONTROL (사용 중단) Pinterest]** 대상만 해당.
   ![찾아보기 탭에서만 Pinterest 데이터 흐름 필터링](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 에 대한 하이퍼링크가 연결된 연결 이름(위의 스크린샷 예에서 로열티 캠페인)을 선택합니다. **[!UICONTROL (사용 중단) Pinterest]** 대상 및 전환 **[!UICONTROL 사용]** 전환 대상 **끔**.
   ![새 연결에 대해 켜기/끄기, 이전 연결에 대해 끄기](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-old-destination.png)
3. 에 대한 하이퍼링크가 연결된 연결 이름(위의 스크린샷 예에서 로열티 캠페인)을 선택합니다. **[!UICONTROL (새로운 기능) Pinterest]** 대상 및 전환 **[!UICONTROL 사용]** 전환 대상 **날짜**.
   ![새 연결에 대해 켜기/끄기, 이전 연결에 대해 끄기](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)
4. 이전 및 새 데이터 흐름에서 활성화된 대상 목록을 비교하고, 새 흐름에서 누락된 이전 흐름의 새 대상이 없는지 확인합니다.

캠페인이 중단되지 않을 것으로 예상되지만, 모든 것이 예상대로 작동하는지 Pinterest UI에서 확인해야 합니다.

## 높은 수준의 타임라인을 공유할 수 있습니까?

예, 아래를 참조하십시오.

**2023년 11월 16일까지**: 새 대상이 준비되었습니다. 카탈로그에 Pinterest 카드 2개가 나란히 표시되고 현재 Pinterest 카드에 대한 기존 데이터 흐름이 모두 새 대상에 복사됩니다.

![이전 및 새로운 Pinterest 대상 나란히](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>2023년 11월 16일 이후에는 기존 Pinterest 대상이 표시됩니다 **[!UICONTROL 사용 중단]**. <span class="preview">11월 16일 이후 (사용하지 않는) Pinterest 대상에 대한 데이터 흐름의 모든 변경 사항은 다음과 같습니다 *아님* 새 Pinterest 대상으로 자동으로 이월됩니다. </span>
>예를 들어 *추천하지 않음* 11월 16일 이후에 이전 대상에 대해 새 대상을 활성화합니다. 그렇게 하면 다음을 따라야 합니다. [일반 활성화 단계](/help/destinations/ui/activate-segment-streaming-destinations.md) 고객 작업이 수행된 후 대상을 새 대상에 추가하는 작업.

**2023년 12월 15일까지**: <span class="preview">고객 작업 1</span>. 새 카드가 Pinterest에 연결되도록 Pinterest에 다시 인증해야 합니다. 에서 전체 지침 보기 [이 섹션](#reauthenticate).

<span class="preview">고객 작업 2</span>.그런 다음 이전 카드에서 Pinterest에 대한 데이터 흐름을 비활성화하고 새 카드에서 데이터 흐름을 활성화해야 합니다. 에서 전체 지침 보기 [이 섹션](#disable-old-enable-new-flows).

>[!IMPORTANT]
>
>2023년 12월 15일 이후 Adobe은 이전 데이터흐름의 무결성을 보장하지 않습니다 **[!UICONTROL (사용 중단) Pinterest]** 대상.

## 참고할 기타 항목

새 대상 카드에서 데이터 흐름을 활성화하고 이전 대상 카드에서 데이터 흐름을 비활성화하면 캠페인이나 Adobe Real-Time CDP에서 들어오는 대상에 있는 적격 프로필 수가 중단되지 않습니다.
