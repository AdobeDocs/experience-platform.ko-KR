---
title: 구성 설정 개요
description: 웹 SDK 태그 확장을 구성할 때 사용할 수 있는 옵션에 대해 알아봅니다.
exl-id: 03f7bc0a-05c9-48ae-ae57-478db6d18f52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 구성 설정 개요 {#config-overview}

Adobe Experience Platform Web SDK 태그 확장은 사용자 지정할 수 있는 몇 가지 옵션을 제공합니다. 이러한 구성 설정은 JavaScript 라이브러리에서 [`configure`](/help/collection/js/commands/configure/overview.md) 명령을 사용하는 것과 같은 태그입니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.

## 사용자 지정 빌드 구성 요소

조직의 빌드 크기 최적화가 우선 순위인 경우 확장의 빌드 크기를 줄이는 데 사용하지 않는 특정 기능을 비활성화할 수 있습니다. 자세한 내용은 [사용자 지정 빌드 구성 요소](custom-build-components.md)를 참조하십시오.

## SDK 인스턴스

대부분의 구현에는 일반적으로 단일 SDK 인스턴스가 필요합니다. 그러나 조직에 여러 개의 웹 SDK 추적 인스턴스가 필요한 경우 **[!UICONTROL Add instance]** 단추를 사용할 수 있습니다. 각 웹 SDK 태그 인스턴스를 구성할 때 사용할 수 있는 주요 섹션은 다음과 같습니다.

* [**[!UICONTROL SDK instance]**](general.md): 인스턴스에 대한 일반 설정입니다. 이 섹션의 모든 필드는 필수입니다.
* [**[!UICONTROL Datastreams]**](datastreams.md): 각 태그 환경에 대한 데이터를 저장할 위치입니다.
* [**[!UICONTROL Consent]**](consent.md): 확장에 대한 기본 동의 설정입니다.
* [**[!UICONTROL Identity]**](identity.md): 쿠키 및 방문자 마이그레이션 설정.
* [**[!UICONTROL Personalization]**](personalization.md): 개별 수준에서 방문자 경험을 사용자 지정합니다.
* [**[!UICONTROL Data collection]**](data-collection.md): 자동으로 수집된 항목을 포함하거나 생략합니다.
* [**[!UICONTROL Streaming media]**](streaming-media.md): 스트리밍 미디어 컬렉션별 설정입니다.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): 특정 조건이 충족되면 구성 설정을 수정합니다.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): Edge Network의 기본 경로를 지정하십시오.
