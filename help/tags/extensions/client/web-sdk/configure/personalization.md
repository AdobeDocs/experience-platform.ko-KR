---
title: Personalization 구성 설정
description: 웹 SDK 태그 확장에서 개인화 설정을 구성합니다.
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Personalization 구성 설정

이 구성 섹션에서는 개인화된 콘텐츠를 로드하는 동안 페이지의 특정 부분을 숨기는 방법을 결정할 수 있습니다. 올바르게 구성된 경우 이러한 설정은 방문자에게 올바른 개인화된 콘텐츠가 표시되도록 합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Personalization]** 섹션까지 아래로 스크롤합니다.

![태그 UI에서 웹 SDK 태그 확장의 개인화 설정을 보여 주는 이미지](../assets/web-sdk-ext-personalization.png)

다음 옵션을 사용할 수 있습니다.

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

웹 SDK에서 `mbox` 1.x 또는 2.x 라이브러리에서 사용하는 레거시 `mboxEdgeCluster` 및 `at.js` 쿠키를 읽고 쓸 수 있도록 하려면 이 옵션을 사용합니다. 이 설정은 동일한 웹 사이트에서 웹 SDK 또는 `at.js`을(를) 사용하여 페이지 간에 이동하는 동안 방문자 프로필을 그대로 유지하는 데 도움이 됩니다. 사이트에 `at.js`이(가) 구현되지 않은 경우 이 확인란을 활성화할 필요가 없습니다. 이 확인란에 해당하는 JavaScript 라이브러리는 [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md)입니다.

이 옵션을 활성화할 때는 [`overrideMboxEdgeServer`에서 &#x200B;](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver)`targetGlobalSettings()`도 활성화해야 합니다.

## [!UICONTROL Prehiding style] {#prehiding-style}

스타일 편집기 사전 숨김을 사용하면 사용자 지정 CSS 규칙을 정의하여 페이지의 특정 섹션을 숨길 수 있습니다. 페이지가 로드되면 웹 SDK은 이 스타일을 사용하여 개인화해야 하는 섹션을 숨기고 개인화를 검색한 다음 개인화된 페이지 섹션을 숨김을 해제합니다. 이 워크플로를 사용하면 방문자가 개인화 검색 프로세스가 로드되거나 깜박이는 것을 보지 않고 개인화된 콘텐츠를 볼 수 있습니다. 이 코드 편집기에 해당하는 JavaScript 라이브러리는 [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md)입니다.

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

이 섹션은 직접적인 구성 설정이 아니라 구현 코드를 얻을 수 있는 편리한 위치입니다. 웹 SDK 라이브러리가 로드되는 동안 원하는 컨텐츠를 숨기려면 사이트의 `<head>` 태그 내에 이 코드 조각 사전 숨김을 구현하십시오.

>[!IMPORTANT]
>
>코드 조각 사전 숨김을 사용하는 경우 Adobe에서는 코드 조각 사전 숨김과 스타일 사전 숨김 간에 동일한 CSS 규칙을 사용하는 것이 좋습니다.

## [!UICONTROL Enable personalization storage]

웹 SDK에서 개인화 이벤트를 저장할 수 있는 확인란입니다. 브라우저의 로컬 저장소에 있습니다. 방문자가 페이지 로드 중에 본 경험을 추적하려는 경우 유용합니다.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

웹 SDK이 Adobe Journey Optimizer에서 반환된 콘텐츠에 대한 클릭 수를 자동으로 수집하는 시기를 결정하는 드롭다운 메뉴입니다.

* **[!UICONTROL Always]**: 제안에 대한 모든 상호 작용을 수집합니다.
* **[!UICONTROL Decorated elements only]**: `data-aep-click-label` 또는 `data-aep-click-token` HTML 특성이 있는 요소의 상호 작용만 수집합니다.
* **[!UICONTROL Never]**: 제안에 대한 상호 작용을 수집하지 마십시오.

이 드롭다운 메뉴에 해당하는 JavaScript 라이브러리는 [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)입니다. 기본값은 [!UICONTROL Always]입니다.

## [!UICONTROL Auto click collection for Adobe Target]

웹 SDK이 Adobe Target에서 반환된 콘텐츠에 대한 클릭 수를 자동으로 수집하는 시기를 결정하는 드롭다운 메뉴입니다.

* **[!UICONTROL Always]**: 제안에 대한 모든 상호 작용을 수집합니다.
* **[!UICONTROL Decorated elements only]**: `data-aep-click-label` 또는 `data-aep-click-token` HTML 특성이 있는 요소의 상호 작용만 수집합니다.
* **[!UICONTROL Never]**: 제안에 대한 상호 작용을 수집하지 마십시오.

이 드롭다운 메뉴에 해당하는 JavaScript 라이브러리는 [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)입니다. 기본값은 [!UICONTROL Never]입니다.
