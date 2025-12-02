---
title: 이벤트 보내기
description: Adobe Experience Platform Edge Network으로 데이터를 전송합니다.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 이벤트 보내기

**[!UICONTROL Send event]** 작업은 Adobe Experience Platform Edge Network의 데이터 스트림으로 페이로드를 보냅니다. 데이터 수집 및 개인화의 핵심 기능입니다. 거의 모든 조직에서 이 작업을 웹 SDK 구현의 일부로 사용합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Send event]**(으)로 설정합니다.

## 일반 필드

![이벤트 보내기 작업 형식에 대한 인스턴스 설정을 보여 주는 Experience Platform 태그 UI 이미지입니다.](../assets/instance-settings.png)

* **[!UICONTROL Instance]**: 작업이 적용되는 SDK 인스턴스입니다. 구현에서 단일 SDK 인스턴스를 사용하는 경우 이 드롭다운 메뉴가 비활성화됩니다.
* **[!UICONTROL Use guided events]**: 특정 사용 사례를 사용하도록 특정 필드를 자동으로 채우거나 숨기려면 이 옵션을 사용합니다. 이 설정은 각 목적에 따라 작업을 설정할 때 사용 가능한 옵션의 소음을 줄이는 데 도움이 되며, [상위/하위 페이지 이벤트](/help/collection/use-cases/personalization/top-bottom-page-events.md)에 대한 Adobe의 모범 사례를 따릅니다. 이 확인란을 활성화하면 다음 라디오 버튼이 표시됩니다.
   * **[!UICONTROL Request personalization]**: Adobe Analytics 이벤트를 기록하지 않고 최신 개인화 결정을 가져옵니다. 이 호출은 페이지 맨 위에서 가장 일반적으로 호출됩니다. 이 라디오 단추를 선택하면 다음 필드가 설정됩니다.
      * [!UICONTROL Type]이(가) [!UICONTROL Decisioning Proposition Fetch]에 잠겨 있습니다.
      * [!UICONTROL Render visual personalization decisions]이(가) 사용하도록 잠겨 있습니다.
      * [!UICONTROL Automatically send a display event]이(가) 사용 안 함으로 잠겨 있습니다.
   * **[!UICONTROL Collect analytics]**: 개인화 결정을 가져오지 않고 이벤트를 기록합니다. 이 호출은 페이지 맨 아래에서 가장 일반적으로 호출됩니다. 이 라디오 단추를 선택하면 다음 필드가 설정됩니다.
      * [!UICONTROL Include rendered propositions]이(가) 사용하도록 잠겨 있습니다.

## 데이터 필드

![이벤트 보내기 작업 형식에 대한 데이터 요소 설정을 보여 주는 Experience Platform 태그 UI 이미지입니다.](../assets/data.png)

