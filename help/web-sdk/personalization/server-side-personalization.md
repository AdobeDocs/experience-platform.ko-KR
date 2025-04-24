---
title: Edge Network API를 사용한 서버측 개인화
description: 이 문서에서는 Edge Network API를 사용하여 웹 속성에 서버측 개인화를 배포하는 방법을 보여 줍니다.
keywords: 개인화, 서버 api, edge network, 서버측
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 2%

---


# Edge Network API를 사용한 서버측 개인화

## 개요 {#overview}

서버측 개인화에는 [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/)를 사용하여 웹 자산에서 고객 경험을 개인화하는 작업이 포함됩니다.

이 문서에 설명된 예에서 개인화 콘텐츠는 Edge Network API를 사용하여 서버측에서 검색됩니다. 그러면 HTML이 검색된 개인화 콘텐츠를 기반으로 서버측에서 렌더링됩니다.

아래 표는 개인화된 컨텐츠와 개인화되지 않은 컨텐츠의 예를 보여 줍니다.

| 개인화가 없는 샘플 페이지 | 개인화가 포함된 샘플 페이지 |
|---|---|
| ![개인 설정이 없는 웹 페이지 예](assets/plain.png) | ![개인 맞춤화가 있는 웹 페이지 예제](assets/personalized.png) |

## 고려 사항 {#considerations}

### 쿠키 {#cookies}

쿠키는 사용자 ID 및 클러스터 정보를 유지하는 데 사용됩니다.  서버측 구현을 사용하는 경우 애플리케이션 서버는 요청 라이프사이클 동안 이러한 쿠키의 저장과 전송을 처리합니다.

| Cookie | 용도 | 저장 주체 | 보낸 사람 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 사용자 ID 세부 사항을 포함합니다. | 애플리케이션 서버 | 애플리케이션 서버 |
| `kndctr_AdobeOrg_cluster` | 요청을 이행하는 데 사용해야 하는 Edge Network 클러스터를 나타냅니다. | 애플리케이션 서버 | 애플리케이션 서버 |

### 배치 요청 {#request-placement}

제안을 가져오고 디스플레이 알림을 보내려면 Personalization 요청이 필요합니다. 서버측 구현을 사용하는 경우 애플리케이션 서버는 Edge Network API에 이러한 요청을 수행합니다.

| 요청 | 만든 사람 |
|---|---|
| 제안 검색에 대한 상호 작용 요청 | Edge Network API를 호출하는 애플리케이션 서버입니다. |
| 디스플레이 알림 전송을 위한 상호 작용 요청 | Edge Network API를 호출하는 애플리케이션 서버입니다. |

## 샘플 애플리케이션 {#sample-app}

아래 설명된 프로세스는 이 유형의 개인화를 실험하고 자세히 알아보기 위한 시작점으로 사용할 수 있는 샘플 애플리케이션을 사용합니다.

이 샘플을 다운로드하고 원하는 대로 사용자 지정할 수 있습니다. 예를 들어 샘플 앱이 자체 Experience Platform 구성에서 오퍼를 가져오도록 환경 변수를 변경할 수 있습니다.

이렇게 하려면 저장소의 루트에서 `.env` 파일을 열고 구성에 따라 변수를 수정합니다. 샘플 앱을 다시 시작하면 나만의 개인화 콘텐츠를 사용하여 실험할 준비가 된 것입니다.

### 샘플 실행 {#running-sample}

샘플 앱을 실행하려면 아래 단계를 따르십시오.

1. 로컬 컴퓨터에 [이 저장소](https://github.com/adobe/alloy-samples)를 복제합니다.
2. 터미널을 열고 `personalization-server-side` 폴더로 이동합니다.
3. `npm install` 실행.
4. `npm start` 실행.
5. 웹 브라우저를 열고 `http://localhost`(으)로 이동합니다.

## 프로세스 개요 {#process}

이 섹션에서는 개인화 콘텐츠를 검색하는 데 사용되는 단계를 설명합니다.

1. [Express](https://expressjs.com/)은(는) 린 서버측 구현에 사용됩니다. 기본 서버 요청 및 라우팅을 처리합니다.
2. 브라우저가 웹 페이지를 요청합니다. 브라우저에서 이전에 저장한 쿠키(`kndctr_` 접두사)가 포함됩니다.
3. 앱 서버에서 페이지를 요청하면 [대화형 데이터 수집 끝점](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)으로 이벤트를 전송하여 개인화 콘텐츠를 가져옵니다. 샘플 앱은 도우미 메서드를 사용하여 API에 대한 요청 빌드 및 전송을 단순화합니다([aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js) 참조). `POST` 요청에 `event` 및 `query`이(가) 포함되어 있습니다. 사용 가능한 경우 이전 단계의 쿠키가 `meta>state>entries` 배열에 포함됩니다.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. 양식 기반 활동의 Target 오퍼를 응답에서 읽고 HTML 응답을 생성할 때 사용합니다.
5. 양식 기반 활동의 경우 오퍼가 표시된 시기를 나타내기 위해 표시 이벤트를 구현에서 수동으로 보내야 합니다. 이 예에서 알림은 요청 라이프사이클 동안 서버측에서 전송됩니다.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)]개의 오퍼는 웹 SDK을 통해서만 렌더링할 수 있으므로 무시됩니다.
7. HTML 응답이 반환되면 ID 및 클러스터 쿠키가 애플리케이션 서버에 의한 응답에 설정됩니다.