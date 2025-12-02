---
title: 스트리밍 미디어 구성 설정
description: 웹 SDK 태그 확장이 스트리밍 미디어 데이터를 수집하는 방법을 사용자 지정합니다.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---

# 스트리밍 미디어 구성 설정

미디어 컬렉션 기능은 미디어 재생, 일시 중지, 완료 및 기타 관련 이벤트와 같은 미디어 세션과 관련된 데이터를 수집하는 데 도움이 됩니다. 수집되면 이 데이터를 Adobe Experience Platform 또는 Adobe Analytics으로 전송하여 보고서를 생성할 수 있습니다. 이 기능은 웹 사이트에서의 미디어 소비 행동을 추적하고 이해하는 포괄적인 솔루션을 제공합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Streaming media]** 섹션까지 아래로 스크롤합니다.

![태그 UI에서 웹 SDK 태그 확장의 미디어 컬렉션 설정을 보여 주는 이미지](../assets/media-collection.png)

## 전제 조건

웹 SDK의 스트리밍 미디어 구성 요소를 사용하려면 다음 사전 요구 사항을 충족해야 합니다.

* Adobe Experience Platform 또는 Adobe Analytics에 액세스할 수 있는지 확인하십시오.
* 사용 중인 데이터 스트림에 대해 **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** 옵션을 사용하도록 설정합니다.
* 데이터 스트림에서 사용하는 스키마에 미디어 컬렉션 스키마 필드가 포함되어 있는지 확인합니다.
* 이 페이지에 표시된 대로 웹 SDK 태그 확장에서 Streaming Media 기능을 구성합니다.

## [!UICONTROL Channel]

미디어 컬렉션이 발생하는 채널의 이름입니다. 예, `Video channel`. 모든 문자열 값이 유효합니다.

## [!UICONTROL Player Name]

속성이 미디어 재생에 사용하는 미디어 플레이어의 이름입니다.

## [!UICONTROL Application Version]

속성이 미디어 재생에 사용하는 미디어 플레이어 응용 프로그램의 버전입니다.

## [!UICONTROL Main ping interval]

기본 콘텐츠에 대한 Ping 빈도(초)입니다. 기본값은 `10`입니다. 값의 범위는 `10`초에서 `50`초까지입니다. 값을 지정하지 않으면 [자동으로 추적된 세션](/help/collection/js/commands/createmediasession.md#automatic)을 사용할 때 기본값이 사용됩니다.

## [!UICONTROL Ad ping interval]

광고 콘텐츠에 대한 Ping 빈도(초)입니다. 기본값은 `10`입니다. 값의 범위는 `1`초에서 `10`초까지입니다. 값을 지정하지 않으면 [자동으로 추적된 세션](/help/collection/js/commands/createmediasession.md#automatic)을 사용할 때 기본값이 사용됩니다.
