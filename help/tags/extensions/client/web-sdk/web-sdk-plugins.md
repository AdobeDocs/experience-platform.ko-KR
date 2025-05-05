---
title: 일반 웹 SDK 플러그인 확장 프로그램 개요
description: Adobe Experience Platform의 일반적인 웹 SDK 플러그인 태그 확장 기능에 대해 알아봅니다.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# 일반 웹 SDK 플러그인 확장 프로그램 개요

>[!IMPORTANT]
>
>확장 프로그램은 Adobe Experience Platform 웹 SDK 확장 프로그램과 함께 사용됩니다. AppMeasurement에 사용할 버전에 대한 정보를 보려면 [일반적인 Analytics 플러그인 확장 프로그램](../plugins/overview.md)의 개요를 참조하십시오.

이 문서에서는 Web SDK 플러그인 태그 확장 기능을 구성하고 이를 사용하여 [Adobe Experience Platform Web SDK 확장 기능](../web-sdk/overview.md)을 확장하는 방법을 다룹니다.

## 일반 웹 SDK 플러그인 확장 프로그램 구성

이 섹션에서는 웹 SDK 플러그인 확장을 구성할 때 사용할 수 있는 옵션에 대한 참조를 제공합니다.

>[!IMPORTANT]
>
>일반 웹 SDK 플러그인 확장은 Adobe Experience Platform 웹 SDK 확장을 보강하기 위한 것입니다. 그러나 확장이 예상대로 작동하도록 하려면 해당 확장을 설치할 필요가 없습니다.

## Adobe Experience Platform Web SDK 확장에 플러그인 추가

일반 웹 SDK 플러그인 확장에서 제공하는 다음 기본 데이터 요소를 사용하는 외에 플러그인을 초기화하거나 라이브러리에 추가하는 구성은 필요하지 않습니다.

