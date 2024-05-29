---
title: Adobe Experience Platform 웹 SDK 확장의 작업 유형
description: Adobe Experience Platform 웹 SDK 태그 확장에서 제공하는 다양한 작업 유형에 대해 알아봅니다.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 377be6d97e6da9b4aaacfa23a188131bd38e66f4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---


# 작업 유형

을(를) 구성한 후 [Adobe Experience Platform 웹 SDK 태그 확장](web-sdk-extension-configuration.md), 작업 유형을 구성해야 합니다.

이 페이지에서는 다음에서 지원하는 작업 유형을 설명합니다. [Adobe Experience Platform 웹 SDK 태그 확장](web-sdk-extension-configuration.md).

## 이벤트 보내기 {#send-event}

Adobe에게 이벤트를 보냅니다. [!DNL Experience Platform] Adobe Experience Platform에서 전송하는 데이터를 수집하고 해당 정보에 대해 조치를 취할 수 있습니다. 인스턴스를 선택합니다(인스턴스가 두 개 이상인 경우). 전송하려는 모든 데이터는 **[!UICONTROL XDM 데이터]** 필드. XDM 스키마의 구조를 준수하는 JSON 개체를 사용합니다. 이 개체는 페이지 또는 **[!UICONTROL 사용자 지정 코드]** **[!UICONTROL 데이터 요소]**.

이벤트 보내기 작업 유형에는 구현에 따라 유용할 수 있는 몇 가지 다른 필드가 있습니다. 이러한 필드는 모두 선택 사항입니다.

- **유형:** 이 필드에서는 XDM 스키마에 기록될 이벤트 유형을 지정할 수 있습니다. 다음을 참조하십시오 [`type`](/help/web-sdk/commands/sendevent/type.md) 다음에서 `sendEvent` 명령 을 참조하십시오.
- **데이터:** XDM 스키마와 일치하지 않는 데이터는 이 필드를 사용하여 보낼 수 있습니다. 이 필드는 Adobe Target 프로필을 업데이트하거나 Target Recommendations 속성을 전송하려는 경우 유용합니다. 다음을 참조하십시오 [`data`](/help/web-sdk/commands/sendevent/data.md) 다음에서 `sendEvent` 명령 을 참조하십시오.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **데이터 세트 ID:** 데이터 스트림에서 지정한 데이터 세트 이외의 데이터 세트로 데이터를 보내야 하는 경우 여기에서 해당 데이터 세트 ID를 지정할 수 있습니다.
- **문서가 언로드됩니다.** 사용자가 페이지를 떠나더라도 이벤트가 서버에 도달하는지 확인하려면 **[!UICONTROL 문서가 언로드됩니다.]** 확인란. 이렇게 하면 이벤트가 서버에 도달할 수 있지만 응답은 무시됩니다.
- **시각적 개인화 결정 렌더링:** 페이지에서 개인화된 콘텐츠를 렌더링하려면 다음을 확인하십시오. **[!UICONTROL 시각적 개인화 결정 렌더링]** 확인란. 필요한 경우 결정 범위 및/또는 서피스를 지정할 수도 있습니다. 다음을 참조하십시오. [개인화 설명서](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) 개인화된 콘텐츠를 렌더링하는 방법에 대한 자세한 정보입니다.

## 동의 설정 {#set-consent}

사용자로부터 동의를 받은 후에는 &quot;동의 설정&quot; 작업 유형을 사용하여 Adobe Experience Platform Web SDK에 이 동의를 전달해야 합니다. 현재 &quot;Adobe&quot; 및 &quot;IAB TCF&quot;, 2가지 유형의 표준이 지원됩니다. 다음을 참조하십시오 [고객 동의 환경 설정 지원](/help/web-sdk/consent/supporting-consent.md). Adobe 버전 2.0을 사용하는 경우 데이터 요소 값만 지원됩니다. 동의 오브젝트로 확인되는 데이터 요소를 만들어야 합니다.

이 작업에서는 동의를 받은 후 ID를 동기화할 수 있도록 ID 맵을 포함할 선택적 필드도 제공됩니다. 동기화는 동의 호출이 처음 실행될 수 있으므로 동의가 &quot;보류 중&quot; 또는 &quot;종료&quot;로 구성된 경우에 유용합니다.

## 변수 업데이트 {#update-variable}

이 작업을 사용하여 이벤트의 결과로 XDM 개체를 수정합니다. 이 작업은 나중에 다음에서 참조할 수 있는 개체를 작성하기 위한 것입니다. **[!UICONTROL 이벤트 보내기]** 작업: 이벤트 XDM 개체를 기록합니다.

