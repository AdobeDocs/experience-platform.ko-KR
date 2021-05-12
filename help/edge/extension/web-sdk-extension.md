---
title: Adobe Experience Platform 웹 SDK 확장 개요
description: Adobe Experience Platform Launch용 Adobe Experience Platform Web SDK 익스텐션에 대한 자세한 내용
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: b70fe5f3a4de2501730cc799125a7181b61186c0
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 16%

---

# Adobe Experience Platform 웹 SDK 확장 개요

Adobe Experience Platform 웹 SDK 익스텐션은 Adobe Experience Platform Edge 네트워크를 통해 웹 속성에서 Adobe Experience Cloud으로 데이터를 전송합니다. 확장 기능을 사용하면 데이터를 플랫폼으로 스트리밍하고 ID를 동기화하며 고객 동의 신호를 처리하며 컨텍스트 데이터를 자동으로 수집할 수 있습니다.

이 문서에서는 Adobe Experience Platform Launch 사용자 인터페이스에서 확장을 구성하는 방법에 대해 설명합니다.

## 확장 프로그램 구성

속성에 대한 플랫폼 웹 SDK 확장이 이미 설치되어 있는 경우 Platform launch UI에서 속성을 열고 **[!UICONTROL Extensions]** 탭을 선택합니다. 플랫폼 웹 SDK 아래에서 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

![](../images/extension/overview/configure.png)

아직 확장을 설치하지 않은 경우 **[!UICONTROL Catalog]** 탭을 선택합니다. 사용 가능한 확장 프로그램 목록에서 플랫폼 웹 SDK 확장 프로그램을 찾아 **[!UICONTROL Install]**&#x200B;을 선택합니다.

![](../images/extension/overview/install.png)

두 경우 모두 플랫폼 웹 SDK의 구성 페이지에 도달합니다. 아래 섹션에서는 익스텐션의 구성 옵션에 대해 설명합니다.

![](../images/extension/overview/config-screen.png)

## 일반 구성 옵션

페이지 상단의 구성 옵션은 Adobe Experience Platform에서 데이터를 라우팅할 위치와 서버에서 사용할 구성을 알려줍니다.

### [!UICONTROL Name]

Adobe Experience Platform 웹 SDK 익스텐션은 페이지에서 여러 인스턴스를 지원합니다. 이 이름은 단일 Platform launch 구성을 사용하여 여러 조직에 데이터를 보내는 데 사용됩니다.

확장 프로그램의 이름은 기본적으로 &quot;[!DNL alloy]&quot;입니다. 그러나 인스턴스 이름을 유효한 JavaScript 개체 이름으로 변경할 수 있습니다.

### **[!UICONTROL IMS Organization ID]**

[!UICONTROL IMS Organization ID]는 Adobe에 데이터를 전송하는 조직입니다. 대부분의 경우 자동 계산되는 기본값을 사용합니다. 페이지에 인스턴스가 여러 개 있으면 데이터를 보내려는 두 번째 조직의 값으로 이 필드를 채웁니다.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain]은 Adobe Experience Platform 확장에서 데이터를 보내고 받는 도메인입니다. 기본 타사 도메인은 프로덕션 트래픽에 자사 CNAME을 사용해야 합니다. 기본 타사 도메인은 개발 환경에서 작동하지만, 프로덕션 환경에는 적합하지 않습니다. 자사 CNAME을 설정하는 방법에 대한 지침은 [여기](https://docs.adobe.com/content/help/ko/core-services/interface/ec-cookies/cookies-first-party.html)에 나와 있습니다.

## [!UICONTROL Datastreams]

요청이 Adobe Experience Platform Edge Network로 전송되면 서버측 구성을 참조하는 데 데이터 스트림 ID가 사용됩니다. 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

자세한 내용은 [데이터 저장소](../fundamentals/datastreams.md)의 안내서를 참조하십시오.


## [!UICONTROL Privacy]

[!UICONTROL Privacy] 섹션에서는 SDK가 웹 사이트의 사용자 동의 신호를 처리하는 방법을 구성할 수 있습니다. 특히, 다른 명시적 동의 기본 설정이 제공되지 않은 경우 사용자에게 가정되는 기본 동의 수준을 선택할 수 있습니다. 기본 동의 수준은 사용자의 프로필에 저장되지 않습니다. 다음 표에서는 각 옵션에 대해 설명합니다.

| [!UICONTROL Default Consent Level] | 설명 |
| --- | --- |
| [!UICONTROL In] | 사용자가 동의 기본 설정을 제공하기 전에 발생하는 이벤트를 수집합니다. |
| [!UICONTROL Out] | 사용자가 동의 기본 설정을 제공하기 전에 발생하는 이벤트를 버립니다. |
| [!UICONTROL Pending] | 사용자가 동의 환경 설정을 제공하기 전에 발생하는 큐 이벤트입니다. 동의 기본 설정이 제공되면 제공된 기본 설정에 따라 이벤트가 수집되거나 무시됩니다. |
| [!UICONTROL Provided by data element] | 기본 동의 수준은 사용자가 정의하는 별도의 데이터 요소에 의해 결정됩니다. 이 옵션을 사용할 때는 제공된 드롭다운 메뉴를 사용하여 데이터 요소를 지정해야 합니다. |

업무 운영에 대한 명시적 사용자 동의를 필요로 하는 경우 종료 또는 보류 중 을 사용하십시오.
