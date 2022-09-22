---
title: Adobe Experience Platform 웹 SDK 확장 구성
description: 데이터 수집 UI에서 Adobe Experience Platform 웹 SDK 태그 확장을 구성하는 방법입니다.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 6%

---

# Adobe Experience Platform 웹 SDK 확장 구성

Adobe Experience Platform Web SDK 태그 확장은 Adobe Experience Platform Edge 네트워크를 통해 웹 속성에서 Adobe Experience Cloud으로 데이터를 전송합니다. 확장을 사용하면 데이터를 플랫폼으로 스트리밍하고 ID를 동기화하고 고객 동의 신호를 처리하며 컨텍스트 데이터를 자동으로 수집할 수 있습니다.

이 문서에서는 데이터 수집 UI에서 확장을 구성하는 방법을 설명합니다.

## 시작하기

속성에 대해 Platform Web SDK 확장이 이미 설치되어 있는 경우 데이터 수집 UI에서 속성을 열고 을 선택합니다. **[!UICONTROL 확장]** 탭. Platform Web SDK에서 **[!UICONTROL 구성]**.

![](../images/extension/overview/configure.png)

확장을 아직 설치하지 않은 경우 **[!UICONTROL 카탈로그]** 탭. 사용 가능한 확장 목록에서 Platform Web SDK 확장을 찾아 을 선택합니다. **[!UICONTROL 설치]**.

![](../images/extension/overview/install.png)

두 경우 모두 Platform Web SDK용 구성 페이지에 도달합니다. 아래 섹션에서는 확장의 구성 옵션에 대해 설명합니다.

![](../images/extension/overview/config-screen.png)

## 일반 구성 옵션

페이지 상단의 구성 옵션은 Adobe Experience Platform에서 데이터를 라우팅할 위치와 서버에서 사용할 구성을 알려줍니다.

### [!UICONTROL 이름]

Adobe Experience Platform Web SDK 확장은 페이지에서 여러 인스턴스를 지원합니다. 이름은 태그 구성을 사용하여 여러 조직에 데이터를 전송하는 데 사용됩니다.

확장의 이름은 기본적으로 &quot;[!DNL alloy]&quot;. 그러나 인스턴스 이름을 유효한 JavaScript 개체 이름으로 변경할 수 있습니다.

### **[!UICONTROL IMS 조직 ID]**

다음 [!UICONTROL IMS 조직 ID] 는 Adobe 시 데이터를 전송하려는 조직입니다. 대부분의 경우 자동 계산되는 기본값을 사용합니다. 페이지에 인스턴스가 여러 개 있으면 데이터를 보낼 두 번째 조직의 값으로 이 필드를 채웁니다.

### **[!UICONTROL Edge 도메인]**

다음 [!UICONTROL Edge 도메인] 은 Adobe Experience Platform 확장에서 데이터를 보내고 받는 도메인입니다. 이 확장에는 자사 도메인(CNAME)을 사용하는 것이 좋습니다. 기본 타사 도메인은 개발 환경에서 작동하지만, 프로덕션 환경에는 적합하지 않습니다. 자사 CNAME을 설정하는 방법에 대한 지침은 [여기](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=ko-KR)에 나와 있습니다.

## [!UICONTROL 데이터스트림]

Adobe Experience Platform Edge Network에 요청이 전송되면 서버측 구성을 참조하는 데이터 스트림 ID가 사용됩니다. 웹 사이트에서 코드를 변경하지 않고도 구성을 업데이트할 수 있습니다.

다음 안내서를 참조하십시오. [데이터 세트](../datastreams/overview.md) 추가 정보.


## [!UICONTROL 개인정보 보호]

![](../images/extension/overview/privacy.png)

다음 [!UICONTROL 개인 정보 보호] 섹션에서 SDK가 웹 사이트에서 사용자 동의 신호를 처리하는 방법을 구성할 수 있습니다. 특히, 다른 명시적 동의 기본 설정이 제공되지 않은 경우 사용자에 가정되는 기본 동의 수준을 선택할 수 있습니다. 기본 동의 수준이 사용자 프로필에 저장되지 않습니다. 다음 표에서는 각 옵션에 포함되는 사항을 설명합니다.

