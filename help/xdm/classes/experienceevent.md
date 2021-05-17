---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;스키마;XDM;개별 프로필;필드;스키마;ID맵;ID 맵;스키마 디자인;맵;결합 스키마;공용 스키마
solution: Experience Platform
title: XDM ExperienceEvent 클래스
topic-legacy: overview
description: 이 문서에서는 XDM ExperienceEvent 클래스의 개요를 제공합니다.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 는 특정 이벤트가 발생하거나 특정 조건 세트에 도달할 때 타임스탬프가 지정된 시스템 스냅샷을 만들 수 있는 표준 XDM(Experience Data Model) 클래스입니다.

경험 이벤트는 관련된 개인의 시점 및 ID를 비롯하여 발생한 사실에 대한 팩트 레코드입니다. 이벤트는 명시적(직접 관찰할 수 있는 인간 작업) 또는 암시적(직접 작업하지 않고 발생)일 수 있으며 집계 또는 해석 없이 기록됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors)를 참조하십시오.

[!DNL XDM ExperienceEvent] 클래스 자체는 스키마에 여러 시간 시리즈 관련 필드를 제공합니다. 이러한 필드 중 일부는 데이터를 인제스트할 때 자동으로 채워집니다.

![](../images/classes/experienceevent/structure.png)

