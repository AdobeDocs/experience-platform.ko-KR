---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;스키마;XDM;개별 프로필;필드;스키마;ID맵;ID 맵;스키마 디자인;맵;결합 스키마;공용 스키마
solution: Experience Platform
title: XDM ExperienceEvent 클래스
topic-legacy: overview
description: 이 문서에서는 XDM ExperienceEvent 클래스의 개요를 제공합니다.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 은 특정 이벤트가 발생하거나 특정 조건 세트에 도달할 때 타임스탬프가 지정된 시스템 스냅샷을 만들 수 있는 표준 XDM 클래스입니다.

경험 이벤트는 관련된 개인의 시점 및 ID를 비롯하여 발생한 사실에 대한 팩트 레코드입니다. 이벤트는 명시적(직접 관찰할 수 있는 인간 작업) 또는 암시적(직접 작업하지 않고 발생)일 수 있으며 집계 또는 해석 없이 기록됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors)를 참조하십시오.

[!DNL XDM ExperienceEvent] 클래스 자체는 스키마에 여러 시간 시리즈 관련 필드를 제공합니다. 이러한 필드 중 일부는 데이터를 인제스트할 때 자동으로 채워집니다.

<img src="../images/classes/experienceevent.png" width="650" /><br />

| 속성 | 설명 |
| --- | --- |
| `_id` | 이벤트에 대한 고유한 시스템 생성 문자열 식별자. 이 필드는 개별 이벤트의 고유성을 추적하고 데이터 중복을 방지하고 다운스트림 서비스에서 해당 이벤트를 조회하는 데 사용됩니다. 이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공해서는 안 됩니다.<br><br>이 필드는 개별 개인 **과 관련된 ID를** 제공하지 않고 데이터 자체의 레코드를 구별하는 것이 중요합니다. 사람과 관련된 ID 데이터는 대신 [ID 필드](../schema/composition.md#identity)로 분류해야 합니다. |
| `eventMergeId` | 레코드를 만든 인제스트된 일괄 처리의 ID. 이 필드는 데이터 수집 시 시스템에 의해 자동으로 채워집니다. |
| `eventType` | 레코드에 대한 기본 이벤트 유형을 나타내는 문자열. 허용된 값과 그 정의는 [부록 섹션](#eventType)에 제공됩니다. |
| `identityMap` | 이벤트가 적용되는 개별 ID 세트를 포함하는 맵 필드입니다. 이 필드는 ID 데이터를 수집할 때 시스템에 의해 자동으로 업데이트됩니다. [실시간 고객 프로필](../../profile/home.md)에 이 필드를 제대로 활용하려면 데이터 작업에서 필드의 내용을 수동으로 업데이트하지 마십시오.<br /><br />사용 사례에 대한 자세한 내용은 스키마 구성 [의 기본 사항](../schema/composition.md#identityMap) 에서 ID 맵에 대한 섹션을 참조하십시오. |
| `timestamp` | [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)에 따라 지정된 이벤트 또는 관찰이 발생한 시간입니다. |

## 호환 가능한 믹싱 {#mixins}

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../mixins/name-updates.md)에 있는 문서를 참조하십시오.

Adobe은 [!DNL XDM ExperienceEvent] 클래스에 사용할 수 있도록 여러 가지 표준 믹스를 제공합니다. 다음은 클래스에 일반적으로 사용되는 일부 믹싱 목록입니다.

* [[!UICONTROL End User ID Details]](../mixins/event/enduserids.md)
* [[!UICONTROL Environment Details]](../mixins/event/environment-details.md)

## 부록

다음 섹션에는 [!UICONTROL XDM ExperienceEvent] 클래스에 대한 추가 정보가 포함되어 있습니다.

### xdm:eventType {#eventType}에 허용된 값

다음 표에서는 `xdm:eventType`에 대해 허용된 값을 해당 정의와 함께 개괄합니다.

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
