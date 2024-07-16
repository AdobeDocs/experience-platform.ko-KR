---
title: sendMediaEvent
description: sendMediaEvent 명령을 사용하여 웹 SDK에서 미디어 세션을 추적하는 방법에 대해 알아봅니다.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

`sendMediaEvent` 명령은 웹 SDK `streamingMedia` 구성 요소에 속합니다. 이 구성 요소를 사용하여 웹 사이트에서 미디어 세션과 관련된 데이터를 수집할 수 있습니다. 이 구성 요소를 구성하는 방법을 알아보려면 `streamingMedia` [설명서](configure/streamingmedia.md)를 참조하세요.

`sendMediaEvent` 명령을 사용하여 미디어 재생, 일시 중지, 완료, 플레이어 상태 업데이트 및 기타 관련 이벤트를 추적합니다.

Web SDK는 미디어 세션 추적 유형에 따라 미디어 이벤트를 처리할 수 있습니다.

* **자동으로 추적된 세션에 대한 이벤트 처리**. 이 모드에서는 미디어 이벤트 또는 플레이헤드 값에 `sessionID`을(를) 전달할 필요가 없습니다. Web SDK는 미디어 세션을 시작할 때 제공된 플레이어 ID와 `getPlayerDetails` 콜백 함수를 기반으로 이 작업을 처리합니다.
* **수동으로 추적된 세션에 대한 이벤트 처리**. 이 모드에서는 플레이헤드 값(정수 값)과 함께 `sessionID`을(를) 미디어 이벤트에 전달해야 합니다. 필요한 경우 체감 품질 데이터 세부 정보를 전달할 수도 있습니다.

## 유형별 미디어 이벤트 처리 {#handle-by-type}

각 이벤트 유형 및 세션 추적 방법(자동 또는 수동)에 대한 이벤트 유형 처리의 예를 보려면 아래 탭을 선택하십시오.


### 재생 {#play}

`media.play` 이벤트 유형은 미디어 재생이 시작되는 시기를 추적하는 데 사용됩니다. 플레이어가 다른 상태에서 &quot;재생 중&quot; 상태로 변경되면 이 이벤트를 전송해야 합니다. 플레이어가 &quot;재생 중&quot;으로 이동하는 다른 상태에는 &quot;버퍼링&quot;, 사용자가 &quot;일시 정지됨&quot;에서 다시 시작하는 상태, 플레이어가 오류에서 복구되는 상태 또는 자동 재생이 포함됩니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 일시 정지 {#pause}

`media.pauseStart` 이벤트 유형은 미디어 재생이 일시 중지된 경우 추적하는 데 사용됩니다. 이 이벤트는 사용자가 **[!UICONTROL 일시 중지]**&#x200B;를 누를 때 전송되어야 합니다. 다시 시작 이벤트 유형이 없습니다. `media.pauseStart` 이후에 `media.play` 이벤트를 보낼 때 다시 시작이 유추됩니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 오류 {#error}

`media.error` 이벤트 유형은 미디어 재생 중 오류가 발생하는 시점을 추적하는 데 사용됩니다. 이 이벤트는 오류가 발생할 때 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 광고 브레이크 시작 {#ad-break-start}

`media.adBreakStart` 이벤트 유형은 광고 브레이크가 시작될 때 추적하는 데 사용됩니다. 이 이벤트는 광고 브레이크가 시작될 때 전송되어야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 광고 브레이크 완료 {#ad-break-complete}

광고 브레이크가 완료되면 `media.adBreakComplete` 이벤트 유형을 사용하여 추적합니다. 광고 브레이크가 완료되면 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 광고 시작 {#ad-start}

`media.adStart` 이벤트 유형은 광고가 시작되는 시기를 추적하는 데 사용됩니다. 이 이벤트는 광고가 시작될 때 전송되어야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### 광고 완료 {#ad-complete}

`media.adComplete` 이벤트 유형은 광고가 완료되는 시점을 추적하는 데 사용됩니다. 광고가 완료될 때 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 광고 건너뛰기 {#ad-skip}

`media.adSkip` 이벤트 유형은 광고를 건너뛸 때 추적하는 데 사용됩니다. 광고를 건너뛸 때 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 챕터 시작 {#chapter-start}

`media.chapterStart` 이벤트 유형은 챕터가 시작되는 시기를 추적하는 데 사용됩니다. 이 이벤트는 챕터가 시작될 때 전송됩니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### 챕터 완료 {#chapter-complete}

`media.chapterComplete` 이벤트 유형은 챕터가 완료되는 시점을 추적하는 데 사용됩니다. 챕터가 완료되면 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 챕터 건너뛰기 {#chapter-skip}

`media.chapterSkip` 이벤트 유형은 챕터를 건너뛸 때 추적하는 데 사용됩니다. 챕터를 건너뛸 때 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 버퍼 시작 {#buffer-start}

`media.bufferStart` 이벤트 형식은 버퍼링이 시작될 때 추적하는 데 사용됩니다. 이 이벤트는 버퍼링이 시작될 때 전송되어야 합니다. `bufferResume` 이벤트 유형이 없습니다. `bufferResume`은(는) 재생 이벤트를 `bufferStart` 뒤에 보낼 때 추론됩니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 비트율 변경 {#bitrate-change}

`media.bitrateChange` 이벤트 유형은 비트율이 변경될 때 추적하는 데 사용됩니다. 이 이벤트는 비트율이 변경될 때 전송되어야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 상태 업데이트 {#state-updates}

`media.stateUpdate` 이벤트 유형은 플레이어 상태가 변경될 때 추적하는 데 사용됩니다. 플레이어 상태가 변경되면 이 이벤트를 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### 세션 종료 {#session-end}

`media.sessionEnd` 이벤트 유형은 사용자가 콘텐츠 보기를 중단한 경우 세션을 즉시 닫도록 Media Analytics 백엔드에 통지하는 데 사용되며, 반환 가능성이 낮습니다.

`sessionEnd` 이벤트를 보내지 않는 경우 중단된 세션은 10분 동안 이벤트가 수신되지 않았거나 30분 동안 플레이헤드 이동이 발생하지 않으면 시간 초과됩니다. 세션이 자동으로 삭제됩니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 세션 완료 {#session-complete}

`media.sessionComplete` 이벤트 유형은 미디어 세션이 완료되는 시점을 추적하는 데 사용됩니다. 이 이벤트는 기본 콘텐츠의 끝에 도달하면 전송해야 합니다.

>[!BEGINTABS]

>[!TAB 자동 세션 추적]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB 수동 세션 추적]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]