* [&#39;getAndPersistValue&#39;](#getAndPersistValue)
* [&#39;getGeoCoordinates&#39;](#getGeoCoordinates)
* [&#39;getNewRepeat&#39;](#getNewRepeat)
* [`getPagename`](#getPagename)
* [&#39;getPreviousValue&#39;](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [&#39;getTimeSinceLastVisit&#39;](#getTimeSInceLastVisit)
* [&#39;getValOnce&#39;](#getValOnce)
* [&#39;getVisitDuration&#39;](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [`pFo`](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정하고, 쿠키에 사용자 생성 값을 저장할 수 있도록 합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getAndPersistValue` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html?lang=ko)을 설정하고 구성할 수 있습니다. `getAndPersistValue` 데이터 요소는 방문 중에 나중에 검색할 수 있는 쿠키에 값을 저장합니다.

`getAndPersistValue` 데이터 요소는 다음 인수를 제공합니다.

* `vtp`(필수): 페이지에서 페이지로 유지할 값입니다.
* `cn`(선택 사항): 값을 저장할 쿠키의 이름입니다. 이 인수를 설정하지 않으면 쿠키의 이름이 `"s_gapv"`로 지정됩니다.
* `ex`(선택 사항): 쿠키가 만료될 때까지 남은 일 수입니다. 이 인수가 `0`이거나 설정되지 않으면 방문이 끝날 때(30분 동안 활동이 없음) 쿠키가 만료됩니다.

`vtp` 인수의 변수가 설정되면 데이터 요소는 쿠키를 설정한 다음 쿠키 값을 반환합니다. `vtp` 인수의 변수가 설정되지 않으면 데이터 요소는 쿠키 값만 반환합니다.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>이 플러그인은 클라이언트에서 위치 액세스가 필요하지만, 이를 얻지 못할 경우 예외를 throw하지 않습니다.

[`getGeoCoordinates` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html?lang=ko)을 설정하고 구성할 수 있습니다. `getGeoCoordinates` 데이터 요소는 방문자 장치의 위도와 경도를 캡처합니다.

`getGeoCoordinates` 데이터 요소는 인수를 사용하지 않습니다. 다음 값 중 하나를 반환합니다.

* `"geo coordinates not available"`: 플러그인이 실행되는 시점에 사용할 수 있는 지리적 위치 데이터가 없는 장치의 경우. 이 값은 방문의 첫 번째 히트에서 일반적입니다. 특히 방문자가 위치 추적에 대해 먼저 동의해야 할 때 사용됩니다.
* `"error retrieving geo coordinates"`: 장치의 위치를 검색하려고 할 때 플러그인에 오류가 발생하는 경우
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: 여기서 [LATITUDE]/[LONGITUDE]은 각각 위도와 경도입니다.

### `getNewRepeat`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getNewRepeat` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html?lang=ko)을 설정하고 구성할 수 있습니다. `getNewRepeat` 데이터 요소는 원하는 일 수 내에 사이트 방문자가 새 방문자인지 반복 방문자인지를 결정합니다.

`getNewRepeat` 데이터 요소는 다음 인수를 사용합니다.

* `d`(정수, 선택 사항): 방문자를 다시 `"New"`(으)로 재설정하기 위해 방문 사이에 필요한 최소 일 수입니다. 이 인수를 설정하지 않으면 기본값이 30일로 지정됩니다.

이 데이터 요소는 데이터 요소에 의해 설정된 쿠키가 없거나 만료된 경우 `"New"` 값을 반환합니다. 데이터 요소에 의해 설정된 쿠키가 있고 현재 히트 이후의 시간과 쿠키에 설정된 시간이 30분을 넘는 경우 `"Repeat"` 값을 반환합니다. 이 메서드는 전체 방문에 대해 동일한 값을 반환합니다.

### `getPageName`

[`getPageName` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html?lang=ko)을 설정하고 구성할 수 있습니다. `getPageName` 데이터 요소는 현재 URL의 읽기 쉽고 친숙한 형식의 버전을 만듭니다.

`getPageName` 데이터 요소는 다음 인수를 사용합니다.

* `si`(선택 사항, 문자열): 사이트의 ID를 나타내는 문자열 시작 부분에 삽입되는 ID입니다. 이 값은 숫자 ID나 친숙한 이름일 수 있습니다. 설정하지 않으면 기본값이 현재 도메인으로 설정됩니다.
* `qv`(선택 사항, 문자열): 쿼리 문자열 매개 변수의 쉼표로 구분된 목록으로서, URL에 있는 경우에는 문자열에 추가됩니다.
* `hv`(선택 사항, 문자열): URL 해시에 있는 매개 변수의 쉼표로 구분된 목록으로서, URL에 있는 경우에는 문자열에 추가됩니다.
* `de`(선택 사항, 문자열): 문자열의 개별 부분을 분할하는 구분 기호입니다. 기본값은 파이프(`|`)입니다.

데이터 요소는 URL의 친숙한 형식 버전을 포함하는 문자열을 반환합니다. 이 문자열은 일반적으로 `pageName` 변수에 할당되지만 다른 변수에서도 사용할 수 있습니다.

### `getPreviousValue`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정하고, 쿠키에 사용자 생성 값을 저장할 수 있도록 합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getPreviousValue` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html?lang=ko)을 설정하고 구성할 수 있습니다. `getPreviousValue` 데이터 요소는 변수를 이전 히트에 설정된 값으로 설정합니다.

`getPreviousValue` 데이터 요소는 다음 인수를 사용합니다.

* `v`(문자열, 필수): 다음 이미지 요청에 전달할 값이 있는 변수입니다. 이전 페이지 값을 검색하는 데 사용되는 일반적인 변수는 `s.pageName`입니다.
* `c`(문자열, 선택 사항): 값을 저장하는 쿠키의 이름입니다.  이 인수를 설정하지 않으면 기본값이 `"s_gpv"`(으)로 설정됩니다.

이 데이터 요소를 호출하면 쿠키에 포함된 문자열 값이 반환됩니다. 그러면 플러그인이 쿠키 만료를 재설정하고 여기에 `v` 인수의 변수 값을 지정합니다. 쿠키는 30분 동안 활동이 없으면 만료됩니다.

### `getQueryParam`

[`getQueryParam` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html?lang=ko)을 설정하고 구성할 수 있습니다. `getQueryParam` 데이터 요소는 URL에 포함된 모든 쿼리 문자열 매개 변수의 값을 추출합니다. 이 플러그인은 랜딩 페이지 URL에서 내부 및 외부의 캠페인 코드를 모두 추출하는 데 유용합니다. 검색어 또는 기타 쿼리 문자열 매개 변수를 추출할 때에도 유용합니다. 이 데이터 요소는 여러 쿼리 문자열 매개 변수를 포함하는 해시 및 URL을 포함하여 복잡한 URL을 구문 분석하는 데 강력한 기능을 제공합니다.

`getQueryParam` 데이터 요소는 다음 인수를 사용합니다.

* `qsp`(필수): URL 내에서 찾을 쿼리 문자열 매개 변수의 쉼표로 구분된 목록입니다. 대/소문자를 구분하지 않습니다.
* `de`(선택 사항): 여러 쿼리 문자열 매개 변수가 일치하는 경우 사용할 구분 기호입니다. 기본값은 빈 문자열입니다.
* `url`(선택 사항): 쿼리 문자열 매개 변수 값을 추출할 사용자 지정 URL, 문자열 또는 변수입니다. 기본값은 `window.location`입니다.

이 데이터 요소를 호출하면 위의 인수 및 URL에 따라 값이 반환됩니다.

* 일치하는 쿼리 문자열 매개 변수를 찾을 수 없으면 이 메서드는 빈 문자열을 반환합니다.
* 일치하는 쿼리 문자열 매개 변수를 찾으면 이 메서드는 쿼리 문자열 매개 변수 값을 반환합니다.
* 일치하는 쿼리 문자열 매개 변수를 찾았지만 값이 비어 있으면 이 메서드는 `true`을(를) 반환합니다.
* 일치하는 쿼리 문자열 매개 변수를 여러 개 찾으면 이 메서드는 `de` 인수의 문자열로 각 매개 변수 값이 구분된 문자열을 반환합니다.

### `getTimeParting`

[`getTimeParting` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=ko)을 설정하고 구성할 수 있습니다. `getTimeParting` 데이터 요소는 사이트에서 측정 가능한 활동이 발생하는 시간을 캡처합니다. 이 데이터 요소는 주어진 날짜 범위에서 반복 가능한 시간 분할로 지표를 분류하려는 경우 유용합니다. 예를 들어 모든 일요일과 모든 목요일 등 두 가지 서로 다른 요일 간의 전환율을 비교할 수 있습니다. 또한 아침과 저녁과 같은 하루 동안의 시간을 비교할 수 있습니다.

`getTimeParting` 데이터 요소는 다음 인수를 사용합니다.

`t`(선택 사항이지만 권장됨, 문자열): 방문자의 현지 시간을 변환하여 구할 시간대의 이름입니다.  기본값은 UTC/GMT 시간으로 설정됩니다. 유효한 값의 전체 목록은 Wikipedia의 [TZ 데이터베이스 시간대 목록](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)을 참조하십시오.

일반적인 유효 값은 다음과 같습니다.

* 동부 표준시 `"America/New_York"`
* 중부 표준시 `"America/Chicago"`
* 산지 시간의 `"America/Denver"`
* 태평양 표준시 `"America/Los_Angeles"`

이 데이터 요소를 호출하면 파이프(`|`)로 구분된 다음 내용을 포함하는 문자열이 반환됩니다.

* 올해
* 이번 달
* 날짜
* 요일
* 현재 시간(오전/오후)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getTimeSinceLastVisit` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html?lang=ko)을 설정하고 구성할 수 있습니다. `getTimeSinceLastVisit` 데이터 요소는 방문자가 마지막 방문 후 사이트를 다시 방문하는 시간을 추적합니다.

`getTimeSinceLastVisit` 데이터 요소는 인수를 사용하지 않습니다. 이 메서드는 방문자가 마지막으로 사이트를 방문한 이후 경과된 시간을 반환합니다(다음 형식으로 변환됨).

* 마지막 방문 이후 30분에서 1시간 사이의 시간이 가장 가까운 0.5분 벤치마크로 설정됩니다. 예: `"30.5 minutes"`, `"53 minutes"`
* 1시간과 1일 사이의 시간은 가장 가까운 1/4시간 벤치마크로 반올림됩니다. 예: `"2.25 hours"`, `"7.5 hours"`
* 하루보다 큰 시간은 가장 가까운 일 벤치마크로 반올림됩니다. 예: `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* 방문자가 전에 방문한 적이 없거나 경과 시간이 2년을 넘는 경우 값이 `"New Visitor"`(으)로 설정됩니다.

### `getValOnce`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정하고, 쿠키에 사용자 생성 값을 저장할 수 있도록 합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getValOnce` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html?lang=ko)을 설정하고 구성할 수 있습니다. `getValOnce` 데이터 요소를 사용하면 변수가 동일한 값에 두 번 이상 설정되지 않습니다.

`getValOnce` 데이터 요소는 다음 인수를 사용합니다.

* `vtc`(필수, 문자열): 변수가 이전에 동일한 값으로 설정되었는지 확인하는 변수입니다.
* `cn`(선택 사항, 문자열): 확인할 값이 들어 있는 쿠키의 이름입니다. 기본값은 `"s_gvo"`입니다.
* `et`(선택 사항, 정수): 쿠키의 만료 기간(`ep` 인수에 따라 일 또는 분 단위)입니다. 기본값은 `0`이며, 브라우저 세션이 끝날 때 만료됩니다.
* `ep`(선택 사항, 문자열): `et` 인수도 설정된 경우에만 이 인수를 설정하십시오. `et` 인수가 일 대신 분 단위로 만료되도록 하려면 이 인수를 `"m"`(으)로 설정하십시오. 기본값은 `"d"`이고, 이 값은 `et` 인수를 일 단위로 설정합니다.

`vtc` 인수와 쿠키 값이 일치하는 경우 이 메서드는 빈 문자열을 반환합니다. `vtc` 인수와 쿠키 값이 일치하지 않으면 이 메서드는 `vtc` 인수를 문자열로 반환합니다.

### `getVisitDuration`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getVisitDuration` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html?lang=ko)을 설정하고 구성할 수 있습니다. `getVisitDuration` 데이터 요소는 방문자가 해당 시점까지 사이트에 있었던 시간(분)을 추적합니다.

`getVisitDuration` 데이터 요소는 인수를 사용하지 않습니다. 다음 값 중 하나를 반환합니다.

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"`(여기서 `[x]`은(는) 방문자가 사이트에 도착한 이후 경과된 분 수입니다.)

### `getVisitNum`

>[!IMPORTANT]
>
>이 데이터 요소는 쿠키를 설정합니다. 자세한 내용은 플러그인 특정 설명서 를 참조하십시오.

[`getVisitNum` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html?lang=ko)을 설정하고 구성할 수 있습니다. `getVisitNum` 데이터 요소는 원하는 일 수 내에 사이트를 방문하는 모든 방문자에 대한 방문 횟수를 반환합니다.

`getVisitNum` 데이터 요소는 다음 인수를 사용합니다.

* `rp`(선택 사항, 정수 또는 문자열): 방문 횟수 카운터가 재설정되기 전 일 수입니다.  설정하지 않으면 기본값이 `365`(으)로 설정됩니다.
   * 이 인수가 `"w"`이면 카운터는 그 주가 끝날 때(이번 주 토요일 오후 11시 59분) 재설정됩니다.
   * 이 인수가 `"m"`이면 카운터는 그 달이 끝날 때(이번 달 마지막 날) 재설정됩니다.
   * 이 인수가 `"y"`이면 카운터는 한 해가 끝날 때(12월 31일) 재설정됩니다.
* `erp`(선택 사항, 부울): `rp` 인수가 숫자인 경우 이 인수는 방문 횟수 만료를 연장할지 여부를 결정합니다. `true`(으)로 설정하면 이후 사이트 히트가 방문 횟수 카운터를 재설정합니다. `false`(으)로 설정하면 방문 횟수 카운터가 재설정될 때 이후 사이트 히트가 연장되지 않습니다. 기본값은 `true`입니다. `rp` 인수가 문자열이면 이 인수는 유효하지 않습니다.

방문자가 30분 동안 활동이 없으면 사이트로 돌아올 때마다 방문 횟수가 증가합니다. 이 메서드를 호출하면 방문자의 현재 방문 횟수를 나타내는 정수가 반환됩니다.

### `p_fo`(첫 번째 페이지만)

[`p_fo` Analytics 플러그인](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html?lang=ko)을 설정하고 구성할 수 있습니다. `p_fo` 데이터 요소는 특정 JavaScript 개체가 있는지 확인하는 유틸리티입니다. 개체가 없으면 플러그인이 개체를 만들고 `true`을(를) 반환합니다. JavaScript 개체가 페이지에 이미 있으면 `false`을(를) 반환합니다. 이 데이터 요소는 페이지에서 코드를 정확히 한 번 실행하는 데 유용합니다.

`p_fo` 데이터 요소는 다음 인수를 사용합니다.

* `on`(필수, 문자열): 개체가 페이지에 아직 없을 경우 데이터 요소가 만드는 JavaScript 개체의 이름입니다.

개체가 아직 없으면 이 메서드는 `true`을(를) 반환하고 개체를 만듭니다. 개체가 이미 있으면 이 메서드는 `false`을(를) 반환합니다.