| 속성 | 설명 |
| --- | --- |
| `_id` | 이벤트에 대한 고유 문자열 식별자입니다. 이 필드는 개별 이벤트의 고유성을 추적하고 데이터 중복을 방지하고 다운스트림 서비스에서 해당 이벤트를 찾는 데 사용됩니다.<br><br>경우에 따라 UUID( `_id` Universal Unique Identifier)  [또는 GUID(](https://tools.ietf.org/html/rfc4122) Globally Unique Identifier) [일 수 있습니다](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0). Adobe Experience Platform 데이터 준비에서 이 값은 [`uuid` 또는 `guid` 매핑 함수](../../data-prep/functions.md#special-operations)를 사용하여 생성할 수 있습니다.<br><br>소스 연결에서 데이터를 스트리밍하거나 Componer 파일에서 직접 인제스트하는 경우 기본 ID, 타임스탬프, 이벤트 유형 등과 같이 고유한 특정 조합 필드를 연결하여 이 값을 생성해야 합니다.<br><br>이 필드는 개인 **과 관련된 ID를 나타내지 않고** 데이터 자체의 레코드를 구별하는 것이 중요합니다. 사람과 관련된 ID 데이터는 호환 가능한 믹스에서 대신 [ID 필드](../schema/composition.md#identity)로 분류해야 합니다. |
| `eventMergeId` | [Adobe Experience Platform Web SDK](../../edge/home.md)를 사용하여 데이터를 인제스트하는 경우 이 값은 레코드를 만드는 인제스트된 일괄 처리의 ID를 나타냅니다. 이 필드는 데이터 수집 시 시스템에 의해 자동으로 채워집니다. 웹 SDK 구현 컨텍스트 외부에서 이 필드의 사용은 지원되지 않습니다. |
| `eventType` | 이벤트의 유형 또는 범주를 나타내는 문자열. 이 필드는 제품 보기 이벤트와 소매 회사의 장바구니 추가/추가 이벤트를 구별하는 것과 같이 동일한 스키마 및 데이터 세트 내의 다른 이벤트 유형을 구별하려는 경우 사용할 수 있습니다.<br><br>이 속성에 대한 표준 값은 해당 사용 사례에 대한 설명을 포함하여  [부록 섹션에](#eventType) 제공됩니다. 이 필드는 확장 가능한 열거형입니다. 즉, 자체 이벤트 유형 문자열을 사용하여 추적 중인 이벤트를 분류할 수도 있습니다. |
| `producedBy` | 이벤트의 프로듀서 또는 원본을 설명하는 문자열 값입니다. 세그멘테이션을 위해 필요한 경우 이 필드를 사용하여 특정 이벤트 프로듀서를 필터링할 수 있습니다.<br><br>이 속성에 대해 제안된 일부 값은  [부록 섹션에 제공됩니다](#producedBy). 이 필드는 확장 가능한 열거형입니다. 즉, 자체 문자열을 사용하여 다른 이벤트 프로듀서를 나타낼 수도 있습니다. |
| `identityMap` | 이벤트가 적용되는 개별 ID 세트를 포함하는 맵 필드입니다. 이 필드는 ID 데이터를 수집할 때 시스템에 의해 자동으로 업데이트됩니다. [실시간 고객 프로필](../../profile/home.md)에 이 필드를 제대로 활용하려면 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />사용 사례에 대한 자세한 내용은 스키마 구성 [의 기본 사항](../schema/composition.md#identityMap) 에서 ID 맵에 대한 섹션을 참조하십시오. |
| `timestamp` | [RFC 3339 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)에 따라 형식이 지정된 이벤트가 발생한 ISO 8601 타임스탬프. 이 타임스탬프는 과거에 발생해야 합니다. 이 필드 사용에 대한 우수 사례가 필요하면 [타임스탬프](#timestamps)의 아래 섹션을 참조하십시오. |

## 이벤트 모델링에 대한 우수 사례

다음 섹션에서는 Adobe Experience Platform에서 이벤트 기반 XDM(Experience Data Model) 스키마를 디자인하기 위한 모범 사례를 설명합니다.

### 타임스탬프 {#timestamps}

이벤트 스키마의 루트 `timestamp` 필드는 **만**&#x200B;에 이벤트 자체의 관찰을 나타낼 수 있으며 과거에 발생해야 합니다. 세그멘테이션 사용 사례가 나중에 발생할 수 있는 타임스탬프를 사용해야 하는 경우 이러한 값은 경험 이벤트 스키마의 다른 부분에 제한되어야 합니다.

예를 들어 여행 및 숙박 업계의 사업이 비행 예약 이벤트를 모델링하는 경우 클래스 수준 `timestamp` 필드는 예약 이벤트가 관찰된 시간을 나타냅니다. 여행 예약 시작 날짜 등 해당 이벤트와 관련된 다른 타임스탬프는 표준 또는 사용자 정의 믹싱으로 제공되는 별도의 필드에 캡처해야 합니다.

![](../images/classes/experienceevent/timestamps.png)

클래스 수준 타임스탬프를 이벤트 스키마의 다른 관련 datetime 값과 구분하도록 함으로써 경험 애플리케이션에서 고객 여정의 타임스탬프가 지정된 계정을 유지하면서 유연한 세그멘테이션 사용 사례를 구현할 수 있습니다.

### 계산된 필드 사용

경험 애플리케이션의 특정 상호 작용으로 인해 기술적으로 동일한 이벤트 타임스탬프를 공유하는 여러 관련 이벤트가 발생할 수 있으므로 단일 이벤트 레코드로 나타낼 수 있습니다. 예를 들어 고객이 웹 사이트에서 제품을 보는 경우 &quot;제품 보기&quot; 속성은 물론 일부 중복된 일반 &quot;페이지 보기&quot; 속성이 포함된 이벤트 레코드가 나타날 수 있습니다. 이러한 경우 여러 이벤트가 기록에서 캡처될 때 계산된 필드를 사용하여 가장 중요한 속성을 캡처할 수 있습니다.

[Adobe Experience Platform Data ](../../data-prep/home.md) Preflight를 사용하면 XDM을 통해 데이터를 매핑, 변형 및 확인할 수 있습니다. 서비스에서 제공하는 사용 가능한 [매핑 함수](../../data-prep/functions.md)를 사용하여 Experience Platform으로 인제스트할 때 논리 연산자를 호출하여 다중 이벤트 레코드의 데이터를 우선 순위를 지정하고, 변형하고/또는 통합할 수 있습니다.

UI를 통해 수동으로 데이터를 플랫폼에 인제스트하는 경우, 계산된 필드를 만드는 방법에 대한 특정 단계는 [CSV 파일을 XDM](../../ingestion/tutorials/map-a-csv-file.md)에 매핑하는 가이드를 참조하십시오.

소스 연결을 사용하여 Platform으로 데이터를 스트리밍하는 경우 소스를 구성하여 계산된 필드를 대신 활용할 수 있습니다. 연결을 구성할 때 계산된 필드를 구현하는 방법에 대한 지침은 특정 소스](../../sources/home.md)에 대한 [설명서를 참조하십시오.

## 호환 가능한 스키마 필드 그룹 {#field-groups}

>[!NOTE]
>
>여러 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../field-groups/name-updates.md)의 문서를 참조하십시오.

Adobe은 [!DNL XDM ExperienceEvent] 클래스에 사용할 수 있도록 여러 개의 표준 필드 그룹을 제공합니다. 다음은 클래스에 일반적으로 사용되는 일부 필드 그룹 목록입니다.

* [[!UICONTROL 최종 사용자 ID 세부 사항]](../field-groups/event/enduserids.md)
* [[!UICONTROL 환경 세부 사항]](../field-groups/event/environment-details.md)

## 부록

다음 섹션에는 [!UICONTROL XDM ExperienceEvent] 클래스에 대한 추가 정보가 포함되어 있습니다.

### `eventType`에 허용된 값 {#eventType}

다음 표에서는 `eventType`에 대해 허용된 값을 해당 정의와 함께 개괄합니다.

| 값 | 정의 |
| --- | --- |
| `advertising.completes` | 완료 시 미디어 에셋을 감시했습니다. 뷰어가 건너뛸 수 있기 때문에 시청자가 전체 비디오를 시청했다고 볼 필요는 없습니다. |
| `advertising.timePlayed` | 특정 시간 제한 미디어 자산에서 사용자가 보낸 시간을 설명합니다. |
| `advertising.federated` | 데이터 통합을 통해 경험 이벤트가 만들어졌는지(고객 간의 데이터 공유) 여부를 나타냅니다. |
| `advertising.clicks` | 광고에서 작업을 클릭합니다. |
| `advertising.conversions` | 성능 평가를 위한 이벤트를 트리거하는 고객이 사전에 정의한 작업입니다. |
| `advertising.firstQuartiles` | 디지털 비디오 광고는 전체 재생 시간의 25%를 정상적인 속도로 재생했습니다. |
| `advertising.impressions` | 고객에게 보여질 가능성이 있는 광고의 노출 수 |
| `advertising.midpoints` | 디지털 비디오 광고는 전체 재생 시간의 50%를 정상적인 속도로 재생했습니다. |
| `advertising.starts` | 디지털 비디오 광고 재생이 시작되었습니다. |
| `advertising.thirdQuartiles` | 디지털 비디오 광고는 재생 시간의 75%를 정상적인 속도로 재생했습니다. |
| `web.webpagedetails.pageViews` | 웹 페이지에서 하나 이상의 보기를 수신했습니다. |
| `web.webinteraction.linkClicks` | 링크가 하나 이상 선택되었습니다. |
| `commerce.checkouts` | 제품 목록에 대해 체크아웃 이벤트가 발생했습니다. 체크아웃 프로세스에 여러 단계가 있을 경우 체크아웃 이벤트를 두 개 이상 사용할 수 있습니다. 여러 단계가 있는 경우 각 이벤트에 대한 타임스탬프 및 참조된 페이지/경험이 각 개별 이벤트(단계)를 순서대로 식별하는 데 사용됩니다. |
| `commerce.productListAdds` | 제품이 제품 목록 또는 장바구니에 추가되었습니다. |
| `commerce.productListOpens` | 새 제품 목록(장바구니)이 초기화되거나 만들어졌습니다. |
| `commerce.productListRemovals` | 제품 목록 또는 장바구니에서 하나 이상의 제품 항목이 제거되었습니다. |
| `commerce.productListReopens` | 더 이상 액세스할 수 없게(중단된) 제품 목록(장바구니)이 재마케팅 활동을 통해 재활성화되었습니다. |
| `commerce.productListViews` | 제품 목록 또는 장바구니에 하나 이상의 보기가 수신되었습니다. |
| `commerce.productViews` | 제품이 하나 이상의 보기를 받았습니다. |
| `commerce.purchases` | 주문이 수락되었습니다. 이것은 상거래 전환에서 유일하게 필요한 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `commerce.saveForLaters` | 나중에 사용할 수 있도록 제품 목록이 저장되었습니다(예: 제품 희망 목록). |
| `delivery.feedback` | 이메일 배달과 같은 배달에 대한 피드백 이벤트입니다. |
| `message.feedback` | 고객에게 보낸 메시지에 대한 전송/바운스/오류 등의 피드백 이벤트. |
| `message.tracking` | 고객에게 전송된 메시지에 대해 열린/클릭/사용자 지정 동작과 같은 이벤트를 추적합니다. |

### `producedBy`에 대해 제안된 값 {#producedBy}

다음 표에서는 `producedBy`에 대해 허용되는 일부 값에 대해 대략적으로 설명합니다.

| 값 | 정의 |
| --- | --- |
| `self` | 자체 |
| `system` | 시스템 |
| `salesRef` | 영업 담당자 |
| `customerRep` | 고객 담당자 |
