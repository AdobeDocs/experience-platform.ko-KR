---
title: 웹 SDK 및 Edge Network API를 사용한 하이브리드 개인화
description: 이 문서에서는 웹 SDK과 Edge Network API를 함께 사용하여 웹 속성에 하이브리드 개인화를 배포하는 방법을 보여 줍니다.
keywords: 개인화, 하이브리드, 서버 api, 서버측, 하이브리드 구현,
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 7b91f4f486db67d4673877477a6be8287693533a
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# 웹 SDK 및 Edge Network API를 사용한 하이브리드 개인화

## 개요 {#overview}

Hybdrid 개인화는 개인화 콘텐츠 서버측을 검색하고, [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)를 사용하고, [Web SDK](../home.md)를 사용하여 클라이언트측을 렌더링하는 프로세스를 설명합니다.

Adobe Target, Adobe Journey Optimizer 또는 Offer Decisioning과 같은 개인화 솔루션에서 하이브리드 개인화를 사용할 수 있습니다. 차이점은 [!UICONTROL Edge Network API] 페이로드의 콘텐츠입니다.

## 전제 조건 {#prerequisites}

웹 속성에 하이브리드 개인화를 구현하기 전에 다음 조건을 충족하는지 확인하십시오.

* 사용할 개인화 솔루션을 결정했습니다. [!UICONTROL Edge Network API] 페이로드의 콘텐츠에 영향을 미칩니다.
* [!UICONTROL Edge Network API]를 호출하는 데 사용할 수 있는 응용 프로그램 서버에 액세스할 수 있습니다.
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)에 액세스할 수 있습니다.
* 개인화할 페이지에 웹 SDK을 올바르게 [구성](/help/web-sdk/commands/configure/overview.md)하고 배포했습니다.

## 흐름 다이어그램 {#flow-diagram}

아래 흐름 다이어그램은 하이브리드 개인화를 제공하기 위해 취한 단계 순서를 설명합니다.

![하이브리드 개인 설정을 제공하는 데 필요한 단계 순서를 보여 주는 시각적 흐름 다이어그램입니다.](assets/hybrid-personalization-diagram.png)

