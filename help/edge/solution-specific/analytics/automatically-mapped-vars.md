---
title: Analytics에 자동으로 매핑되는 변수
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Analytics에 자동으로 매핑되는 변수
description: Experience Platform 웹 SDK를 사용하여 Analytics에서 자동으로 매핑되는 변수 알아보기
seo-description: Experience Platform 웹 SDK를 사용하여 Analytics에서 자동으로 매핑되는 변수 알아보기
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) Analytics에 자동으로 매핑되는 변수

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

다음은 Adobe Experience Platform Edge Network가 자동으로 Analytics에 매핑하는 변수 목록입니다.

| XDM 필드 경로 | Analytics 쿼리 문자열/HTTP 헤더 | 설명 |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | HTTP 헤더 매핑인 HEADER_USER_AGENT입니다. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | HTTP 헤더 매핑인 HEADER_ACCEPT_LANGUAGE입니다. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement 쿼리 매개 변수 COOKIES 매핑과 전환 BOOLEAN_TO_YN이 함께 매핑됩니다. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement 쿼리 매개 변수 J_JSCRIPT 매핑입니다. |
| `environment.browserDetails.javaEnabled` | `v` | 전환 BOOLEAN_TO_YN을 사용한 AppMeasurement 쿼리 매개 변수 JAVA_ENABLED 매핑. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement 쿼리 매개 변수 BROWSER_HEIGHT 매핑입니다. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement 쿼리 매개 변수 BROWSER_WIDTH 매핑입니다. |
| `environment.connectionType` | `ct` | AppMeasurement 쿼리 매개 변수 CT_CONNECT_TYPE 매핑입니다. |
| `device.colorDepth` | `c` | AppMeasurement 쿼리 매개 변수 C_COLOR 매핑입니다. |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement 쿼리 매개 변수 STATE 매핑을 참조하십시오. |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement 쿼리 매개 변수 ZIP 매핑입니다. |
| `placeContext.geo.latitude` | `lat` | AppMeasurement 쿼리 매개 변수 LATITUDE 매핑입니다. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement 쿼리 매개 변수 위도 매핑을 참조하십시오. |
| `web.webPageDetails.server` | `sv` | AppMeasurement 쿼리 매개 변수 USER_SERVER 매핑입니다. |
| `web.webPageDetails.name` | `gn` | AppMeasurement 쿼리 매개 변수 PAGENAME 매핑을 참조하십시오. |
| `web.webPageDetails.URL` | `g` | AppMeasurement 쿼리 매개 변수 PAGE_URL 매핑입니다. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement 쿼리 매개 변수 BOOLEAN_TO_YN이 포함된 홈 페이지 매핑. |
| `web.webReferrer.URL` | `r` | AppMeasurement 쿼리 매개 변수 REFERRER 매핑을 참조하십시오. |
| `application.id` | `c.a.appid` | AppMeasurement 컨텍스트 데이터 `c.a.appid` 매핑을 참조하십시오. |
| `application.launches.value` | `c.a.launches` | AppMeasurement 컨텍스트 데이터 `c.a.launches` 매핑을 참조하십시오. |
| `marketing.trackingCode` | `v0` | AppMeasurement 쿼리 매개 변수 CAMPAIGN 매핑을 참조하십시오. |
| `commerce.purchaseID` | `pi` | AppMeasurement 쿼리 매개 변수 PURCHASEID 매핑. |
| `commerce.currencyCode` | `cc` | AppMeasurement 쿼리 매개 변수 CURRENCY 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement 컨텍스트 데이터 `a.media.name` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement 컨텍스트 데이터 `c.a.media.length` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement 컨텍스트 데이터 `c.a.contentType` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement 컨텍스트 데이터 `c.a.media.playerName` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement 컨텍스트 데이터 `c.a.media.channel` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement 컨텍스트 데이터 `c.a.media.segment` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement 컨텍스트 데이터 `c.a.media.friendlyName` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement 컨텍스트 데이터 `c.a.media.sdkVersion` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement 컨텍스트 데이터 `c.a.media.show` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement 컨텍스트 데이터 `c.a.media.format` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement 컨텍스트 데이터 `c.a.media.season` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement 컨텍스트 데이터 `c.a.media.episode` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement 컨텍스트 데이터 `c.a.media.network` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 전환 AUDIO_SHOW_TYPE을 사용한 AppMeasurement 컨텍스트 데이터 `c.a.media.type` 매핑. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement 컨텍스트 데이터 `c.a.media.feed` 매핑을 참조하십시오. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement 컨텍스트 데이터 `c.a.media.timePlayed` 매핑을 참조하십시오. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement 컨텍스트 데이터 `c.a.media.totalTimePlayed` 매핑을 참조하십시오. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement 컨텍스트 데이터 `c.a.media.federated` 매핑을 참조하십시오. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseCount` 매핑을 참조하십시오. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseTime` 매핑을 참조하십시오. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement 컨텍스트 데이터 `c.a.media.resume` 매핑을 참조하십시오. |
| `identitymap.ecid.[0].id` | `mid` | AppMeasurement 쿼리 매개 변수 MID 매핑입니다. |
