---
title: createMediaSession
description: 미디어 세션을 자동으로 관리하도록 웹 SDK를 구성하는 방법에 대해 알아봅니다
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

다음 `createMediaSession` 명령은 웹 SDK의 일부입니다 `streamingMedia` 구성 요소. 이 구성 요소를 사용하여 웹 사이트에서 미디어 세션과 관련된 데이터를 수집할 수 있습니다. 다음을 참조하십시오. `streamingMedia` [설명서](configure/streamingmedia.md) 구성 요소를 구성하는 방법을 알아봅니다.

수집된 데이터에는 미디어 재생, 일시 정지, 완료 및 기타 관련 이벤트에 대한 정보가 포함될 수 있습니다. 수집되면 이 데이터를에 보낼 수 있습니다. [適用於串流媒體的 Adobe Analytics](https://experienceleague.adobe.com/ko/docs/media-analytics/using/media-overview)을 클릭하여 지표를 집계합니다. 이 기능은 웹 사이트에서의 미디어 소비 행동을 추적하고 이해하는 포괄적인 솔루션을 제공합니다.

Web SDK에서 미디어 세션을 만드는 방법에는 두 가지가 있습니다.

* [자동으로 추적되는 미디어 세션](#automatic) 웹 SDK가 미디어 ping 이벤트의 디스패치를 관리할 수 있도록 허용 [適用於串流媒體的 Adobe Analytics](https://experienceleague.adobe.com/ko/docs/media-analytics/using/media-overview). 이러한 ping의 빈도는 의 구성 설정에 따라 결정됩니다. [스트리밍 미디어](configure/streamingmedia.md) 구성 요소.
* [수동으로 추적된 미디어 세션](#manual) 에 대한 세션 ping 이벤트 발송을 보다 효과적으로 제어 [適用於串流媒體的 Adobe Analytics](https://experienceleague.adobe.com/ko/docs/media-analytics/using/media-overview). 또한 을 저장할 수 있습니다. `sessionID` 미디어 세션의 경우.

## 자동으로 추적되는 미디어 세션 만들기 {#automatic}

미디어 세션 추적을 자동으로 시작하려면 다음을 호출합니다. `createMediaSession` 아래에 설명된 옵션을 사용하는 방법:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| 속성 | 유형 | 필수 여부 | 설명 |
|---------|----------|---------|---------|
| `playerId` | 문자열 | 예 | 미디어 세션을 나타내는 고유 식별자인 플레이어 ID입니다. |
| `getPlayerDetails` | 함수 | 예 | 플레이어 세부 정보를 반환하는 함수입니다. 이 콜백 함수는 웹 SDK에 대해 모든 미디어 이벤트 전에 호출됩니다. `playerId` 을(를) 입력했습니다. |
| `xdm.eventType ` | 오브젝트 | 아니요 | 미디어 이벤트 유형. 제공되지 않으면 자동으로 로 설정됩니다. `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 오브젝트 | 예 | 세션 세부 정보 개체입니다. 다음 `sessionDetails` 개체에는 세션 세부 정보 속성이 포함되어야 합니다. 다음을 참조하십시오. [미디어 컬렉션 스키마](../../xdm/data-types/media-collection-details.md) 설명서 를 참조하십시오. |


## 수동으로 추적된 미디어 세션 만들기 {#manual}

미디어 세션 추적을 수동으로 시작하려면 다음을 호출하십시오. `createMediaSession` 아래에 설명된 옵션을 사용하는 방법:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| 속성 | 유형 | 필수 | 설명 |
|---------|----------|---------|---------|
| `xdm.eventType` | 오브젝트 | 아니요 | 미디어 이벤트 유형. 제공되지 않으면 자동으로 로 설정됩니다. `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 오브젝트 | 예 | 세션 세부 정보 개체입니다. 다음 `sessionDetails` 개체에는 세션 세부 정보 속성이 포함되어야 합니다. 다음을 참조하십시오. [미디어 컬렉션 스키마](../../xdm/data-types/media-collection-details.md) 설명서 를 참조하십시오. |
| `xdm.mediaCollection.playhead` | 정수 | 예 | 현재 플레이헤드입니다. |
| `xdm.mediaCollection.qoeDataDetails` | 오브젝트 | 아니요 | 체감 품질 데이터 세부 정보. 다음을 참조하십시오. [미디어 컬렉션 스키마](../../xdm/data-types/media-collection-details.md) 설명서 를 참조하십시오. |
