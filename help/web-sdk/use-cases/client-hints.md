---
title: 사용자 에이전트 클라이언트 힌트
description: 사용자 에이전트 클라이언트 힌트가 Web SDK에서 작동하는 방식을 알아봅니다. 클라이언트 힌트를 사용하면 웹 사이트 소유자가 사용자 에이전트 문자열에서 사용할 수 있는 동일한 정보의 대부분에 액세스할 수 있지만 보다 개인정보 보호에 특화되었습니다.
keywords: 사용자 에이전트;클라이언트 힌트; 문자열; 사용자 에이전트 문자열; 낮은 엔트로피; 높은 엔트로피
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 3%

---

# 사용자 에이전트 클라이언트 힌트

## 개요 {#overview}

웹 브라우저가 웹 서버에 요청할 때마다 요청의 헤더에는 브라우저가 실행 중인 환경 및 브라우저에 대한 정보가 포함됩니다. 이 모든 데이터는 사용자 에이전트 문자열이라는 문자열로 집계됩니다.

다음은 [!DNL Mac OS] 장치에서 실행되는 Chrome 브라우저에서 받은 요청에서 사용자 에이전트 문자열의 모습입니다.

>[!NOTE]
>
>수년에 걸쳐 사용자 에이전트 문자열에 포함된 브라우저 및 장치 정보의 양이 여러 번 증가하고 수정되었습니다. 아래 예는 가장 일반적인 사용자 에이전트 정보를 선택한 것입니다.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 필드 | 값 |
|---|---|
| 소프트웨어 이름 | Chrome |
| 소프트웨어 버전 | 105 |
| 전체 소프트웨어 버전 | 105.0.0.0 |
| 레이아웃 엔진 이름 | AppleWebkit |
| 레이아웃 엔진 버전 | 537.36 |
| 운영 체제 | Mac |
| 운영 체제 버전 | 10.15.7 |
| 디바이스 | 인텔 Mac OS X 10_15_7 |

## 사용 사례 {#use-cases}

사용자 에이전트 문자열은 오랫동안 마케팅 및 개발 팀에게 브라우저, 운영 체제 및 디바이스에 사이트 콘텐츠가 표시되는 방식과 사용자가 웹 사이트와 상호 작용하는 방식에 대한 중요한 통찰력을 제공하는 데 사용되었습니다.

사용자 에이전트 문자열은 스팸을 차단하고 다양한 추가 목적을 위해 사이트를 크롤링하는 봇을 필터링하는 데에도 사용됩니다.

## Adobe Experience Cloud의 사용자 에이전트 문자열 {#user-agent-in-adobe}

Adobe Experience Cloud 솔루션은 다양한 방식으로 사용자 에이전트 문자열을 활용합니다.

* Adobe Analytics은 사용자 에이전트 문자열을 사용하여 웹 사이트를 방문하는 데 사용되는 운영 체제, 브라우저 및 장치와 관련된 추가 정보를 보강하고 파생합니다.
* Adobe Audience Manager 및 Adobe Target은 사용자 에이전트 문자열에서 제공한 정보를 기반으로 하여 최종 사용자에게 세그멘테이션 및 개인화 캠페인을 위한 자격을 부여합니다.

## 사용자 에이전트 클라이언트 힌트 소개 {#ua-ch}

최근 몇 년 동안 사이트 소유자와 마케팅 공급업체는 사용자 에이전트 문자열과 요청 헤더에 포함된 다른 정보를 사용하여 디지털 지문을 생성했습니다. 이러한 지문은 자신이 모르게 사용자를 식별하는 수단으로 활용될 수 있다.

사용자 에이전트 문자열이 사이트 소유자에게 제공하는 중요한 목적에도 불구하고 브라우저 개발자는 최종 사용자의 잠재적인 개인 정보 보호 문제를 제한하기 위해 사용자 에이전트 문자열의 작동 방식을 변경하기로 결정했습니다.

개발한 솔루션은 [사용자 에이전트 클라이언트 힌트](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)입니다. 클라이언트 힌트를 사용하면 웹 사이트에서 필요한 브라우저, 운영 체제 및 디바이스 정보를 수집하는 동시에 지문과 같은 은밀한 추적 방법에 대한 보호를 강화할 수 있습니다.

