---
title: 이벤트 전달 개요
description: Platform Edge Network를 사용하여 태그 구현을 변경하지 않고 작업을 실행할 수 있도록 Adobe Experience Platform의 이벤트 전달에 대해 알아봅니다.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 8%

---

# 이벤트 전달 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform의 이벤트 전달을 통해 수집된 이벤트 데이터를 서버측 처리를 위해 대상으로 전송할 수 있습니다. 이벤트 전달은 Adobe Experience Platform Edge Network를 사용하여 클라이언트에서 일반적으로 수행된 작업을 실행함으로써 웹 페이지 및 앱 가중치를 줄입니다. 태그와 유사한 방식으로 구현된 이벤트 전달 규칙은 데이터를 변형하고 새 대상으로 전송할 수 있지만 웹 브라우저와 같은 클라이언트 애플리케이션에서 이 데이터를 전송하는 대신 Adobe 서버에서 전송됩니다.

이 문서에서는 Platform의 이벤트 전달에 대한 높은 수준의 개요를 제공합니다.

![데이터 수집 생태계에서 이벤트 전달](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Platform의 데이터 수집 에코시스템에 이벤트 전달을 적용하는 방법에 대한 자세한 내용은 [데이터 수집 개요](../../../collection/home.md).

Adobe Experience Platform과 결합된 이벤트 전달 [웹 SDK](../../../edge/home.md) 및 [Mobile SDK](https://aep-sdks.gitbook.io/docs/) 은 다음과 같은 이점을 제공합니다.

**공연**:

* 데이터 페이로드가 포함된 페이지에서 한 번의 호출로 서버 측에서 페더레이션하여 클라이언트 측 네트워크 트래픽을 줄이고 고객을 위한 보다 빠른 경험을 제공합니다.
* 사이트 성능을 개선하기 위해 웹 페이지를 로드하는 데 걸리는 시간을 줄입니다.
* 경험을 전달하고 데이터를 많은 대상으로 전송하는 데 필요한 클라이언트측 기술 수를 줄입니다.

**데이터 거버넌스**:

* 투명도를 높이고 모든 속성에서 어느 데이터가 전송되는지 제어합니다.

## 이벤트 전달과 태그 간의 차이점 {#differences-from-tags}

구성 측면에서 이벤트 전달에서는 태그와 같은 많은 동일한 개념을 사용합니다 [규칙](../managing-resources/rules.md), [데이터 요소](../managing-resources/data-elements.md), 및 [확장](../managing-resources/extensions/overview.md). 그 둘의 주요 차이점은 다음과 같이 요약할 수 있다.

* 태그 **수집** 이벤트 데이터를 웹 사이트 또는 기본 모바일 애플리케이션에서 가져와 Platform Edge Network로 전송합니다.
* 이벤트 전달 **전송** Platform Edge Network에서 원래 페이로드를 보강할 데이터를 제공하는 최종 대상 또는 종단점을 나타내는 종단점으로 들어오는 이벤트 데이터입니다.

태그는 Platform Web 및 Mobile SDK를 사용하여 사이트 또는 기본 모바일 애플리케이션에서 직접 이벤트 데이터를 수집하지만 이벤트 전달을 사용하려면 대상에 전달하기 위해 Platform Edge 네트워크를 통해 이미 이벤트 데이터를 전송해야 합니다. 즉, 이벤트 전달을 사용하려면 디지털 속성(태그를 통해 또는 원시 코드 사용)에서 Platform Web 또는 Mobile SDK를 구현해야 합니다.

### 속성 {#properties}

이벤트 전달은 태그와 별도로 고유한 속성 저장소를 유지 관리하며, Experience Platform UI 또는 데이터 수집 UI에서 를 선택하여 볼 수 있습니다 **[!UICONTROL 이벤트 전달]** 을 클릭합니다.

![데이터 수집 UI의 이벤트 전달 속성](../../images/ui/event-forwarding/overview/properties.png)

모든 이벤트 전달 속성 목록 **[!UICONTROL Edge]** 플랫폼 Platform Edge Network에서 수신한 데이터만 처리하므로 웹 또는 모바일 플랫폼에서는 웹 및 모바일 플랫폼 모두에서 이벤트 데이터를 받을 수 있으므로 웹 또는 모바일을 구별하지 않습니다.

### 확장 {#extensions}

이벤트 전달에는 와 같은 호환되는 확장 카탈로그가 있습니다 [코어](../../extensions/server/core/overview.md) 확장 및 [Adobe 클라우드 커넥터](../../extensions/server/cloud-connector/overview.md) 확장. UI에서 을 선택하여 이벤트 전달 속성에 사용할 수 있는 확장을 볼 수 있습니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 를 차례로 클릭하거나 **[!UICONTROL 카탈로그]**.

![데이터 수집 UI의 이벤트 전달 확장](../../images/ui/event-forwarding/overview/extensions.png)

### 데이터 요소 {#data-elements}

이벤트 전달에서 사용할 수 있는 데이터 요소 유형은 호환 가능한 카탈로그로 제한됩니다 [확장](#extensions) 그것이 그들을 제공합니다.

데이터 요소 자체가 태그와 동일한 방식으로 이벤트 전달에서 만들어지고 구성되는 반면, Platform Edge Network에서 데이터를 참조하는 방법과 관련하여 몇 가지 중요한 구문 차이가 있습니다.

#### Platform Edge Network의 데이터 참조 {#data-element-path}

Platform Edge Network에서 데이터를 참조하려면 해당 데이터에 올바른 경로를 제공하는 데이터 요소를 만들어야 합니다. UI에서 데이터 요소를 만들 때 **[!UICONTROL 코어]** 확장 및 **[!UICONTROL 경로]** 참조하십시오.

다음 **[!UICONTROL 경로]** 데이터 요소의 값은 패턴을 따라야 합니다 `arc.event.{ELEMENT}` (예: `arc.event.xdm.web.webPageDetails.URL`). 데이터를 전송하려면 이 경로를 올바르게 지정해야 합니다.

![이벤트 전달을 위한 경로 유형 데이터 요소의 예](../../images/ui/event-forwarding/overview/data-reference.png)

### 규칙 {#rules}

이벤트 전달 속성에서 규칙을 만드는 것은 태그와 유사한 방식으로 작동하지만, 주요 차이점은 이벤트를 규칙 구성 요소로 선택할 수 없다는 것입니다. 대신, 이벤트 전달 규칙은 [데이터 스트림](../../../edge/datastreams/overview.md) 및 은 특정 조건이 충족되는 경우 해당 이벤트를 대상에 전달합니다.

![데이터 수집 UI의 이벤트 전달 규칙](../../images/ui/event-forwarding/overview/rules.png)

#### 데이터 요소 토큰화 {#tokenization}

태그 규칙에서 데이터 요소는 `%` 데이터 요소 이름의 시작 및 끝(예: `%viewportHeight%`). 이벤트 전달 규칙에서 데이터 요소는 대신 `{{` 시작 및 `}}` 데이터 요소 이름의 끝(예: `{{viewportHeight}}`).

![이벤트 전달을 위한 경로 유형 데이터 요소의 예](../../images/ui/event-forwarding/overview/tokenization.png)

#### 규칙 작업 순서 {#action-sequencing}

다음 [!UICONTROL 작업] 이벤트 전달 규칙의 섹션은 항상 순차적으로 실행됩니다. 규칙을 저장할 때 작업 순서가 올바른지 확인합니다. 이 실행 시퀀스는 태그를 사용할 수 있는 것처럼 비동기식으로 실행할 수 없습니다.

## 비밀 {#secrets}

이벤트 전달을 사용하면 데이터를 보내는 서버를 인증하는 데 사용할 수 있는 암호를 만들고, 관리하고 저장할 수 있습니다. 다음 안내서를 참조하십시오. [비밀](./secrets.md) 사용 가능한 여러 종류의 암호 유형과 UI에서 구현되는 방법에 대해 설명합니다.

## 다음 단계

이 문서에서는 이벤트 전달에 대한 높은 수준의 소개를 제공합니다. 조직에 대해 이 기능을 설정하는 방법에 대한 자세한 내용은 [시작 안내서](./getting-started.md).