* **[!UICONTROL Type]**: 이벤트 유형입니다. 사전 정의된 값 집합에서 선택하거나 고유한 값을 정의할 수 있습니다. 자세한 내용은 [에 대해 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)허용된 값을 참조하십시오. 이 필드에 해당하는 JavaScript 라이브러리는 [`eventType`](/help/collection/js/commands/sendevent/eventtype.md)입니다.
* **[!UICONTROL XDM]**: Adobe에 보낼 XDM 페이로드입니다. 이 필드에서는 [XDM 개체](../data-element-types.md#xdm-object) 또는 [변수](../data-element-types.md#variable)를 사용할 수 있습니다. 여러 XDM 개체를 채우는 규칙이 있는 경우 [병합된 개체](../../core/overview.md#merged-objects)를 사용하여 결합할 수 있습니다.
* **[!UICONTROL Data]**: Adobe에 보낼 데이터 페이로드입니다. 일부 앱 및 서비스는 Adobe Analytics 또는 Adobe Target과 같은 XDM 스키마를 준수할 필요가 없습니다. 이 필드에 [변수](../data-element-types.md#variable) 데이터 요소 형식을 사용하십시오.
* **[!UICONTROL Include rendered propositions]**: &quot;자동으로 표시 이벤트 보내기&quot;를 선택 취소한 경우 렌더링된 제안을 포함하여 이 이벤트를 표시 이벤트로 사용하려면 이 확인란을 선택하세요. `_experience.decisioning` XDM 필드는 렌더링된 개인화에 대한 정보로 채워집니다.
* **[!UICONTROL Document will unload]**: 이 확인란을 사용하면 사용자가 페이지를 떠나더라도 이벤트가 서버에 도달하는지 확인할 수 있습니다. 이 설정을 사용하면 이벤트가 서버에 도달할 수 있지만 Edge Network의 응답은 무시됩니다.
* **[!UICONTROL Merge ID]** _(사용되지 않음)_: `eventMergeId` XDM 필드를 채웁니다.

## 개인화 필드

![이벤트 보내기 작업 유형에 대한 Personalization 설정을 보여 주는 Experience Platform 태그 UI 이미지입니다.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: 개인화에서 명시적으로 요청하려는 범위의 배열입니다. 범위를 수동으로 입력하거나 데이터 요소를 제공할 수 있습니다. 수동으로 범위를 입력할 때 각 필드는 하나의 범위를 나타냅니다. 작업에 범위를 더 추가하려면 **[!UICONTROL Add scope]**&#x200B;을(를) 선택하십시오.
* **[!UICONTROL Surfaces]**: 이벤트를 사용하여 쿼리할 표면 배열입니다. 자세한 내용은 Adobe Journey Optimizer 설명서의 [웹 경험 만들기](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)를 참조하십시오. 서피스를 수동으로 입력할 때 각 필드는 하나의 서피스를 나타냅니다. **[!UICONTROL Add surface]**&#x200B;을(를) 선택하여 더 많은 표면을 작업에 추가합니다.
* **시각적 개인화 결정 렌더링:** 활성화되면 페이지에서 개인화된 콘텐츠를 렌더링할 수 있는 확인란입니다. 자세한 내용은 [개인화된 콘텐츠 렌더링](/help/collection/use-cases/personalization/rendering-personalization-content.md#automatically-rendering-content)을 참조하십시오.
* **[!UICONTROL Request default personalization]**: 페이지 범위 및 기본 표면을 요청할지 여부를 제어합니다. 기본적으로 페이지 로드 중 처음 `sendEvent` 호출 중에 자동으로 요청됩니다. 이 라디오 단추에 해당하는 JavaScript 라이브러리는 [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md)입니다. 다음 옵션 중에서 선택할 수 있습니다.
   * **[!UICONTROL Automatic]**: 기본 동작입니다. 아직 요청되지 않은 경우에만 기본 개인화를 요청합니다.
   * **[!UICONTROL Enabled]**: 페이지 범위 및 기본 표면을 명시적으로 요청합니다. SPA 보기 캐시를 업데이트합니다.
   * **[!UICONTROL Disabled]**: 페이지 범위 및 기본 표면에 대한 요청을 명시적으로 표시하지 않습니다.
* **[!UICONTROL Decision context]**: 온디바이스 의사 결정을 위해 Adobe Journey Optimizer 규칙 세트를 평가할 때 사용되는 키-값 맵입니다. 결정 컨텍스트를 수동으로 또는 데이터 요소를 통해 제공할 수 있습니다.

## Advertising 필드

![이벤트 보내기 작업에 대한 광고 설정을 표시하는 Experience Platform 태그 UI](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**: 라이브러리가 광고 정보를 XDM 페이로드에 추가하는 시기(또는 여부)를 결정합니다. 다음 옵션 중에서 선택할 수 있습니다.
   * **[!UICONTROL Automatic]**: 이벤트 시 사용할 수 있는 모든 광고 데이터가 이벤트 페이로드에 추가됩니다.
   * **[!UICONTROL Wait]**: 광고 데이터를 받을 때까지 이벤트 전송을 지연합니다.
   * **[!UICONTROL Disabled]**: 이벤트 페이로드에 광고 데이터를 추가하지 마십시오. 구현에서 Adobe Analytics 또는 Customer Journey Analytics을 사용하지 않는 경우 이 옵션을 선택합니다.

## 데이터 스트림 구성 재정의

이 명령은 데이터 스트림 구성 재정의를 지원하므로 이 데이터를 수신하는 앱 및 서비스를 제어할 수 있습니다. 개별 명령과 태그 확장 구성 설정 모두에서 데이터스트림 구성 재정의를 설정하면 개별 명령이 우선합니다. 자세한 내용은 [데이터 스트림 구성 재정의](../configure/configuration-overrides.md)를 참조하십시오.
