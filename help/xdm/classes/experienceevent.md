---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;ID 맵;ID 맵;스키마 디자인;맵;맵;이벤트 모델링;이벤트 모델링;우수 사례;이벤트;이벤트;이벤트;ID;
solution: Experience Platform
title: XDM ExperienceEvent 클래스
description: 이 문서에서는 XDM ExperienceEvent 클래스에 대한 개요와 이벤트 데이터 모델링에 대한 모범 사례를 제공합니다.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: e4e87fdb5f6dfbca882f924d38397a904d8b0cff
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 는 특정 이벤트가 발생하거나 특정 조건 세트에 도달했을 때 시스템의 타임스탬프가 지정된 스냅샷을 만들 수 있는 표준 XDM(Experience Data Model) 클래스입니다.

경험 이벤트는 관련된 개인의 시점 및 ID를 포함하여 발생한 일에 대한 팩트 레코드입니다. 이벤트는 명시적(직접 관찰가능한 사람 작업) 또는 암시적(직접적인 사용자 작업 없이 발생)일 수 있으며 집계 또는 해석 없이 기록됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors).

다음 [!DNL XDM ExperienceEvent] 클래스 자체는 스키마에 여러 시계열 관련 필드를 제공합니다. 이러한 필드 중 두 개(`_id` 및 `timestamp`) **필수** 클래스를 기반으로 하는 모든 스키마에 대해 나머지 스키마는 선택 사항입니다. 데이터를 수집할 때 일부 필드의 값이 자동으로 채워집니다.

![Platform UI에 표시되는 XDM ExperienceEvent의 구조](../images/classes/experienceevent/structure.png)