클라이언트 힌트를 사용하면 웹 사이트 소유자가 사용자 에이전트 문자열에서 사용할 수 있는 동일한 정보의 대부분에 액세스할 수 있지만 보다 개인정보 보호에 특화되었습니다.

최신 브라우저에서 사용자를 웹 서버로 보내면 필수 여부와 관계없이 모든 요청에 대해 전체 사용자 에이전트 문자열이 전송됩니다. 반면 클라이언트 힌트는 서버가 클라이언트에 대해 알고자 하는 추가 정보를 브라우저에 요청해야 하는 모델을 시행합니다. 이 요청을 수신하면 브라우저는 자체 정책 또는 사용자 구성을 적용하여 반환되는 데이터를 결정할 수 있습니다. 이제 모든 요청에 대해 기본적으로 전체 사용자 에이전트 문자열을 노출하는 대신 액세스가 명시적이고 감사 가능한 방식으로 관리됩니다.

## 브라우저 지원 {#browser-support}

[사용자 에이전트 클라이언트 힌트](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)이(가) [!DNL Google Chrome]버전 89과 함께 도입되었습니다.

추가 Chromium 기반 브라우저는 다음과 같은 클라이언트 힌트 API를 지원합니다.

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## 범주 {#categories}

사용자 에이전트 클라이언트 힌트에는 두 가지 범주가 있습니다.

