---
keywords: Analytics 매핑 필드;분석 매핑
solution: Experience Platform
title: Adobe Analytics 소스 커넥터에 대한 매핑 필드
description: Analytics 소스 커넥터를 사용하여 Adobe Analytics 필드를 XDM 필드에 매핑합니다.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 6cbd902c6a1159d062fb38bf124a09bb18ad1ba8
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 14%

---

# Analytics 필드 매핑

Adobe Experience Platform을 사용하면 Analytics 소스를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. ADC를 통해 수집된 데이터 중 일부는 Analytics 필드에서 직접 XDM(Experience Data Model) 필드로 매핑될 수 있지만 다른 데이터에는 성공적으로 매핑될 변환 및 특정 함수가 필요합니다.

![](../images/analytics-data-experience-platform.png)

## 직접 매핑 필드

선택 필드는 Adobe Analytics에서 XDM(Experience Data Model)으로 직접 매핑됩니다.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 문자열 | 사용자 지정 Analytics eVar. 각 조직은 eVar를 다르게 사용할 수 있습니다. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 문자열 | 사용자 지정 Analytics prop. 각 조직은 prop을 다르게 사용할 수 있습니다. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | 정수 | 브라우저의 번호 ID입니다. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| `m_campaign` | `marketing.trackingCode` | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| `m_channel` | `web.webPageDetails.siteSection` | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| `m_domain` | `environment.domain` | 문자열 | 도메인 차원에 사용되는 변수입니다. 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| `m_geo_city` | `placeContext.geo.city` | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_dma` | `placeContext.geo.dmaID` | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_region` | `placeContext.geo.stateProvince` | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_zip` | `placeContext.geo.postalCode` | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_keywords` | `search.keywords` | 문자열 | 키워드 차원에 사용되는 변수입니다. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| `m_page_url` | `web.webPageDetails.URL` | 문자열 | 페이지 조회수의 URL입니다. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | 문자열 | 페이지 이름이 있는 히트에서 1과 같습니다. 이 기능은 Adobe Analytics 페이지 보기 수 지표와 유사합니다. |
| `m_referrer` | `web.webReferrer.URL` | 문자열 | 이전 페이지의 페이지 URL. |
| `m_search_page_num` | `search.pageDepth` | 정수 | 모든 검색 페이지 등급 차원에 사용됩니다. 사용자가 사이트에 클릭 스루하기 전에 사이트가 표시된 검색 결과 페이지를 나타냅니다. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 문자열 | 상태 변수입니다. |
| `m_user_server` | `web.webPageDetails.server` | 문자열 | 서버 차원에 사용되는 변수입니다. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 문자열 | Accept-Language HTTP 헤더에 표시된 대로 모든 수락된 언어를 나열합니다. |
| `homepage` | `web.webPageDetails.isHomePage` | 부울 | 더 이상 사용되지 않습니다. 현재 URL이 브라우저의 홈 페이지인 경우 표시됩니다. |
| `ipv6` | `environment.ipV6` | 문자열 |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 문자열 | 브라우저가 지원하는 JavaScript 버전입니다. |
| `user_agent` | `environment.browserDetails.userAgent` | 문자열 | HTTP 헤더에서 전송된 사용자 에이전트 문자열입니다. |
| `mobileappid` | `application.name` | 문자열 | 다음 형식으로 저장된 모바일 앱 ID입니다. `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | 문자열 | 모바일 장치의 이름입니다. iOS에서는 쉼표로 구분된 2자리 문자열로 저장됩니다. 첫 번째 숫자는 디바이스 생성을 나타내고 두 번째 숫자는 디바이스 제품군을 나타냅니다. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 문자열 | 모바일 서비스에서 사용됩니다. 관심 영역을 나타냅니다. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 숫자 | 모바일 서비스에서 사용됩니다. 관심 영역 거리를 나타냅니다. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 숫자 | 컨텍스트 데이터 변수 a.loc.acc에서 수집됩니다. 수집 시 GPS의 정확도를 미터 단위로 나타냅니다. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 문자열 | 컨텍스트 데이터 변수 a.loc.category에서 수집됩니다. 특정 위치의 카테고리를 설명합니다. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 문자열 | 컨텍스트 데이터 변수 a.loc.id에서 수집됩니다. 지정된 관심 영역에 대한 식별자입니다. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | 문자열 | 비디오의 이름입니다. |
| `videoad` | `advertising.adAssetReference._id` | 문자열 | 광고 자산 식별자. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | 문자열 | 비디오 콘텐츠 유형입니다. 모든 비디오 보기에 대해 자동으로 &quot;비디오&quot;로 설정됩니다. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 문자열 | 비디오 광고가 포함된 pod. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | 정수 | Pod에서 비디오 광고의 위치입니다. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | 문자열 | 비디오 플레이어의 이름입니다. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | 문자열 | 비디오 채널입니다. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | 문자열 | 비디오 광고 플레이어의 이름입니다. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | 문자열 | 비디오 챕터의 이름 |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | 문자열 | 비디오 이름입니다. |
| `videoadname` | `advertising.adAssetReference._dc.title` | 문자열 | 비디오 광고의 이름입니다. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | 문자열 | 비디오 표시. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | 문자열 | 비디오 시즌. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | 문자열 | 비디오 에피소드. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | 문자열 | 비디오 네트워크. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | 문자열 | 비디오 표시 유형. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | 문자열 | 비디오 광고가 로드됩니다. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | 문자열 | 비디오 피드 유형. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 숫자 | Mobile Services 비콘 Major. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 숫자 | Mobile Services 비콘 Minor. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 문자열 | Mobile Services 비콘 UUID |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | 문자열 | 비디오 세션 ID. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | 배열 | 비디오 장르. | {title(객체), description(객체), type(객체), meta:xdmType(객체), items(문자열), meta:xdmField(객체)} |
| `mobileinstalls` | `application.firstLaunches` | 오브젝트 | 설치 또는 재설치 후 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| `mobileupgrades` | `application.upgrades` | 오브젝트 | 앱 업그레이드 수를 보고합니다. 업그레이드 후 또는 버전 번호가 변경될 때 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| `mobilelaunches` | `application.launches` | 오브젝트 | 앱을 시작한 횟수입니다. | {id (문자열), 값 (숫자)} |
| `mobilecrashes` | `application.crashes` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `mobilemessageclicks` | `directMarketing.clicks` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videotime` | `media.mediaTimed.timePlayed` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videostart` | `media.mediaTimed.impressions` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videocomplete` | `media.mediaTimed.completes` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoadstart` | `advertising.impressions` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoadcomplete` | `advertising.completes` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoadtime` | `advertising.timePlayed` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoplay` | `media.mediaTimed.starts` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 오브젝트 | 비디오 품질 시작 시간입니다. | {id (문자열), 값 (숫자)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 오브젝트 | 비디오 품질 버퍼 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 오브젝트 | 비디오 품질 버퍼 시간 | {id (문자열), 값 (숫자)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 오브젝트 | 비디오 품질 변경 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 오브젝트 | 비디오 품질 평균 비트 전송률 | {id (문자열), 값 (숫자)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 오브젝트 | 비디오 품질 오류 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoprogress10` | `media.mediaTimed.progress10` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoprogress25` | `media.mediaTimed.progress25` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoprogress50` | `media.mediaTimed.progress50` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoprogress75` | `media.mediaTimed.progress75` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoprogress95` | `media.mediaTimed.progress95` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videoresume` | `media.mediaTimed.resumes` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videopausecount` | `media.mediaTimed.pauses` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | 오브젝트 | <!-- MISSING --> | {id (문자열), 값 (숫자)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | 정수 |

{style="table-layout:auto"}

## 필드 분할 매핑

이러한 필드에는 단일 소스가 있지만 **복수** XDM 위치.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | 정수 | 모니터의 해상도를 나타내는 숫자 ID입니다. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | 문자열 | 모바일 운영 체제 버전. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | 정수 | 비디오 광고 길이. |

{style="table-layout:auto"}

## 생성된 매핑 필드

ADC에서 제공되는 선택 필드는 변환해야 하며 XDM에서 Adobe Analytics의 직접 복사본 이상의 로직이 생성되어야 합니다.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 오브젝트 | 목록 prop으로 구성된 사용자 지정 Analytics prop. 여기에는 구분된 값 목록이 포함되어 있습니다. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 오브젝트 | 계층 변수에서 사용됩니다. 여기에는 구분된 값 목록이 포함되어 있습니다. | {values (배열), 구분 기호 (문자열)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 배열 | 사용자 지정 분석 목록 변수입니다. 구분된 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| `m_color` | `device.colorDepth` | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다. | {id (오브젝트), value (오브젝트)} |
| `m_geo_country` | `placeContext.geo.countryCode` | 문자열 | IP를 기반으로 하는, 히트가 발생한 국가의 약어입니다. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 숫자 | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 숫자 | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 부울 | Java™이 활성화되어 있는지 여부를 나타내는 플래그입니다. |
| `m_latitude` | `placeContext.geo._schema.latitude` | 숫자 | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | 숫자 | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 이 변수에는 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL이 포함됩니다. |
| `m_page_event_var2` | `web.webInteraction.name` | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 지정된 경우 링크의 사용자 지정 이름이 나열됩니다. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용되는 변수입니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| `m_pagename_no_url` | `web.webPageDetails.name` | 숫자 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비워 둡니다. |
| `m_paid_search` | `search.isPaid` | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| `m_product_list` | `productListItems[].items` | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| `m_ref_type` | `web.webReferrer.type` | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다.<br/>`1`: 사이트 내부<br/>`2`: 기타 웹 사이트<br/>`3`: 검색 엔진<br/>`4`: 하드 드라이브<br/>`5`: USENET<br/>`6`: 입력/책갈피 표시(레퍼러 없음)<br/>`7`: 이메일<br/>`8`: JavaScript 없음<br/>`9`: 소셜 네트워크 |
| `m_search_engine` | `search.searchEngine` | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| `post_currency` | `commerce.order.currencyCode` | 문자열 | 거래 중에 사용된 통화 코드입니다. |
| `post_cust_hit_time_gmt` | `timestamp` | 문자열 | 타임스탬프가 활성화된 데이터 세트에서만 사용됩니다. UNIX® 시간을 기준으로 히트와 함께 전송된 타임스탬프입니다. |
| `post_cust_visid` | `identityMap` | 오브젝트 | 고객 방문자 ID입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 부울 | 고객 방문자 ID입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 문자열 | 고객 방문자 ID입니다. |
| `post_visid_high` + `visid_low` | `identityMap` | 오브젝트 | 방문에 대한 고유 식별자. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 문자열 | 방문에 대한 고유 식별자. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 부울 | 과 함께 사용됨 `visid_low` 방문을 고유하게 식별합니다. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 문자열 | 과 함께 사용됨 `visid_low` 방문을 고유하게 식별합니다. |
| `post_visid_low` | `identityMap` | 오브젝트 | 방문을 고유하게 식별하기 위해 visid_high와 함께 사용됩니다. |
| `hit_time_gmt` | `receivedTimestamp` | 문자열 | UNIX® 시간을 기반으로 한 히트의 타임스탬프입니다. |
| `hitid_high` + `hitid_low` | `_id` | 문자열 | 히트를 식별하는 고유 식별자입니다. |
| `hitid_low` | `_id` | 문자열 | 히트를 고유하게 식별하기 위해 hitid_high와 함께 사용됩니다. |
| `ip` | `environment.ipV4` | 문자열 | 이미지 요청의 HTTP 헤더를 기반으로 한 IP 주소입니다. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 부울 | 사용된 JavaScript 버전입니다. |
| `mcvisid_high` + `mcvisid_low` | identityMap | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| `mcvisid_high` + `mcvisid_low` | endUserID_experience.mcid.id | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 부울 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_low` | `identityMap` | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 문자열 | 히트 결합 ID. Analytics 필드 sdid_high 및 sdid_low 는 두 개(또는 그 이상) 수신 히트를 함께 연결하는 데 사용되는 보조 데이터 ID입니다. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 문자열 | Mobile Services 비콘 Proximity. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | 정수 | 비디오 챕터의 이름입니다. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | 정수 | 비디오의 길이입니다. |

{style="table-layout:auto"}

## 고급 매핑 필드

선택 필드(&quot;게시물 값&quot;이라고 함)에는 Adobe이 처리 규칙, VISTA 규칙 및 조회 테이블을 사용하여 값을 조정한 후의 데이터가 포함됩니다. 대부분의 게시물 값에는 사전 처리된 대응 항목이 있습니다. 조직은 사전 처리된 필드, 사후 처리된 필드 또는 둘 다를 사용할지 여부를 결정할 수 있습니다.

쿼리 서비스를 사용하여 이러한 변환을 수행하는 방법에 대한 자세한 내용은 [Adobe 정의 함수](/help/query-service/sql/adobe-defined-functions.md) ( 쿼리 서비스 사용 안내서)를 참조하십시오.

| Analytics 필드 | XDM 필드 | XDM 유형 | 설명 |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 문자열 | 사용자 지정 Analytics eVar. 각 조직은 eVar를 다르게 사용할 수 있습니다. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 문자열 | 사용자 지정 Analytics prop. 각 조직은 prop을 다르게 사용할 수 있습니다. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| `post_campaign` | `marketing.trackingCode` | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| `post_channel` | `web.webPageDetails.siteSection` | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | 문자열 | 설정된 경우 사용자 지정 방문자 ID입니다. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | 문자열 | 방문자가 도달하는 첫 번째 페이지의 URL입니다. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | 문자열 | 원래 시작 페이지 차원에 사용되는 변수입니다. 방문자의 시작 페이지에 대한 페이지 이름입니다. |
| `post_keywords` | `search.keywords` | 문자열 | 히트에 대해 수집된 키워드입니다. |
| `post_page_url` | `web.webPageDetails.URL` | 문자열 | 페이지 조회수의 URL입니다. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | 문자열 | 페이지 이름이 있는 히트에서 1과 같습니다. 이 기능은 Adobe Analytics 페이지 보기 수 지표와 유사합니다. |
| `post_purchaseid` | `commerce.order.purchaseID` | 문자열 | 구매를 고유하게 식별하는 데 사용되는 변수입니다. |
| `post_referrer` | `web.webReferrer.URL` | 문자열 | 이전 페이지의 URL. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 문자열 | 상태 변수입니다. |
| `post_user_server` | `web.webPageDetails.server` | 문자열 | 서버 차원에 사용되는 변수입니다. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | 정수 | 브라우저의 숫자 ID입니다. |
| `domain` | `environment.domain` | 문자열 | 도메인 차원에 사용되는 변수입니다. 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | 문자열 | 방문자에 대한 첫 번째 참조 URL입니다. |
| `geo_city` | `placeContext.geo.city` | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_dma` | `placeContext.geo.dmaID` | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_region` | `placeContext.geo.stateProvince` | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_zip` | `placeContext.geo.postalCode` | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| `search_page_num` | `search.pageDepth` | 정수 | 이 변수는 모든 검색 페이지 등급 차원에 사용되며 사이트의 검색 결과 중 어느 페이지가 검색되는지 나타냅니다 | 사용자가 사이트를 클릭스루하기 전에 표시되었습니다. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | 문자열 | 검색 키워드 차원에 사용되는 변수입니다. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | 정수 | 방문 횟수 차원에 사용되는 변수입니다. 1에서 시작하며 새 방문이 시작될 때마다 (사용자당) 증가합니다. |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | 정수 | 히트 깊이 차원에 사용되는 변수입니다. 이 값은 사용자가 생성할 각 히트에 대해 1씩 증가하며 각 방문 후에 재설정됩니다. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | 문자열 | 방문의 첫 번째 레퍼러입니다. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | 정수 | 방문의 첫 번째 페이지 이름입니다. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 오브젝트 | 목록 prop으로 구성된 사용자 지정 Analytics prop. 여기에는 구분된 값 목록이 포함되어 있습니다. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 오브젝트 | 계층 변수에서 사용되며 구분된 값 목록을 포함합니다. | {values (배열), 구분 기호 (문자열)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 배열 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다. | {id (오브젝트), value (오브젝트)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 부울 | Java™이 활성화되어 있는지 여부를 나타내는 플래그입니다. |
| `post_latitude` | `placeContext.geo._schema.latitude` | 숫자 | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | 숫자 | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | 문자열 | 이미지 요청(표준 히트, 다운로드 링크, 종료 링크 또는 클릭한 사용자 지정 링크)에서 전송된 히트 유형입니다. |
| `post_page_event` | `web.webInteraction.linkClicks.value` | 숫자 | 히트가 링크 클릭인 경우 1입니다. 이는 Adobe Analytics의 페이지 이벤트 지표와 유사합니다. |
| `post_page_event_var1` | `web.webInteraction.URL` | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL입니다. |
| `post_page_event_var2` | `web.webInteraction.name` | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 링크의 사용자 지정 이름입니다. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용됩니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| `post_pagename_no_url` | `web.webPageDetails.name` | 숫자 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비워 둡니다. |
| `post_product_list` | `productListItems[].items` | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| `post_search_engine` | `search.searchEngine` | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| `mvvar1_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `mvvar2_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `mvvar3_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `color` | `device.colorDepth` | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | 문자열 | 방문자의 첫 번째 레퍼러 유형을 나타내는 숫자 ID입니다. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | 정수 | UNIX® 시간에서 방문자의 첫 번째 히트 타임스탬프입니다. |
| `geo_country` | `placeContext.geo.countryCode` | 문자열 | IP를 기반으로 한, 히트가 발생한 국가의 약어입니다. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 숫자 | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 숫자 | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| `ref_type` | `web.webReferrer.type` | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 부울 | 방문의 첫 번째 히트가 유료 검색 히트에서 왔는지를 나타내는 플래그(1=유료, 0=유료 아님)입니다. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 문자열 | 방문의 첫 번째 레퍼러 유형을 나타내는 숫자 ID. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 문자열 | 방문의 첫 번째 검색 엔진에 대한 숫자 ID입니다. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 정수 | UNIX® 시간 내 방문의 첫 번째 히트 타임스탬프. |

{style="table-layout:auto"}