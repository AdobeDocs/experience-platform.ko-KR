---
title: 컨텍스트
description: 장치, 환경 또는 위치 데이터를 자동으로 수집합니다.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: dc2a2ecf7b602d2fcfd3b6c93cecdb6f3368a3f9
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 5%

---

# `context`

다음 `context` 속성은 웹 SDK에서 자동으로 수집할 수 있는 항목을 결정하는 문자열 배열입니다. 이 데이터는 큰 가치를 제공할 수 있지만 이 데이터 중 일부를 생략하면 조직의 개인정보 처리방침을 준수하는 데 도움이 될 수 있습니다.

## 컨텍스트 키워드 및 XDM 요소

주어진 컨텍스트 키워드를 포함하면 Web SDK가 연관된 모든 XDM 요소를 자동으로 채웁니다. 다른 요소를 허용하면서 특정 XDM 요소를 생략하려면 다음을 사용하여 값을 지울 수 있습니다. [`onBeforeEventSend`](onbeforeeventsend.md). 페이지에서 여러 이벤트를 보내는 경우 웹 SDK는 다음 필드에 모두 해당 필드를 포함합니다 `SendEvent` 호출합니다.

### 웹

다음 `"web"` 키워드는 현재 페이지에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 페이지 URL | 현재 페이지의 URL. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 레퍼러 URL | 방문한 이전 페이지의 URL입니다. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### 디바이스

다음 `"device"` 키워드는 사용자의 디바이스에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 화면 높이 | 화면의 픽셀 단위 높이입니다. | `xdm.device.screenHeight` | `900` |
| 화면 너비 | 화면의 픽셀 단위 폭입니다. | `xdm.device.screenWidth` | `1440` |
| 화면 방향 | 화면의 방향입니다. | `xdm.device.screenOrientation` | `landscape` 또는 `portrait` |

{style="table-layout:auto"}

### 환경

다음 `"environment"` 키워드는 사용자의 브라우저에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 환경 유형 | 경험이 표시되는 환경의 유형입니다. Web SDK는 항상 이 필드를 다음으로 설정합니다. `browser`. | `xdm.environment.type` | `browser` |
| 뷰포트 높이 | 브라우저 컨텐츠 영역의 픽셀 단위 높이입니다. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 뷰포트 폭 | 브라우저 컨텐츠 영역의 픽셀 단위 폭입니다. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### 위치 컨텍스트

다음 `"placeContext"` 키워드는 사용자의 위치에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 현지 시간 | 간소화된 확장에서 최종 사용자의 로컬 타임스탬프 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 포맷. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 로컬 시간대 오프셋 | 사용자가 GMT에서 오프셋된 시간(분)입니다. | `xdm.placeContext.localTimezoneOffset` | `360` |
| 국가 코드 | 최종 사용자의 국가 코드. | `xdm.placeContext.geo.countryCode` | `US` |
| 시/도 | 최종 사용자의 시/도 코드입니다. | `xdm.placeContext.geo.stateProvince` | `CA` |
| 위도 | 최종 사용자 위치의 위도입니다. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| 경도 | 최종 사용자 위치의 경도입니다. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### 타임스탬프

다음 `timestamp` 키워드는 이벤트의 타임스탬프에 대한 정보를 수집합니다. 컨텍스트의 이 부분은 제거할 수 없습니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 이벤트의 타임스탬프 | 간소화된 확장의 최종 사용자에 대한 UTC 타임스탬프 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 포맷. | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### 구현 세부 사항

다음 `implementationDetails` 키워드는 이벤트를 수집하는 데 사용되는 SDK 버전에 대한 정보를 수집합니다.