1. 브라우저에서 이전에 저장한 기존 쿠키(접두사가 `kndctr_`인)는 브라우저 요청에 포함됩니다.
1. 클라이언트 웹 브라우저는 애플리케이션 서버에서 웹 페이지를 요청합니다.
1. 응용 프로그램 서버가 페이지 요청을 받으면 [Edge Network API 대화형 데이터 수집 끝점](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)에 `POST` 요청을 하여 개인화 콘텐츠를 가져옵니다. `POST` 요청에 `event` 및 `query`이(가) 포함되어 있습니다. 사용 가능한 경우 이전 단계의 쿠키가 `meta>state>entries` 배열에 포함됩니다.
1. Edge Network API는 개인화 콘텐츠를 애플리케이션 서버에 반환합니다.
1. 응용 프로그램 서버가 클라이언트 브라우저에 [ID 및 클러스터 쿠키](#cookies)를 포함하는 HTML 응답을 반환합니다.
1. 클라이언트 페이지에서 [!DNL Web SDK] `applyResponse` 명령이 호출되어 이전 단계의 [!UICONTROL Edge Network API] 응답의 헤더와 본문을 전달합니다.
1. `renderDecisions` 플래그가 `true`(으)로 설정되어 있으므로 [!DNL Web SDK]에서 Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 오퍼 및 Journey Optimizer 웹 채널 항목을 자동으로 렌더링합니다.
1. Target 양식 기반 [!DNL HTML]/[!DNL JSON] 오퍼 및 Journey Optimizer 코드 기반 경험은 `applyProposition` 메서드를 통해 수동으로 적용되어 제안의 개인화 콘텐츠를 기반으로 [!DNL DOM]을(를) 업데이트합니다.
1. Target 양식 기반 [!DNL HTML]/[!DNL JSON] 오퍼 및 Journey Optimizer 코드 기반 경험의 경우 반환된 콘텐츠가 표시된 시기를 나타내기 위해 표시 이벤트를 수동으로 보내야 합니다. 이 작업은 `sendEvent` 명령을 통해 수행됩니다.

## 쿠키 {#cookies}

쿠키는 사용자 ID 및 클러스터 정보를 유지하는 데 사용됩니다.  하이브리드 구현을 사용하는 경우 웹 애플리케이션 서버는 요청 라이프사이클 동안 이러한 쿠키의 저장 및 전송을 처리합니다.

| Cookie | 용도 | 저장 주체 | 보낸 사람 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 사용자 ID 세부 사항을 포함합니다. | 애플리케이션 서버 | 애플리케이션 서버 |
| `kndctr_AdobeOrg_cluster` | 요청을 이행하는 데 사용해야 하는 Edge Network 클러스터를 나타냅니다. | 애플리케이션 서버 | 애플리케이션 서버 |

## 배치 요청 {#request-placement}

제안을 가져오고 디스플레이 알림을 보내려면 Edge Network API 요청이 필요합니다. 하이브리드 구현을 사용하는 경우 애플리케이션 서버는 Edge Network API에 이러한 요청을 수행합니다.

| 요청 | 만든 사람 |
|---|---|
| 제안 검색에 대한 상호 작용 요청 | 애플리케이션 서버 |
| 디스플레이 알림 전송을 위한 상호 작용 요청 | 애플리케이션 서버 |


## Edge Network 지역 호스트 설정 {#regional-host}

Edge Network 지역 호스트를 설정하려면 먼저 `kndctr_<orgId>_AdobeOrg_cluster` 쿠키에서 다음 값을 가질 수 있는 위치 힌트를 읽습니다.

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

예: `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

Edge Network 지역 호스트는 `<location_hint>.server.adobedc.net` 형식을 사용하며 다음 값을 가질 수 있습니다.

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

이러한 특정 호스트를 사용하면 요청이 이전에 사용자가 방문했던 동일한 Edge Network 위치로 이동하며, 사용자 데이터가 해당 호스트에 있으므로 시스템에서 최상의 경험을 제공할 수 있습니다.

위치 힌트(즉, 쿠키 없음)가 없으면 기본 호스트 `server.adobedc.net`을(를) 사용합니다.

>[!TIP]
>
>가장 좋은 방법은 허용된 위치 목록을 사용하는 것입니다. 이렇게 하면 클라이언트측 쿠키를 통해 제공되므로 위치 힌트가 로 강화되지 않습니다.

## Analytics 영향 {#analytics}

하이브리드 개인화를 구현할 때에는 Analytics에서 페이지 히트가 여러 번 계산되지 않도록 특별히 주의해야 합니다.

Analytics에 대해 [데이터 스트림을 구성](../../datastreams/overview.md)하면 페이지 히트가 캡처되도록 이벤트가 자동으로 전달됩니다.

이 구현의 샘플은 두 개의 서로 다른 데이터 스트림을 사용합니다.

* Analytics에 대해 구성된 데이터 스트림입니다. 이 데이터 스트림은 웹 SDK 상호 작용에 사용됩니다.
* Analytics 구성이 없는 두 번째 데이터 스트림입니다. 이 데이터 스트림은 Edge Network API 요청에 사용됩니다. Analytics에 대해 구성한 데이터 스트림과 동일한 대상 구성으로 이 데이터 스트림을 구성해야 합니다.

이렇게 하면 서버측 요청은 Analytics 이벤트를 등록하지 않지만 클라이언트측 요청은 등록합니다. 이렇게 하면 Analytics 요청이 정확하게 계산됩니다.

## 서버측 요청 빌드 {#server-side-request}

아래 샘플 요청은 애플리케이션 서버가 개인화 콘텐츠를 검색하는 데 사용할 수 있는 Edge Network API 요청을 보여 줍니다.

>[!IMPORTANT]
>
>이 샘플 요청은 Adobe Target을 개인화 솔루션으로 사용합니다. 요청은 선택한 개인화 솔루션에 따라 달라질 수 있습니다.


**API 형식**

```http
POST /ee/v2/interact
```

### 요청 {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예. | Edge Network에 상호 작용을 전달하는 데 사용하는 데이터 스트림의 ID입니다. 데이터 스트림을 구성하는 방법을 알아보려면 [데이터 스트림 개요](../../datastreams/overview.md)를 참조하세요. |
| `requestId` | `String` | 아니요 | 내부 서버 요청의 상관 관계를 나타내는 임의의 ID입니다. 아무 것도 제공되지 않으면 Edge Network이 하나를 생성하고 응답에서 반환합니다. |

### 프록시 헤더 {#proxy-headers}

요청을 올바르게 처리하려면 다음 헤더가 필요합니다.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

이러한 항목이 실제 클라이언트 정보를 가리키도록 올바르게 설정되었는지 확인하십시오. 예를 들어 `X-Forwarded-For` 헤더에는 적절한 지리적 위치를 사용하려면 클라이언트 IP가 포함되어야 합니다.

### 사용자 에이전트 헤더 {#user-agent-headers}

요청을 올바르게 처리하려면 다음 사용자 에이전트 헤더를 사용하십시오.

**기본값**

* `User-Agent`

**낮은 엔트로피(필수):**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**높은 엔트로피(선택 사항):**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

[Edge Network API 사양](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)에 표시된 대로 요청을 보내야 합니다. 사용 사례에 필요한 경우 [개인화 설명서](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/)를 참조하세요.

### 서버측 응답 {#server-response}

Edge Network 응답에는 `Set-Cookie` 헤더에서 변환해야 하는 `state:store` 명령이 포함됩니다. 브라우저에 저장되고 웹 SDK 구현에서 사용할 수 있습니다.

쿠키는 클라이언트 쿠키뿐만 아니라 서버 구현에 대한 요청과 함께 전송되도록 최상위 도메인에서 설정해야 합니다. (또는 적어도 두 구현에서 모두 사용하는 공통 하위 도메인)

예:

* 서버측 호출에서 `api.example.com` 사용
* 클라이언트측 호출은 `adobe.example.com` 사용

쿠키가 두 경우에 공유되도록 `.example.com`에 설정해야 합니다.

서버측 응답은 데이터 스트림 구성에 따라 생성된 `Handles`(이)라는 조각으로 구성됩니다. 예를 들어 실시간 개인화 엔진은 `personalization:decisions`개의 핸들을 반환하지만 실시간 활성화 엔진은 `activation:pull`개의 핸들을 생성합니다.

아래 샘플 응답은 Edge Network API 응답의 모양을 보여줍니다.

```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```



## 클라이언트측 요청 {#client-request}

클라이언트 페이지에서 [!DNL Web SDK] `applyResponse` 명령이 호출되어 서버측 응답의 헤더와 본문을 전달합니다.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

양식 기반 [!DNL JSON] 오퍼는 `applyPersonalization` 메서드를 통해 수동으로 적용되어 개인화 오퍼에 따라 [!DNL DOM]을(를) 업데이트합니다. 양식 기반 활동의 경우 오퍼가 표시된 시기를 나타내기 위해 표시 이벤트를 수동으로 보내야 합니다. 이 작업은 `sendEvent` 명령을 통해 수행됩니다.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## 샘플 애플리케이션 {#sample-app}

이 유형의 개인화를 실험하고 자세히 알아볼 수 있도록 다운로드하여 테스트에 사용할 수 있는 샘플 애플리케이션을 제공합니다. 이 [GitHub 저장소](https://github.com/adobe/alloy-samples)에서 응용 프로그램을 사용하는 방법에 대한 자세한 지침과 함께 다운로드할 수 있습니다.
