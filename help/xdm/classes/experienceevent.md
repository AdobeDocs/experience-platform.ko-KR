---
keywords: Experience Platform;홈;인기 주제;스키마;스키마;XDM;필드;스키마;스키마;ID 맵;ID 맵;ID 맵;스키마 디자인;맵;맵;이벤트 모델링;이벤트 모델링;우수 사례;이벤트;이벤트;이벤트;
solution: Experience Platform
title: XDM ExperienceEvent 클래스
description: XDM ExperienceEvent 클래스와 이벤트 데이터 모델링을 위한 모범 사례에 대해 알아봅니다.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] 클래스

[!DNL XDM ExperienceEvent]은(는) 표준 XDM(Experience Data Model) 클래스입니다. 특정 이벤트가 발생하거나 특정 조건 집합에 도달한 경우 이 클래스를 사용하여 시스템의 타임스탬프가 지정된 스냅샷을 만듭니다.

경험 이벤트 는 시점 및 관련된 개인의 ID를 포함하여 발생한 사항에 대한 팩트 레코드입니다. 사건은 명시적(직접 관찰 가능한 인간 행동) 또는 암시적(직접 인간 행동 없이 발생)일 수 있으며 집계나 해석 없이 기록된다. Experience Platform 에코시스템에서 이 클래스의 사용에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors)를 참조하세요.

[!DNL XDM ExperienceEvent] 클래스 자체는 스키마에 여러 시계열 관련 필드를 제공합니다. 이 필드 중 두 개(`_id` 및 `timestamp`)는 이 클래스를 기반으로 하는 모든 스키마에 대해 **필수**&#x200B;이고 나머지는 선택 사항입니다. 일부 필드의 값은 데이터가 수집될 때 자동으로 채워집니다.

![Experience Platform UI에 표시되는 XDM ExperienceEvent 구조입니다.](../images/classes/experienceevent/structure.png)