* [낮은 엔트로피 클라이언트 힌트](#low-entropy)
* [높은 엔트로피 클라이언트 힌트](#high-entropy)

### 낮은 엔트로피 클라이언트 힌트 {#low-entropy}

낮은 엔트로피 클라이언트 힌트에는 사용자를 지문화하는 데 사용할 수 없는 기본 정보가 포함되어 있습니다. 브라우저 브랜드, 플랫폼 및 모바일 디바이스에서 요청이 오는지 여부 등의 정보입니다.

낮은 엔트로피 클라이언트 힌트는 Web SDK에서 기본적으로 활성화되어 있으며 모든 요청에서 전달됩니다.

| HTTP 헤더 | JavaScript | 기본적으로 사용자 에이전트에 포함됨 | 기본적으로 클라이언트 힌트에 포함됨 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 예 | 예 |
| `Sec-CH-UA-Platform` | `platform` | 예 | 예 |
| `Sec-CH-UA-Mobile` | `mobile` | 예 | 예 |

### 높은 엔트로피 클라이언트 힌트 {#high-entropy}

높은 엔트로피 클라이언트 힌트는 플랫폼 버전, 아키텍처, 모델, 비트(64비트 또는 32비트 플랫폼) 또는 전체 운영 체제 버전과 같은 클라이언트 디바이스에 대한 보다 자세한 정보입니다. 이 정보는 잠재적으로 지문 검사에 사용될 수 있습니다.

| 속성 | 설명 | HTTP 헤더 | XDM 경로 | 예 | 기본적으로 사용자 에이전트에 포함됨 | 기본적으로 클라이언트 힌트에 포함됨 |
| --- | --- | --- | --- | --- |---|---|
| 운영 체제 버전 | 운영 체제의 버전입니다. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | 예 | 아니요 |
| 아키텍처 | 기본 CPU 아키텍처. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | 예 | 아니요 |
| 장치 모델 | 사용된 디바이스의 이름입니다. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | 예 | 아니요 |
| 비트니스 | 기본 CPU 아키텍처가 지원하는 비트 수입니다. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | 예 | 아니요 |
| 브라우저 공급업체 | 브라우저를 만든 회사입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | 예 | 아니요 |
| 브라우저 이름 | 사용된 브라우저입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | 예 | 아니요 |
| 브라우저 버전 | 브라우저의 중요 버전입니다. 낮은 엔트로피 힌트 `Sec-CH-UA`도 이 요소를 수집합니다. 정확한 브라우저 버전은 자동으로 수집되지 않습니다. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | 예 | 아니요 |


높은 엔트로피 클라이언트 힌트는 Web SDK에서 기본적으로 비활성화되어 있습니다. 이를 활성화하려면 높은 엔트로피 클라이언트 힌트를 요청하도록 Web SDK를 수동으로 구성해야 합니다.

## 높은 엔트로피 클라이언트 힌트는 Experience Cloud 솔루션에 영향을 미칩니다. {#impact-in-experience-cloud-solutions}

일부 Adobe Experience Cloud 솔루션은 보고서를 생성할 때 높은 엔트로피 클라이언트 힌트에 포함된 정보를 사용합니다.

사용자 환경에서 높은 엔트로피 클라이언트 힌트를 활성화하지 않으면 아래에 설명된 Adobe Analytics 및 Audience Manager 보고서와 트레이트가 작동하지 않습니다.

### Adobe Analytics은 높은 엔트로피 클라이언트 힌트에 의존하여 보고서를 보고합니다 {#analytics}

[운영 체제](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) 차원에는 높은 엔트로피 클라이언트 힌트로 저장된 운영 체제 버전이 포함되어 있습니다. 높은 엔트로피 클라이언트 힌트가 활성화되지 않으면 Chromium 브라우저에서 수집한 히트에 대해 운영 체제 버전이 정확하지 않을 수 있습니다.

### 높은 엔트로피 클라이언트 힌트에 의존하는 Audience Manager 트레이트 {#aam}

[!DNL Google]이(가) `User-Agent` 헤더를 통해 수집된 정보를 최소화하도록 [!DNL Chrome] 브라우저 기능을 업데이트했습니다. 따라서 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=ko-KR)을 사용하는 Audience Manager 고객은 더 이상 [플랫폼 수준 키](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html)를 기반으로 하는 트레이트에 대한 신뢰할 수 있는 정보를 받지 못하게 됩니다.

타깃팅에 플랫폼 수준 키를 사용하는 Audience Manager 고객은 [Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=ko-KR) 대신 [DIL Web SDK](/help/web-sdk/home.md)(으)로 전환하고 [높은 엔트로피 클라이언트 힌트](#enabling-high-entropy-client-hints)를 활성화하여 신뢰할 수 있는 트레이트 데이터를 계속 받아야 합니다.

## 높은 엔트로피 클라이언트 힌트 활성화 {#enabling-high-entropy-client-hints}

웹 SDK 배포에서 높은 엔트로피 클라이언트 힌트를 활성화하려면 [`context`](/help/web-sdk/commands/configure/context.md) 필드에 추가 `highEntropyUserAgentHints` 컨텍스트 옵션을 포함해야 합니다.

예를 들어 웹 속성에서 높은 엔트로피 클라이언트 힌트를 검색하려면 다음과 같이 구성하십시오.

`context: ["highEntropyUserAgentHints", "web"]`

## 예 {#example}

브라우저가 웹 서버에 보낸 첫 번째 요청의 헤더에 포함된 클라이언트 힌트에는 브라우저 브랜드, 브라우저의 주요 버전 및 클라이언트가 모바일 디바이스인지 여부에 대한 표시기가 포함됩니다. 각 데이터 조각은 아래와 같이 단일 사용자 에이전트 문자열로 그룹화되지 않고 고유한 헤더 값을 갖습니다.

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

동일한 브라우저의 해당 [!DNL User-Agent] 헤더는 다음과 같습니다.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

정보는 유사하지만 서버에 대한 첫 번째 요청에는 클라이언트 힌트가 포함되어 있습니다. 사용자 에이전트 문자열에서 사용할 수 있는 항목의 하위 집합만 포함됩니다. 요청에서 누락된 사항은 운영 체제 아키텍처, 전체 운영 체제 버전, 레이아웃 엔진 이름, 레이아웃 엔진 버전 및 전체 브라우저 버전입니다.

그러나 후속 요청에서 [!DNL Client Hints API]을(를) 사용하면 웹 서버에서 장치에 대한 추가 정보를 요청할 수 있습니다. 이러한 값이 요청되면 브라우저 정책 또는 사용자 설정에 따라 브라우저 응답에 해당 정보가 포함될 수 있습니다.

다음은 높은 엔트로피 값이 요청될 때 [!DNL Client Hints API]에서 반환되는 JSON 개체의 예입니다.


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
