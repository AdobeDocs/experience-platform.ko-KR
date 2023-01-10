---
title: 사용자 에이전트 클라이언트 힌트
description: 웹 SDK에서 사용자 에이전트 클라이언트 힌트가 작동하는 방식을 알아봅니다
keywords: 사용자 에이전트;클라이언트 힌트; string; user-agent 문자열; 낮은 엔트로피 높은 엔트로피
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 4a2ae40fc64c4340ddb05db881c2176bb2aedc46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 6%

---

# 사용자 에이전트 클라이언트 힌트

## 개요 {#overview}

웹 브라우저가 웹 서버에 요청을 할 때마다 요청 헤더에 브라우저 및 브라우저가 실행 중인 환경에 대한 정보가 포함됩니다. 이 모든 데이터는 라는 문자열로 집계됩니다 [!DNL User-Agent] 문자열.

다음은 가 제공하는 예제입니다 [!DNL User-Agent] 문자열은 [!DNL Mac OS] 장치.

>[!NOTE]
>
>수년 동안 에 포함된 브라우저 및 장치 정보의 양 [!DNL User-Agent] 문자열이 여러 번 커지고 수정되었습니다. 아래 예제는 가장 일반적인 [!DNL User-Agent] 정보.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 필드 | 값 |
|---|---|
| 소프트웨어 이름 | Chrome |
| 소프트웨어 버전 | 105 |
| 전체 소프트웨어 버전 | 105.0.0.0 |
| 레이아웃 엔진 이름 | AppleWebKit |
| 레이아웃 엔진 버전 | 537.36 |
| 운영 체제 | Mac OS X |
| 운영 체제 버전 | 10.15.7 |
| 디바이스 | 인텔 Mac OS X 10_15_7 |

## 사용 사례 {#use-cases}

[!DNL User-Agent] 문자열은 오랫동안 마케팅 및 개발 팀에게 브라우저, 운영 체제 및 장치가 사이트 콘텐츠를 표시하는 방법과 사용자가 웹 사이트와 상호 작용하는 방법에 대한 중요한 인사이트를 제공하는 데 사용되었습니다.

[!DNL User-Agent] 또한 문자열은 스팸을 차단하거나 다양한 추가 목적으로 사이트를 크롤링하는 보트를 필터링하는 데 사용됩니다.

## [!DNL User-Agent] Adobe Experience Cloud의 문자열 {#user-agent-in-adobe}

Adobe Experience Cloud 솔루션은 [!DNL User-Agent] 다양한 방식으로 문자열.

* Adobe Analytics은 [!DNL User-Agent] 문자열을 사용하여 웹 사이트를 방문하는 데 사용되는 운영 체제, 브라우저 및 장치와 관련된 추가 정보를 증폭하고 파생시킵니다.
* Adobe Audience Manager 및 Adobe Target은 [!DNL User-Agent] 문자열.

## 사용자 에이전트 클라이언트 힌트 소개 {#ua-ch}

최근 몇 년간 사이트 소유자 및 마케팅 공급업체는 [!DNL User-Agent] 디지털 지문을 만들기 위해 요청 헤더에 포함된 다른 정보와 함께 문자열입니다. 이 지문들은 그들의 지식 없이 사용자를 식별하는 수단으로 사용될 수 있다.

중요한 목적에도 불구하고 [!DNL User-Agent] 사이트 소유자를 위한 문자열 제공, 브라우저 개발자가 방법 변경을 결정함 [!DNL User-Agent] 최종 사용자의 잠재적인 개인 정보 문제를 방지하기 위해 문자열이 작동합니다.

