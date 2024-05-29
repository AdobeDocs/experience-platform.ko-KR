---
title: getMediaAnalyticsTracker
description: Media Analytics 추적기 개체를 만들고 이를 사용하여 미디어 이벤트를 추적하는 방법에 대해 알아봅니다.
source-git-commit: 9384c1cc15441199e898d6cc0850e5422253f106
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# `getMediaAnalyticsTracker`

이 웹 SDK 명령은 Media Analytics 추적기를 검색합니다. 이 명령을 사용하여 개체 인스턴스를 만든 다음, [미디어 JS 라이브러리](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), 미디어 이벤트를 추적합니다.

다음 `getMediaAnalyticsTracker` 명령은 기존 Media Analytics API를 반환합니다.


| 메서드 이름 | 설명 | 구문 |
|-----------------|---|----------------|
| `getInstance` | 재생 세션을 추적할 미디어 인스턴스를 만듭니다. | `Media.getInstance()` |
| `createMediaObject` | 미디어 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | 광고 브레이크 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | 광고 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | 챕터 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | 상태 정보를 포함하는 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createStateObject(name)` |
| `createQoEObject` | QoE 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## 인스턴스 메서드

| 메서드 이름 | 설명 | 구문 |
|---|---|----|
| `trackSessionStart` | 재생을 시작하려는 의도를 추적합니다. 이렇게 하면 미디어 추적기 인스턴스에서 추적 세션이 시작됩니다. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | 이전 일시 중지 후 미디어 재생 또는 다시 시작을 추적합니다. | `trackerInstance.trackPlay()` |
| `trackPause` | 미디어 일시 중지를 추적합니다. | `trackerInstance.trackPause()` |
| `trackComplete` | 미디어 추적 완료. 미디어를 완전히 본 경우에만 이 메서드를 호출합니다. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | 보기 세션의 끝을 추적합니다. 사용자가 완료할 미디어를 보지 않은 경우에도 이 메서드를 호출합니다. | `trackerInstance.trackSessionEnd()` |
| `trackError` | 미디어 재생 중에 발생한 오류를 추적합니다. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | 사용자 지정 이벤트를 추적합니다. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | 플레이헤드 위치를 업데이트합니다. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | 체감 품질을 업데이트합니다. | `trackerInstance.updateQoEObject(qoe)` |

## 상수

| 상수 이름 | 설명 | 값 |
|-----------------|--|-----------------|
| `MediaType` | 미디어 유형 | `Video`, `Audio` |
| `StreamType` | 스트림 유형 | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | 비디오 스트림에 대한 표준 메타데이터 키를 정의합니다. | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | 오디오 스트림에 대한 표준 메타데이터 키를 정의합니다. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | 광고의 표준 메타데이터 키를 정의합니다. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | 추적 이벤트의 유형을 정의합니다. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | 플레이어 상태 추적을 위한 표준 값을 정의합니다. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
