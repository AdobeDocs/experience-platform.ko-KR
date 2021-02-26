---
title: Adobe Experience Platform 웹 SDK 확장 개요
description: Adobe Experience Platform Launch용 Adobe Experience Platform Web SDK 익스텐션에 대한 자세한 내용
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 19%

---


# Adobe Experience Platform 웹 SDK 확장 개요

Adobe Experience Platform 웹 SDK 익스텐션은 Adobe Experience Platform Edge 네트워크를 통해 웹 속성에서 Adobe Experience Cloud으로 데이터를 전송합니다. 확장 기능을 사용하면 데이터를 플랫폼으로 스트리밍하고 ID를 동기화하며 고객 동의 신호를 처리하며 컨텍스트 데이터를 자동으로 수집할 수 있습니다.

이 문서에서는 Adobe Experience Platform Launch 사용자 인터페이스에서 확장을 구성하는 방법에 대해 설명합니다.

## 확장 프로그램 구성

속성에 대한 플랫폼 웹 SDK 확장이 이미 설치되어 있는 경우 Platform launch UI에서 속성을 열고 **[!UICONTROL 확장]** 탭을 선택합니다. 플랫폼 웹 SDK 아래에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![](../images/extension/overview/configure.png)

아직 확장을 설치하지 않은 경우 **[!UICONTROL 카탈로그]** 탭을 선택합니다. 사용 가능한 확장 프로그램 목록에서 플랫폼 웹 SDK 확장 프로그램을 찾아 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![](../images/extension/overview/install.png)

두 경우 모두 플랫폼 웹 SDK의 구성 페이지에 도달합니다. 아래 섹션에서는 익스텐션의 구성 옵션에 대해 설명합니다.

![](../images/extension/overview/config-screen.png)

## 일반 구성 옵션

페이지 상단의 구성 옵션은 Adobe Experience Platform에 데이터를 라우팅할 위치와 서버에서 사용해야 하는 구성을 알려줍니다.

### [!UICONTROL 이름]

Adobe Experience Platform 웹 SDK 익스텐션은 페이지에서 여러 인스턴스를 지원합니다. 이 확장은 단일 Platform Launch 구성을 사용하여 여러 조직에 데이터를 전송하는 데 사용됩니다.

확장 프로그램의 이름은 기본적으로 &quot;[!DNL alloy]&quot;입니다. 그러나 인스턴스 이름을 유효한 JavaScript 개체 이름으로 변경할 수 있습니다.

### **[!UICONTROL IMS 조직 ID]**

[!UICONTROL IMS 조직 ID]는 Adobe에서 데이터를 보내려는 조직입니다. 대부분의 경우 자동 채우기되는 기본값을 사용해야 합니다. 페이지에 인스턴스가 여러 개 있으면 데이터를 보내려는 두 번째 조직의 값으로 이 필드를 채웁니다.

### **[!UICONTROL Edge 도메인]**

[!UICONTROL Edge 도메인]은 Adobe Experience Platform 확장이 데이터를 보내고 받는 도메인입니다. 기본 타사 도메인은 프로덕션 트래픽에 자사 CNAME을 사용해야 합니다. 기본 타사 도메인은 개발 환경에서 작동하지만, 프로덕션 환경에는 적합하지 않습니다. 자사 CNAME을 설정하는 방법에 대한 지침은 [여기](https://docs.adobe.com/content/help/ko-KR/core-services/interface/ec-cookies/cookies-first-party.html)에 나와 있습니다.

## [!UICONTROL 에지 구성]

Adobe Experience Platform Edge Network에 요청이 전송되면 서버측 구성을 참조하는 데 Edge 구성 ID가 사용됩니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

자세한 내용은 [edge 구성](../fundamentals/edge-configuration.md)의 안내서를 참조하십시오.

## [!UICONTROL 개인 정보 보호]

[!UICONTROL 개인 정보] 섹션에서는 SDK가 웹 사이트의 고객 동의 신호를 처리하는 방법을 구성할 수 있습니다. 특히, 다른 명시적 동의 기본 설정이 제공되지 않은 경우 고객에 대해 가정되는 기본 동의 수준을 선택할 수 있습니다. 다음 표에서는 각 옵션에 대해 설명합니다.

| [!UICONTROL 기본 동의 수준] | 설명 |
| --- | --- |
| [!UICONTROL 시작] | 옵트인. 기본적으로 고객의 동의를 가정하고 옵트아웃 신호만 준수하는 경우 이 옵션을 사용합니다. |
| [!UICONTROL 보류 중] | &quot;보류 중&quot; 동의의 고객은 옵트인 신호가 전송될 때까지 옵트아웃되는 것으로 간주됩니다. 업무 운영에 대한 명시적 고객 동의를 필요로 하는 경우 이 옵션을 사용합니다. |
| [!UICONTROL 데이터 요소로 제공] | 기본 동의 수준은 사용자가 정의하는 별도의 데이터 요소에 의해 결정됩니다. 이 옵션을 사용할 때는 제공된 드롭다운 메뉴를 사용하여 데이터 요소를 지정해야 합니다. |