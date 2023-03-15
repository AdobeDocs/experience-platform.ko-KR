---
keywords: Experience Platform;홈;인기 항목;Analytics 매핑 필드;Analytics 매핑
solution: Experience Platform
title: Adobe Analytics 소스 커넥터에 대한 매핑 필드
description: Adobe Experience Platform을 사용하면 Analytics 소스를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. ADC를 통해 수집된 데이터 중 일부는 Analytics 필드에서 직접 XDM(Experience Data Model) 필드로 매핑될 수 있지만 다른 데이터가 성공적으로 매핑되려면 변환 및 특정 함수가 필요합니다.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 15%

---

# Analytics 필드 매핑

Adobe Experience Platform을 사용하면 Analytics 소스를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. ADC를 통해 수집된 데이터 중 일부는 Analytics 필드에서 직접 XDM(Experience Data Model) 필드로 매핑될 수 있지만 다른 데이터가 성공적으로 매핑되려면 변환 및 특정 함수가 필요합니다.

![](../images/analytics-data-experience-platform.png)

## 직접 매핑 필드

선택 필드는 Adobe Analytics에서 XDM(Experience Data Model)으로 직접 매핑됩니다.

다음 표에는 Analytics 필드( )의 이름을 보여 주는 열이 포함되어 있습니다.*Analytics 필드*), 해당 XDM 필드(*XDM 필드*) 및 그 유형(*XDM 유형*)와 필드 설명(*설명*).

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 문자열 | 사용자 지정 변수입니다. 범위는 1-250입니다. 각 조직은 이러한 사용자 정의 eVar를 다르게 사용합니다. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 문자열 | 사용자 지정 트래픽 변수 (1~75까지 가능) |
| m_browser | _experience.analytics.environment.browserID | 정수 | 브라우저의 번호 ID입니다. |
| m_browser_height | environment.browserDetails.viewportHeight | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| m_browser_width | environment.browserDetails.viewportWidth | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| m_campaign | marketing.trackingCode | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| m_channel | web.webPageDetails.siteSection | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| m_domain | environment.domain | 문자열 | 도메인 차원에 사용되는 변수입니다. 이는 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| m_geo_city | placeContext.geo.city | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| m_geo_dma | placeContext.geo.dmaID | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| m_geo_region | placeContext.geo.stateProvince | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| m_geo_zip | placeContext.geo.postalCode | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| m_keywords | search.keywords | 문자열 | 키워드 차원에 사용되는 변수입니다. |
| m_os | _experience.analytics.environment.operatingSystemID | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| m_page_url | web.webPageDetails.URL | 문자열 | 페이지 조회수의 URL입니다. |
| m_pagename_no_url | web.webPageDetails.</span>이름 | 문자열 | 페이지 차원을 채우는 데 사용되는 변수입니다. |
| m_referrer | web.webReferrer.URL | 문자열 | 이전 페이지의 페이지 URL. |
| m_search_page_num | search.pageDepth | 정수 | 모든 검색 페이지 등급 차원에 사용됩니다. 사용자가 사이트에 클릭 스루하기 전에 사이트가 표시된 검색 결과 페이지를 나타냅니다. |
| m_state | _experience.analytics.customDimensions.stateProvince | 문자열 | 상태 변수입니다. |
| m_user_server | web.webPageDetails.server | 문자열 | 서버 차원에 사용되는 변수입니다. |
| m_zip | _experience.analytics.customDimensions.postalCode | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| accept_language | environment.browserDetails.acceptLanguage | 문자열 | Accept-Language HTTP 헤더에 표시된 대로 모든 수락된 언어를 나열합니다. |
| homepage | web.webPageDetails.isHomePage | 부울 | 더 이상 사용되지 않습니다. 현재 URL이 브라우저의 홈 페이지인 경우 표시됩니다. |
| ipv6 | environment.ipV6 | 문자열 |
| j_jscript | environment.browserDetails.javaScriptVersion | 문자열 | 브라우저가 지원하는 JavaScript 버전입니다. |
| user_agent | environment.browserDetails.userAgent | 문자열 | HTTP 헤더에서 전송된 사용자 에이전트 문자열입니다. |
| mobileappid | 응용 프로그램.</span>이름 | 문자열 | 다음 형식으로 저장된 모바일 앱 ID입니다. `[AppName][BundleVersion]`. |
| mobiledevice | device.model | 문자열 | 모바일 장치의 이름입니다. iOS에서는 쉼표로 구분된 2자리 문자열로 저장됩니다. 첫 번째 숫자는 디바이스 생성을 나타내고 두 번째 숫자는 디바이스 제품군을 나타냅니다. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>이름 | 문자열 | 모바일 서비스에서 사용됩니다. 관심 영역을 나타냅니다. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 숫자 | 모바일 서비스에서 사용됩니다. 관심 영역 거리를 나타냅니다. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 숫자 | 컨텍스트 데이터 변수 a.loc.acc에서 수집됩니다. 수집 시 GPS의 정확도를 미터 단위로 나타냅니다. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 문자열 | 컨텍스트 데이터 변수 a.loc.category에서 수집됩니다. 특정 위치의 카테고리를 설명합니다. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 문자열 | 컨텍스트 데이터 변수 a.loc.id에서 수집됩니다. 지정된 관심 영역에 대한 식별자입니다. |
| video | media.mediaTimed.primaryAssetReference._ID | 문자열 | 비디오의 이름입니다. |
| videoad | advertising.adAssetReference._ID | 문자열 | 광고 자산 식별자. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 문자열 | 비디오 콘텐츠 유형입니다. 모든 비디오 보기에 대해 자동으로 &quot;비디오&quot;로 설정됩니다. |
| videoadpod | advertising.adAssetViewDetails.adBreak._ID | 문자열 | 비디오 광고가 포함된 pod. |
| videoadinpod | advertising.adAssetViewDetails.index | 정수 | Pod에서 비디오 광고의 위치입니다. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 문자열 | 비디오 플레이어의 이름입니다. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 문자열 | 비디오 채널입니다. |
| videoadplayername | advertising.adAssetViewDetails.playerName | 문자열 | 비디오 광고 플레이어의 이름입니다. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._ID | 문자열 | 비디오 챕터의 이름 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 문자열 | 비디오 이름입니다. |
| videoadname | advertising.adAssetReference._dc.title | 문자열 | 비디오 광고의 이름입니다. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | 문자열 | 비디오 표시. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | 문자열 | 비디오 시즌. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | 문자열 | 비디오 에피소드. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 문자열 | 비디오 네트워크. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 문자열 | 비디오 표시 유형. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 문자열 | 비디오 광고 로드. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 문자열 | 비디오 피드 유형. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 숫자 | Mobile Services 비콘 Major. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 숫자 | Mobile Services 비콘 Minor. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 문자열 | Mobile Services 비콘 UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._ID | 문자열 | 비디오 세션 ID. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 배열 | 비디오 장르. | {title(객체), description(객체), type(객체), meta:xdmType(객체), items(문자열), meta:xdmField(객체)} |
| mobileinstalls | application.firstLaunches | 오브젝트 | 설치 또는 재설치 후 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| mobileupgrades | application.upgrades | 오브젝트 | 앱 업그레이드 수를 보고합니다. 업그레이드 후 또는 버전 번호가 변경될 때 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| mobilelaunches | application.launches | 오브젝트 | 앱을 시작한 횟수입니다. | {id (문자열), 값 (숫자)} |
| mobilecrashes | application.crashes | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| mobilemessageclicks | directMarketing.clicks | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videotime | media.mediaTimed.timePlayed | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videostart | media.mediaTimed.impressions | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videocomplete | media.mediaTimed.completes | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoadstart | advertising.impressions | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoadcomplete | advertising.completes | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoadtime | advertising.timePlayed | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoplay | media.mediaTimed.starts | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videototaltime | media.mediaTimed.totalTimePlayed | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 오브젝트 | 비디오 품질 시작 시간입니다. | {id (문자열), 값 (숫자)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 오브젝트 | 비디오 품질 버퍼 카운트 | {id (문자열), 값 (숫자)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 오브젝트 | 비디오 품질 버퍼 시간 | {id (문자열), 값 (숫자)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 오브젝트 | 비디오 품질 변경 카운트 | {id (문자열), 값 (숫자)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 오브젝트 | 비디오 품질 평균 비트 전송률 | {id (문자열), 값 (숫자)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 오브젝트 | 비디오 품질 오류 카운트 | {id (문자열), 값 (숫자)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoprogress10 | media.mediaTimed.progress10 | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoprogress25 | media.mediaTimed.progress25 | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoprogress50 | media.mediaTimed.progress50 | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoprogress75 | media.mediaTimed.progress75 | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoprogress95 | media.mediaTimed.progress95 | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videoresume | media.mediaTimed.resumes | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videopausecount | media.mediaTimed.pauses | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videopausetime | media.mediaTimed.pauseTime | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 정수 |

{style="table-layout:auto"}

## 매핑 필드 분할

이러한 필드에는 단일 소스가 있지만 **복수** XDM 위치.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | 정수 | 모니터의 해상도를 나타내는 숫자 ID입니다. |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | 문자열 | 모바일 운영 체제 버전. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 정수 | 비디오 광고 길이. |

{style="table-layout:auto"}

## 생성된 매핑 필드

XDM에서 생성하려면 Adobe Analytics에서 직접 복사한 것 이상의 논리가 필요하며 ADC에서 오는 선택 필드를 변환해야 합니다.

다음 표에는 Analytics 필드( )의 이름을 보여 주는 열이 포함되어 있습니다.*Analytics 필드*), 해당 XDM 필드(*XDM 필드*) 및 그 유형(*XDM 유형*)와 필드 설명(*설명*).

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 오브젝트 | 사용자 지정 트래픽 변수, 1-75 범위 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 오브젝트 | 계층 변수에서 사용됩니다. 여기에는 | 구분된 값 목록입니다. | {values (배열), 구분 기호 (문자열)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 배열 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| m_color | device.colorDepth | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| m_cookies | environment.browserDetails.cookiesEnabled | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to40 .event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to70.event 01 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다. | {id (오브젝트), value (오브젝트)} |
| m_geo_country | placeContext.geo.countryCode | 문자열 | IP를 기반으로 하는, 히트가 발생한 국가의 약어입니다. |
| m_geo_latitude | placeContext.geo._schema.latitude | 숫자 | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | 숫자 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 부울 | Java 활성화 여부를 나타내는 플래그입니다. |
| m_latitude | placeContext.geo._schema.latitude | 숫자 | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | 숫자 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 이 변수에는 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL이 포함됩니다. |
| m_page_event_var2 | web.webInteraction.name | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 지정된 경우 링크의 사용자 지정 이름이 나열됩니다. |
| m_page_type | web.webPageDetails.isErrorPage | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용되는 변수입니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 숫자 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비어 있습니다. |
| m_paid_search | search.isPaid | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| m_product_list | productListItem[].items | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| m_ref_type | web.webReferrer.type | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다. 1은 사이트 내부를 의미하며, 2는 기타 웹 사이트를 의미하며, 3은 검색 엔진을 의미하며, 4는 하드 드라이브를 의미하며, 5는 USENET를 의미하며, 6은 입력/책갈피 표시(레퍼러 없음), 7은 이메일, 8은 JavaScript 없음, 9는 소셜 네트워크를 의미합니다. |
| m_search_engine | search.searchEngine | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| post_currency | commerce.order.currencyCode | 문자열 | 거래 중에 사용된 통화 코드입니다. |
| post_cust_hit_time_gmt | timestamp | 문자열 | 타임스탬프가 활성화된 데이터 세트에서만 사용됩니다. 이는 Unix 시간을 기준으로 와 함께 전송되는 타임스탬프입니다. |
| post_cust_visid | identityMap | 오브젝트 | 고객 방문자 ID입니다. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | 부울 | 고객 방문자 ID입니다. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | 문자열 | 고객 방문자 ID입니다. |
| post_visid_high + visid_low | identityMap | 오브젝트 | 방문에 대한 고유 식별자. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | 문자열 | 방문에 대한 고유 식별자. |
| post_visid_high | endUserIDs._experience.aaid.primary | 부울 | 방문을 고유하게 식별하기 위해 visid_low와 함께 사용됩니다. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | 문자열 | 방문을 고유하게 식별하기 위해 visid_low와 함께 사용됩니다. |
| post_visid_low | identityMap | 오브젝트 | 방문을 고유하게 식별하기 위해 visid_high와 함께 사용됩니다. |
| hit_time_gmt | receivedTimestamp | 문자열 | Unix 시간을 기반으로 한 히트의 타임스탬프입니다. |
| hitid_high + hitid_low | _ID | 문자열 | 히트를 식별하는 고유 식별자입니다. |
| hitid_low | _ID | 문자열 | 히트를 고유하게 식별하기 위해 hitid_high와 함께 사용됩니다. |
| ip | environment.ipV4 | 문자열 | 이미지 요청의 HTTP 헤더를 기반으로 한 IP 주소입니다. |
| j_jscript | environment.browserDetails.javaScriptEnabled | 부울 | 사용된 JavaScript 버전입니다. |
| mcvisid_high + mcvisid_low | identityMap | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| mcvisid_high | endUserIDs._experience.mcid.primary | 부울 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| mcvisid_low | identityMap | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | 문자열 | 히트 결합 ID. Analytics 필드 sdid_high 및 sdid_low 는 두 개(또는 그 이상) 수신 히트를 함께 연결하는 데 사용되는 보조 데이터 ID입니다. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 문자열 | Mobile Services 비콘 Proximity. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 정수 | 비디오 챕터의 이름입니다. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 정수 | 비디오의 길이입니다. |

{style="table-layout:auto"}

## 고급 매핑 필드

선택 필드(&quot;postvalues&quot;라고 함)를 Adobe Analytics 필드에서 XDM(Experience Data Model)으로 성공적으로 매핑하려면 먼저 고급 변환이 더 필요합니다. 이러한 고급 변환을 수행하려면 세션, 속성 및 중복 제거를 위해 Adobe Experience Platform 쿼리 서비스 및 사전 빌드된 함수(Adobe 정의 함수라고 함)를 사용해야 합니다.

쿼리 서비스를 사용하여 이러한 변환을 수행하는 방법에 대한 자세한 내용은 [Adobe 정의 함수](../../../../query-service/sql/adobe-defined-functions.md) 설명서를 참조하십시오.

다음 표에는 Analytics 필드( )의 이름을 보여 주는 열이 포함되어 있습니다.*Analytics 필드*), 해당 XDM 필드(*XDM 필드*) 및 그 유형(*XDM 유형*)와 필드 설명(*설명*).

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 문자열 | 사용자 지정 변수입니다. 범위는 1-250입니다. 각 조직은 이러한 사용자 정의 eVar를 다르게 사용합니다. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 문자열 | 사용자 지정 트래픽 변수 (1~75까지 가능) |
| post_browser_height | environment.browserDetails.viewportHeight | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| post_browser_width | environment.browserDetails.viewportWidth | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| post_캠페인 | marketing.trackingCode | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| post_channel | web.webPageDetails.siteSection | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | 문자열 | 설정된 경우 사용자 지정 방문자 ID입니다. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 문자열 | 방문자가 도달하는 첫 번째 페이지의 URL입니다. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 문자열 | 원래 시작 페이지 차원에 사용되는 변수입니다. 방문자의 시작 페이지에 대한 페이지 이름입니다. |
| post_keywords | search.keywords | 문자열 | 히트에 대해 수집된 키워드입니다. |
| post_page_url | web.webPageDetails.URL | 문자열 | 페이지 조회수의 URL입니다. |
| post_pagename_no_url | web.webPageDetails.name | 문자열 | 페이지 차원을 채우는 데 사용되는 변수입니다. |
| post_purchaseid | commerce.order.purchaseID | 문자열 | 구매를 고유하게 식별하는 데 사용되는 변수입니다. |
| post_referrer | web.webReferrer.URL | 문자열 | 이전 페이지의 URL. |
| post_state | _experience.analytics.customDimensions.stateProvince | 문자열 | 상태 변수입니다. |
| post_user_server | web.webPageDetails.server | 문자열 | 서버 차원에 사용되는 변수입니다. |
| post_zip | _experience.analytics.customDimensions.postalCode | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| 브라우저 | _experience.analytics.environment.browserID | 정수 | 브라우저의 숫자 ID입니다. |
| 도메인 | environment.domain | 문자열 | 도메인 차원에 사용되는 변수입니다. 이는 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | 문자열 | 방문자에 대한 첫 번째 참조 URL입니다. |
| geo_city | placeContext.geo.city | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| geo_dma | placeContext.geo.dmaID | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| geo_region | placeContext.geo.stateProvince | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| geo_zip | placeContext.geo.postalCode | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| os | _experience.analytics.environment.operatingSystemID | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| search_page_num | search.pageDepth | 정수 | 이 변수는 모든 검색 페이지 등급 차원에 사용되며 사이트의 검색 결과 중 어느 페이지가 검색되는지 나타냅니다 | 사용자가 사이트를 클릭스루하기 전에 표시되었습니다. |
| visit_keywords | _experience.analytics.session.search.keywords | 문자열 | 검색 키워드 차원에 사용되는 변수입니다. |
| visit_num | _experience.analytics.session.num | 정수 | 방문 횟수 차원에 사용되는 변수입니다. 1에서 시작하며 새 방문이 시작될 때마다 (사용자당) 증가합니다. |
| visit_page_num | _experience.analytics.session.depth | 정수 | 히트 깊이 차원에 사용되는 변수입니다. 이 값은 사용자가 생성할 각 히트에 대해 1씩 증가하며 각 방문 후에 재설정됩니다. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | 문자열 | 방문의 첫 번째 레퍼러입니다. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 정수 | 방문의 첫 번째 페이지 이름입니다. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 오브젝트 | 사용자 정의 트래픽 변수 1 - 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 오브젝트 | 계층 변수에서 사용되며 구분된 값 목록을 포함합니다. | {values (배열), 구분 기호 (문자열)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 배열 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to40 .event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to70.event 01 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다. | {id (오브젝트), value (오브젝트)} |
| post_java_enabled | environment.browserDetails.javaEnabled | 부울 | Java 활성화 여부를 나타내는 플래그입니다. |
| post_latitude | placeContext.geo._schema.latitude | 숫자 | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | 숫자 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 문자열 | 이미지 요청(표준 히트, 다운로드 링크, 종료 링크 또는 클릭한 사용자 지정 링크)에서 전송된 히트 유형입니다. |
| post_page_event | web.webInteraction.linkClicks.value | 숫자 | 이미지 요청(표준 히트, 다운로드 링크, 종료 링크 또는 클릭한 사용자 지정 링크)에서 전송된 히트 유형입니다. |
| post_page_event_var1 | web.webInteraction.URL | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL입니다. |
| post_page_event_var2 | web.webInteraction.name | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 링크의 사용자 지정 이름이 됩니다. |
| post_page_type | web.webPageDetails.isErrorPage | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용됩니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 숫자 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비어 있습니다. |
| post_product_list | productListItem[].items | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| post_search_engine | search.searchEngine | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| mvvar1_instances | .list.items[] | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| mvvar2_instances | .list.items[] | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
|  | mvvar3_instances | .list.items[] | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| 색상 | device.colorDepth | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 문자열 | 방문자의 첫 번째 레퍼러 유형을 나타내는 숫자 ID입니다. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 정수 | Unix 시간에서 방문자의 첫 번째 히트 타임스탬프입니다. |
| 지역_국가 | placeContext.geo.countryCode | 문자열 | IP를 기반으로 한, 히트가 발생한 국가의 약어입니다. |
| geo_latitude | placeContext.geo._schema.latitude | 숫자 | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | 숫자 | <!-- MISSING --> |
| paid_search | search.isPaid | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| ref_type | web.webReferrer.type | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다. |
| visit_paid_search | _experience.analytics.session.search.isPaid | 부울 | 방문의 첫 번째 히트가 유료 검색 히트에서 왔는지를 나타내는 플래그(1=유료, 0=유료 아님)입니다. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 문자열 | 방문의 첫 번째 레퍼러 유형을 나타내는 숫자 ID입니다. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | 문자열 | 방문의 첫 번째 검색 엔진에 대한 숫자 ID입니다. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | 정수 | Unix 시간에서 방문의 첫 번째 히트 타임스탬프입니다. |

{style="table-layout:auto"}