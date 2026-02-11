---
title: 데이터 수집 구성 설정
description: 웹 SDK 태그 확장에서 데이터 수집 설정을 구성합니다.
exl-id: 88c34545-9a58-4d49-a939-36edaa9a46be
source-git-commit: 9693f53cc1a31622d63fb93c0d51e1f5896c6524
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# 데이터 수집 구성 설정

이 구성 섹션에서는 확장 간에 데이터를 수집하는 방법을 결정할 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Data collection]** 섹션까지 아래로 스크롤합니다.

![Tags UI에서 웹 SDK 태그 확장의 데이터 수집 설정을 보여 주는 이미지입니다.](../assets/web-sdk-ext-collection.png)

다음 옵션을 사용할 수 있습니다.

## [!UICONTROL On before event send callback]

Adobe으로 전송된 페이로드를 평가하고 수정하는 콜백 함수입니다. 코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.xdm`**: 이벤트에 대한 XDM 페이로드입니다.
* **`content.data`**: 이벤트에 대한 데이터 개체 페이로드입니다.
* **`return true`**: 콜백을 즉시 종료하고 `content` 개체의 현재 값으로 Adobe에 데이터를 보냅니다.
* **`return false`**: 콜백을 즉시 종료하고 Adobe으로 데이터 전송을 중단합니다.

`content`의 외부에서 정의된 모든 변수를 사용할 수 있지만, Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. **데이터가 Adobe으로 전송되지 않았습니다.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>페이지의 첫 번째 이벤트에서 `false`을(를) 반환하지 마십시오. 첫 번째 이벤트에서 `false`을(를) 반환하면 개인화에 부정적인 영향을 줄 수 있습니다.

이 콜백은 JavaScript 라이브러리의 [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md)에 해당하는 태그입니다.

## [!UICONTROL Collect internal link clicks]

사이트 또는 속성 내부의 링크 추적 데이터 수집을 활성화하는 확인란입니다. 이 확인란은 JavaScript 라이브러리의 [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)에 해당하는 태그입니다. 이 확인란을 활성화하면 이벤트 그룹화 옵션이 표시됩니다.

* **[!UICONTROL No event grouping]**: 링크 추적 데이터가 별도의 이벤트로 Adobe에 전송됩니다. 별도의 이벤트에서 전송된 링크 클릭으로 Adobe Experience Platform에 전송된 데이터의 계약적 사용이 늘어날 수 있습니다.
* **[!UICONTROL Event grouping using session storage]**: 다음 &quot;페이지 보기&quot; 이벤트까지 링크 추적 데이터를 세션 저장소에 저장합니다. &quot;페이지 보기&quot;로 간주되는 다음 이벤트에서 저장된 링크 추적 데이터는 &quot;페이지 보기&quot; 이벤트 페이로드와 병합됩니다. Adobe에서는 내부 링크를 추적할 때 이 설정을 활성화하는 것이 좋습니다.
* **[!UICONTROL Event grouping using local object]**: 다음 &quot;페이지 보기&quot; 이벤트까지 링크 추적 데이터를 로컬 개체에 저장합니다. 방문자가 새 브라우저 페이지로 이동하면 링크 추적 데이터가 손실됩니다. 이 설정은 단일 페이지 애플리케이션 컨텍스트에서 가장 유용합니다.

태그 라이브러리는 다음 요소가 페이로드에 포함될 때 주어진 이벤트를 &quot;페이지 보기&quot;로 간주합니다.

* `xdm.web.webPageDetails.name`에 문자열 값이 있습니다.
* `xdm.web.webPageDetails.pageViews.value`이(가) `0`보다 큽니다.

## [!UICONTROL Collect external link clicks]

외부 링크 컬렉션을 활성화하는 확인란입니다. 이 확인란은 JavaScript 라이브러리의 [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)에 해당하는 태그입니다.

## [!UICONTROL Collect download link clicks]

다운로드 링크 컬렉션을 활성화하는 확인란입니다. 이 확인란은 JavaScript 라이브러리의 [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)에 해당하는 태그입니다.

## [!UICONTROL Download link qualifier]

링크 URL을 다운로드 링크로 규정하는 정규 표현식입니다. 이 문자열은 JavaScript 라이브러리의 [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md)에 해당하는 태그입니다.

## [!UICONTROL Filter click properties]

컬렉션 전에 클릭 관련 속성을 평가하고 수정하는 콜백 함수입니다. 이 함수는 [!UICONTROL On before event send callback] 전에 실행되며, JavaScript 라이브러리의 [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md)에 해당하는 태그입니다. 코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.clickedElement`**: 클릭한 DOM 요소입니다.
* **`content.pageName`**: 클릭이 발생했을 때의 페이지 이름입니다.
* **`content.linkName`**: 클릭한 링크의 이름입니다.
* **`content.linkRegion`**: 클릭한 링크의 영역입니다.
* **`content.linkType`**: 링크 유형(종료, 다운로드 또는 기타)입니다.
* **`content.linkURL`**: 클릭한 링크의 대상 URL.
* **`return true`**: 현재 변수 값이 있는 콜백을 즉시 종료합니다.
* **`return false`**: 콜백을 즉시 종료하고 데이터 수집을 중단합니다.
* `content`의 외부에서 정의된 모든 변수를 사용할 수 있지만, Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

>[!TIP]
>
>**[!UICONTROL On before link click send]** 필드는 이미 구성된 속성에만 표시되는 사용되지 않는 콜백입니다. JavaScript 라이브러리의 [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md)에 해당하는 태그입니다. **[!UICONTROL Filter click properties]** 콜백을 사용하여 클릭 데이터를 필터링하거나 조정하거나 **[!UICONTROL On before event send callback]**&#x200B;을(를) 사용하여 Adobe으로 전송되는 전체 페이로드를 필터링하거나 조정하십시오. **[!UICONTROL Filter click properties]** 콜백과 **[!UICONTROL On before link click send]** 콜백이 모두 설정된 경우 **[!UICONTROL Filter click properties]** 콜백만 실행됩니다.

## 컨텍스트 설정

특정 XDM 필드를 채우는 방문자 정보를 자동으로 수집합니다. **[!UICONTROL All default context information]** 또는 **[!UICONTROL Specific context information]**&#x200B;을(를) 선택할 수 있습니다. JavaScript 라이브러리의 [`context`](/help/collection/js/commands/configure/context.md)에 해당하는 태그입니다.

* **[!UICONTROL Web]**: 현재 페이지에 대한 정보를 수집합니다.
* **[!UICONTROL Device]**: 사용자의 장치에 대한 정보를 수집합니다.
* **[!UICONTROL Environment]**: 사용자의 브라우저에 대한 정보를 수집합니다.
* **[!UICONTROL Place context]**: 사용자의 위치에 대한 정보를 수집합니다.
* **[!UICONTROL High entropy user-agent hints]**: 사용자 장치에 대한 자세한 정보를 수집합니다.
* **[!UICONTROL Send referrer to Adobe Analytics only once per page view]**: 중복 레퍼러 데이터가 Adobe Analytics으로 전송되지 않도록 합니다.
