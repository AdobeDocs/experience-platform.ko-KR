---
title: Adobe Experience Platform Web SDK에서 자동으로 매핑된 Adobe Analytics 변수
description: Experience Platform Web SDK를 사용하여 Adobe Analytics에서 자동으로 매핑되는 변수를 알아봅니다
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;변수;analytics;자동 맵;자동 매핑
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: b2d949232674bb4c4ebcb7754726730b966a0e02
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 5%

---

# 변수가 [!DNL Analytics]에 자동으로 매핑됨

다음은 Adobe Experience Platform Edge Network가 자동으로 Adobe Analytics에 매핑하는 변수 목록입니다. Adobe Analytics 데이터 수집 쿼리 매개 변수에 대한 자세한 내용은 [Analytics 구현 안내서](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html)에서 확인할 수 있습니다.

| XDM 필드 경로 | [!DNL Analytics Query String] / HTTP 헤더 | 설명 |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement 컨텍스트 데이터 `c.a.appid` 매핑. |
| application.launches.value | c.a.launches | AppMeasurement 컨텍스트 데이터 `c.a.launches` 매핑. |
| commerce.checkouts.id | events | `scCheckout` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.checkouts.value | events | 구분 기호 `,`을 사용하여 전환 COMMERCE_SC_CHECKOUT을 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑입니다. |
| commerce.order.currencyCode | cc | AppMeasurement 쿼리 매개 변수 CURRENCY 매핑. |
| commerce.order.purchaseID | pi | AppMeasurement 쿼리 매개 변수 PURCHASEID 매핑입니다. |
| commerce.productListAdds.id | events | `scAdd` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.productListAdds.value | events | 구분 기호 `,`을 사용하여 전환 COMMERCE_SC_ADD를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑입니다. |
| commerce.productListOpens.id | events | `scOpen` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.productListOpens.value | events | 구분 기호 `,`을 사용하여 전환 COMMERCE_SC_OPEN을 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑입니다. |
| commerce.productListRemovals.id | events | `scRemove` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.productListRemovals.value | events | 구분 기호 `,`을 사용하여 전환 COMMERCE_SC_REMOVE를 사용하는 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑입니다. |
| commerce.productListViews.id | events | `scView` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.productListViews.value | events | 구분 기호 `,`을 사용하여 COMMERCE_SC_VIEW와 함께 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑을 수행합니다. |
| commerce.productViews.id | events | `prodView` 이벤트 직렬화. 이 필드가 제외되면(즉, 직렬화되지 않은 이벤트의 경우) 시스템에서 엔티티에 자체 ID 값을 생성하여 할당합니다. |
| commerce.productViews.value | events | 구분 기호 `,`를 사용하여 COMMERCE_PROD_VIEW를 사용하여 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑이 변환되는 AppMeasurement |
| commerce.purchases.value | events | 구분 기호 `,`를 사용하여 COMMERCE_PURCHASE와 함께 AppMeasurement 쿼리 매개 변수 EVENT_LIST_FULL 매핑을 수행합니다. |
| device.colorDepth | c | AppMeasurement 쿼리 매개 변수 C_COLOR 매핑입니다. |
| device.screenHeight | s | AppMeasurement 쿼리 매개 변수 화면 해상도 매핑입니다. |
| device.screenWidth | s | AppMeasurement 쿼리 매개 변수 화면 해상도 매핑입니다. |
| environment.browserDetails.acceptLanguage | Accept-Language | HTTP 헤더 매핑인 HEADER_ACCEPT_LANGUAGE입니다. |
| environment.browserDetails.cookiesEnabled | k | AppMeasurement 쿼리 매개 변수 COOKIES 매핑에 변환 BOOLEAN_TO_YN을 사용합니다. |
| environment.browserDetails.javaEnabled | v | AppMeasurement 쿼리 매개 변수 JAVA_ENABLED 매핑과 전환 BOOLEAN_TO_YN을 사용합니다. |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement 쿼리 매개 변수 J_JSCRIPT 매핑입니다. |
| environment.browserDetails.userAgent | User-Agent | HTTP 헤더 매핑인 HEADER_USER_AGENT입니다. |
| environment.browserDetails.viewportHeight | bh | AppMeasurement 쿼리 매개 변수 BROWSER_HEIGHT 매핑. |
| environment.browserDetails.viewportWidth | bw | AppMeasurement 쿼리 매개 변수 BROWSER_WIDTH 매핑. |
| environment.connectionType | ct | AppMeasurement 쿼리 매개 변수 CT_CONNECT_TYPE 매핑. |
| environment.ipV4 | X-Forwarded-For | HTTP 헤더 매핑이며, X-FORWARDED-FOR입니다. |
| identityMap.ECID.[0].id | mid | AppMeasurement 쿼리 매개 변수 MID 매핑입니다. |
| marketing.trackingCode | v0 | AppMeasurement 쿼리 매개 변수 CAMPAIGN 매핑입니다. |
| media.mediaTimed.completes.value | c.a.media.complete | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement 컨텍스트 데이터 `c.a.media.federated` 매핑. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseTime` 매핑. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement 컨텍스트 데이터 `c.a.media.pauseCount` 매핑. |
| media.mediaTimed.primaryAssetReference.@ID | c.a.media.asset | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement 컨텍스트 데이터 `c.a.media.friendlyName` 매핑. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name | c.a.media.originator | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement 컨텍스트 데이터 `c.a.media.episode` 매핑. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue | c.a.media.rating | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement 컨텍스트 데이터 `c.a.media.season` 매핑. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement 컨텍스트 데이터 `a.media.name` 매핑. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement 컨텍스트 데이터 `c.a.media.show` 매핑. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement 컨텍스트 데이터 `c.a.media.type` 매핑과 전환 STUDIO_SHOW_TYPE입니다. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement 컨텍스트 데이터 `c.a.media.type` 매핑과 전환 VIDEO_SHOW_TYPE입니다. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement 컨텍스트 데이터 `c.a.media.length` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.@ID | c.a.media.vsid | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement 컨텍스트 데이터 `c.a.media.channel` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement 컨텍스트 데이터 `c.a.contentType` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement 컨텍스트 데이터 `c.a.media.network` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement 컨텍스트 데이터 `c.a.media.segment` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement 컨텍스트 데이터 `c.a.media.playerName` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement 컨텍스트 데이터 `c.a.media.sdkVersion` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement 컨텍스트 데이터 `c.a.media.feed` 매핑. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement 컨텍스트 데이터 `c.a.media.format` 매핑. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement 컨텍스트 데이터 `c.a.media.resume` 매핑. |
| media.mediaTimed.starts.value | c.a.media.view | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | AppMeasurement 컨텍스트 데이터. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement 컨텍스트 데이터 `c.a.media.timePlayed` 매핑. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement 컨텍스트 데이터 `c.a.media.totalTimePlayed` 매핑. |
| placeContext.geo.latitude | 위도 | AppMeasurement 쿼리 매개 변수 LATITUDE 매핑입니다. |
| placeContext.geo.longitude | lon | AppMeasurement 쿼리 매개 변수 LONGITUDE 매핑입니다. |
| placeContext.geo.postalCode | zip | AppMeasurement 쿼리 매개 변수 ZIP 매핑. |
| placeContext.geo.stateProvince | state | AppMeasurement 쿼리 매개 변수 STATE 매핑입니다. |
| productlistitems[N]._[NAME_SPACE].* | products | AppMeasurement 쿼리 매개 변수 제품 상품 이벤트/Evar 매핑 . |
| productListItems[N].lineItemId | products | AppMeasurement 쿼리 매개 변수 제품 이름 매핑입니다. |
| productlistitems[N].name | products | AppMeasurement 쿼리 매개 변수 제품 카테고리 매핑입니다. |
| productlistitems[N].priceTotal | products | AppMeasurement 쿼리 매개 변수 제품 가격 매핑입니다. |
| productlistitems[N].quantity | products | AppMeasurement 쿼리 매개 변수 제품 수량 매핑입니다. |
| web.webInteraction.URL | pev1 | AppMeasurement 쿼리 매개 변수 PAGE_EVENT_VAR1 매핑입니다. |
| web.webInteraction.name | pev2 | AppMeasurement 쿼리 매개 변수 PAGE_EVENT_VAR2 매핑입니다. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` 대상:  `pe=lnk_o`  `web.webInteraction.type=download` 대상:  `pe=lnk_d`  `web.webInteraction.type=exit` to  `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement 쿼리 매개 변수 PAGE_URL 매핑. |
| web.webPageDetails.errorPage | pageType | AppMeasurement 쿼리 매개 변수 PAGE_TYPE_FULL 매핑과 변환 ERROR_PAGE_TYPE입니다. |
| web.webPageDetails.homePage | hp | AppMeasurement 쿼리 매개 변수 HOMEPAGE 매핑과 전환 BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | AppMeasurement 쿼리 매개 변수 PAGENAME 매핑입니다. |
| web.webPageDetails.server | sv | AppMeasurement 쿼리 매개 변수 USER_SERVER 매핑. |
| web.webPageDetails.siteSection | ch | AppMeasurement 쿼리 매개 변수 CHANNEL 매핑입니다. |
| web.webReferrer.URL | r | AppMeasurement 쿼리 매개 변수 REFERRER 매핑입니다. |

{style=&quot;table-layout:auto&quot;}