| [!UICONTROL 기본 동의 수준] | 설명 |
| --- | --- |
| [!UICONTROL in] | 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집합니다. |
| [!UICONTROL 종료] | 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 삭제합니다. |
| [!UICONTROL 보류 중] | 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 큐에 추가합니다. 동의 환경 설정이 제공되면 제공된 환경 설정에 따라 이벤트가 수집되거나 무시됩니다. |
| [!UICONTROL 데이터 요소에서 제공] | 기본 동의 수준은 사용자가 정의하는 별도의 데이터 요소에 의해 결정됩니다. 이 옵션을 사용하는 경우 제공된 드롭다운 메뉴를 사용하여 데이터 요소를 지정해야 합니다. |

비즈니스 운영에 대한 명시적 사용자 동의가 필요한 경우 종료 또는 보류 중 을 사용합니다.

## [!UICONTROL 신원]

![](../images/extension/overview/identity.png)

### [!UICONTROL VisitorAPI에서 ECID 마이그레이션]

이 옵션은 기본적으로 활성화되어 있습니다. 이 기능이 활성화되면 SDK는 AMCV 및 s_ecid 쿠키를 읽고 Visitor.js에서 사용하는 AMCV 쿠키를 설정할 수 있습니다. 일부 페이지에서 Visitor.js를 계속 사용할 수 있으므로 이 기능은 Adobe Experience Platform Web SDK로 마이그레이션할 때 중요합니다. 이를 통해 SDK는 동일한 ECID를 계속 사용하여 사용자가 두 개의 개별 사용자로 식별되지 않도록 할 수 있습니다.

### [!UICONTROL 타사 쿠키 사용]

이 옵션을 사용하면 SDK가 타사 쿠키에 사용자 ID를 저장하려고 할 수 있습니다. 성공적인 경우, 사용자는 각 도메인에서 별도의 사용자로 식별되지 않고 여러 도메인을 탐색할 때 단일 사용자로 식별됩니다. 이 옵션이 활성화되어 있으면 브라우저가 타사 쿠키를 지원하지 않거나 사용자가 타사 쿠키를 허용하지 않도록 구성한 경우 SDK가 여전히 사용자 식별자를 타사 쿠키에 저장할 수 없습니다. 이 경우 SDK는 자사 도메인에만 식별자를 저장합니다.

## [!UICONTROL 개인화]

![](../images/extension/overview/personalization.png)

개인화된 컨텐츠가 로드되는 동안 사이트에서 특정 부분을 숨기려면 사전 숨김 스타일 편집기에서 숨길 요소를 지정할 수 있습니다. 제공된 기본 코드 조각 사전 숨김을 복사하여 내부에 붙여넣을 수 있습니다 `<head>`HTML 사이트의 요소입니다.

## [!UICONTROL 데이터 수집]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL 콜백 함수]

확장에서 제공되는 콜백 함수를 [`onBeforeEventSend` 함수](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) 참조하십시오. 이 함수를 사용하면 이벤트를 Adobe Edge 네트워크로 전송하기 전에 전체적으로 수정할 수 있습니다. 이 함수 사용 방법에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL 데이터 수집 클릭]

SDK는 자동으로 링크 클릭 정보를 수집할 수 있습니다. 기본적으로 이 기능은 활성화되어 있지만 이 옵션을 사용하여 비활성화할 수 있습니다. 또한, 링크는 [!UICONTROL 다운로드 링크 한정자] 텍스트 상자 Adobe은 몇 가지 기본 다운로드 링크 한정자를 제공하지만 언제든지 편집할 수 있습니다.

### [!UICONTROL 자동으로 수집된 컨텍스트 데이터]

기본적으로 SDK는 장치, 웹, 환경 및 배치 컨텍스트에 대한 특정 컨텍스트 데이터를 수집합니다. Adobe이 수집하는 정보 목록을 보려면 해당 정보를 찾을 수 있습니다 [여기](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). 이 데이터를 수집하지 않으려는 경우 또는 특정 데이터 카테고리만 수집하려는 경우 이러한 옵션을 변경할 수 있습니다.

## [!UICONTROL 고급 설정]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL 에지 기본 경로]

Adobe Edge 네트워크와 상호 작용하는 데 사용되는 기본 경로를 변경해야 하는 경우 이 필드를 사용합니다. 업데이트하지 않아도 되지만, 베타 또는 알파에 참여하는 경우 Adobe에서 이 필드를 변경하도록 요청할 수 있습니다.
