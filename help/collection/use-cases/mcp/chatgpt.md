---
title: ChatGPT 앱에서 분석 수집 및 개인화 적용(MCP 데이터 수집)
description: 하이브리드 MCP 서버 + 웹 SDK applyResponse 패턴을 사용하여 Adobe Experience Platform Edge Network으로 이벤트를 전송하고 ChatGPT 앱 UI 내에서 개인화를 렌더링합니다.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, ChatGPT 앱, applyResponse, interact 엔드포인트, 개인화, 분석
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# ChatGPT 앱에서 분석 수집 및 개인화 적용(MCP 데이터 수집)

이 사용 사례에서는 ChatGPT 앱(Model Context Protocol 서버 + 선택적 UI 구성 요소)을 Adobe Experience Platform Edge Network에 연결하는 방법을 보여 줍니다. 이 유형의 데이터 수집을 사용하면 도구를 호출하는 대화 상호 작용에 대한 분석을 기록하고 Edge Network의 개인화 결정을 ChatGPT에서 렌더링된 위젯으로 전달할 수 있습니다.

>[!NOTE]
>
>이 문서는 Adobe 데이터 수집 팀의 최신 업데이트와 OpenAI의 최신 기술 업데이트를 기반으로 유지 관리됩니다. 따라서 Adobe은 이 문서가 시간이 지남에 따라 발전할 것으로 예상하며 업데이트를 다시 확인하는 것이 좋습니다.

이 사용 사례에서는 데이터 수집을 위한 서버측 구현과 개인화된 콘텐츠를 렌더링하기 위한 클라이언트측 구현을 모두 사용하여 하이브리드 접근 방식을 선호합니다. MCP 도구 호출이 분석을 수집하는 가장 신뢰할 수 있는 순간이므로 이 접근 방식이 이상적입니다. 위젯은 브라우저 컨텍스트에서 실행되며 ID(쿠키에)를 저장하고 개인화 결정을 적용할 수 있는 올바른 위치입니다.

이 사용 사례에는 완전한 작동 코드 예제가 포함되어 있습니다. 샘플 코드 및 구현 지침은 GitHub의 [ 리포지토리에서 ](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app)ChatGPT 앱 + Adobe Experience Platform Edge`alloy-samples`을(를) 참조하십시오.

>[!IMPORTANT]
>
>이 페이지에서는 통합 패턴을 설명하기 위한 참조 구현에 대해 간략하게 설명합니다. 애플리케이션에서 접근 방식을 채택하기 전에 보안, 개인 정보, 동의 및 프로덕션 요구 사항을 검토하십시오.

## 아키텍처

높은 수준에서, 5개의 움직이는 부품이 있습니다.

1. **MCP 호스트(ChatGPT)**: ChatGPT는 MCP 서버에서 노출된 도구를 호출하고 요청 메타데이터에 안정적인 익명 사용자 식별자를 제공합니다.
1. **MCP 서버(백 엔드)**: 조직이 소유합니다. 항목 나열, 세부 정보 가져오기 또는 요청 제출과 같은 도구를 구현합니다.
1. **Adobe IMS**: MCP 서버에서 Adobe 데이터 수집 API를 호출하는 데 사용하는 액세스 토큰을 발급합니다.
1. **Adobe Experience Platform Edge Network**: MCP 서버에서 보낸 경험 이벤트를 수신하고 분석 승인, 상태 업데이트(예: ID) 및 개인화 결정을 반환합니다.
1. **임베드된 웹 UI(MCP 호스트에서 렌더링된 프론트엔드 위젯)**: 구조화된 결과를 표시하고 MCP 서버 백엔드에서 받은 Adobe 메타데이터를 적용합니다.

## 데이터 흐름

1. **사용자**&#x200B;이(가) MCP 서버를 사용하여 **ChatGPT**&#x200B;에 메시지를 표시합니다.
1. **ChatGPT**&#x200B;은(는) 프롬프트의 의도를 해석하고 적절한 **백엔드 MCP 도구**&#x200B;를 호출합니다.
1. **백엔드 MCP 서버**&#x200B;는 데이터 수집 API(`interact` 끝점)를 사용하여 분석 수집 및 선택적 개인화를 위해 경험 이벤트를 **Edge Network**&#x200B;에 보냅니다.
1. **Edge Network**&#x200B;이(가) 상태 업데이트 및 개인화 결정을 포함한 응답 핸들을 **백엔드 MCP 도구**&#x200B;에 반환합니다.
1. **백엔드 MCP 도구**&#x200B;이(가) `structuredContent`의 비즈니스 데이터와 `_meta`의 Adobe 메타데이터가 포함된 도구 결과를 **ChatGPT**&#x200B;에 반환합니다.
1. **ChatGPT**&#x200B;은(는) 도구 결과를 **프론트엔드 위젯**&#x200B;에 전달합니다. 이 위젯은 Web SDK JavaScript 라이브러리의 `applyResponse` 명령을 사용하여 비즈니스 데이터를 렌더링하고 Adobe 메타데이터를 적용합니다. 이 명령은 클라이언트측 상태를 하이드레이션하고 UI에서 적격한 개인화 결정을 렌더링합니다.

다음 섹션에서는 각 단계에 대해 자세히 설명합니다.

## 1단계: 사용자가 MCP 서버를 사용하여 ChatGPT에 프롬프트

이 단계는 워크플로의 진입점입니다. 사용자는 다음과 같은 자연어 의도를 제공합니다.

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

