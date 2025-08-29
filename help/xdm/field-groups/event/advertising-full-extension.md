---
title: Adobe Advertising Cloud ExperienceEvent 전체 확장 스키마 필드 그룹
description: Adobe Advertising Cloud ExperienceEvent 전체 확장 스키마 필드 그룹에 대해 알아봅니다.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Adobe Advertising Cloud ExperienceEvent 전체 확장] 스키마 필드 그룹

>[!AVAILABILITY]
>
>[!UICONTROL Adobe Advertising Cloud ExperienceEvent 전체 확장] 필드 그룹은 현재 Beta 상태입니다. 설명서 및 기능은 변경될 수 있습니다.

[!UICONTROL Adobe Advertising Cloud ExperienceEvent 전체 확장 기능]은(는) Adobe Advertising에서 수집하는 일반적인 지표(이전의 &quot;[[!DNL XDM ExperienceEvent] &quot;)를 캡처하는 ](../../classes/experienceevent.md)클래스[!DNL Advertising Cloud]에 대한 표준 스키마 필드 그룹입니다.

이 문서에서는 [!DNL Advertising Cloud] 확장 필드 그룹의 구조 및 사용 사례를 설명합니다.

>[!NOTE]
>
>Experience Platform UI에서 이 필드 그룹 [을(를) 조회하거나](../../ui/explore.md) [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)에서 전체 스키마를 볼 수도 있습니다.

## 필드 그룹 구조

필드 그룹은 스키마에 단일 `_experience` 개체를 제공하며, 이 개체 자체에는 단일 `adcloud` 개체가 있습니다.

