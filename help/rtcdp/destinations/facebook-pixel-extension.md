---
title: Facebook 픽셀 확장
seo-title: Facebook 픽셀 확장
description: Facebook 픽셀 확장 기능은 Adobe 실시간 고객 데이터 Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
seo-description: null
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 5%

---


# [!DNL Facebook Pixel] 확장 프로그램 {#facebook-pixel-extension}

## 개요 {#overview}

이 [!DNL Facebook Pixel] 는 사람들이 웹 사이트에서 취하는 행동을 파악하여 광고의 효과를 측정할 수 있는 분석 도구입니다.

[!DNL Facebook Pixel] 는 Adobe 실시간 고객 데이터 Platform의 광고 확장입니다. 확장 기능에 대한 자세한 내용은 [Facebook Pixel 웹 사이트를 참조하십시오](https://developers.facebook.com/docs/facebook-pixel/).

이 대상은 Experience Platform Launch 확장자입니다. Launch 익스텐션이 Adobe 실시간 CDP에서 작동하는 방법에 대한 자세한 내용은 [Experience Platform Launch 확장 개요를 참조하십시오](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Facebook 픽셀 확장](assets/facebook-pixel-extension.png)

## 전제 조건 {#prerequisites}

이 익스텐션은 Adobe의 실시간 CDP를 구매한 모든 고객을 위한 [!DNL Destinations] 카탈로그에서 제공됩니다.

이 확장을 사용하려면 Experience Platform Launch에 액세스해야 합니다. Experience Platform Launch은 Adobe Experience Cloud 고객에게 부가가치 기능으로 제공됩니다. 조직 관리자에게 문의하여 Launch에 액세스할 수 있고 Extension을 설치할 수 있도록 **[!UICONTROL manage_properties]** 권한을 부여받으라고 요청하십시오.

## 확장 설치 {#install-extension}

익스텐션을 설치하려면 [!DNL Facebook Pixel] 다음을 수행하십시오.

1. Adobe [Real-time CDP 인터페이스에서](http://platform.adobe.com/)대상 > **[!UICONTROL 카탈로그로 이동합니다]**.
2. 카탈로그에서 익스텐션을 선택하거나 검색 막대를 사용합니다.
3. 대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 확장]** 설치 를 선택합니다. 확장 **[!UICONTROL 설치]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없습니다. 전제 조건 [을 참조하십시오](#prerequisites).
4. 사용 **[!UICONTROL 가능한 론치 속성]** 선택 창에서 확장을 설치할 론치 속성을 선택합니다. Launch에서 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. Launch 설명서의 [속성 페이지](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 섹션에서 속성에 대해 알아봅니다.
5. Launch로 이동하여 설치를 완료합니다.

또한 [Experience Platform Launch 인터페이스에서 직접 익스텐션을 설치할 수 있습니다](https://launch.adobe.com/). 론치 [설명서에서 새 확장](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 추가를 참조하십시오.


## 익스텐션 사용 방법 {#how-to-use}

확장 프로그램을 설치한 후에는 Launch에서 직접 확장 기능에 대한 규칙을 설정할 수 있습니다.

론치에서는 특정 상황에서만 이벤트 데이터를 확장 대상에 전송하기 위해 설치된 익스텐션에 대한 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙 설명서를 참조하십시오](https://docs.adobe.com/help/ko-KR/launch/using/reference/manage-resources/rules.html).

## 확장 기능 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

Launch 인터페이스에서 익스텐션을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>익스텐션이 속성 중 하나에 이미 설치되어 있는 경우 Adobe 실시간 CDP UI에 **[!UICONTROL Install for the extension]** 이 여전히 표시됩니다. Launch로 이동하여 확장 기능을 [구성](#install-extension) 또는 삭제하려면 설치 확장 프로그램에 설명된 대로 설치 워크플로우를 시작합니다.

익스텐션을 업그레이드하려면 Launch [설명서에서 Extension 업그레이드를](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 참조하십시오.