자세한 내용은 OpenAI 개발자 설명서에서 [MCP 서버 구축](https://developers.openai.com/apps-sdk/build/mcp-server/)을 참조하십시오.

## 2단계: ChatGPT는 의도를 해석하고 MCP 도구를 호출합니다.

ChatGPT는 MCP 서버의 메타데이터를 기반으로 의도를 해석하고 MCP 서버에서 적절한 도구 핸들러를 호출합니다. 이 도구 호출은 UI 렌더링 성공과 무관한 상호 작용에 대한 서버측 참 지점을 만듭니다. 도구 중 하나에 다음 메타데이터가 있을 수 있습니다.

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

각 MCP 도구가 수행하는 작업을 ChatGPT에 알리는 방법에 대한 자세한 내용은 OpenAI 개발자 설명서에서 [도구 정의](https://developers.openai.com/apps-sdk/plan/tools/)를 참조하십시오.

## 3단계: MCP 서버가 경험 이벤트를 Edge Network에 전송

MCP 서버가 요청을 수신하면 분석 데이터를 기록하고 필요한 경우 의사 결정/개인화를 요청하기 위해 Adobe Experience Platform Edge Network 호출을 트리거합니다. 이 요청은 서버 간 요청이므로 인증된 [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) 끝점을 [데이터 수집 API](https://developer.adobe.com/data-collection-apis/docs/)의 일부로 사용합니다. Adobe에서는 [사용자 지정 네임스페이스](https://experienceleague.adobe.com/ko/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities)를 사용하여 OpenAI 고유 식별자를 전달하는 것이 좋습니다. ID UI에서 만드는 네임스페이스와 호출에서 정의하는 ID 네임스페이스가 일치하는지 확인합니다(대/소문자 구분).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## 4단계: Edge Network이 핸들을 반환합니다.

Edge Network이 `interact` 호출을 받으면 `handle` 배열로 응답합니다. 이 배열에는 데이터 스트림 구성에 따라 ID 및 개인화 결정이 포함될 수 있습니다. 예제 응답은 다음과 같습니다.

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

그런 다음 MCP 서버는 Edge Network 응답에서 정보를 추출하여 ID 정보를 유지할 수 있습니다.

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## 5단계: MCP 서버가 구조화된 도구 출력과 Adobe 메타데이터를 ChatGPT에 반환

MCP 도구 응답에는 Edge Network의 구조화된 도구 출력과 개인화가 모두 포함됩니다.

* `structuredContent` 개체에는 ChatGPT가 안전하게 읽고 내레이팅할 수 있는 비즈니스 데이터가 포함되어 있습니다.
* `_meta` 개체에는 Adobe 응답 핸들과 서버가 계산한 `identityMap`이(가) 포함되어 있으므로 해당 데이터를 ChatGPT에 노출하지 않고 위젯에서 읽을 수 있습니다. 이 정보를 `_meta.adobe`에 보관하면 해당 데이터가 있는 위치에서 일관성을 유지할 수 있습니다. 동일한 `identityMap` 전달을 전달하면 위젯이 이후 UI측 이벤트에서 동일한 사용자 지정 ID를 사용하는 데 도움이 됩니다.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

자세한 내용은 OpenAI 개발자 참조의 [도구 결과](https://developers.openai.com/apps-sdk/reference/#tool-results)를 참조하십시오.

## 6단계: 위젯이 결과를 렌더링하고 `_adobe.handles`을(를) 사용하여 `applyResponse`을(를) 적용합니다.

위젯은 `structuredContent`에서 비즈니스 데이터를 렌더링한 다음 `_meta.adobe`에서 Adobe 메타데이터를 읽습니다. ChatGPT에서 호환성 레이어를 통해 위젯에 동일한 데이터를 사용할 수 있습니다.

* `window.openai.toolOutput`에 `structuredContent` 포함
* `window.openai.toolResponseMetadata`에 `_meta` 포함

위젯은 웹 SDK JavaScript 라이브러리의 [`applyResponse`](../../js/commands/applyresponse.md) 명령을 사용하여 클라이언트측 상태를 하이드레이션하고 서버측 `interact` 호출에서 반환된 개인화 결정을 렌더링합니다. [`configure`](../../js/commands/configure/overview.md)을(를) 호출하기 전에 `applyResponse` 명령을 호출했는지 확인하십시오. MCP 서버가 `interact` 호출을 수행했으므로 도구 호출의 상호 작용을 위해 [`sendEvent`](../../js/commands/sendevent/overview.md) 명령을 즉시 호출할 필요가 없습니다.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

위젯이 나중에 추가 UI측 이벤트를 전송하는 경우 해당 호출에 동일한 `identityMap`을(를) 포함할 수 있습니다.

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

이 패턴은 서버측 `interact` 호출이 Analytics 수집 및 의사 결정에 대한 올바른 소스로 유지되도록 하는 동시에 서버측 및 UI측 ID 사용을 정렬합니다.

## 유효성 검사

위의 모든 단계가 구성되면 다음을 확인할 수 있습니다.

* **데이터 수집:** 이벤트가 원하는 데이터 집합에 도달하는지, 각 이벤트가 예상대로 처리되는지 확인하십시오.
* **Personalization:** Edge Network에서 결정을 반환하고 해당 결정이 위젯에서 렌더링되는지 확인합니다.

## 보안 및 개인 정보 고려 사항

* ChatGPT의 식별자가 익명 경우에도 이를 민감한 것으로 취급합니다.
* 조직의 동의 및 데이터 거버넌스 사례를 이 워크플로우에 적용해야 합니다.
* Adobe에서는 권한 부여에 OAuth 2.1 워크플로를 사용하는 것이 좋습니다.
* 액세스 토큰 및 비밀이 클라이언트나 UI에 도달하지 않는지 확인하십시오.
