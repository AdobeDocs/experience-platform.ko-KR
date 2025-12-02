---
title: 데이터 스트림 구성 재정의 설정
description: 특정 조건이 충족되면 구성 설정을 수정합니다.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# 데이터 스트림 구성 재정의 설정

데이터 스트림 재정의를 사용하면 웹 SDK을 통해 Edge Network에 전달되는 데이터 스트림에 대한 추가 구성을 정의할 수 있습니다. 이 기능을 사용하면 새 데이터스트림을 만들거나 기존 설정을 수정하지 않고 조건부로 다른 데이터스트림 동작을 트리거할 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Datastream configuration overrides]** 섹션까지 아래로 스크롤합니다.

데이터스트림 구성 재정의는 2단계 프로세스입니다.

1. 먼저 데이터 스트림 UI에서 [데이터 스트림을 구성](/help/datastreams/configure.md)할 때 데이터 스트림 구성 재정의를 정의해야 합니다. 재정의를 구성하는 방법에 대한 지침은 데이터스트림 설명서에서 [데이터스트림 구성 재정의](/help/datastreams/overrides.md)를 참조하십시오.
1. 데이터스트림 UI에서 데이터스트림 재정의를 구성한 후 태그 확장을 구성할 수 있습니다.

데이터 스트림 재정의는 환경별로 구성해야 합니다. 개발, 스테이징 및 프로덕션 환경에는 모두 별도의 재정의가 있습니다. 원하는 환경 간에 무시 설정을 복사할 수 있습니다.

![웹 SDK 태그 확장 페이지를 사용하여 데이터 스트림 구성 재정의를 표시하는 이미지입니다.](../assets/datastream-overrides.png)

기본적으로 데이터 스트림 구성 재정의는 비활성화되어 있습니다. 기본적으로 **[!UICONTROL Match datastream configuration]** 옵션이 선택되어 있습니다.

![데이터 스트림 구성을 표시하는 웹 SDK 태그 확장 사용자 인터페이스가 기본 설정을 재정의합니다.](../assets/datastream-override-default.png)

태그 확장에서 데이터 스트림 재정의를 사용하려면 드롭다운 메뉴에서 **[!UICONTROL Enabled]**&#x200B;을(를) 선택합니다.

![데이터 스트림 구성 재정의 사용 설정을 표시하는 웹 SDK 태그 확장 사용자 인터페이스입니다.](../assets/datastream-override-enabled.png)

데이터스트림 구성 재정의를 활성화한 후에는 아래에 설명된 각 서비스에 대한 재정의를 구성할 수 있습니다. 이러한 데이터스트림 재정의 설정은 선택한 환경에 대한 서버측 데이터스트림 구성 및 규칙을 재정의합니다.

## Adobe Analytics

Adobe Analytics 서비스로 데이터 라우팅을 재정의합니다.

![Adobe Analytics 데이터 스트림 재정의 설정을 보여 주는 웹 SDK 태그 확장 UI 이미지입니다.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Adobe Analytics에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Report suites]**: Adobe Analytics에 있는 대상 보고서 세트의 ID입니다. 값은 데이터 스트림 구성에서 미리 구성된 재정의 보고서 세트(또는 쉼표로 구분된 보고서 세트 목록)여야 합니다. 이 설정은 기본 보고서 세트를 무시합니다.
* **[!UICONTROL Add Report Suite]**: 보고서 세트를 더 추가하려면 이 옵션을 선택하십시오.

## Adobe Audience Manager

Adobe Audience Manager으로 데이터 라우팅을 재정의합니다.

![Adobe Audience Manager 데이터 스트림 재정의 설정을 보여 주는 웹 SDK 태그 확장 UI 이미지입니다.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Adobe Audience Manager에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Third-party ID sync container]**: Audience Manager에서 대상 타사 ID 동기화 컨테이너의 ID입니다. 값은 데이터 스트림 구성에서 미리 구성된 보조 컨테이너여야 하며 기본 컨테이너를 무시합니다.

## Adobe Experience Platform

Adobe Experience Platform으로 데이터 라우팅을 재정의합니다.

![Adobe Experience Platform 데이터 스트림 재정의 설정을 보여 주는 웹 SDK 태그 확장 UI 이미지입니다.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Adobe Experience Platform에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Event dataset]**: Adobe Experience Platform의 대상 이벤트 데이터 세트에 대한 ID입니다. 값은 데이터 스트림 구성에서 미리 구성된 보조 데이터 세트여야 합니다.
* **[!UICONTROL Offer Decisioning]**: [!DNL Offer Decisioning] 서비스에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Edge Segmentation]**: [!DNL Edge Segmentation] 서비스에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Personalization Destinations]**: 개인화 대상에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
* **[!UICONTROL Adobe Journey Optimizer]**: [!DNL Adobe Journey Optimizer]&#x200B;(으)로 데이터 라우팅을 활성화하거나 비활성화합니다.

## Adobe 서버측 이벤트 전달

Adobe 서버측 이벤트 전달 서비스로 데이터 라우팅을 재정의합니다.

![Adobe 서버측 이벤트 전달 데이터스트림 재정의 설정을 보여 주는 웹 SDK 태그 확장 UI 이미지입니다.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Adobe 서버측 이벤트 전달 서비스에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.

## Adobe Target {#target}

Adobe Target으로 데이터 라우팅을 재정의합니다.

![Adobe Target 데이터 스트림 재정의 설정을 보여 주는 웹 SDK 태그 확장 UI 이미지입니다.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Adobe Target에 대한 데이터 라우팅을 활성화하거나 비활성화합니다.
