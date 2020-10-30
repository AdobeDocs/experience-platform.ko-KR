---
title: Adobe Analytics에 자동으로 매핑되는 변수
seo-title: Adobe Analytics에서 Adobe Experience Platform 웹 SDK와 자동으로 매핑되는 변수
description: Experience Platform 웹 SDK를 사용하여 Adobe Analytics에서 자동으로 매핑되는 변수 알아보기
seo-description: Experience Platform 웹 SDK를 사용하여 Adobe Analytics에서 자동으로 매핑되는 변수 알아보기
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 3ed89011313006cf627945bf8c75bfd0b87a69bc
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---


# 변수가 [!DNL Analytics]

아래는 Adobe Experience Platform이 자동으로 매핑되는 변수 [!DNL Edge Network] 목록입니다 [!DNL Analytics].

| XDM 필드 경로 | [!DNL Analytics Query String] / HTTP 헤더 | 설명 |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | AppMeasurement 컨텍스트 데이터 `c.a.appid` 매핑을 참조하십시오. |
| `application.launches.value` | `c.a.launches` | AppMeasurement 컨텍스트 데이터 `c.a.launches` 매핑을 참조하십시오. |
| `commerce.checkouts.id` | `events` | `scCheckout` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.checkouts.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_SC_CHECKOUT을 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.order.currencyCode` | `cc` | AppMeasurement 쿼리 매개 변수 CURRENCY 매핑을 참조하십시오. |
| `commerce.order.purchaseID` | `pi` | AppMeasurement 쿼리 매개 변수 PURCHASEID 매핑입니다. |
| `commerce.productListAdds.id` | `events` | `scAdd` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.productListAdds.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_SC_ADD를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.productListOpens.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_SC_OPEN을 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.productListRemovals.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_SC_REMOVE를 사용한 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.productListViews.id` | `events` | `scView` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.productListViews.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_SC_VIEW를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.productViews.id` | `events` | `prodView` 이벤트 정리. 이 필드가 제외되면(즉, 일련화되지 않은 이벤트의 경우) 시스템에서 자체 ID 값을 생성하여 엔티티에 할당합니다. |
| `commerce.productViews.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_PROD_VIEW를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `commerce.purchases.value` | `events` | 구분 기호를 사용하여 전환 COMMERCE_PURCHASE를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑 `,`. |
| `device.colorDepth` | `c` | AppMeasurement 쿼리 매개 변수 C_COLOR 매핑을 참조하십시오. |
| `device.screenHeight` | `s` | AppMeasurement 쿼리 매개 변수 화면 해상도 매핑입니다. |
| `device.screenWidth` | `s` | AppMeasurement 쿼리 매개 변수 화면 해상도 매핑입니다. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | HTTP 헤더 매핑인 HEADER_ACCEPT_LANGUAGE입니다. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement 쿼리 매개 변수 전환 BOOLEAN_TO_YN이 있는 쿠키 매핑을 참조하십시오. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement 쿼리 매개 변수 JAVA_ENABLED 매핑(전환 BOOLEAN_TO_YN). |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement 쿼리 매개 변수 J_JSCRIPT 매핑입니다. |
| `environment.browserDetails.userAgent` | `User-Agent` | HTTP 헤더 매핑인 HEADER_USER_AGENT입니다. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement 쿼리 매개 변수 BROWSER_HEIGHT 매핑입니다. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement 쿼리 매개 변수 BROWSER_WIDTH 매핑을 참조하십시오. |
| `environment.connectionType` | `ct` | AppMeasurement 쿼리 매개 변수 CT_CONNECT_TYPE 매핑입니다. |
| `environment.ipV4` | `X-Forwarded-For` | HTTP 헤더 매핑인 X-FORWARDED-FOR입니다. |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement 쿼리 매개 변수 MID 매핑입니다. |
| `marketing.trackingCode` | `v0` | AppMeasurement 쿼리 매개 변수 CAMPAIGN 매핑을 참조하십시오. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement 컨텍스트 데이터 `c.a.media.federated` 매핑을 참조하십시오. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseTime` 매핑을 참조하십시오. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseCount` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement 컨텍스트 데이터 `c.a.media.friendlyName` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement 컨텍스트 데이터 `c.a.media.episode` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement 컨텍스트 데이터 `c.a.media.season` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement 컨텍스트 데이터 `a.media.name` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement 컨텍스트 데이터 `c.a.media.show` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 전환 STUDIO_SHOW_TYPE을 사용한 AppMeasurement 컨텍스트 데이터 `c.a.media.type` 매핑. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 전환 VIDEO_SHOW_TYPE을 사용한 AppMeasurement 컨텍스트 데이터 `c.a.media.type` 매핑 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement 컨텍스트 데이터 `c.a.media.length` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement 컨텍스트 데이터 `c.a.media.channel` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement 컨텍스트 데이터 `c.a.contentType` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement 컨텍스트 데이터 `c.a.media.network` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement 컨텍스트 데이터 `c.a.media.segment` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement 컨텍스트 데이터 `c.a.media.playerName` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement 컨텍스트 데이터 `c.a.media.sdkVersion` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement 컨텍스트 데이터 `c.a.media.feed` 매핑을 참조하십시오. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement 컨텍스트 데이터 `c.a.media.format` 매핑을 참조하십시오. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement 컨텍스트 데이터 `c.a.media.resume` 매핑을 참조하십시오. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement 컨텍스트 데이터. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement 컨텍스트 데이터 `c.a.media.timePlayed` 매핑을 참조하십시오. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement 컨텍스트 데이터 `c.a.media.totalTimePlayed` 매핑을 참조하십시오. |
| `placeContext.geo.latitude` | `lat` | AppMeasurement 쿼리 매개 변수 LATITUDE 매핑입니다. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement 쿼리 매개 변수 위도 매핑을 참조하십시오. |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement 쿼리 매개 변수 ZIP 매핑을 참조하십시오. |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement 쿼리 매개 변수 STATE 매핑을 참조하십시오. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement 쿼리 매개 변수 제품 상품 이벤트/Evar 매핑. |
| `productlistitems.[N].lineitemid` | `products` | AppMeasurement 쿼리 매개 변수 제품 카테고리 매핑을 참조하십시오. |
| `productlistitems.[N].name` | `products` | AppMeasurement 쿼리 매개 변수 제품 이름 매핑을 참조하십시오. |
| `productlistitems.[N].pricetotal` | `products` | AppMeasurement 쿼리 매개 변수 제품 가격 매핑을 참조하십시오. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement 쿼리 매개 변수 제품 수량 매핑을 참조하십시오. |
| `web.webInteraction.URL` | `pev1` | AppMeasurement 쿼리 매개 변수 PAGE_EVENT_VAR1 매핑을 참조하십시오. |
| `web.webInteraction.name` | `pev2` | AppMeasurement 쿼리 매개 변수 PAGE_EVENT_VAR2 매핑입니다. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` to `pe=lnk_o``web.webInteraction.type=download` to `pe=lnk_d``web.webInteraction.type=exit` to `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | AppMeasurement 쿼리 매개 변수 PAGE_URL 매핑입니다. |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement 쿼리 매개 변수 PAGE_TYPE_FULL 매핑과 전환 ERROR_PAGE_TYPE입니다. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement 쿼리 매개 변수 HOMEPAGE 매핑과 전환 BOOLEAN_TO_YN입니다. |
| `web.webPageDetails.name` | `gn` | AppMeasurement 쿼리 매개 변수 PAGENAME 매핑을 참조하십시오. |
| `web.webPageDetails.server` | `sv` | AppMeasurement 쿼리 매개 변수 USER_SERVER 매핑을 참조하십시오. |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement 쿼리 매개 변수 CHANNEL 매핑을 참조하십시오. |
| `web.webReferrer.URL` | `r` | AppMeasurement 쿼리 매개 변수 REFERRER 매핑을 참조하십시오. |