| 속성 | 설명 |
| --- | --- |
| `_id`<br>**(필수 여부)** | 이벤트에 대한 고유한 문자열 식별자입니다. 이 필드는 개별 이벤트의 고유성을 추적하고 데이터의 중복을 방지하며 다운스트림 서비스에서 해당 이벤트를 찾는 데 사용됩니다. 어떤 경우에는 `_id` 다음을 수행할 수 있습니다. [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>소스 연결에서 데이터를 스트리밍하거나 Parquet 파일에서 직접 수집하는 경우 기본 ID, 타임스탬프, 이벤트 유형 등과 같이 이벤트를 고유하게 만드는 특정 필드 조합을 연결하여 이 값을 생성해야 합니다. 연결된 값은 `uri-reference` 형식이 지정된 문자열. 즉, 콜론 문자를 제거해야 합니다. 그런 다음 연결된 값을 SHA-256 또는 선택한 다른 알고리즘을 사용하여 해시해야 합니다.<br><br>그것을 구분하는 것은 중요하다 **이 필드는 개별 사용자와 관련된 ID를 나타내지 않습니다**&#x200B;하지만, 오히려 데이터 자체의 기록입니다. 한 사람에 대한 신분자료는 다음과 같이 분류되어야 한다 [id 필드](../schema/composition.md#identity) 호환 필드 그룹에서 대신 제공합니다. |
| `eventMergeId` | 를 사용하는 경우 [Adobe Experience Platform Web SDK](../../edge/home.md) 데이터를 수집하기 위해 레코드를 만든 수집된 일괄 처리의 ID를 나타냅니다. 이 필드는 데이터 수집 시 시스템에 의해 자동으로 채워집니다. 웹 SDK 구현 컨텍스트에서 벗어난 이 필드의 사용은 지원되지 않습니다. |
| `eventType` | 이벤트의 유형 또는 카테고리를 나타내는 문자열입니다. 이 필드는 제품 보기 이벤트를 소매 회사의 추가-장바구니 이벤트와 구별하는 것과 같이, 동일한 스키마 및 데이터 세트 내에서 서로 다른 이벤트 유형을 구분하려는 경우 사용할 수 있습니다.<br><br>이 속성에 대한 표준 값은 [부록 섹션](#eventType): 의도한 사용 사례에 대한 설명을 포함합니다. 이 필드는 확장 가능한 열거형입니다. 즉, 고유한 이벤트 유형 문자열을 사용하여 추적 중인 이벤트를 분류할 수도 있습니다. 다음을 수행할 수도 있습니다 [표준 제안 값 중 하나를 비활성화합니다](../ui/fields/enum.md#standard-fields) 사용 사례에 맞지 않는 경우 이 필드에 대해 설명합니다.<br><br>`eventType` 애플리케이션의 히트당 하나의 이벤트만 사용하도록 제한하므로 시스템에서 가장 중요한 이벤트를 알리는 데 계산된 필드를 사용해야 합니다. 자세한 내용은 [계산된 필드의 우수 사례](#calculated). |
| `producedBy` | 이벤트의 생성자나 출처를 설명하는 문자열 값입니다. 이 필드는 세그먼테이션을 위해 필요한 경우 특정 이벤트 생성자를 필터링하는 데 사용할 수 있습니다.<br><br>이 속성에 대한 일부 추천 값은 [부록 섹션](#producedBy). 이 필드는 확장 가능한 열거형입니다. 즉, 고유한 문자열을 사용하여 다른 이벤트 생성자를 나타낼 수도 있습니다. |
| `identityMap` | 이벤트가 적용되는 개별 ID에 대해 이름이 지정된 ID 세트가 포함된 맵 필드입니다. ID 데이터를 수집할 때 시스템에서 이 필드를 자동으로 업데이트합니다. 에 이 필드를 적절히 활용하려면 [실시간 고객 프로필](../../profile/home.md)에서는 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />의 ID 맵에 대한 섹션을 참조하십시오. [스키마 구성 기본 사항](../schema/composition.md#identityMap) 를 참조하십시오. |
| `timestamp`<br>**(필수 여부)** | 이벤트가 발생한 시점의 ISO 8601 타임스탬프이며, [RFC 3339 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). 이 타임스탬프는 과거에 발생해야 합니다. 다음에서 아래 섹션을 참조하십시오. [타임스탬프](#timestamps) 을 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

## 이벤트 모델링 우수 사례

다음 섹션에서는 Adobe Experience Platform에서 이벤트 기반 XDM(Experience Data Model) 스키마를 디자인하기 위한 우수 사례를 다룹니다.

### 타임스탬프 {#timestamps}

루트 `timestamp` 이벤트 스키마의 필드는 다음과 같이 지정할 수 있습니다 **전용** 은 이벤트 자체의 관찰을 나타내며 과거에 발생해야 합니다. 세그먼테이션 사용 사례에서 나중에 발생할 수 있는 타임스탬프를 사용해야 하는 경우 이러한 값은 경험 이벤트 스키마의 다른 위치에서 제한되어야 합니다.

예를 들어, 여행 및 숙박 업계의 한 기업이 비행 예약 이벤트를 모델링하고 있다면 클래스 수준입니다 `timestamp` 필드는 예약 이벤트가 관찰된 시간을 나타냅니다. 여행 예약 시작 날짜와 같이 이벤트와 관련된 기타 타임스탬프는 표준 또는 사용자 지정 필드 그룹에서 제공하는 별도의 필드에 캡처해야 합니다.

![플라이트 예약 및 시작 날짜가 강조 표시된 샘플 경험 이벤트 스키마.](../images/classes/experienceevent/timestamps.png)

클래스 수준 타임스탬프를 이벤트 스키마의 다른 관련 날짜/시간 값과 별도로 유지하면 경험 애플리케이션에서 고객 여정의 타임스탬프가 지정된 계정을 유지하면서 유연한 세그먼테이션 사용 사례를 구현할 수 있습니다.

### 계산된 필드 사용 {#calculated}

경험 애플리케이션에서 특정 상호 작용으로 인해 기술적으로 동일한 이벤트 타임스탬프를 공유하는 여러 관련 이벤트가 발생할 수 있으므로 단일 이벤트 레코드로 나타낼 수 있습니다. 예를 들어 고객이 웹 사이트에서 제품을 보는 경우 두 가지 가능성이 있는 이벤트 레코드가 발생할 수 있습니다 `eventType` 값: &quot;제품 보기&quot; 이벤트(`commerce.productViews`) 또는 일반적인 &quot;페이지 보기&quot; 이벤트(`web.webpagedetails.pageViews`). 이러한 경우 하나의 히트에서 여러 이벤트가 캡처될 때 계산된 필드를 사용하여 가장 중요한 속성을 캡처할 수 있습니다.

[Adobe Experience Platform 데이터 준비](../../data-prep/home.md) xdm을 통해 데이터를 매핑, 변환 및 XDM에서 확인할 수 있습니다. 사용 가능 [매핑 함수](../../data-prep/functions.md) 서비스에서 Experience Platform으로 수집할 때 논리 연산자를 호출하여 다중 이벤트 레코드의 데이터를 우선 순위 지정, 변환 및/또는 통합할 수 있습니다. 위의 예에서 `eventType` 둘 다 발생할 때마다 &quot;페이지 보기&quot;보다 &quot;제품 보기&quot;를 우선시하는 계산된 필드입니다.

UI를 통해 Platform으로 데이터를 수동으로 수집하는 경우, [계산된 필드](../../data-prep/ui/mapping.md#calculated-fields) 를 참조하십시오.

소스 연결을 사용하여 Platform으로 데이터를 스트리밍하는 경우 계산된 필드를 대신 사용하도록 소스를 구성할 수 있습니다. 자세한 내용은 [특정 소스에 대한 설명서](../../sources/home.md) 를 참조하십시오.

## 호환 가능한 스키마 필드 그룹 {#field-groups}

>[!NOTE]
>
>여러 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../field-groups/name-updates.md) 추가 정보.

Adobe은 와 함께 사용할 여러 표준 필드 그룹을 제공합니다 [!DNL XDM ExperienceEvent] 클래스 이름을 지정합니다. 다음은 클래스에 일반적으로 사용되는 몇 가지 필드 그룹 목록입니다.

* [[!UICONTROL Adobe Analytics Experience Event Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 잔액 이전]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 캠페인 마케팅 세부 사항]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 카드 작업]](../field-groups/event/card-actions.md)
* [[!UICONTROL 채널 세부 사항]](../field-groups/event/channel-details.md)
* [[!UICONTROL 상거래 세부 사항]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 예금 상세내역]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 장치 거래 세부 사항]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 식사 예약]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 최종 사용자 ID 세부 정보]](../field-groups/event/enduserids.md)
* [[!UICONTROL 환경 세부 정보]](../field-groups/event/environment-details.md)
* [[!UICONTROL 비행 예약]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0 동의]](../field-groups/event/iab.md)
* [[!UICONTROL 숙박예약]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL 견적 요청 세부 정보]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 예약 세부 정보]](../field-groups/event/reservation-details.md)
* [[!UICONTROL 웹 세부 사항]](../field-groups/event/web-details.md)

