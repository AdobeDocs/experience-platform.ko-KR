---
title: 컨텍스트
description: 장치, 환경 또는 위치 데이터를 자동으로 수집합니다.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 7%

---

# `context`

`context` 속성은 웹 SDK에서 자동으로 수집할 수 있는 항목을 결정하는 문자열 배열입니다. 이 데이터는 큰 가치를 제공할 수 있지만 이 데이터 중 일부를 생략하면 조직의 개인정보 처리방침을 준수하는 데 도움이 될 수 있습니다.

## 컨텍스트 키워드 및 XDM 요소

주어진 컨텍스트 키워드를 포함하면 Web SDK가 연관된 모든 XDM 요소를 자동으로 채웁니다. 다른 요소를 허용하면서 특정 XDM 요소를 생략하려면 [`onBeforeEventSend`](onbeforeeventsend.md)을(를) 사용하여 값을 지울 수 있습니다. 페이지에서 여러 이벤트를 전송하는 경우 Web SDK는 `SendEvent` 호출 시마다 이러한 필드를 포함합니다.

### 웹

`"web"` 키워드는 현재 페이지에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 페이지 URL | 현재 페이지의 URL. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 레퍼러 URL | 방문한 이전 페이지의 URL입니다. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### 디바이스

`"device"` 키워드는 사용자의 장치에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 화면 높이 | 화면의 픽셀 단위 높이입니다. | `xdm.device.screenHeight` | `900` |
| 화면 폭 | 화면의 픽셀 단위 폭입니다. | `xdm.device.screenWidth` | `1440` |
| 화면 방향 | 화면의 방향입니다. | `xdm.device.screenOrientation` | `landscape` 또는 `portrait` |

{style="table-layout:auto"}

### 환경

`"environment"` 키워드는 사용자의 브라우저에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 환경 유형 | 경험이 표시되는 환경의 유형입니다. Web SDK는 항상 이 필드를 `browser`(으)로 설정합니다. | `xdm.environment.type` | `browser` |
| 뷰포트 높이 | 브라우저 컨텐츠 영역의 픽셀 단위 높이입니다. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 뷰포트 폭 | 브라우저 컨텐츠 영역의 픽셀 단위 폭입니다. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### 위치 컨텍스트

`"placeContext"` 키워드는 사용자의 위치에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 로컬 시간 | 단순화된 확장 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 형식의 최종 사용자의 로컬 타임스탬프입니다. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 로컬 시간대 오프셋 | 사용자가 GMT에서 오프셋된 시간(분)입니다. | `xdm.placeContext.localTimezoneOffset` | `360` |
| 국가 코드 | 최종 사용자의 국가 코드. | `xdm.placeContext.geo.countryCode` | `US` |
| 시/도 | 최종 사용자의 시/도 코드입니다. | `xdm.placeContext.geo.stateProvince` | `CA` |
| 위도 | 최종 사용자 위치의 위도입니다. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| 경도 | 최종 사용자 위치의 경도입니다. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### 타임스탬프

`timestamp` 키워드는 이벤트의 타임스탬프에 대한 정보를 수집합니다. 컨텍스트의 이 부분은 제거할 수 없습니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 이벤트의 타임스탬프 | 간소화된 확장 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 형식의 최종 사용자에 대한 UTC 타임스탬프입니다. | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### 구현 세부 정보

`implementationDetails` 키워드는 이벤트를 수집하는 데 사용되는 SDK 버전에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 이름 | 소프트웨어 개발 키트(SDK) 식별자. 이 필드는 URI를 사용하여 다른 소프트웨어 라이브러리에서 제공하는 식별자 간의 고유성을 개선합니다. | `xdm.implementationDetails.name` | 독립 실행형 라이브러리를 사용할 때 값은 `https://ns.adobe.com/experience/alloy`입니다. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 `https://ns.adobe.com/experience/alloy+reactor`입니다. |
| 버전 | 소프트웨어 개발 키트(SDK) 버전. | `xdm.implementationDetails.version` | 독립형 라이브러리를 사용하는 경우 값은 라이브러리 버전입니다. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 라이브러리 버전 및 `+`(으)로 연결된 태그 확장 버전입니다. 예를 들어 라이브러리 버전이 `2.1.0`이고 태그 확장 버전이 `2.1.3`인 경우 값은 `2.1.0+2.1.3`이 됩니다. |
| 환경 | 데이터가 수집된 환경입니다. 항상 `browser`(으)로 설정됩니다. | `xdm.implementationDetails.environment` | `browser` |


