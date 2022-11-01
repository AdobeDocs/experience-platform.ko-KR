---
title: 웹 SDK 및 Edge Network Server API를 사용한 하이브리드 개인화
description: 이 문서에서는 서버 API와 함께 웹 SDK를 사용하여 웹 속성에 하이브리드 개인화를 배포하는 방법을 보여줍니다.
keywords: 개인화; hybrid; 서버 api; 서버측; 하이브리드 구현;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# 웹 SDK 및 Edge Network Server API를 사용한 하이브리드 개인화

## 개요 {#overview}

하이브리드 개인화는 다음을 사용하여 개인화 콘텐츠 서버측을 검색하는 프로세스를 설명합니다 [Edge Network Server API](../..//server-api/overview.md)를 사용하여 클라이언트 측에서 렌더링하고 [웹 SDK](../home.md).

Adobe Target 또는 Offer decisioning과 같은 개인화 솔루션을 사용하여 하이브리드 개인화를 사용할 수 있습니다. 차이점은 다음과 같습니다 [!UICONTROL 서버 API] 페이로드.

## 전제 조건 {#prerequisites}

웹 속성에서 하이브리드 개인화를 구현하려면 먼저 다음 조건을 충족하는지 확인하십시오.

* 사용할 개인화 솔루션을 결정했습니다. 이렇게 하면 의 내용에 영향을 줍니다 [!UICONTROL 서버 API] 페이로드.
* 응용 프로그램 서버에 액세스할 수 있습니다. 응용 프로그램 서버는 [!UICONTROL 서버 API] 호출.
* 에 액세스할 수 있습니다 [Edge Network Server API](../../server-api/authentication.md).
* 네 말이 맞다 [구성 및 배포](../fundamentals/configuring-the-sdk.md) 개인화할 페이지의 Web SDK.

## 흐름 다이어그램 {#flow-diagram}

아래 흐름 다이어그램은 하이브리드 개인화를 제공하기 위해 수행되는 단계의 순서에 대해 설명합니다.

![하이브리드 개인화를 전달하는 데 필요한 단계의 순서를 보여주는 시각적 흐름 다이어그램입니다.](assets/hybrid-personalization-diagram.png)

1. 브라우저에 의해 이전에 저장된 모든 기존 쿠키, `kndctr_`은 브라우저 요청에 포함됩니다.
1. 클라이언트 웹 브라우저가 애플리케이션 서버에서 웹 페이지를 요청합니다.
1. 애플리케이션 서버가 페이지 요청을 받으면 다음을 수행합니다 `POST` 에 요청 [서버 API 대화형 데이터 수집 끝점](../../server-api/interactive-data-collection.md) 개인화 콘텐츠를 가져오려면 다음을 수행하십시오. 다음 `POST` 요청에 가 포함되어 있습니다. `event` 그리고 `query`. 사용 가능한 경우 이전 단계의 쿠키가 `meta>state>entries` 배열입니다.
1. 서버 API는 애플리케이션 서버에 개인화 콘텐츠를 반환합니다.
1. 애플리케이션 서버는 클라이언트 브라우저에 대한 HTML 응답을 반환하며, [id 및 클러스터 쿠키](#cookies).
1. 클라이언트 페이지에서 [!DNL Web SDK] `applyResponse` 명령이 호출되고, [!UICONTROL 서버 API] 이전 단계의 응답입니다.
1. 다음 [!DNL Web SDK] 페이지 로드 렌더링 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 이 자동으로 제공되는 이유는 `renderDecisions` 플래그가 로 설정되어 있습니다. `true`.
1. 양식 기반 [!DNL JSON] 오퍼는 를 통해 수동으로 적용됩니다. `applyPersonalization` 메서드, [!DNL DOM] 개인화 오퍼를 기반으로 합니다.
1. 양식 기반 활동의 경우, 오퍼가 표시된 시기를 나타내려면 디스플레이 이벤트를 수동으로 보내야 합니다. 이 작업은 를 통해 수행됩니다 `sendEvent` 명령.

## 쿠키 {#cookies}

쿠키는 사용자 ID 및 클러스터 정보를 유지하는 데 사용됩니다.  하이브리드 구현을 사용하는 경우 웹 애플리케이션 서버는 요청 라이프사이클 동안 이러한 쿠키의 저장 및 전송을 처리합니다.

| Cookie | 용도 | 저장 기준 | 보낸 사람 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 사용자 ID 세부 사항을 포함합니다. | 애플리케이션 서버 | 애플리케이션 서버 |
| `kndctr_AdobeOrg_cluster` | 요청을 이행하는 데 사용해야 하는 에지 네트워크 클러스터를 나타냅니다. | 애플리케이션 서버 | 애플리케이션 서버 |

## 배치 요청 {#request-placement}

제안을 가져오고 디스플레이 알림을 전송하려면 서버 API 요청이 필요합니다. 하이브리드 구현을 사용할 때 애플리케이션 서버는 서버 API에 이러한 요청을 수행합니다.

| 요청 | 작성자 |
|---|---|
| 상호 작용하여 proposition 검색 | 애플리케이션 서버 |
| 상호 작용 요청으로 디스플레이 알림 보내기 | 애플리케이션 서버 |

## Analytics 의미 {#analytics}

하이브리드 개인화를 구현할 때 Analytics에서 페이지 히트가 여러 번 계산되지 않도록 특별한 주의를 기울여야 합니다.

다음 경우에 [데이터 스트림 구성](../datastreams/overview.md) Analytics의 경우 페이지 히트가 캡처되도록 이벤트가 자동으로 전달됩니다.

이 구현의 샘플은 두 개의 서로 다른 데이터 세트를 사용합니다.

* Analytics용으로 구성된 데이터 스트림. 이 데이터 스트림은 웹 SDK 상호 작용에 사용됩니다.
* Analytics 구성이 없는 두 번째 데이터 스트림. 이 데이터 스트림은 서버 API 요청에 사용됩니다.

이 방법을 통해 서버측 요청은 Analytics 이벤트를 등록하지 않지만 클라이언트측 요청은 등록됩니다. 이로 인해 Analytics 요청이 정확하게 카운트됩니다.


## 서버측 요청 {#server-side-request}

아래 샘플 요청은 애플리케이션 서버가 개인화 컨텐츠를 검색하는 데 사용할 수 있는 서버 API 요청을 보여줍니다.

>[!IMPORTANT]
>
>이 샘플 요청에서는 Adobe Target 을 개인화 솔루션으로 사용합니다. 요청은 선택한 개인화 솔루션에 따라 달라질 수 있습니다.


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
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| 매개 변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 예. | Edge 네트워크에 상호 작용을 전달하는 데 사용하는 데이터 스트림의 ID입니다. 자세한 내용은 [데이터 세트 개요](../datastreams/overview.md) 데이터 스트림을 구성하는 방법을 알아봅니다. |
| `requestId` | `String` | 아니요 | 내부 서버 요청과 상관 관계가 있는 임의 ID입니다. 아무 것도 제공되지 않으면 에지 네트워크에서 하나를 생성하여 응답으로 반환합니다. |

### 서버측 응답 {#server-response}

아래 샘플 응답에는 서버 API 응답이 어떤 모습일지 보여 줍니다.


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

클라이언트 페이지에서 [!DNL Web SDK] `applyResponse` 명령이 호출되고 서버측 응답의 헤더 및 본문을 전달합니다.

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

양식 기반 [!DNL JSON] 오퍼는 를 통해 수동으로 적용됩니다. `applyPersonalization` 메서드, [!DNL DOM] 개인화 오퍼를 기반으로 합니다. 양식 기반 활동의 경우, 오퍼가 표시된 시기를 나타내려면 디스플레이 이벤트를 수동으로 보내야 합니다. 이 작업은 를 통해 수행됩니다 `sendEvent` 명령.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## 샘플 애플리케이션 {#sample-app}

이러한 유형의 개인화를 실험하고 자세히 학습하는 데 도움이 되도록 Adobe에서는 테스트를 위해 다운로드하여 사용할 수 있는 샘플 애플리케이션을 제공합니다. 응용 프로그램 사용 방법에 대한 자세한 지침과 함께 이 응용 프로그램을 다운로드할 수 있습니다 [GitHub 리포지토리](https://github.com/adobe/alloy-samples).






