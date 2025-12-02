---
title: Adobe Advertising 구성 설정
description: 수요 측 플랫폼 기능을 활성화하거나 비활성화합니다.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Adobe Advertising 구성 설정

>[!AVAILABILITY]
>
>웹 SDK용 Adobe Advertising은 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

**[!UICONTROL Adobe Advertising]** 섹션을 사용하면 구현에 사용되는 경우 수요 측 플랫폼(DSP) 기능을 활성화하거나 비활성화할 수 있습니다. 구현에서 DSP을 사용하는 경우에만 이 필드를 설정하면 됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Adobe Advertising]** 섹션까지 아래로 스크롤합니다.

현재 한 가지 옵션을 사용할 수 있습니다.

## [!UICONTROL Adobe Advertising DSP]

Adobe Advertising에 대한 DSP 기능을 활성화하거나 비활성화하는 드롭다운 메뉴.

* **[!UICONTROL Enabled]**: 뷰스루 추적을 사용합니다.
* **[!UICONTROL Disabled]**: 뷰스루 추적을 비활성화합니다.

활성화되면 다음 설정을 사용할 수 있습니다.

* **[!UICONTROL Advertisers]**: 뷰스루 추적을 활성화할 광고주.
* **[!UICONTROL ID5 partner ID]**: 선택 사항입니다. 조직의 ID5 파트너 ID입니다. 이 설정을 사용하면 웹 SDK에서 ID5 범용 ID를 수집할 수 있습니다.
* **[!UICONTROL RampID JavaScript path]**: 선택 사항입니다. 조직의 [!DNL LiveRamp RampID] JavaScript 코드(`ats.js`) 경로입니다.  이 설정을 사용하면 웹 SDK에서 [!DNL RampID]개의 유니버설 ID를 수집할 수 있습니다.
