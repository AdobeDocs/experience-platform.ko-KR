---
title: 클릭콜렉션활성화됨
description: 링크 클릭 데이터가 자동으로 수집되는지 여부를 결정하도록 Web SDK를 구성하는 방법에 대해 알아봅니다.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

다음 `clickCollectionEnabled` 속성은 웹 SDK가 링크 데이터를 자동으로 수집하는지 여부를 결정하는 부울입니다. 이 변수를 설정하지 않으면 기본값은 입니다. `true` 즉, 링크 추적 데이터는 기본적으로 자동으로 수집됩니다. 이 속성을 다음으로 설정 `false` 는 링크 데이터를 수동으로 추적하려는 경우에 유용합니다.

날짜 `clickCollectionEnabled` 가 활성화되면 다음 XDM 요소가 자동으로 데이터로 채워집니다.

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

이 부울을 활성화하면 기본적으로 내부 링크, 다운로드 링크 및 종료 링크가 모두 자동으로 추적됩니다. Adobe 자동 링크 추적을 보다 세밀하게 제어하려면 다음을 사용하는 것이 좋습니다. [`clickCollection`](clickcollection.md) 개체.

## 자동 링크 추적 논리

Web SDK는 의 모든 클릭 수를 추적합니다. `<a>` 및 `<area>` HTML 요소가 없는 경우 요소 `onClick` 특성. 클릭은 [캡처](https://www.w3.org/TR/uievents/#capture-phase) 문서에 첨부된 이벤트 리스너를 누릅니다. 유효한 링크를 클릭하면 다음 논리가 순서대로 실행됩니다.

1. 링크가 의 값을 기반으로 한 기준과 일치하는 경우 [`downloadLinkQualifier`](downloadlinkqualifier.md)또는 링크에 `download` HTML 속성, `xdm.web.webInteraction.type` 이(가) (으)로 설정됨 `"download"` (if `clickCollection.downloadLinkEnabled` 이 활성화되었습니다).
1. 링크 대상 도메인이 현재 도메인과 다른 경우 `window.location.hostname`, `xdm.web.webInteraction.type` 이(가) (으)로 설정됨 `"exit"` (if `clickCollection.exitLinkEnabled` 이 활성화되었습니다).
1. 링크가 다음 중 하나에 적합하지 않은 경우 `"download"` 또는 `"exit"`, `xdm.web.webInteraction.type` 이(가) (으)로 설정됨 `"other"`.

모든 경우에, `xdm.web.webInteraction.name` 는 링크 텍스트 레이블로 설정되고 `xdm.web.webInteraction.URL` 링크 대상 URL로 설정됩니다. 링크 이름을 URL로도 설정하려면 다음을 사용하여 이 XDM 필드를 재정의할 수 있습니다. `filterClickDetails` 콜백 `clickCollection` 개체.

## 웹 SDK 태그 확장을 사용하여 자동 링크 추적 활성화 {#tag-extension}

다음 항목 선택 **[!UICONTROL 클릭 데이터 수집 활성화]** 다음과 같은 경우 확인란 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL 클릭 데이터 수집 활성화]**.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 자동 링크 추적 활성화 {#library}

설정 `clickCollectionEnabled` 를 실행할 때 부울 `configure` 명령입니다. Web SDK를 구성할 때 이 속성을 생략하면 기본값이 로 설정됩니다. `true`. 이 값을 다음으로 설정 `false` 을(를) 설정하려면 `xdm.web.webInteraction.type` 및 `xdm.web.webInteraction.value` 수동으로.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