이 작업 유형을 사용하려면 다음을 정의해야 합니다. [변수](data-element-types.md#variable) 데이터 요소입니다. 수정할 변수 데이터 요소를 선택하면 편집기가 나타납니다. 편집기의 편집기와 유사합니다. [XDM 개체](data-element-types.md#xdm-object) 데이터 요소입니다.

![](assets/update-variable.png)

편집기에 사용되는 XDM 스키마는에서 선택된 스키마입니다. [!UICONTROL 변수] 데이터 요소입니다. 왼쪽의 트리에서 속성 중 하나를 클릭한 다음 오른쪽의 값을 수정하여 개체의 속성을 하나 이상 설정할 수 있습니다.예를 들어 아래 스크린샷에서 producedBy 속성은 &quot;Produced by data element&quot; 데이터 요소로 설정됩니다.

![](assets/update-variable-set-property.png)

변수 업데이트 작업의 편집기와 XDM 개체 데이터 요소의 편집기 간에는 몇 가지 차이점이 있습니다. 먼저 변수 업데이트 작업에 &quot;xdm&quot; 레이블이 지정된 루트 수준 항목이 있습니다. 이 항목을 클릭하면 전체 개체를 설정하는 데 사용할 데이터 요소를 지정할 수 있습니다. 둘째, 변수 업데이트 작업에는 xdm 개체에서 데이터를 지우는 확인란이 있습니다. 왼쪽의 속성 중 하나를 클릭한 다음 오른쪽의 확인란을 선택하여 값을 지웁니다. 이렇게 하면 변수에 값을 설정하기 전에 현재 값이 지워집니다.

## 미디어 이벤트 보내기 {#send-media-event}

Adobe Experience Platform 및/또는 Adobe Analytics에 미디어 이벤트를 보냅니다. 이 작업은 웹 사이트에서 미디어 이벤트를 추적할 때 유용합니다. 인스턴스를 선택합니다(인스턴스가 두 개 이상인 경우). 작업에는 다음이 필요합니다. `playerId` 추적된 미디어 세션의 고유 식별자를 나타냅니다. 또한 **[!UICONTROL 체감 품질]** 및 a `playhead` 미디어 세션을 시작할 때 데이터 요소입니다.

![미디어 이벤트 보내기 화면을 보여 주는 플랫폼 UI 이미지입니다.](assets/send-media-event.png)

다음 **[!UICONTROL 미디어 이벤트 보내기]** 작업 유형은 다음 속성을 지원합니다.

- **[!UICONTROL 인스턴스]**: 사용 중인 웹 SDK 인스턴스.
- **[!UICONTROL 미디어 이벤트 유형]**: 추적 중인 미디어 이벤트 유형.
- **[!UICONTROL 플레이어 ID]**: 미디어 세션 고유 식별자입니다.
- **[!UICONTROL 플레이헤드]**: 미디어 재생의 현재 위치(초)입니다.
- **[!UICONTROL 미디어 세션 세부 정보]**: 미디어 시작 이벤트를 전송할 때 필요한 미디어 세션 세부 사항을 지정해야 합니다.
- **[!UICONTROL 챕터 세부 정보]**: 이 섹션에서는 챕터 시작 미디어 이벤트를 전송할 때 챕터 세부 사항을 지정할 수 있습니다.
- **[!UICONTROL 광고 세부 정보]**: 전송 시 `AdBreakStart` 이벤트, 필요한 광고 세부 정보를 지정해야 합니다.
- **[!UICONTROL Advertising pod 세부 정보]**: 를 전송할 때 광고 pod에 대한 세부 정보 `AdStart` 이벤트.
- **[!UICONTROL 오류 세부 정보]**: 추적 중인 재생 오류에 대한 세부 사항입니다.
- **[!UICONTROL 상태 업데이트 세부 정보]**: 업데이트 중인 플레이어 상태입니다.
- **[!UICONTROL 사용자 지정 메타데이터]**: 추적 중인 미디어 이벤트에 대한 사용자 지정 메타데이터입니다.
- **[!UICONTROL 체감 품질]**: 추적 중인 경험 미디어 품질 데이터입니다.

## Media Analytics 추적기 가져오기 {#get-media-analytics-tracker}

이 작업은 기존 Media Analytics API를 가져오는 데 사용됩니다. 작업을 구성하고 개체 이름이 제공되면 기존 Media Analytics API가 해당 창 개체로 내보내집니다. 아무 것도 제공되지 않으면 (으)로 내보내집니다. `window.Media` 현재 Media JS 라이브러리가 그러하듯이.

![Media Analytics 추적기 가져오기 작업 유형을 보여주는 플랫폼 UI 이미지입니다.](assets/get-media-analytics-tracker.png)

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 작업을 구성하는 방법을 더 잘 이해할 수 있습니다. 다음으로, 방법에 대해 읽어 보십시오. [데이터 요소 유형 구성](data-element-types.md).
