---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM ExperienceEvent 클래스
topic: overview
description: 이 문서에서는 XDM ExperienceEvent 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 은 특정 이벤트가 발생하거나 특정 조건 세트에 도달할 때 타임스탬프가 지정된 시스템 스냅샷을 만들 수 있는 표준 XDM 클래스입니다.

경험 이벤트는 관련된 개인의 시점 및 ID를 비롯하여 발생한 사실에 대한 팩트 레코드입니다. 이벤트는 명시적(직접 관찰 가능한 인간 작업) 또는 암시적(직접 행동 없이 발생)일 수 있으며 집계 또는 해석 없이 기록됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요를 참조하십시오](../home.md#data-behaviors).

클래스 자체는 [!DNL XDM ExperienceEvent] 스키마에 여러 시간 연속 관련 필드를 제공합니다. 이러한 필드 중 일부는 데이터를 수집할 때 자동으로 채워집니다.

<img src="../images/classes/experienceevent.png" width="650" /><br />

| 속성 | 설명 |
| --- | --- |
| `_id` | 이벤트에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 이벤트의 고유성을 추적하고 데이터 중복을 방지하며 다운스트림 서비스에서 해당 이벤트를 조회하는 데 사용됩니다. 이 필드는 시스템에서 생성되므로 데이터 수집 중에 명시적 값을 제공해서는 안 됩니다.<br><br>이 필드는 개인 사용자와 관련된 ID가 **아니라** 데이터 자체의 기록을 나타낸다는 것을 구분하는 것이 중요합니다. 신분자료는 신분관계를 조건으로 해서 [신분관계로](../schema/composition.md#identity) 분류한다. |
| `eventMergeId` | 레코드를 만든 인제스트된 일괄 처리 ID입니다. 이 필드는 데이터 수집 시 시스템에 의해 자동으로 채워집니다. |
| `eventType` | 레코드의 기본 이벤트 유형을 나타내는 문자열. 승인된 값과 그 정의는 [부록 섹션에 제공됩니다](#eventType). |
| `identityMap` | 이벤트가 적용되는 개별 ID의 세트가 포함된 지도 필드. ID 데이터가 수집되면 이 필드는 시스템에 의해 자동으로 업데이트됩니다. 실시간 고객 프로필에 이 필드를 [적절히 활용하려면 데이터](../../profile/home.md)작업에서 필드 내용을 수동으로 업데이트하지 마십시오.<br /><br />사용 사례에 대한 자세한 내용은 스키마 구성 [의 기본 사항에](../schema/composition.md#identityMap) 있는 ID 맵에 대한 섹션을 참조하십시오. |
| `timestamp` | 사건이나 관찰이 발생한 시간입니다. |

## 호환 가능한 믹싱 {#mixins}

Adobe은 [!DNL XDM ExperienceEvent] 클래스에 사용할 수 있는 여러 가지 표준 믹스를 제공합니다. 다음은 이 교실에 일반적으로 사용되는 믹스인 목록입니다.

* [[!UICONTROL ExperienceEvent EndUserIDs]](../mixins/event/enduserids.md)
* [[!UICONTROL ExperienceEvent 환경 세부 사항]](../mixins/event/environment-details.md)

## 부록

다음 섹션에는 [!UICONTROL XDM ExperienceEvent 클래스에 대한 추가 정보가] 포함되어 있습니다.

### xdm:eventType에 허용된 값 {#eventType}

다음 표에서는 허용된 값과 해당 정의 `xdm:eventType`의 개요를 설명합니다.

| 값 | 정의 |
| --- | --- |
| `advertising.completes` | 시간 미디어 자산이 완료되는 것을 확인했습니다. 시청자가 미리 건너뛸 수 있기 때문에 시청자가 전체 비디오를 시청했다는 의미는 아닙니다. |
| `advertising.timePlayed` | 특정 시간 제한 미디어 자산에서 사용자가 보낸 시간을 설명합니다. |
| `advertising.federated` | 데이터 통합을 통해 경험 이벤트를 만들었는지(고객 간의 데이터 공유) 여부를 나타냅니다. |
| `advertising.clicks` | 광고에서 작업을 클릭합니다. |
| `advertising.conversions` | 성능 평가를 위한 이벤트를 트리거하는 고객이 사전에 정의한 작업입니다. |
| `advertising.firstQuartiles` | 디지털 동영상 광고가 전체 재생 기간의 25%를 보통 속도로 재생했다. |
| `advertising.impressions` | 볼 수 있는 가능성이 있는 고객에 대한 광고 노출 |
| `advertising.midpoints` | 디지털 동영상 광고가 전체 재생 시간의 50%를 평상시보다 빠르게 재생했다. |
| `advertising.starts` | 디지털 비디오 광고 재생이 시작되었습니다. |
| `advertising.thirdQuartiles` | 디지털 동영상 광고가 전체 재생 기간의 75%를 평상시보다 빠르게 재생했다. |
| `web.webpagedetails.pageViews` | 웹 페이지에서 하나 이상의 보기를 수신했습니다. |
| `web.webinteraction.linkClicks` | 링크가 하나 이상의 클릭을 수신했습니다. |
| `commerce.checkouts` | 제품 목록에 대해 체크아웃 이벤트가 발생했습니다. 체크아웃 프로세스에 여러 단계가 있을 경우 체크아웃 이벤트가 두 개 이상 있을 수 있습니다. 여러 단계가 있는 경우 각 이벤트에 대한 타임스탬프 및 참조된 페이지/경험이 각 개별 이벤트(단계)를 순서대로 식별하는 데 사용됩니다. |
| `commerce.productListAdds` | 제품이 제품 목록 또는 장바구니에 추가되었습니다. |
| `commerce.productListOpens` | 새 제품 목록(장바구니)이 초기화되었거나 만들어졌습니다. |
| `commerce.productListRemovals` | 제품 목록 또는 장바구니에서 하나 이상의 제품 항목이 제거되었습니다. |
| `commerce.productListReopens` | 더 이상 액세스(중단)되지 않은 제품 목록(장바구니)이 재마케팅 활동을 통해 재활성화되었습니다. |
| `commerce.productListViews` | 제품 목록 또는 장바구니에 보기가 하나 이상 수신되었습니다. |
| `commerce.productViews` | 제품이 하나 이상의 보기를 수신했습니다. |
| `commerce.purchases` | 주문이 수락되었습니다. 이것은 상거래 전환에서 필요한 유일한 작업입니다. 구매 이벤트에는 참조된 제품 목록이 있어야 합니다. |
| `commerce.saveForLaters` | 나중에 사용할 수 있도록 제품 목록이 저장되었습니다(예: 제품 위시리스트). |
| `delivery.feedback` | 이메일 배달과 같은 배달 피드백 이벤트입니다. |
| `message.feedback` | 고객에게 보낸 메시지에 대한 전송/바운스/오류 등의 피드백 이벤트. |
| `message.tracking` | 고객에게 보낸 메시지에 대한 열기/클릭/사용자 지정 동작과 같은 이벤트를 추적합니다. |