| 차원 | 설명 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- |
| 이름 | 소프트웨어 개발 키트(SDK) 식별자. 이 필드는 URI를 사용하여 다른 소프트웨어 라이브러리에서 제공하는 식별자 간의 고유성을 개선합니다. | `xdm.implementationDetails.name` | 독립형 라이브러리를 사용하는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy`. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 입니다. `https://ns.adobe.com/experience/alloy+reactor`. |
| 버전 | 소프트웨어 개발 키트(SDK) 버전. | `xdm.implementationDetails.version` | 독립형 라이브러리를 사용하는 경우 값은 라이브러리 버전입니다. 라이브러리가 태그 확장의 일부로 사용되는 경우 값은 라이브러리 버전 및 와 연결된 태그 확장 버전입니다. `+`. 예를 들어 라이브러리 버전이 `2.1.0` 및 태그 확장 버전은 입니다. `2.1.3`, 값은 다음과 같습니다 `2.1.0+2.1.3`. |
| 환경 | 데이터가 수집된 환경입니다. 항상 (으)로 설정됩니다. `browser`. | `xdm.implementationDetails.environment` | `browser` |


### 높은 엔트로피 클라이언트 힌트

다음 `"highEntropyUserAgentHints"` 키워드는 사용자 디바이스에 대한 세부 정보를 수집합니다. 이 데이터는 Adobe으로 전송된 요청의 HTTP 헤더에 포함됩니다. 데이터가 Edge 네트워크 내에 도달하면 XDM 개체가 해당 XDM 경로를 채웁니다. 에서 해당 XDM 경로를 설정하는 경우 `sendEvent` 를 호출하면 HTTP 헤더 값보다 우선합니다.

다음과 같은 경우에 디바이스 조회를 사용하는 경우 [데이터 스트림 구성](/help/datastreams/configure.md), 디바이스 조회 값을 위해 데이터를 지울 수 있습니다. 일부 클라이언트 힌트 필드와 장치 조회 필드가 동일한 히트에 있을 수 없습니다.

| 차원 | 설명 | HTTP 헤더 | XDM 경로 | 예제 값 |
| --- | --- | --- | --- | --- |
| 운영 체제 버전 | 운영 체제의 버전입니다. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| 아키텍처 | 기본 CPU 아키텍처. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| 디바이스 모델 | 사용된 디바이스의 이름입니다. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| 비트니스 | 기본 CPU 아키텍처가 지원하는 비트 수입니다. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| 브라우저 공급업체 | 브라우저를 만든 회사입니다. 낮은 엔트로피 힌트 `Sec-CH-UA` 는 이 요소를 수집합니다. | `Sec-CH-UA-Full-Version-List` | | |
| 브라우저 이름 | 사용된 브라우저입니다. 낮은 엔트로피 힌트 `Sec-CH-UA` 는 이 요소를 수집합니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| 브라우저 버전 | 브라우저의 중요 버전입니다. 낮은 엔트로피 힌트 `Sec-CH-UA` 는 이 요소를 수집합니다. 정확한 브라우저 버전은 자동으로 수집되지 않습니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## 웹 SDK 태그 확장을 사용하여 컨텍스트 정보 수집

컨텍스트 정보 설정은 다음과 같은 경우 라디오 단추와 확인란의 조합입니다 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 각 확인란은 컨텍스트 키워드에 매핑됩니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 후 다음 중 하나를 선택합니다. **[!UICONTROL 모든 기본 컨텍스트 정보]** 또는 **[!UICONTROL 특정 컨텍스트 정보]**.
1. 다음을 선택하는 경우 **[!UICONTROL 특정 컨텍스트 정보]**&#x200B;원하는 각 컨텍스트 정보 요소 옆의 확인란을 활성화합니다.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 컨텍스트 정보 수집

설정 `context` 를 실행할 때의 문자열 배열 `configure` 명령입니다. SDK를 구성할 때 이 속성을 생략하면 를 제외한 모든 컨텍스트 정보가 `"highEntropyUserAgentHints"` 는 기본적으로 수집됩니다. 높은 엔트로피 클라이언트 힌트를 수집하거나 데이터 수집에서 다른 컨텍스트 정보를 생략하려면 이 속성을 설정하십시오. 문자열은 임의의 순서로 포함될 수 있습니다.

>[!NOTE]
>
>높은 엔트로피 클라이언트 힌트를 포함하여 모든 컨텍스트 정보를 수집하려면 `context` 배열 문자열입니다. 기본값 `context` 값 생략 `highEntropyUserAgentHints`및 를 설정하는 경우 `context` 속성, 생략된 값은 데이터를 수집하지 않습니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
