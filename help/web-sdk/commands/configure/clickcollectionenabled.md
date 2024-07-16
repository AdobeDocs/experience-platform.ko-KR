---
title: 클릭콜렉션활성화됨
description: 링크 클릭 데이터가 자동으로 수집되는지 여부를 결정하도록 Web SDK를 구성하는 방법에 대해 알아봅니다.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

`clickCollectionEnabled` 속성은 Web SDK에서 자동으로 링크 데이터를 수집하는지 여부를 결정하는 부울입니다. 이 변수를 설정하지 않으면 기본값은 `true`입니다. 즉, 기본적으로 링크 추적 데이터가 자동으로 수집됩니다. 링크 데이터를 수동으로 추적하려는 경우 이 속성을 `false`(으)로 설정하는 것이 좋습니다.

`clickCollectionEnabled`이(가) 활성화되면 다음 XDM 요소가 자동으로 데이터로 채워집니다.

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

이 부울을 활성화하면 기본적으로 내부 링크, 다운로드 링크 및 종료 링크가 모두 자동으로 추적됩니다. Adobe 자동 링크 추적을 추가로 제어하려면 [`clickCollection`](clickcollection.md) 개체를 사용하는 것이 좋습니다.

## 자동 링크 추적 논리

Web SDK는 `onClick` 특성이 없는 경우 `<a>` 및 `<area>` HTML 요소에 대한 모든 클릭 수를 추적합니다. 문서에 연결된 [capture](https://www.w3.org/TR/uievents/#capture-phase) 클릭 이벤트 수신기로 클릭 수를 캡처합니다. 유효한 링크를 클릭하면 다음 논리가 순서대로 실행됩니다.

1. 링크가 [`downloadLinkQualifier`](downloadlinkqualifier.md)의 값을 기반으로 하는 기준과 일치하거나 링크에 `download` HTML 특성이 포함되어 있는 경우 `xdm.web.webInteraction.type`이(가) `"download"`(`clickCollection.downloadLinkEnabled`이(가) 활성화된 경우)로 설정됩니다.
1. 링크 대상 도메인이 현재 `window.location.hostname`과(와) 다른 경우 `xdm.web.webInteraction.type`이(가) `"exit"`(활성화된 경우)으로 설정됩니다.`clickCollection.exitLinkEnabled`
1. 링크가 `"download"` 또는 `"exit"`에 적합하지 않으면 `xdm.web.webInteraction.type`이(가) `"other"`(으)로 설정됩니다.

모든 경우에 `xdm.web.webInteraction.name`은(는) 링크 텍스트 레이블로 설정되고 `xdm.web.webInteraction.URL`은(는) 링크 대상 URL로 설정됩니다. 링크 이름도 URL로 설정하려면 `clickCollection` 개체에서 `filterClickDetails` 콜백을 사용하여 이 XDM 필드를 재정의할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 자동 링크 추적 활성화 {#tag-extension}

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 클릭 데이터 수집 사용]** 확인란을 선택하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 데이터 수집 사용]** 확인란을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 자동 링크 추적 활성화 {#library}

`configure` 명령을 실행할 때 `clickCollectionEnabled` 부울을 설정합니다. Web SDK를 구성할 때 이 속성을 생략하면 기본적으로 `true`(으)로 설정됩니다. `xdm.web.webInteraction.type` 및 `xdm.web.webInteraction.value`을(를) 수동으로 설정하려면 이 값을 `false`(으)로 설정하십시오.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