### 높은 엔트로피 클라이언트 힌트 {#high-entropy-client-hints}

>[!TIP]
>
>구성 방법에 대한 자세한 내용은 [사용자 에이전트 클라이언트 힌트](../../use-cases/client-hints.md)에 대한 설명서를 참조하십시오.

`"highEntropyUserAgentHints"` 키워드는 사용자 장치에 대한 자세한 정보를 수집합니다. 이 데이터는 Adobe으로 전송된 요청의 HTTP 헤더에 포함됩니다. 데이터가 Edge 네트워크 내에 도달하면 XDM 개체가 해당 XDM 경로를 채웁니다. `sendEvent` 호출에서 각 XDM 경로를 설정하면 HTTP 헤더 값보다 우선합니다.

[데이터 스트림을 구성](/help/datastreams/configure.md)할 때 장치 조회를 사용하는 경우 장치 조회 값을 위해 데이터를 지울 수 있습니다. 일부 클라이언트 힌트 필드와 장치 조회 필드가 동일한 히트에 있을 수 없습니다.

| 속성 | 설명 | HTTP 헤더 | XDM 경로 | 예 |
| --- | --- | --- | --- | --- |
| 운영 체제 버전 | 운영 체제의 버전입니다. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| 아키텍처 | 기본 CPU 아키텍처. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| 장치 모델 | 사용된 디바이스의 이름입니다. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| 비트니스 | 기본 CPU 아키텍처가 지원하는 비트 수입니다. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| 브라우저 공급업체 | 브라우저를 만든 회사입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| 브라우저 이름 | 사용된 브라우저입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| 브라우저 버전 | 브라우저의 중요 버전입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. 정확한 브라우저 버전은 자동으로 수집되지 않습니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

{style="table-layout:auto"}

## 웹 SDK 태그 확장을 사용하여 컨텍스트 정보 수집

컨텍스트 정보 설정은 [태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 라디오 단추와 확인란의 조합입니다. 각 확인란은 컨텍스트 키워드에 매핑됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 **[!UICONTROL 모든 기본 컨텍스트 정보]** 또는 **[!UICONTROL 특정 컨텍스트 정보]**&#x200B;를 선택하십시오.
1. **[!UICONTROL 특정 컨텍스트 정보]**&#x200B;를 선택하는 경우 원하는 각 컨텍스트 정보 요소 옆에 있는 확인란을 활성화하십시오.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 컨텍스트 정보 수집

`configure` 명령을 실행할 때 `context` 문자열 배열을 설정하십시오. SDK를 구성할 때 이 속성을 생략하면 기본적으로 `"highEntropyUserAgentHints"`을(를) 제외한 모든 컨텍스트 정보가 수집됩니다. 높은 엔트로피 클라이언트 힌트를 수집하거나 데이터 수집에서 다른 컨텍스트 정보를 생략하려면 이 속성을 설정하십시오. 문자열은 임의의 순서로 포함될 수 있습니다.

>[!NOTE]
>
>높은 엔트로피 클라이언트 힌트를 포함하여 모든 컨텍스트 정보를 수집하려면 `context` 배열 문자열에 모든 값을 포함해야 합니다. 기본 `context` 값은 `highEntropyUserAgentHints`을(를) 생략하고 `context` 속성을 설정하는 경우 누락된 값은 데이터를 수집하지 않습니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
