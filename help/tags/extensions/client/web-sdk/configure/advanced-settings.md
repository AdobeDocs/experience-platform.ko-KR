---
title: 고급 구성 설정
description: 웹 SDK 태그 확장에 대한 고급 설정을 구성합니다.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 고급 구성 설정

이 구성 섹션에서는 고급 설정을 변경할 수 있습니다. Adobe에서는 대부분의 구현에 이러한 옵션을 있는 그대로 두는 것이 좋습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Advanced Settings]** 섹션까지 아래로 스크롤합니다.

![웹 SDK 태그 확장 페이지를 사용하여 고급 설정을 보여 주는 이미지](../assets/advanced-settings.png)

현재 한 가지 옵션을 사용할 수 있습니다.

## [!UICONTROL Edge base path]

이 필드를 사용하여 Edge Network과 상호 작용하는 데 사용되는 기본 경로를 변경합니다. 특정 알파 또는 베타 테스트에 참여하는 경우 Adobe에서 이 필드를 변경하도록 요청할 수 있습니다. 그렇지 않으면 Adobe에서 기본값을 `ee`(으)로 유지하는 것이 좋습니다.

이 필드는 JavaScript 라이브러리를 구성할 때 [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md)에 해당하는 태그입니다.