## 부록

다음 섹션에는 [!UICONTROL XDM ExperienceEvent] 클래스 이름을 지정합니다.

### 에 대한 제안 값 `eventType` {#eventType}

다음 테이블은에 대한 표준 제안 값에 대해 설명합니다 `eventType`, 정의 및

| 값 | 정의 |
| --- | --- |
| `advertising.clicks` | 광고에서 작업을 클릭합니다. |
| `advertising.completes` | 시간이 지정된 미디어 자산을 끝까지 시청했습니다. 이것은 뷰어가 건너뛸 수 있었으므로 뷰어가 반드시 전체 비디오를 시청했음을 의미하지는 않습니다. |
| `advertising.conversions` | 고객이 성능 평가를 위해 이벤트를 트리거하는 사전 정의된 작업입니다. |
| `advertising.federated` | 데이터 페더레이션(고객 간의 데이터 공유)를 통해 경험 이벤트가 생성되었는지 여부를 나타냅니다. |
| `advertising.firstQuartiles` | 디지털 비디오 광고는 그 지속 시간의 25%를 보통 속도로 재생했다. |
| `advertising.impressions` | 잠재 고객이 볼 수 있는 광고에 대한 노출 수입니다. |
| `advertising.midpoints` | 디지털 비디오 광고는 그 지속 시간의 50%를 보통 속도로 재생했다. |
| `advertising.starts` | 디지털 비디오 광고 재생이 시작되었습니다. |
| `advertising.thirdQuartiles` | 디지털 비디오 광고는 그 기간의 75%를 보통 속도로 재생했다. |
| `advertising.timePlayed` | 특정 시간 미디어 자산에서 사용자가 사용한 시간을 설명합니다. |
| `application.close` | 응용 프로그램을 닫았거나 백그라운드로 보냈습니다. |
| `application.launch` | 응용 프로그램을 시작하거나 전경으로 가져왔습니다. |
| `commerce.checkouts` | 제품 목록에 대해 체크아웃 이벤트가 발생했습니다. 체크아웃 프로세스에 여러 단계가 있는 경우 두 개 이상의 체크아웃 이벤트가 있을 수 있습니다. 여러 단계가 있는 경우 각 이벤트에 대한 타임스탬프 및 참조된 페이지/경험이 순서대로 표시된 각 개별 이벤트(단계)를 식별하는 데 사용됩니다. |
| `commerce.productListAdds` | 제품 목록 또는 장바구니에 제품이 추가되었습니다. |
| `commerce.productListOpens` | 새 제품 목록(장바구니)이 초기화되거나 만들어졌습니다. |
| `commerce.productListRemovals` | 제품 목록 또는 장바구니에서 하나 이상의 제품 항목이 제거되었습니다. |
| `commerce.productListReopens` | 더 이상 액세스(포기)하지 않은 제품 목록(장바구니)이 재마케팅 활동을 통해 활성화되었습니다. |
| `commerce.productListViews` | 제품 목록 또는 장바구니가 하나 이상의 보기를 수신했습니다. |
| `commerce.productViews` | 제품이 하나 이상의 보기를 받았습니다. |
| `commerce.purchases` | 주문이 수락되었습니다. 이는 상거래 전환에서 유일하게 필요한 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `commerce.saveForLaters` | 제품 목록이 나중에 사용할 수 있도록 저장되었습니다(예: 제품 희망 목록). |
| `decisioning.propositionDisplay` | 한 사람에게 의사 결정 제안이 표시되었습니다. |
| `decisioning.propositionInteract` | 한 사람이 의사결정 제안과 상호 작용했다. |
| `delivery.feedback` | 전자 메일 게재와 같은 게재에 대한 피드백 이벤트입니다. |
| `directMarketing.emailBounced` | 바운스된 사람에게 이메일 보내기. |
| `directMarketing.emailBouncedSoft` | 소프트 바운스된 사람에게 이메일 보내기. |
| `directMarketing.emailClicked` | 마케팅 이메일의 링크를 클릭한 사람이 있습니다. |
| `directMarketing.emailDelivered` | 전자 메일이 사용자의 전자 메일 서비스에 배달되었습니다. |
| `directMarketing.emailOpened` | 마케팅 이메일을 열람한 사람이 있습니다. |
| `directMarketing.emailUnsubscribed` | 마케팅 이메일의 구독을 취소한 사람. |
| `inappmessageTracking.dismiss` | 인앱 메시지가 해제되었습니다. |
| `inappmessageTracking.display` | 인앱 메시지가 표시되었습니다. |
| `inappmessageTracking.interact` | 인앱 메시지가 와 상호 작용했습니다. |
| `leadOperation.callWebhook` | 리드에 대한 응답으로 웹 후크가 호출되었습니다. |
| `leadOperation.convertLead` | 리드가 전환되었습니다. |
| `leadOperation.interestingMoment` | 한 사람을 위한 흥미로운 순간이 기록되었다. |
| `leadOperation.newLead` | 리드가 생성되었습니다. |
| `leadOperation.scoreChanged` | 리드의 점수 속성 값이 변경되었습니다. |
| `leadOperation.statusInCampaignProgressionChanged` | 캠페인에서 리드의 상태가 변경되었습니다. |
| `listOperation.addToList` | 마케팅 목록에 사람이 추가되었습니다. |
| `listOperation.removeFromList` | 마케팅 목록에서 사람이 제거되었습니다. |
| `message.feedback` | 고객에게 전송되는 메시지에 대한 전송/반송/오류와 같은 피드백 이벤트입니다. |
| `message.tracking` | 고객에게 전송된 메시지에 대한 열기/클릭/사용자 지정 작업과 같은 이벤트 추적. |
| `opportunityEvent.addToOpportunity` | 한 사람이 기회에 추가되었다. |
| `opportunityEvent.opportunityUpdated` | 기회가 업데이트되었습니다. |
| `opportunityEvent.removeFromOpportunity` | 한 사람이 기회를 박탈당했다. |
| `pushTracking.applicationOpened` | 푸시 알림에서 애플리케이션을 연 사람. |
| `pushTracking.customAction` | 한 사람이 푸시 알림에서 사용자 지정 작업을 클릭했습니다. |
| `web.formFilledOut` | 한 사람이 wep 페이지에서 양식을 입력했습니다. |
| `web.webinteraction.linkClicks` | 링크가 하나 이상 선택되었습니다. |
| `web.webpagedetails.pageViews` | 웹 페이지가 하나 이상의 보기를 받았습니다. |

{style=&quot;table-layout:auto&quot;}

### 에 대한 제안 값 `producedBy` {#producedBy}

다음 테이블은에 대한 표준 제안 값에 대해 설명합니다 `producedBy`:

| 값 | 정의 |
| --- | --- |
| `self` | 자체 |
| `system` | 시스템 |
| `salesRef` | 영업 담당자 |
| `customerRep` | 고객 담당자 |