| 속성 | 설명 |
| --- | --- |
| `_id`<br>**(필수)** | 경험 이벤트 클래스 `_id` 필드는 Adobe Experience Platform에 수집되는 개별 이벤트를 고유하게 식별합니다. 이 필드는 개별 이벤트의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 이벤트를 조회하는 데 사용됩니다.<br><br>중복 이벤트가 검색되면 Experience Platform 응용 프로그램 및 서비스에서 중복을 다르게 처리할 수 있습니다. 예를 들어 동일한 `_id`을(를) 가진 이벤트가 프로필 저장소에 이미 있는 경우 프로필 서비스의 중복 이벤트가 삭제됩니다.<br><br>경우에 따라 `_id`은(는) [UUID(Universally Unique Identifier)](https://datatracker.ietf.org/doc/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)일 수 있습니다.<br><br>소스 연결에서 데이터를 스트리밍하거나 Parquet 파일에서 직접 수집하는 경우, 이벤트를 고유하게 만드는 특정 필드 조합을 연결하여 이 값을 생성해야 합니다. 연결할 수 있는 이벤트의 예로는 기본 ID, 타임스탬프, 이벤트 유형 등이 있습니다. 연결된 값은 `uri-reference` 형식의 문자열이어야 합니다. 즉, 콜론 문자는 모두 제거해야 합니다. 그런 다음 연결된 값을 SHA-256 또는 선택한 다른 알고리즘을 사용하여 해시해야 합니다.<br><br>이 필드가 개별 사용자와 관련된 ID를 나타내는 것이 아니라 데이터 기록 자체를 나타내는 것임을 구별하는 것이 중요합니다&#x200B;**.** 사용자와 관련된 ID 데이터는 대신 호환 가능한 필드 그룹에서 제공하는 [ID 필드](../schema/composition.md#identity)(으)로 수준을 내려야 합니다. |
| `eventMergeId` | [Adobe Experience Platform Web SDK](/help/web-sdk/home.md)을(를) 사용하여 데이터를 수집하는 경우, 레코드가 생성되도록 한 수집된 일괄 처리의 ID를 나타냅니다. 이 필드는 데이터 수집 시 시스템에서 자동으로 채워집니다. 웹 SDK 구현의 컨텍스트 외부에서 이 필드를 사용하는 것은 지원되지 않습니다. |
| `eventType` | 이벤트의 유형 또는 범주를 나타내는 문자열입니다. 이 필드는 제품 보기 이벤트를 소매 회사에 대한 장바구니에 추가 이벤트와 구분하는 것처럼 동일한 스키마 및 데이터 세트 내에서 다른 이벤트 유형을 구분하려는 경우 사용할 수 있습니다.<br><br>이 속성의 표준 값은 의도한 사용 사례에 대한 설명을 포함하여 [부록 섹션](#eventType)에 제공됩니다. 이 필드는 확장 가능한 열거형입니다. 즉, 고유한 이벤트 유형 문자열을 사용하여 추적 중인 이벤트를 분류할 수도 있습니다.<br><br>`eventType`은(는) 응용 프로그램에서 히트당 하나의 이벤트만 사용하도록 제한하므로 시스템에서 가장 중요한 이벤트를 알려주기 위해 계산된 필드를 사용해야 합니다. 자세한 내용은 [계산된 필드에 대한 모범 사례](#calculated)의 섹션을 참조하십시오. |
| `producedBy` | 이벤트의 생성자 또는 출처를 설명하는 문자열 값입니다. 이 필드는 세분화 목적으로 필요한 경우 특정 이벤트 제작자를 필터링하는 데 사용할 수 있습니다.<br><br>이 속성에 대해 제안된 일부 값은 [부록 섹션](#producedBy)에 제공됩니다. 이 필드는 확장 가능한 열거형입니다. 즉, 고유한 문자열을 사용하여 다른 이벤트 생성자를 나타낼 수도 있습니다. |
| `identityMap` | 이벤트가 적용되는 개인에 대한 네임스페이스 ID 세트가 포함된 맵 필드입니다. 이 필드는 ID 데이터가 수집될 때 시스템에 의해 자동으로 업데이트됩니다. [실시간 고객 프로필](../../profile/home.md)에 대해 이 필드를 제대로 활용하려면 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />사용 사례에 대한 자세한 내용은 [스키마 컴포지션의 기본 사항](../schema/composition.md#identityMap)에서 ID 맵에 대한 섹션을 참조하십시오. |
| `timestamp`<br>**(필수)** | 이벤트가 발생한 시간의 ISO 8601 타임스탬프([RFC 3339 섹션 5.6](https://datatracker.ietf.org/doc/html/rfc3339)에 따라 형식 지정). 이 타임스탬프 **must**&#x200B;은(는) 과거 날짜이지만 **must**&#x200B;은(는) 1970년 이후부터 시작됩니다. 이 필드 사용에 대한 모범 사례는 [타임스탬프](#timestamps)의 아래 섹션을 참조하십시오. |

{style="table-layout:auto"}

## 이벤트 모델링에 대한 우수 사례

다음 섹션에서는 Adobe Experience Platform에서 이벤트 기반 XDM(경험 데이터 모델) 스키마를 디자인하는 모범 사례를 다룹니다.

### 타임스탬프 {#timestamps}

이벤트 스키마의 루트 `timestamp` 필드는 이벤트 자체의 관찰을 **전용**&#x200B;할 수 있으며 과거에 발생해야 합니다. 그러나 이벤트 **must**&#x200B;은(는) 1970년 이후에 발생합니다. 세분화 사용 사례에서 향후 발생할 수 있는 타임스탬프를 사용해야 하는 경우 이러한 값은 경험 이벤트 스키마의 다른 곳에서 제한되어야 합니다.

예를 들어 여행 및 접대 업계의 비즈니스가 비행 예약 이벤트를 모델링하는 경우 클래스 수준 `timestamp` 필드는 예약 이벤트가 관찰된 시간을 나타냅니다. 여행 예약 시작 날짜와 같이 이벤트와 관련된 다른 타임스탬프는 표준 또는 사용자 지정 필드 그룹에서 제공하는 별도의 필드에 캡처해야 합니다.

![비행 예약 및 시작 날짜가 강조 표시된 샘플 경험 이벤트 스키마.](../images/classes/experienceevent/timestamps.png)

클래스 수준 타임스탬프를 이벤트 스키마의 다른 관련 날짜/시간 값과 별도로 유지함으로써 경험 애플리케이션에서 고객 여정의 타임스탬프가 지정된 계정을 유지하면서 유연한 세분화 사용 사례를 구현할 수 있습니다.

### 계산된 필드 사용 {#calculated}

경험 애플리케이션의 특정 상호 작용으로 인해 동일한 이벤트 타임스탬프를 기술적으로 공유하는 여러 관련 이벤트가 발생할 수 있으므로 단일 이벤트 레코드로 나타낼 수 있습니다. 예를 들어 고객이 웹 사이트에서 제품을 보는 경우 &quot;제품 보기&quot; 이벤트(`commerce.productViews`) 또는 일반 &quot;페이지 보기&quot; 이벤트(`web.webpagedetails.pageViews`)의 두 가지 가능한 `eventType` 값이 있는 이벤트 레코드가 발생할 수 있습니다. 이러한 경우 단일 히트에서 여러 이벤트가 캡처될 때 계산된 필드를 사용하여 가장 중요한 속성을 캡처할 수 있습니다.

[Adobe Experience Platform 데이터 준비](../../data-prep/home.md)를 사용하여 XDM과 데이터를 매핑, 변환 및 확인합니다. 서비스에서 제공하는 사용 가능한 [매핑 함수](../../data-prep/functions.md)를 사용하여 Experience Platform으로 수집될 때 여러 이벤트 레코드의 데이터를 우선 순위 지정, 변환 및/또는 통합하기 위해 논리 연산자를 호출할 수 있습니다. 위의 예에서 `eventType`을(를) 계산된 필드로 지정하여 둘 다 발생할 때마다 &quot;페이지 보기&quot;보다 &quot;제품 보기&quot;의 우선 순위를 지정할 수 있습니다.

UI를 통해 수동으로 Experience Platform에 데이터를 수집하는 경우 계산된 필드를 만드는 방법에 대한 특정 단계는 [계산된 필드](../../data-prep/ui/mapping.md#calculated-fields)의 안내서를 참조하십시오.

소스 연결을 사용하여 Experience Platform으로 데이터를 스트리밍하는 경우 계산된 필드를 대신 활용하도록 소스를 구성할 수 있습니다. 연결을 구성할 때 계산된 필드를 구현하는 방법에 대한 지침은 특정 원본의 [설명서](../../sources/home.md)를 참조하세요.

## 호환 가능한 스키마 필드 그룹 {#field-groups}

>[!NOTE]
>
>여러 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../field-groups/name-updates.md)에 대한 문서를 참조하십시오.

Adobe에서는 [!DNL XDM ExperienceEvent] 클래스와 함께 사용할 수 있는 여러 표준 필드 그룹을 제공합니다. 다음은 클래스에서 일반적으로 사용되는 몇 가지 필드 그룹 목록입니다.

* [[!UICONTROL Adobe Analytics ExperienceEvent 전체 확장]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 잔고 전송]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 캠페인 마케팅 세부 정보]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 카드 동작]](../field-groups/event/card-actions.md)
* [[!UICONTROL 채널 세부 정보]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce 세부 정보]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 예금 세부 정보]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 장치 거래 세부 정보]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 식사 예약]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 최종 사용자 ID 세부 정보]](../field-groups/event/enduserids.md)
* [[!UICONTROL 환경 세부 정보]](../field-groups/event/environment-details.md)
* [[!UICONTROL 비행 예약]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0 동의]](../field-groups/event/iab.md)
* [[!UICONTROL 숙박 예약]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics 상호 작용 세부 정보]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL 견적 요청 세부 정보]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 예약 세부 정보]](../field-groups/event/reservation-details.md)
* [[!UICONTROL 웹 세부 정보]](../field-groups/event/web-details.md)

