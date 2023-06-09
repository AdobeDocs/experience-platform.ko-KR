---
keywords: Experience Platform;미디어 에지;인기 항목;날짜 범위
solution: Experience Platform
title: Media Edge API 시작하기
description: Media Edge API 시작하기
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 7%

---


# Media Edge API 시작

이 안내서에서는 Media Edge API 서비스와 성공적인 초기 상호 작용을 수행하기 위한 지침을 제공합니다. 여기에는 미디어 세션을 시작한 다음 Customer Journey Analytics(CJA)와 같은 Adobe Experience Platform(AEP) 솔루션으로 전송된 이벤트를 추적하는 작업이 포함됩니다. Media Edge API 서비스는 세션 시작 끝점으로 시작됩니다. 세션이 시작되면 다음 이벤트 중 하나 이상을 추적할 수 있습니다.

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* 라는 오류가 표시됩니다
* sessionEnd
* sessionComplete
* statesUpdate

각 이벤트에는 자체 끝점이 있습니다. 모든 Media Edge API 끝점은 POST 메서드이며, 이벤트 데이터에 대한 JSON 요청 본문이 있습니다. Media Edge API 끝점, 매개 변수 및 예제에 대한 자세한 내용은 Media Edge Swagger 파일을 참조하십시오.

이 안내서에서는 세션을 시작한 후 다음 이벤트를 추적하는 방법을 보여 줍니다.

* 버퍼 시작
* 재생
* 세션 완료

## API 구현

Media Edge API는 모델 및 호출된 경로의 사소한 차이점 외에도 Media Collection API와 동일합니다. Media Collection의 구현 세부 사항은 다음 설명서에 설명된 대로 Media Edge API에 계속 유효합니다.

