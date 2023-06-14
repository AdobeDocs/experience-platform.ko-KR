---
keywords: Experience Platform;미디어 에지;인기 항목;날짜 범위
solution: Experience Platform
title: Media Edge API 시작하기
description: Media Edge API 문제 해결 안내서
source-git-commit: f723114eebc9eb6bfa2512b927c5055daf97188b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Media Edge API 문제 해결 안내서

이 안내서에서는 오류를 처리하고 성공적인 응답을 얻기 위한 문제 해결 지침을 제공합니다.

## 오류 응답 지원 사용

실패한 응답을 해결하는 데 도움이 되도록 오류 개체가 포함된 응답 본문이 오류와 함께 표시됩니다. 이 경우 응답 본문에 정의된 문제 세부 정보가 포함됩니다. [RFC 7807 HTTP API에 대한 문제 세부 정보](https://datatracker.ietf.org/doc/html/rfc7807). API 사용자 경험을 개선하기 위해 문제 세부 정보가 설명적입니다(배열 키의 세부 정보는 누락되거나 잘못된 필드에 JsonPath를 사용하여 표시됨). 또한 누적됩니다(모든 잘못된 필드가 동일한 요청에 보고됨).


## 세션 시작 확인

세션 시작 요청을 작성하는 데 발생하는 대부분의 문제는 207 다중 상태 응답입니다.
페이로드는 Experience Edge Network Server API의 치명적이지 않은 오류와 유사합니다. 모든 Media Analytics 오류의 유형은 다음과 같습니다.  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. 응답에 표시된 숫자는 오류 상태에 해당합니다.

다음 예는 세션 시작 요청에 대한 응답 본문을 보여줍니다. 둘 다 필수 필드가 없고 응답 본문이 잘못되었습니다.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

위의 예에서 두 문제는 모두 `name` 및 `reason` 아래에 `details`: 첫 번째 이유가 표시됩니다 `missing required field` 두 번째는 ISO 8601 표준에 대한 비준수에 대해 설명합니다.


>[!NOTE]
>
> Adobe Media Analytics에서 업스트림으로 발생한 오류의 경우 생성된 미디어 세션을 계속 처리하는 것이 좋습니다.

## 이벤트 확인

잘못된 이벤트 요청은 대부분 400개의 잘못된 요청 응답을 초래합니다. 이러한 경우 페이로드는 Experience Edge Network Server API 치명적 오류와 유사합니다.

이벤트 요청의 경우 Media Edge API 서비스에는 XDM 모델 자체에서 캡처되지 않은 추가 검사가 포함됩니다. 여기에는 경로 확인이 포함됩니다 `eventType` 요청 페이로드와 일치 `eventType`.


다음 예제는 `eventType` 와(과) 불일치 `adBreakStart` 페이로드 전송 대상 `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

다음 예는 다음을 찾는 추가 Media Edge API 확인을 보여 줍니다. `chapterStart` 호출 누락 `chapterDetails` 정보:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## 400 레벨 및 500 레벨 오류 처리

다음 표에서는 상태 응답 오류 처리에 대한 지침을 제공합니다.


| 오류 코드 | 설명 |
| ---------- | --------- |
| 4xx 잘못된 요청 | 대부분의 4xx 오류(예: `400`, `403`, `404`)는 사용자가 재시도하면 안 됩니다. 요청을 다시 시도해도 응답이 성공하지 않습니다. 사용자는 요청을 다시 시도하기 전에 오류를 해결해야 합니다. 4xx 상태 코드를 발생시키는 이벤트는 추적되지 않으며, 이는 4xx 응답을 받은 세션의 데이터 정확성에 영향을 미칠 수 있습니다. |
| 410 없어짐 | 추적하려는 세션이 더 이상 서버측에서 계산되지 않음을 나타냅니다. 이에 대한 가장 일반적인 이유는 세션이 24시간 이상 길기 때문입니다. 를 받은 후 `410`새 세션을 시작하고 추적해 보십시오. |
| 429 요청이 너무 많음 | 이 응답 코드는 서버가 요청을 속도 제한하고 있음을 나타냅니다. 다음 **다음 시간 이후에 다시 시도** 응답 헤더의 지침 뒤로 흐르는 모든 응답은 도메인별 오류 코드와 함께 HTTP 응답 코드를 전달해야 합니다. |
| 500 내부 서버 오류 | `500` 오류는 일반적인 catch-all 오류입니다. `500` 오류를 재시도해서는 안 됩니다. 단, `502`, `503` 및 `504`. |
| 502 잘못된 게이트웨이 | 이 오류 코드는 서버가 게이트웨이로 작동하는 동안 업스트림 서버에서 잘못된 응답을 받았음을 나타냅니다. 이 문제는 서버 간 네트워크 문제로 인해 발생할 수 있습니다. 임시 네트워크 문제는 자체적으로 해결될 수 있으므로 요청을 다시 시도하면 문제가 해결될 수 있습니다. |
| 503 서비스를 사용할 수 없음 | 이 오류 코드는 서비스를 일시적으로 사용할 수 없음을 나타냅니다. 이 문제는 유지 관리 기간 동안 발생할 수 있습니다. 수신자 `503` 오류는 요청을 다시 시도할 수 있지만 **다음 시간 이후에 다시 시도** 헤더 지침 |


## 세션 응답이 느린 경우 큐에 이벤트 저장

미디어 추적 세션을 시작한 후 미디어 플레이어는 (세션 ID 매개 변수와 함께) 백엔드에서 세션 시작 응답이 반환되기 전에 실행될 수 있습니다. 이 경우 앱은 세션 시작 요청과 해당 응답 사이에 도착하는 모든 추적 이벤트를 큐에 추가해야 합니다. 세션 응답이 도착하면 먼저 큐에 있는 이벤트를 처리해야 실시간 이벤트 처리를 시작할 수 있습니다.

최상의 결과를 얻으려면 배포의 참조 플레이어에서 세션 ID를 수신하기 전에 이벤트를 처리하는 방법에 대한 지침을 확인하십시오.

다음 예는 세션 ID를 수신하기 전에 이벤트를 처리하는 방법을 보여줍니다.


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