그들이 개발한 해결안은 바로 [사용자 에이전트 클라이언트 힌트](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 클라이언트 힌트는 여전히 웹 사이트에서 필요한 브라우저, 운영 체제 및 장치 정보를 수집할 수 있을 뿐만 아니라 지문 채취와 같은 비밀 추적 방법으로부터 더욱 강력한 보호를 제공합니다.

클라이언트 힌트를 사용하면 웹 사이트 소유자는 [!DNL User-Agent] 하지만 개인 정보 보호 방식으로 사용됩니다.

최신 브라우저가 사용자를 웹 서버로 보내면 전체 페이지가 [!DNL User-Agent] 문자열은 필요 여부에 관계없이 모든 요청 시 전송됩니다. 반면 클라이언트 힌트는 서버가 브라우저에 클라이언트에 대해 알고 싶은 추가 정보를 요청해야 하는 모델을 적용합니다. 이 요청을 받으면 브라우저가 자체 정책 또는 사용자 구성을 적용하여 반환되는 데이터를 확인할 수 있습니다. 전체 [!DNL User-Agent] 기본적으로 모든 요청에서 문자열은 이제 명시적 및 감사 가능한 방식으로 액세스를 관리합니다.

## 브라우저 지원 {#browser-support}

[사용자 에이전트 클라이언트 힌트](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 에서 [!DNL Google Chrome ]버전 89.

추가적인 Chromium 기반 브라우저는 다음과 같이 클라이언트 힌트 API를 지원합니다.

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## 카테고리 {#categories}

사용자 에이전트 클라이언트 힌트는 두 가지 범주로 구성됩니다.

* [낮은 엔트로피 클라이언트 힌트](#low-entropy)
* [높은 엔트로피 클라이언트 힌트](#high-entropy)

### 낮은 엔트로피 클라이언트 힌트 {#low-entropy}

낮은 엔트로피 클라이언트 힌트에는 지문 사용자에게 사용할 수 없는 기본 정보가 포함되어 있습니다. 브라우저 브랜드, 플랫폼 및 요청이 모바일 장치에서 오고 있는지 여부와 같은 정보입니다.

낮은 엔트로피 클라이언트 힌트는 Web SDK에서 기본적으로 활성화되며 모든 요청 시 전달됩니다.

| HTTP 헤더 | JavaScript | 기본적으로 사용자-에이전트에 포함됨 | 기본적으로 클라이언트 힌트에 포함됩니다 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 예 | 예 |
| `Sec-CH-UA-Platform` | `platform` | 예 | 예 |
| `Sec-CH-UA-Mobile` | `mobile` | 예 | 예 |

### 높은 엔트로피 클라이언트 힌트 {#high-entropy}

높은 엔트로피 클라이언트 힌트는 플랫폼 버전, 아키텍처, 모델, 비트도(64비트 또는 32비트 플랫폼) 또는 전체 운영 체제 버전과 같은 클라이언트 장치에 대한 자세한 정보입니다. 이 정보는 지문에 사용될 수 있다.

| HTTP 헤더 | JavaScript | 기본적으로 사용자-에이전트에 포함됨 | 기본적으로 클라이언트 힌트에 포함됨 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 예 | 아니요 |
| `Sec-CH-UA-Arc` | `architecture` | 예 | 아니요 |
| `Sec-CH-UA-Model` | `model` | 예 | 아니요 |
| `Sec-CH-UA-Bitness` | `Bitness` | 예 | 아니요 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 예 | 아니요 |

웹 SDK에서는 기본적으로 높은 엔트로피 클라이언트 힌트가 비활성화됩니다. 이를 활성화하려면 높은 엔트로피 클라이언트 힌트를 요청하도록 웹 SDK를 수동으로 구성해야 합니다.

## 높은 엔트로피 클라이언트 힌트는 Experience Cloud 솔루션에 영향을 줍니다. {#impact-in-experience-cloud-solutions}

일부 Adobe Experience Cloud 솔루션은 보고서를 생성할 때 높은 엔트로피 클라이언트 힌트에 포함된 정보를 사용합니다.

환경에서 높은 엔트로피 클라이언트 힌트를 활성화하지 않으면 아래에 설명된 Adobe Analytics 및 Audience Manager 보고서와 트레이트가 작동하지 않습니다.

### 높은 엔트로피 클라이언트 힌트를 사용하는 Adobe Analytics 보고서 {#analytics}

다음 [운영 체제](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) 차원은 높은 엔트로피 클라이언트 힌트로 저장된 운영 체제 버전을 포함합니다. 높은 엔트로피 클라이언트 힌트가 활성화되지 않으면 Chromium 브라우저에서 수집된 히트에 대해 운영 체제 버전이 부정확할 수 있습니다.

### 높은 엔트로피 클라이언트 힌트에 의존하는 Audience Manager 트레이트 {#aam}

Audience Manager 트레이트에서 다음 속성을 사용하는 경우 높은 엔트로피 클라이언트 힌트를 활성화해야 합니다. 그렇지 않으면 트레이트의 작동이 중지됩니다.

* 운영 체제 버전
* 디바이스 모델
* 장치 제조업체
* 장치 공급업체

## 높은 엔트로피 클라이언트 힌트 사용 {#enabling-high-entropy-client-hints}

웹 SDK 배포에서 높은 엔트로피 클라이언트 힌트를 활성화하려면 추가 항목을 포함해야 합니다 `highEntropyUserAgentHints` 컨텍스트 옵션이에 설명된 대로 [구성 설명서](configuring-the-sdk.md#context)기존 구성과 함께 사용됩니다.

예를 들어 웹 속성에서 높은 엔트로피 클라이언트 힌트를 검색하려면 구성은 다음과 같습니다.

`context: ["highEntropyUserAgentHints", "web"]`

## 예 {#example}

브라우저가 웹 서버에 대해 수행하는 첫 번째 요청의 헤더에 포함된 클라이언트 힌트에는 브라우저 브랜드, 브라우저의 주요 버전 및 클라이언트가 모바일 장치인지 여부에 대한 표시기가 포함됩니다. 각 데이터 조각은 하나의 [!DNL User-Agent] 문자열 를 참조하십시오.

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

동등한 [!DNL User-Agent] 동일한 브라우저의 헤더는 다음과 같습니다.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

정보가 유사하지만 서버에 대한 첫 번째 요청에는 클라이언트 힌트가 포함됩니다. 여기에는 [!DNL User-Agent] 문자열. 요청에서 누락된 항목은 운영 체제 아키텍처, 전체 운영 체제 버전, 레이아웃 엔진 이름, 레이아웃 엔진 버전 및 전체 브라우저 버전입니다.

그러나 후속 요청에서 [!DNL Client Hints API] 웹 서버에서 장치에 대한 추가 세부 정보를 요청할 수 있습니다. 이러한 값이 요청되면 브라우저 정책이나 사용자 설정에 따라 브라우저 응답에 해당 정보가 포함될 수 있습니다.

다음은 에서 반환하는 JSON 개체의 예입니다 [!DNL Client Hints API] 높은 엔트로피 값을 요청할 때:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