* [플레이어에서 HTTP 요청 유형 설정](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Ping 이벤트 보내기](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [시간 제한 조건](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [이벤트 순서 제어](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

현재 Media Edge API는 요청에 인증 헤더가 필요하지 않습니다.


## 세션 시작

서버에서 미디어 세션을 시작하려면 세션 시작 끝점을 사용합니다. 성공적인 응답에는 다음이 포함됩니다. `sessionId`: 후속 이벤트 요청에 필요한 매개 변수입니다.

세션 시작 요청을 수행하기 전에 다음이 필요합니다.

* 다음 `datastreamId` 는 POST 세션 시작 요청에 필요한 매개 변수입니다. 을(를) 검색하려면 `datastreamId`, 참조 [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ko-KR).

* 필요한 최소 데이터가 포함된 요청 페이로드에 대한 JSON 개체. (아래 예제 요청에 표시된 대로)

이 정보가 있으면 다음을 제공합니다. `datastreamId` 다음 호출:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### 요청 예

다음 예는 세션 시작 cURL 요청을 보여줍니다.

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

위의 예제 요청에서 `eventType` 값에 접두사 포함 `media` 에 따라 [경험 데이터 모델(XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 도메인을 지정합니다.

또한 데이터 유형 매핑도 `eventType` 위의 예는 다음과 같습니다(보고 전용 필드는 페이로드에 없어야 함).

| eventType | 데이터 형식 | 보고 전용 필드(무시됨) |
| -------- | ------ | ---------- |
| media세션 시작 | sessionDetails | ID, adCount, averageMinuteAudience,chapterCount, estimatedStreams, hasProgress10, hasProgress25, hasProgress50, hasProgress75, hasSegmentView, isCompleted, isDownloaded, isFederated, isPlayed, isViewed, pauseCount, pauseTime, secondsSinceLastCall, segment, timePlayed, totalTimePlayed, uniqueTimePlayed, pev3, pccr |
| media.chapterStart | chapterDetails | ID, isCompleted, isStarted, timePlay |
| media.adBreakStart | advertisingPodDetails | ID |
| media.adStart | advertisingDetails | ID, isCompleted, isStarted, timePlay |
| media.error | errorDetails | - |
| media.statesUpdate | statesStart: 배열[playerStateData], statesEnd: 배열[playerStateData] | playerStateData.isSet, playerStateData.count, playerStateData.time |
| media.sessionStart, media.chapterStart, media.adStart | 사용자 지정 메타데이터 | - |
| 모두 | qoeDataDetails | bitrateAverage, bitrateAverageBucket, bitrateChangeCount, bufferTime, errorCount, externalErrors, hasBitrateChangeImpactedStreams, hasBufferImpactedStreams, hasErrorImpactedStreams, hasStallImpactedStreams, isDroppedBeforeStart, mediaSdkErrors, playerSdkErrors, stallCount, stallTime |

### 응답 예

다음 예는 세션 시작 요청에 대한 성공적인 응답을 보여 줍니다.

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

위의 예제 응답에서 `sessionId` 다음으로 표시됨 `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. 이 ID는 후속 이벤트 요청에서 필수 매개 변수로 사용됩니다.

세션 시작 끝점 매개 변수 및 예제에 대한 자세한 내용은 Media Edge Swagger 파일을 참조하십시오.

XDM 미디어 데이터 매개 변수에 대한 자세한 내용은 [미디어 세부 정보 스키마](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## 버퍼 시작 이벤트 요청

버퍼 시작 이벤트는 미디어 플레이어에서 버퍼링이 시작될 때 신호를 보냅니다. 버퍼 다시 시작은 API 서비스의 이벤트가 아닙니다. 대신 버퍼 시작 후 재생 이벤트가 전송될 때 추론됩니다. 버퍼 시작 이벤트를 요청하려면 `sessionId` (다음 끝점 호출 페이로드):

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### 요청 예

다음 예는 버퍼 시작 cURL 요청을 보여줍니다.

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

위의 예 요청에서도 동일합니다 `sessionId` 이전 호출에서 반환된 값은 버퍼 시작 요청에서 필수 매개 변수로 사용됩니다.

버퍼 시작 끝점 매개 변수 및 예제에 대한 자세한 내용은 Media Edge Swagger 파일을 참조하십시오.

## 이벤트 요청 재생

재생 이벤트는 미디어 플레이어가 &quot;버퍼링&quot;, &quot;일시 중지됨&quot; 또는 &quot;오류&quot;와 같이 다른 상태에서 &quot;재생 중&quot; 상태로 변경되면 전송됩니다. 재생 이벤트를 요청하려면 `sessionId` (다음 끝점 호출 페이로드):

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### 요청 예

다음 예는 cURL 재생 요청을 보여줍니다.

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

재생 끝점 매개 변수 및 예제에 대한 자세한 내용은 Media Edge Swagger 파일을 참조하십시오.

## 세션 완료 이벤트 요청

세션 완료 이벤트는 기본 콘텐츠의 끝에 도달하면 전송됩니다. 세션 완료 이벤트 요청을 수행하려면 다음을 사용하십시오. `sessionId` (다음 끝점 호출 페이로드):

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### 요청 예

다음 예는 세션 완료 cURL 요청을 보여줍니다.

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

세션 완료 끝점 매개 변수 및 예제에 대한 자세한 내용은 Media Edge Swagger 파일을 참조하십시오.

## 응답 코드

다음 표는 Media Edge API 요청으로 인해 발생할 수 있는 응답 코드를 보여 줍니다.

| 상태 | 설명 |
| ---------- | --------- |
| 200 | 세션이 정상적으로 생성되었습니다. |
| 207 | Experience Edge Network에 연결된 서비스 중 하나에 문제가 있습니다(문제 해결 안내서의 자세한 내용 참조). |
| 레벨 | 잘못된 요청 |
| 레벨 | 서버 오류 |

오류 및 실패한 응답 코드 처리에 대한 자세한 내용은 Media Edge 문제 해결 안내서를 참조하십시오.