![ 필드 그룹의 [!DNL Advertising Cloud]최상위 필드](../../images/field-groups/advertising-full-extension/full-schema.png "필드 그룹의  [!DNL Advertising Cloud] 최상위 필드")

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `adDeliveryDetails` | 오브젝트 | 광고 게재 세부 정보. 이 개체의 내용에 대한 자세한 내용은 [ 개체에 대한 아래 `adDeliveryDetails`하위 섹션](#adDeliveryDetails)을 참조하세요. |
| `advertisement` | 오브젝트 | 디지털 광고 세부 정보. 이 개체의 내용에 대한 자세한 내용은 광고 개체에 대한 아래 [하위 섹션](#advertisement)을 참조하세요. |
| `campaign` | 오브젝트 | Campaign 계층 세부 정보. 이 개체의 내용에 대한 자세한 내용은 캠페인 개체에 대한 아래 [하위 섹션](#campaign-campaign)을 참조하세요. |
| `conversionDetails` | 오브젝트 | 광고에 대한 전환 세부 정보. 이 개체의 내용에 대한 자세한 내용은 아래 [하위 섹션](#conversionDetails)을 참조하세요. |
| `eventType` | 문자열 | Adobe Advertising 이벤트 유형. |
| `fees` | 오브젝트 | Advertising 수수료 세부 정보. 이 개체의 내용에 대한 자세한 내용은 수수료 개체에 대한 아래 [하위 섹션](#fees)을 참조하십시오. |
| `inventory` | 오브젝트 | 인벤토리 세부 정보. 이 개체의 내용에 대한 자세한 내용은 아래 [하위 섹션](#inventory)을 참조하세요. |
| `productDetails` | 오브젝트 | 제품 광고 세부 정보. 이 개체의 내용에 대한 자세한 내용은 productDetails 개체의 아래 [하위 섹션](#productDetails)을 참조하십시오. |
| `stitchId` | 문자열 | 서드파티 쿠키를 차단하는 브라우저에서 클릭스루 전환을 추적할 Adobe Advertising 광고 서버의 ID입니다. |

## `adDeliveryDetails` {#adDeliveryDetails}

adDeliveryDetails 개체는 배치 웹 사이트 및 위치 식별자를 포함하여 광고가 게재된 위치와 방법에 대한 정보를 제공합니다.

![ 개체와 해당 필드를 표시하는 `adDeliveryDetails`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `placementWebsite` | 문자열 | 광고가 게재된 웹 사이트입니다. |
| `siteLinkText` | 문자열 | 광고에서 선택한 실제 사이트 링크. |
| `interestLocationID` | 문자열 | 검색 쿼리에서 추론한 위치입니다. 예를 들어 &quot;Hotel in Goa&quot;에 대한 쿼리는 사용자의 실제 탐색 위치에 관계없이 Goa에 대한 ID를 반환합니다. |
| `physicalLocationID` | 문자열 | 광고 네트워크의 참조 ID로 표시되는 사용자의 검색 위치입니다. 이 ID는 읽을 수 있는 위치 이름(예: 도시 또는 국가)이 아니라 지리적 대상을 식별하기 위해 광고 네트워크에서 할당한 코드입니다. |

## `advertisement` {#advertisement}

광고 개체는 식별자, 유형, 크리에이티브, 타기팅 및 관련 키워드와 같은 디지털 광고에 대한 세부 사항을 설명합니다.

![ 개체와 해당 필드를 표시하는 `advertisement`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/advertisement.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `adId` | 문자열 | 해당 이벤트와 연계된 광고 식별자. 이 ID는 광고 ID 업계 표준과 관련이 없습니다. |
| `runtime` | 문자열 | 브라우저 또는 운영 체제의 런타임과 구별되는 광고 단위의 런타임입니다. 가능한 값은 `unknown` 및 `HTML5`입니다. |
| `adClass` | 문자열 | 구동 이벤트의 광고 클래스: `display`, `video` 또는 `social`. |
| `adUnitType` | 문자열 | 브라우저 또는 장치에서 광고를 렌더링하는 코드의 식별자입니다. 가능한 값은 다음과 같습니다.<ul><li>`linearVideo`: 선형 비디오</li><li>`interactiveVideo`: 대화형 비디오</li><li>`banner`: 배너,</li><li>`richMediaBanner`: 리치 미디어 배너,</li><li>`newsFeedVideo`: 뉴스 피드 비디오,</li><li>`newsFeedDisplay`: 뉴스 피드 표시,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: 페이지 비디오에서</li><li>`inPageDisplay`: 페이지 표시,</li><li>`facebook`: Facebook,</li><li>`twitter`: 트위터,</li><li>`linearTv`: 선형 TV,</li><li>`vod`: 주문형 비디오</li></ul> |
| `promotedAssetId` | 문자열 | 이 이벤트와 연계된 광고에서 홍보된 에셋의 식별자입니다. |
| `creativeID` | 문자열 | 해당 이벤트와 연계된 광고 크리에이티브(예: 배너, 비디오 또는 소셜 광고)용 식별자. |
| `keywordID` | 문자열 | 이 이벤트를 트리거한 검색 쿼리에서 사용자가 입력한 키워드의 식별자입니다. |
| `keyword` | 문자열 | 고객이 입찰한 목록 키워드입니다. |
| `isDynamicSearchAd` | 부울 | 이벤트가 동적 검색 광고에서 오는지 여부를 나타냅니다. |
| `audienceID` | 문자열 | 광고에서 타겟팅하는 대상 세그먼트의 식별자입니다. |
| `adGroupID` | 문자열 | 이 이벤트를 트리거한 광고에 연결된 광고 그룹의 식별자입니다. |
| `campaignID` | 문자열 | 이 이벤트를 트리거한 광고와 연결된 캠페인의 식별자입니다. |
| `networkType` | 문자열 | 이벤트가 발생한 네트워크 유형입니다. 가능한 값은 다음과 같습니다. <ul><li>`search`: 광고가 검색 네트워크에 표시되었습니다.</li><li>`content`: 광고가 콘텐츠 네트워크에 표시되었습니다.</li></ul> |
| `matchType` | 문자열 | 키워드 일치 유형입니다. 가능한 값은 다음과 같습니다. <ul><li>`exact`: 키워드의 정확한 일치</li><li>`broad`: 키워드의 광범위한 일치</li><li>`phrase`: 키워드의 구 일치</li></ul> |

## `campaign` {#campaign}

캠페인 개체는 통화 세부 정보와 함께 계정, 광고주, 배치 및 패키지 식별자를 포함한 광고 캠페인 계층을 정의합니다.

![ 개체와 해당 필드를 표시하는 `campaign`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/campaign.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `accountId` | 문자열 | 계정용 식별자. |
| `dspId` | 문자열 | 캠페인이 정의된 Demand Side Platform(DSP)의 식별자입니다. 일반적으로 이 식별자는 Adobe Advertising Cloud DSP용 ID입니다. |
| `campaignId` | 문자열 | 캠페인에 대한 식별자. |
| `placementId` | 문자열 | 배치용 식별자. |
| `packageId` | 문자열 | Advertising DSP 패키지의 식별자입니다. |
| `advertiserId` | 문자열 | 광고주용 식별자. |
| `experimentId` | 문자열 | 실험용 식별자. |
| `sampleGroupId` | 문자열 | 샘플 그룹에 대한 식별자. |
| `currency` | 문자열 | 계정에 대한 ISO 4217 청구 통화 코드. 정규 표현식 패턴 ^[A-Z]{3}$(대문자 3개)을 사용합니다. 예: USD, EUR. |

## `conversionDetails` {#conversionDetails}

conversionDetails 개체는 추적 코드, ID 및 전환 속성을 포함한 광고 전환에 대한 추적 정보를 캡처합니다.

![ 개체와 해당 필드를 표시하는 `conversionDetails`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/conversionDetails.png "conversionDetails 필드")

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `trackingCode` | 문자열 | 이벤트에 대한 전환 추적 코드입니다. 가능한 형식 목록은 [AMO ID 형식](https://experienceleague.adobe.com/ko/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats)을 참조하십시오. |
| `trackingIdentities` | 문자열 | 이벤트에 대한 EF ID 또는 추적 ID 세부 정보. 가능한 형식 목록은 [EF ID 형식](https://experienceleague.adobe.com/ko/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats)을 참조하십시오. |
| `conversionProperties` | 오브젝트 | 키-값 쌍 문자열의 배열로 표시되는 전환 속성 맵(예: `subscriptions=253`). |

## `fees` {#fees}

수수료 오브젝트는 Advertising DSP, 계정 및 광고주별로 분류된 미디어, 데이터 및 기타 광고 비용을 캡처합니다.

![ 개체와 해당 필드를 표시하는 `fees`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/fees.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `DSPMediaFees` | 숫자 | Advertising DSP에서 청구할 수 있는 미디어 요금. |
| `DSPDataFees` | 숫자 | Advertising DSP에서 청구할 수 있는 데이터 요금입니다. |
| `DSPOtherFees` | 숫자 | 기타 요금은 Advertising DSP에서 청구할 수 있습니다. |
| `accountMediaFees` | 숫자 | 계정에 대한 미디어 요금이지만 Advertising DSP에서 청구할 수 없습니다. |
| `accountDataFees` | 숫자 | 계정에 대한 데이터 요금이지만 Advertising DSP에서 청구할 수 없습니다. |
| `accountOtherFees` | 숫자 | 계정에 대한 기타 요금이지만 Advertising DSP에서 청구할 수 없습니다. |
| `advertiserMediaFees` | 숫자 | 미디어 광고주 요금은 계정에서 광고주에게 청구됩니다. |
| `advertiserDataFees` | 숫자 | 계정에서 광고주에게 청구된 기타 광고주 수수료. |
| `advertiserOtherFees` | 숫자 | 계정에서 광고주에게 청구된 기타 광고주 수수료. |
| `billableMediaNetSpend` | 숫자 | 미디어 광고에 대한 청구 가능 순 지출. |
| `totalMediaNetSpend` | 숫자 | 미디어 광고에 대한 총 순 지출. |
| `billableDataNetSpend` | 숫자 | 데이터 광고에 대한 청구 가능 순 지출. |
| `billableOtherNetSpend` | 숫자 | 다른 유형의 광고에 대한 청구 가능 순 지출. |
| `totalBillableNetSpend` | 숫자 | 총 청구 가능 순 지출. |
| `totalNonBillableNetSpend` | 숫자 | 청구 불가능한 총 순 지출. |
| `totalNetSpend` | 숫자 | 총 순 지출 |

## `inventory` {#inventory}

인벤토리 개체는 세션 데이터, 파트너 코드, 사이트 ID, 비용 통화 및 세분화 규칙을 포함하여 광고 인벤토리 영업 기회에 대한 세부 정보를 기록합니다.

![ 개체와 해당 필드를 표시하는 `inventory`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/inventory.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `sessionId` | 문자열 | 동일한 세션에서 발생한 독립 이벤트를 연결하는 데 사용되는 경험 이벤트와 연결된 세션 ID입니다. |
| `feedID` | 문자열 | 게시자, 광고 교환 및 기타 기능의 복합 ID. |
| `sspPartnerCode` | 문자열 | Adobe Advertising Cloud가 인벤토리 기회를 받는 파트너(교환)입니다. |
| `siteID` | 문자열 | 광고 노출이 제공된 웹 사이트의 식별자입니다. |
| `costCurrency` | 문자열 | 광고 기회에 대해 파트너에게 지급하는 데 사용되는 ISO 4217 통화 코드. 값은 일반 표현식 패턴 ^[A-Z]{3}$(대문자 3개)을 따라야 합니다. 예: USD, EUR. |
| `inventorySourceId` | 문자열 | 해당 영업 기회가 제공된 Adobe Advertising Cloud 인벤토리 소스의 ID입니다. |
| `segment` | 오브젝트 | 사용자 세분화 규칙과 관련된 세부 정보. 속성에는 다음이 포함됩니다.<ul><li>`attributablePartnerId`(String): improvisedSegmentId를 소유한 세그먼트 공급자의 식별자입니다.</li><li>`attributableSegmentId`(문자열): 배치의 타깃팅 규칙에서 사용자 타깃팅에 대해 크레딧이 부여된 세그먼트입니다. 이는 비용 추적 및 지불 파트너 목적으로 사용됩니다.</li><li>`segments`(문자열): 사용자가 속한 a\)와 광고가 대상으로 하는 b\)의 사용자 세그먼트 교차. 이는 경매 당시 사용자가 속했던 세그먼트의 전체 목록이 아닙니다.</li></ul> |
| `optimizationTag` | 문자열 | 최적화와 관련된 태그입니다. |
| `attributableDeviceGraphId` | 문자열 | 전환 이벤트에 기인하는 Device Graph의 식별자입니다. |

## `productDetails` {#productDetails}

`productDetails` 개체에는 제품 식별자, 국가, 언어, 파티션, 제목, 광고 유형 등 [!DNL Adobe Advertising Search, Social, & Commerce]의 쇼핑 광고에 포함된 제품에 대한 정보가 들어 있습니다.

![ 개체와 해당 필드를 표시하는 `productDetails`스키마 다이어그램입니다.](../../images/field-groups/advertising-full-extension/productDetails.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productID` | 문자열 | 해당 이벤트와 연계된 광고에 포함된 제품의 식별자. |
| `country` | 문자열 | 이벤트와 연계된 광고에 포함된 제품의 판매 국가입니다. |
| `language` | 문자열 | 클라이언트의 머천트 센터 데이터 피드에 표시된 제품 정보의 언어. |
| `partitionID` | 문자열 | 이 이벤트의 광고에 연결된 제품 그룹 식별자. |
| `title` | 문자열 | 광고에 표시되는 제품 제목입니다. |
| `adType` | 문자열 | [!DNL Google] 쇼핑 캠페인에 사용되는 제품에 대한 광고 유형입니다. 가능한 값은 다음과 같습니다.<ul><li>`pla_with_pog`: 쇼핑 광고를 통한 구매에서 이벤트가 발생한 경우</li><li>`pla`: 쇼핑 광고에서 이벤트가 발생한 때입니다.</li><li>`pla_multichannel`: 쇼핑 광고의 이벤트에 &quot;온라인&quot; 및 &quot;로컬&quot; 쇼핑 채널 모두에 대한 옵션이 포함된 경우.</li><li>`pla_with_promotion`: 쇼핑 광고의 이벤트에 판매자 프로모션이 표시되는 경우.</li></ul> |

## 다음 단계

이 문서에서는 [!DNL Advertising Cloud] 확장 필드 그룹의 구조 및 사용 사례를 다룹니다. 필드 그룹 자체에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json)를 참조하세요.

이 필드 그룹을 사용하여 Adobe Experience Platform Web SDK을 사용하여 [!DNL Advertising] 데이터를 수집하는 경우 서버측의 XDM에 데이터를 매핑하는 방법에 대해 알아보려면 [데이터 스트림 구성](../../../datastreams/overview.md)에 대한 안내서를 참조하십시오.