## 부록

다음 섹션에는 [!UICONTROL XDM ExperienceEvent] 클래스에 대한 추가 정보가 포함되어 있습니다.

### `eventType`에 대해 허용되는 값 {#eventType}

다음 표에서는 `eventType`에 대해 허용되는 값과 해당 정의를 설명합니다.

| 값 | 정의 |
| --- | --- |
| `advertising.clicks` | 이 이벤트는 광고를 선택하는 작업이 발생하면 추적합니다. |
| `advertising.completes` | 이 이벤트는 시간 미디어 에셋이 완료될 때까지 관찰되면 추적합니다. 이는 뷰어가 앞으로 건너뛸 수도 있었으므로, 뷰어가 전체 비디오를 시청했다는 것을 반드시 의미하지는 않습니다. |
| `advertising.conversions` | 이 이벤트는 성능 평가를 위해 이벤트를 트리거하는 고객이 수행한 사전 정의된 작업을 추적합니다. |
| `advertising.federated` | 이 이벤트는 데이터 페더레이션(고객 간 데이터 공유)을 통해 경험 이벤트가 생성되었는지 추적합니다. |
| `advertising.firstQuartiles` | 이 이벤트는 디지털 비디오 광고 재생이 정상 속도로 25% 진행되면 추적합니다. |
| `advertising.impressions` | 이 이벤트는 잠재 고객이 볼 수 있는 광고의 노출 횟수를 추적합니다. |
| `advertising.midpoints` | 이 이벤트는 디지털 비디오 광고 재생이 정상 속도로 50% 진행되면 추적합니다. |
| `advertising.starts` | 이 이벤트는 디지털 비디오 광고 재생이 시작되면 추적합니다. |
| `advertising.thirdQuartiles` | 이 이벤트는 디지털 비디오 광고 재생이 정상 속도로 75% 진행되면 추적합니다. |
| `advertising.timePlayed` | 이 이벤트는 특정 시간 미디어 에셋에서 사용자가 사용한 시간을 추적합니다. |
| `application.close` | 이 이벤트는 애플리케이션이 닫히거나 백그라운드로 전송되면 추적합니다. |
| `application.launch` | 이 이벤트는 애플리케이션을 시작하거나 포그라운드로 가져올 때 추적합니다. |
| `click` | **사용하지 않음** 대신 `decisioning.propositionInteract`을(를) 사용하십시오. |
| `commerce.backofficeCreditMemoIssued` | 이 이벤트는 고객에게 신용 공지가 발행되면 추적합니다. |
| `commerce.backofficeOrderCancelled` | 이 이벤트는 이전에 시작된 구매 프로세스가 완료 전에 종료되면 추적합니다. |
| `commerce.backofficeOrderItemsShipped` | 이 이벤트는 구매한 항목이 실제로 고객에게 배송된 경우를 추적합니다. |
| `commerce.backofficeOrderPlaced` | 이 이벤트는 주문 배치를 추적합니다. |
| `commerce.backofficeShipmentCompleted` | 이 이벤트는 전체 선적 프로세스의 성공적인 완료를 추적합니다. |
| `commerce.checkouts` | 이 이벤트는 제품 목록에 대해 체크아웃 이벤트가 발생하면 추적합니다. 체크아웃 프로세스에 여러 단계가 있는 경우 두 개 이상의 체크아웃 이벤트가 있을 수 있습니다. 여러 단계가 있는 경우 타임스탬프 및 각 이벤트에 대해 참조된 페이지/경험을 사용하여 순서대로 표시되는 각 개별 이벤트(단계)를 식별합니다. |
| `commerce.productListAdds` | 이 이벤트는 제품이 제품 목록 또는 장바구니에 추가되면 추적합니다. |
| `commerce.productListOpens` | 이 이벤트는 새 제품 목록(장바구니)이 초기화되거나 생성될 때 추적합니다. |
| `commerce.productListRemovals` | 이 이벤트는 제품 항목이 제품 목록 또는 장바구니에서 제거되면 추적합니다. |
| `commerce.productListReopens` | 이 이벤트는 고객이 더 이상 액세스할 수 없는(포기된) 제품 목록(장바구니)을 재활성화한 경우(예: 리마케팅 활동을 통해) 추적합니다. |
| `commerce.productListViews` | 이 이벤트는 제품 목록 또는 장바구니가 보기를 받으면 추적합니다. |
| `commerce.productViews` | 이 이벤트는 제품이 하나 이상의 보기를 수신하면 추적합니다. |
| `commerce.purchases` | 이 이벤트는 주문이 수락되면 추적합니다. 이것은 상거래 전환에서 유일한 필수 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `commerce.saveForLaters` | 이 이벤트는 제품 위시리스트 등 향후 사용을 위해 제품 목록이 저장되면 추적합니다. |
| `decisioning.propositionDisplay` | 이 이벤트는 웹 SDK이 페이지에 표시되는 내용에 대한 정보를 자동으로 보낼 때 사용됩니다. 하지만 페이지 히트의 상단과 하단과 같은 다른 방식으로 표시 정보를 이미 포함하고 있는 경우에는 이 이벤트 유형이 필요하지 않습니다. 페이지 히트의 맨 아래에서 원하는 이벤트 유형을 선택할 수 있습니다. |
| `decisioning.propositionDismiss` | 이 이벤트 유형은 Adobe Journey Optimizer 신청 내 메시지 또는 콘텐츠 카드가 기각될 때 사용됩니다. |
| `decisioning.propositionFetch` | 이벤트가 주로 의사 결정을 가져오기 위한 것임을 나타내는 데 사용됩니다. Adobe Analytics에서 이 이벤트를 자동으로 삭제합니다. |
| `decisioning.propositionInteract` | 이 이벤트 유형은 개인화된 콘텐츠에서 클릭 수와 같은 상호 작용을 추적하는 데 사용됩니다. |
| `decisioning.propositionSend` | 이 이벤트는 잠재 고객에게 추천 또는 고려 제안을 보내기로 결정한 경우 추적합니다. |
| `decisioning.propositionTrigger` | 이 유형의 이벤트는 [Web SDK](../../web-sdk/home.md)에서 로컬 저장소에 저장되지만 Experience Edge으로 전송되지 않습니다. 규칙 세트가 충족될 때마다 이벤트가 생성되고 로컬 저장소에 저장됩니다(해당 설정이 활성화된 경우). |
| `delivery.feedback` | 이 이벤트는 이메일 게재와 같은 게재의 피드백 이벤트를 추적합니다. |
| `directMarketing.emailBounced` | 이 이벤트는 개인에게 전송된 이메일이 반송되면 추적합니다. |
| `directMarketing.emailBouncedSoft` | 이 이벤트는 개인에게 보낸 이메일이 소프트 바운스되면 추적합니다. |
| `directMarketing.emailClicked` | 이 이벤트는 사용자가 마케팅 이메일의 링크를 클릭했을 때 추적됩니다. |
| `directMarketing.emailDelivered` | 이 이벤트는 이메일이 개인의 이메일 서비스에 성공적으로 전달될 때 추적합니다. |
| `directMarketing.emailOpened` | 이 이벤트는 사용자가 마케팅 이메일을 열었을 때 추적합니다. |
| `directMarketing.emailSent` | 이 이벤트는 마케팅 이메일이 사용자에게 전송되면 추적합니다. |
| `directMarketing.emailUnsubscribed` | 이 이벤트는 사용자가 마케팅 이메일의 구독을 취소하면 추적합니다. |
| `display` | **사용하지 않음** 대신 `decisioning.propositionDisplay`을(를) 사용하십시오. |
| `inappmessageTracking.dismiss` | 이 이벤트는 인앱 메시지가 무시되면 추적합니다. |
| `inappmessageTracking.display` | 이 이벤트는 인앱 메시지가 표시되면 추적합니다. |
| `inappmessageTracking.interact` | 이 이벤트는 인앱 메시지가 상호 작용할 때 추적합니다. |
| `leadOperation.callWebhook` | 이 이벤트는 리드에 대한 응답으로 Webhook이 호출되면 추적합니다. |
| `leadOperation.changeCampaignStream` | 이 이벤트는 특정 비즈니스 리드에 대한 마케팅 또는 참여 전략의 전환을 나타냅니다. |
| `leadOperation.changeEngagementCampaignCadence` | 이 이벤트는 잠재 고객이 캠페인의 일부로 참여하는 빈도가 변경된 경우 추적합니다. |
| `leadOperation.convertLead` | 이 이벤트는 잠재 고객 전환 시 추적합니다. |
| `leadOperation.interestingMoment` | 이 이벤트는 한 사람에게 재미있는 순간을 기록할 때 추적합니다. |
| `leadOperation.mergeLeads` | 이 이벤트는 동일한 엔터티를 참조하는 여러 리드의 정보가 통합되면 추적합니다. |
| `leadOperation.newLead` | 이 이벤트는 잠재 고객 생성 시 추적합니다. |
| `leadOperation.scoreChanged` | 이 이벤트는 잠재 고객의 스코어 속성 값이 변경되면 추적합니다. |
| `leadOperation.statusInCampaignProgressionChanged` | 이 이벤트는 캠페인에서 잠재 고객의 상태가 변경되면 추적합니다. |
| `listOperation.addToList` | 이 이벤트는 마케팅 목록에 개인이 추가되면 추적합니다. |
| `listOperation.removeFromList` | 이 이벤트는 마케팅 목록에서 개인이 제거되면 추적합니다. |
| `media.adBreakComplete` | 이 이벤트는 광고 브레이크를 완료한다는 신호를 보냅니다. |
| `media.adBreakStart` | 이 이벤트는 광고 브레이크를 시작한다는 신호를 보냅니다. |
| `media.adComplete` | 이 이벤트는 광고가 완료되었음을 나타냅니다. |
| `media.adSkip` | 이 이벤트는 광고를 건너뛸 때 신호를 보냅니다. |
| `media.adStart` | 이 이벤트는 광고를 시작한다는 신호를 보냅니다. |
| `media.bitrateChange` | 이 이벤트는 비트 전송률이 변경되면 신호를 보냅니다. |
| `media.bufferStart` | 버퍼링이 시작되면 `media.bufferStart` 이벤트 유형이 전송됩니다. 특정 `bufferResume` 이벤트 유형이 없습니다. `bufferStart` 이벤트 다음에 `play` 이벤트가 전송될 때 버퍼링이 다시 시작된 것으로 간주됩니다. |
| `media.chapterComplete` | 이 이벤트는 챕터를 완료한다는 신호를 보냅니다. |
| `media.chapterSkip` | 이 이벤트는 사용자가 다른 섹션이나 챕터로 앞이나 뒤로 건너뛸 때 트리거됩니다. |
| `media.chapterStart` | 이 이벤트는 챕터를 시작한다는 신호를 보냅니다. |
| `media.downloaded` | 이 이벤트는 미디어가 다운로드한 콘텐츠가 발생하면 추적합니다. |
| `media.error` | 이 이벤트는 미디어 재생 중에 오류가 발생하면 신호를 보냅니다. |
| `media.pauseStart` | 이 이벤트는 `pauseStart` 이벤트가 발생하면 추적합니다. 이 이벤트는 사용자가 미디어 재생에서 일시 중지를 시작할 때 트리거됩니다. 다시 시작 이벤트 유형이 없습니다. 다시 시작은 재생 이벤트를 `pauseStart` 뒤에 보낼 때 추론됩니다. |
| `media.ping` | `media.ping` 이벤트 유형은 진행 중인 재생 상태를 나타내는 데 사용됩니다. 기본 콘텐츠의 경우, 이 이벤트는 재생 중에 10초마다 전송되어야 하며 재생이 시작된 후 10초부터 시작됩니다. 광고 콘텐츠의 경우 광고 추적 중에 매초마다 전송되어야 합니다. Ping 이벤트는 요청 본문에 매개 변수 맵을 포함하지 않아야 합니다. |
| `media.play` | `media.play` 이벤트 유형은 플레이어가 다른 상태(예: `buffering,` `paused`(사용자가 다시 시작할 때) 또는 `error`(복구될 때)에서 `playing` 상태로 전환될 때 전송됩니다. 여기에는 자동 재생과 같은 시나리오도 포함됩니다. 이 이벤트는 플레이어의 `on('Playing')` 콜백에 의해 트리거됩니다. |
| `media.sessionComplete` | 이 이벤트는 기본 콘텐츠의 끝에 도달하면 전송됩니다. |
| `media.sessionEnd` | `media.sessionEnd` 이벤트 유형은 사용자가 보기를 중단하여 반환할 가능성이 낮은 경우 세션을 즉시 닫도록 Media Analytics 백엔드에 알립니다. 이 이벤트가 전송되지 않으면, 10분 동안 활동이 없거나 플레이헤드 이동 없이 30분 후에 세션이 시간 초과됩니다. 해당 세션 ID를 사용하는 후속 미디어 호출은 무시됩니다. |
| `media.sessionStart` | `media.sessionStart` 이벤트 유형이 세션 시작 호출과 함께 전송됩니다. 응답을 받으면 위치 헤더에서 세션 ID가 추출되고 수집 서버에 대한 모든 후속 이벤트 호출에 사용됩니다. |
| `media.statesUpdate` | 이 이벤트는 `statesUpdate` 이벤트가 발생하면 추적합니다. 플레이어 상태 추적 기능을 오디오 또는 비디오 스트림에 연결할 수 있습니다. 표준 상태는 `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` 및 `inFocus`입니다. |
| `opportunityEvent.addToOpportunity` | 이 이벤트는 한 사람이 기회에 추가되면 추적합니다. |
| `opportunityEvent.opportunityUpdated` | 이 이벤트는 기회가 업데이트되면 추적합니다. |
| `opportunityEvent.removeFromOpportunity` | 이 이벤트는 영업 기회에서 개인이 제거되면 추적합니다. |
| `personalization.request` | **사용하지 않음** 대신 `decisioning.propositionFetch`을(를) 사용하십시오. |
| `pushTracking.applicationOpened` | 이 이벤트는 사용자가 푸시 알림에서 애플리케이션을 열 때 추적합니다. |
| `pushTracking.customAction` | 이 이벤트는 사용자가 푸시 알림에서 사용자 지정 작업을 선택할 때 추적합니다. |
| `web.formFilledOut` | 이 이벤트는 사용자가 웹 페이지에서 양식을 작성할 때 추적합니다. |
| `web.webinteraction.linkClicks` | 이 이벤트는 링크 클릭이 웹 SDK에 의해 자동으로 기록되었음을 나타냅니다. |
| `web.webpagedetails.pageViews` | 이 이벤트 유형은 히트를 페이지 보기로 표시하는 표준 방법입니다. |
| `location.entry` | 이 이벤트는 특정 위치에 있는 사용자 또는 장치의 항목을 추적합니다. |
| `location.exit` | 이 이벤트는 특정 위치에서 개인 또는 장치의 종료를 추적합니다. |

{style="table-layout:auto"}

### `producedBy`에 대한 제안 값 {#producedBy}

다음 표에서는 `producedBy`에 대해 허용되는 일부 값을 간략하게 설명합니다.

| 값 | 정의 |
| --- | --- |
| `self` | 자가 |
| `system` | 시스템 |
| `salesRef` | 영업 담당자 |
| `customerRep` | 고객 담당자 |
