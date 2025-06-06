---
title: 이벤트 전달 개요
description: Experience Platform Edge Network를 사용하여 태그 구현을 변경하지 않고 작업을 실행할 수 있도록 Adobe Experience Platform의 이벤트 게재에 대해 알아봅니다.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 8%

---

# 이벤트 전달 개요

>[!NOTE]
>
>이벤트 전달은 Adobe Real-Time Customer Data Platform 연결, Prime 또는 Ultimate 오퍼링의 일부로 포함된 유료 기능입니다.

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform의 이벤트 전달을 사용하면 수집된 이벤트 데이터를 서버측 처리를 위해 대상으로 전송할 수 있습니다. 이벤트 전달은 Adobe Experience Platform Edge Network을 사용하여 클라이언트에서 일반적으로 수행되는 작업을 실행하여 웹 페이지 및 앱 가중치를 줄입니다. 태그와 유사한 방식으로 구현된 이벤트 전달 규칙은 데이터를 변환하여 새 대상으로 전송할 수 있지만 웹 브라우저와 같은 클라이언트 애플리케이션에서 이 데이터를 전송하는 대신 Adobe 서버에서 전송됩니다.

이 문서에서는 Experience Platform의 이벤트 전달에 대한 높은 수준의 개요를 제공합니다.

![데이터 수집 생태계의 이벤트 전달.](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>이벤트 전달이 Experience Platform의 데이터 수집 생태계에 어떻게 적합한지에 대한 자세한 내용은 [데이터 수집 개요](../../../collection/home.md)를 참조하십시오.

Adobe Experience Platform [Web SDK](/help/web-sdk/home.md) 및 [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html?lang=ko)와 결합된 이벤트 전달은 다음과 같은 이점을 제공합니다.

**성능**:

* 데이터 페이로드가 포함된 페이지에서 한 번의 호출을 만들어 서버측에서 연합하여 클라이언트측 네트워크 트래픽을 줄이고 고객에게 보다 빠른 경험을 제공합니다.
* 웹 페이지를 로드하는 데 걸리는 시간을 줄여 사이트 성능을 향상시킵니다.
* 경험을 전달하고 데이터를 여러 대상에 전송하는 데 필요한 클라이언트측 기술의 수를 줄입니다.

**데이터 관리**:

* 투명도를 높이고 모든 속성에서 데이터를 보낼 위치를 제어합니다.

## 이벤트 전달과 태그의 차이점 {#differences-from-tags}

구성 측면에서 이벤트 전달에는 [규칙](../managing-resources/rules.md), [데이터 요소](../managing-resources/data-elements.md) 및 [확장](../managing-resources/extensions/overview.md)과 같은 태그와 동일한 개념이 많이 사용됩니다. 양자의 주요 차이점은 다음과 같이 요약할 수 있습니다.

* 태그 **웹 사이트 또는 기본 모바일 애플리케이션에서 이벤트 데이터를 수집**&#x200B;하여 Experience Platform Edge Network으로 보냅니다.
* 이벤트 전달 **은(는) Experience Platform Edge Network에서 들어오는 이벤트 데이터를 최종 대상을 나타내는 끝점 또는 원본 페이로드를 보강할 데이터를 제공하는 끝점으로 보냅니다**.

태그는 Experience Platform 웹 및 Mobile SDK를 사용하여 사이트 또는 기본 모바일 애플리케이션에서 직접 이벤트 데이터를 수집하지만, 이벤트를 전달하려면 이벤트 데이터를 대상으로 전달하기 위해 Experience Platform Edge Network을 통해 이미 전송해야 합니다. 즉, 이벤트 전달을 사용하려면 태그를 통해 또는 원시 코드를 사용하여 디지털 속성에 Experience Platform 웹 또는 Mobile SDK을 구현해야 합니다.

### 속성 {#properties}

이벤트 전달은 태그와 별도로 고유한 속성 저장소를 유지 관리합니다. 이 저장소는 왼쪽 탐색에서 **[!UICONTROL 이벤트 전달]**&#x200B;을(를) 선택하여 Experience Platform UI 또는 데이터 수집 UI에서 볼 수 있습니다.

>[!TIP]
>
>오른쪽 패널의 제품 도움말에서 이벤트 전달에 대한 자세한 내용을 살펴보고 사용 가능한 추가 리소스를 확인하십시오.

![데이터 수집 UI의 이벤트 전달 속성입니다.](../../images/ui/event-forwarding/overview/properties.png)

모든 이벤트 전달 속성은 플랫폼으로 **[!UICONTROL Edge]**&#x200B;을(를) 나열합니다. 웹 및 모바일 플랫폼 모두에서 이벤트 데이터를 받을 수 있는 Experience Platform Edge Network에서 받은 데이터만 처리하므로 웹 또는 모바일을 구분하지 않습니다.

### 확장 {#extensions}

이벤트 전달에는 [Core](../../extensions/server/core/overview.md) 확장 및 [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md) 확장과 같은 호환되는 확장에 대한 자체 카탈로그가 있습니다. 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 카탈로그]**&#x200B;를 선택하여 UI에서 이벤트 전달 속성에 사용 가능한 확장을 볼 수 있습니다.

오른쪽 패널에서 ![정보](../../images/ui/event-forwarding/overview/about.png)을(를) 선택하여 이 기능에 대해 자세히 알아볼 수 있는 추가 리소스를 볼 수 있습니다.

![데이터 수집 UI의 이벤트 전달 확장.](../../images/ui/event-forwarding/overview/extensions.png)

### 데이터 요소 {#data-elements}

이벤트 전달에서 사용할 수 있는 데이터 요소 유형은 해당 요소를 제공하는 호환 가능한 [확장](#extensions)의 카탈로그로 제한됩니다.

데이터 요소 자체는 태그에 대한 것과 동일한 방식으로 이벤트 전달에서 만들어지고 구성되지만, Experience Platform Edge Network의 데이터를 참조하는 방식과 관련하여 몇 가지 중요한 구문 차이가 있습니다.

#### Experience Platform Edge Network의 데이터 참조 {#data-element-path}

Experience Platform Edge Network의 데이터를 참조하려면 해당 데이터에 올바른 경로를 제공하는 데이터 요소를 만들어야 합니다. UI에서 데이터 요소를 만들 때 확장에 대해 **[!UICONTROL Core]**&#x200B;을(를) 선택하고 유형에 대해 **[!UICONTROL Path]**&#x200B;을(를) 선택합니다.

데이터 요소의 **[!UICONTROL Path]** 값은 `arc.event.{ELEMENT}` 패턴(예: `arc.event.xdm.web.webPageDetails.URL`)을 따라야 합니다. 데이터를 전송하려면 이 경로를 올바르게 지정해야 합니다.

오른쪽 패널에서 ![정보](../../images/ui/event-forwarding/overview/about.png)을(를) 선택하여 이 기능에 대해 자세히 알아볼 수 있는 추가 리소스를 볼 수 있습니다.

![이벤트 전달을 위한 경로 유형 데이터 요소의 예입니다.](../../images/ui/event-forwarding/overview/data-reference.png)

### 규칙 {#rules}

이벤트 전달 속성에서 규칙을 만드는 것은 태그와 유사한 방식으로 작동하며 주요 차이점은 이벤트를 규칙 구성 요소로 선택할 수 없다는 것입니다. 대신 이벤트 전달 규칙은 [데이터스트림](../../../datastreams/overview.md)에서 받은 모든 이벤트를 처리하고 특정 조건이 충족되는 경우 이러한 이벤트를 대상으로 전달합니다.

또한 이벤트 전달 속성 내의 모든 규칙(및 따라서 모든 작업)에 걸쳐 처리되므로 단일 이벤트에 적용되는 30초 시간 초과가 있습니다. 즉, 이 시간대에 단일 이벤트에 대한 모든 규칙과 모든 작업을 완료해야 합니다.

오른쪽 패널에서 ![정보](../../images/ui/event-forwarding/overview/about.png)을(를) 선택하여 이 기능에 대해 자세히 알아볼 수 있는 추가 리소스를 볼 수 있습니다.

![데이터 수집 UI의 이벤트 전달 규칙입니다.](../../images/ui/event-forwarding/overview/rules.png)

#### 데이터 요소 토큰화 {#tokenization}

태그 규칙에서 데이터 요소는 데이터 요소 이름의 시작 및 끝에 `%`(예: `%viewportHeight%`)로 토큰화됩니다. 이벤트 전달 규칙에서 데이터 요소는 대신 데이터 요소 이름의 시작 부분에 `{{`, 끝 부분에 `}}`(예: `{{viewportHeight}}`)으로 토큰화됩니다.

오른쪽 패널에서 ![정보](../../images/ui/event-forwarding/overview/about.png)을(를) 선택하여 이 기능에 대해 자세히 알아볼 수 있는 추가 리소스를 볼 수 있습니다.

![이벤트 전달을 위한 경로 유형 데이터 요소의 예입니다.](../../images/ui/event-forwarding/overview/tokenization.png)

#### 규칙 작업 순서 {#action-sequencing}

이벤트 전달 규칙의 [!UICONTROL 작업] 섹션은 항상 순차적으로 실행됩니다. 예를 들어 규칙에 두 개의 작업이 있는 경우 이전 작업이 완료될 때까지(그리고 끝점에서 응답이 예상되는 경우 해당 끝점이 응답함) 두 번째 작업은 실행을 시작하지 않습니다. 규칙을 저장할 때 작업 순서가 올바른지 확인합니다. 이 실행 시퀀스는 태그 규칙과 마찬가지로 비동기식으로 실행할 수 없습니다.

## 비밀 {#secrets}

이벤트 전달을 통해 데이터를 전송하는 서버를 인증하는 데 사용할 수 있는 비밀을 생성, 관리 및 저장할 수 있습니다. 사용 가능한 다양한 종류의 암호 유형과 UI에서 구현되는 방법에 대한 [암호](./secrets.md)에 대한 안내서를 참조하십시오.

## 비디오 개요 {#video}

다음 비디오는 이벤트 전달 및 Real-Time CDP 연결을 더 잘 이해하는 데 도움을 주기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## 다음 단계

이 문서는 이벤트 전달에 대한 높은 수준의 소개를 제공했습니다. 조직의 이 기능을 설정하는 방법에 대한 자세한 내용은 [시작 안내서](./getting-started.md)를 참조하십시오.
