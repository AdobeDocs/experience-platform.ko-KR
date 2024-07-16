---
title: Adobe Analytics 확장 개요
description: Adobe Experience Platform의 Adobe Analytics 태그 확장 기능에 대해 알아봅니다.
exl-id: 33ebdcb6-9bf0-44e6-b016-e93fe78af578
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 81%

---

# Adobe Analytics 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe Analytics 확장 구성 및 이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

## Adobe Analytics 확장 구성

이 섹션에서는 Adobe Analytics 확장을 구성할 때 사용할 수 있는 옵션에 대한 참조를 제공합니다.

Adobe Analytics 확장이 아직 설치되지 않은 경우 속성을 연 다음, **[!UICONTROL 확장 > 카탈로그]**&#x200B;를 선택하고 Adobe Analytics 확장을 마우스로 가리킨 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

확장을 구성하려면 Extensions 탭을 열고 확장을 마우스로 가리킨 다음 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![](../../../images/ext-analytics-config.png)

## 라이브러리 관리

구성 페이지의 Library Management 섹션에서 옵션을 선택합니다. 다음 구성 옵션을 사용할 수 있습니다.

### Manage the library for me

#### 보고서 세트

다음 각 환경에 대해 하나 이상의 보고서 세트를 지정합니다.

* 개발
* 스테이징
* 프로덕션

### 페이지에 이미 설치된 라이브러리 사용

#### 추적기에서 다음 보고서 세트 설정

이 옵션을 선택하는 경우 다음 각 환경에 대해 하나 이상의 보고서 세트를 지정합니다.

* 개발
* 스테이징
* 프로덕션

#### 활동 맵 모듈 사용

활동 맵은 AAM 모듈과 같은 별도의 모듈로 로드됩니다. 기본적으로 활동 맵이 켜져 있지만 비활성화하려는 경우, 구성의 상자 선택을 취소하여 설정할 수 있습니다.

#### 추적기는 명명된 글로벌 변수에서 액세스 가능함

이 상자를 선택하면 추적기 개체를 전체적으로 사용할 수 있습니다. 예를 들어 사이트의 어디에나 `window.s.pageName` 변수를 정의할 수 있습니다.

### 사용자 지정 URL에서 라이브러리 로드

#### HTTP URL

라이브러리가 있는 URL을 지정합니다.

#### HTTPS URL

라이브러리가 있는 URL을 지정합니다.

#### 추적기에서 다음 보고서 세트 설정

이 옵션을 선택하는 경우 다음 각 환경에 대해 하나 이상의 보고서 세트를 지정합니다.

* 개발
* 스테이징
* 프로덕션

#### 추적기는 명명된 글로벌 변수에서 액세스 가능함

전체적으로 사용할 추적기 개체를 지정합니다.

### 사용자 지정 라이브러리 코드를 제공할 수 있음

#### 편집기 열기

코어 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko-KR) 코드를 삽입할 수 있습니다. 이 코드는 자동 구성 메서드를 사용할 때 자동으로 입력됩니다.

>[!NOTE]
>
>태그 코드 편집기에 사용된 유효성 검사기는 개발자가 작성한 코드의 문제를 확인하도록 설계되었습니다. 축소 프로세스를 거친 코드(예: 코드 관리자에서 다운로드한 AppMeasurement.js 코드)는 태그 유효성 검사기에 문제가 있는 것으로 플래그가 잘못 지정될 수 있으며, 일반적으로 이 오류는 무시할 수 있습니다.

#### 추적기에서 다음 보고서 세트 설정

이 옵션을 선택하는 경우 다음 각 환경에 대해 하나 이상의 보고서 세트를 지정합니다.

* 개발
* 스테이징
* 프로덕션

#### 추적기는 명명된 글로벌 변수에서 액세스 가능함

전체적으로 사용할 추적기 개체를 지정합니다.

## 일반

구성 페이지의 General 섹션에서 옵션을 선택합니다. 다음 구성 옵션을 사용할 수 있습니다.

### Adobe Analytics에 대한 EU 규정 준수 활성화

EU 개인 정보 쿠키를 기반으로 추적을 활성화 또는 비활성화합니다.

EU 규정 준수 확인란을 선택하면 [!UICONTROL 추적 쿠키 이름] 필드가 나타납니다. 추적 쿠키는 기본 추적 쿠키 이름을 무시합니다. 태그가 다른 쿠키를 받기 위해 옵트아웃 상태를 추적하는 데 사용하는 이름을 사용자 지정할 수 있습니다.

페이지가 로드될 때 시스템에서는 sat\_track이라는 쿠키가 설정되어 있는지(또는 속성 편집 페이지에 지정된 사용자 지정 쿠키 이름) 확인합니다. 다음 정보를 고려하십시오.

* 쿠키가 없거나 쿠키가 있고 true를 제외한 다른 값으로 설정된 경우 이 설정을 활성화하면 도구 로드가 생략됩니다. 이것은 그 도구를 사용하는 규칙의 어떠한 부분도 적용되지 않음을 의미합니다. 규칙에 EU 규정 준수하는 분석과 타사 코드가 있고 쿠키가 false로 설정되어 있으면 타사 코드가 실행됩니다. 하지만 분석 변수는 설정되지 않습니다.
* 쿠키가 있지만 true로 설정되면 도구가 정상적으로 로드됩니다.

방문자가 옵트아웃하면 sat\_track(또는 사용자 지정 이름이 지정된) 쿠키를 false로 설정해야 합니다. 사용자 지정 코드를 사용하여 다음을 완수할 수 있습니다.

```javascript
_satellite.cookie.set("sat_track", "false");
```

방문자가 나중에 옵트인할 수 있도록 하려면 해당 쿠키를 true로 설정하는 메커니즘이 있어야 합니다.

```javascript
_satellite.cookie.set("sat_track", "true");
```

### 문자 집합

이미지 요청이 인코딩되는 방식을 결정합니다. 구현이나 사이트에서 ASCII가 아닌 문자를 사용하는 경우 여기에 문자 집합을 정의하는 것이 중요합니다. 사전 설정된 문자 집합을 선택하거나 사용자 지정 문자 집합을 지정할 수 있습니다. 사이트와 동일한 문자 코딩을 사용하는 것이 좋습니다. 일반적으로 이 값은 UTF-8입니다.

문자 집합은 `s.charSet` 변수를 사용하여 Analytics 사용자 지정 코드에 설정할 수 있습니다.
문자 집합에 대한 자세한 내용은 [charSet 설명서](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html)를 참조하십시오.

### 통화 코드

수익과 통화 이벤트에 적용할 전환율을 결정합니다. 사이트에서 방문자가 여러 통화로 구매할 수 있는 경우 통화 코드를 설정하면 금액이 올바르게 변환되고 저장됩니다.

지원되는 통화 코드에 대한 자세한 내용은 [currencyCode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html)를 참조하십시오.

### 추적 서버

자사 쿠키 구현에서 자사 쿠키가 저장되는 위치를 나타내는 데 사용됩니다. Experience Cloud ID 서비스를 사용하는 경우 이 필드를 채우지 않는 것이 좋습니다.

추적 서버는 `s.trackingServer` 변수를 사용하여 Analytics 사용자 지정 코드에 설정할 수 있습니다.

Adobe Analytics 구현 안내서의 [trackingServer](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html)를 참조하십시오.

### SSL 추적 서버

SSL 자사 쿠키 구현에서 자사 쿠키가 저장되는 위치를 나타내는 데 사용됩니다. Experience Cloud ID 서비스를 사용하는 경우 이 필드를 채우지 않는 것이 좋습니다. 정의되지 않은 경우 SSL 데이터는 추적 서버를 사용합니다.

SSL 추적 서버는 `s.trackingServerSecure` 변수를 사용하여 Analytics 사용자 지정 코드에 설정할 수 있습니다.

[trackingServerSecure](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html)를 참조하십시오.

## 전역 변수

이 섹션을 사용하여 [eVar 및 Prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html)을 설정하고 계층을 만듭니다.

글로벌 변수는 페이지에서 Analytics 추적 개체가 초기화될 때 해당 개체에 설정되는 변수입니다. 여기서 설정한 모든 변수는 추적 개체가 각 페이지에서 만들어질 때 설정됩니다. 이러한 변수가 설정되면 다른 방법으로 설정된 다른 변수와 같습니다. 즉, 규칙이 이러한 변수를 수정하거나, 변경하거나, 지울 수 있습니다.

웹 애플리케이션이 일반적으로 페이지당 한 개의 비콘을 전송하는 경우 이 섹션을 통해 한 곳에 변수를 편리하게 설정할 수 있습니다. 애플리케이션이 페이지당 두 개 이상의 비콘을 전송하는 경우(예: 단일 페이지 애플리케이션) 변수를 지우고 동일한 추적 개체를 사용하여 재설정해야 하면 규칙을 사용하여 변수를 설정하고 지우는 것이 더 쉽습니다.

## 링크 추적

구성 페이지의 링크 추적 섹션에서 옵션을 선택합니다. 다음 구성 옵션을 사용할 수 있습니다.

### ClickMap 활성화

[ClickMap은 Internet Explorer와 Firefox용 플러그인이며 Reports &amp; Analytics의 한 모듈입니다.](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html)

### 다운로드 링크 추적

사이트에서 다운로드 가능한 파일을 연결하는 링크를 추적합니다.

[s.trackDownLoadLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html)를 참조하십시오.

### 확장 기능 다운로드

Track Download Links 옵션이 활성화되어 있으면 다운로드 보고서에 포함된 파일 링크의 확장자를 선택할 수 있습니다. 사이트에 나열된 확장자가 있는 파일에 대한 링크가 포함되어 있으면 이러한 링크의 URL이 보고에 나타납니다.

[s.linkDownloadFileTypes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html)를 참조하십시오.

### 아웃바운드 링크 추적

선택한 링크가 종료 링크인지 여부를 결정합니다.

[s.trackExternalLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html)를 참조하십시오.

**단일 페이지 앱 고려 사항:**&#x200B;일부 SPA 웹 사이트의 코딩 방식 때문에 SPA 사이트의 페이지에 대한 내부 연결이 아웃바운드 링크로 보일 수 있습니다.

다음 방법 중 하나를 사용해 SPA 사이트에서 유래한 아웃바운드 링크를 추적할 수 있습니다.

* SPA의 아웃바운드 링크를 추적하지 않으려면 추적 안 함 섹션에 항목을 삽입합니다.  예, `http://testsite.com/spa/\#`. 이 호스트에 대한 모든 \# 링크는 무시됩니다. 다른 호스트에 대한 모든 아웃바운드 링크는 추적됩니다(예: [https://www.google.com](https://www.google.com)).
* SPA에서 추적하려는 링크가 있으면 항상 추적 섹션을 사용합니다.

예를 들어 spa/\#/about 페이지가 있으면 Always Track 섹션에 &quot;about&quot;을 삽입할 수 있습니다.

about 페이지는 유일하게 추적되는 아웃바운드 링크이며 페이지의 다른 모든 링크(예: [https://www.google.com](https://www.google.com))는 추적되지 않습니다.

>[!NOTE]
>
>이 두 옵션은 상호적으로 사용할 수 없습니다.

### URL 매개 변수 유지

쿼리 문자열을 유지합니다.

[s.linkLeaveQueryString](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html)을 참조하십시오.

## 쿠키

Adobe Analytics 확장 배포에 사용되는 쿠키 글로벌 설정에 대한 필드 설명을 구성합니다. 다음 구성 옵션을 사용할 수 있습니다.

### 방문자 ID

온라인과 오프라인 시스템 모두에서 고객을 나타내는 고유한 값입니다.

[visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=ko-KR)를 참조하십시오.

### 방문자 네임스페이스

쿠키가 설정된 도메인을 식별하는 변수입니다.

[visitorNamespace](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html)를 참조하십시오.

### 도메인 점 수

페이지 URL의 도메인에 있는 점의 수를 파악하여 Analytics 쿠키 `s_cc` 및 `s_sq`가 설정되는 도메인. 이 변수는 일부 플러그인에서 플러그인의 쿠키를 설정할 올바른 도메인을 결정할 때 사용하기도 합니다.

[s.cookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html)를 참조하십시오.

### 자사 도메인 점 수

`fpCookieDomainPeriods` 변수는 구현에 타사 2o7.net 또는 omtrdc.net 도메인을 사용하는 경우에도 기본적으로 자사 쿠키인 JavaScript 설정 쿠키(`s_sq`, `s_cc`, 플러그인)에 사용됩니다.

[s.fpCookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html)를 참조하십시오.

### 쿠키 수명

쿠키의 수명을 결정합니다.

[s.cookieLifetime](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html)을 참조하십시오.

### 보안 쿠키

이 변수를 사용하면 AppMeasurement에서 보안 쿠키를 작성할 수 있습니다.

[writeSecureCookies](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html)를 참조하십시오.


## 페이지 코드 사용자 지정

편집기를 사용하여 페이지 코드를 사용자 지정합니다.

## Adobe Audience Manager

확장 구성의 이 섹션을 사용하여 Audience Manager에서 Analytics를 사용하는 방법을 지정합니다.

**Automatically share Analytics data with Audience Manager**&#x200B;를 활성화합니다.

다음 옵션이 표시됩니다.

![](../../../images/an-ext-aam.png)

Audience Manager 하위 도메인은 Adobe Audience Manager에 의해 지정됩니다. 경우에 따라 &quot;파트너 이름&quot; 또는 &quot;파트너 하위 도메인&quot;이라고도 합니다. 파트너 이름을 모르는 경우 Adobe 컨설턴트나 고객 지원에 문의하십시오.

**고급 설정 표시**&#x200B;를 선택하고 기본 설정을 입력하여 고급 설정을 구성할 수 있습니다.

![](../../../images/an-ext-aam-adv.png)

각 설정에 대한 자세한 내용을 보려면 정보 아이콘을 선택하거나 [Adobe Audience Manager 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)를 참조하십시오.

## Analytics 확장 작업 유형

이 섹션에서는 Analytics 확장에서 사용할 수 있는 작업 유형을 설명합니다.

Analytics 확장은 다음 작업을 제공합니다.

* [변수 설정](#set-variables)
* [비콘 보내기](#send-beacon)
* [변수 지우기](#clear-variables)

### 변수 설정 {#set-variables}

중요: &quot;변수 설정&quot; 작업을 사용하면 비콘이 전송되지 않습니다. 비콘 보내기 작업을 사용해야 합니다.

#### eVar

[eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html)를 한 개 이상 설정합니다.

1. 드롭다운에서 eVar를 선택합니다.
1. eVar를 값으로 설정할지(Set As) 아니면 다른 eVar를 복사할지(Duplicate From) 지정합니다.
1. Set As 값을 제공하거나 복제할 eVar를 선택합니다.
1. (선택 사항) Add eVar를 선택하여 더 많은 eVar를 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

#### Prop

[prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html)을 한 개 이상 설정합니다.

1. 드롭다운에서 prop을 선택합니다.
1. prop을 값으로 설정할지(Set As) 아니면 다른 eVar를 복사할지(Duplicate From) 지정합니다.
1. Set As 값을 제공하거나 prop을 복제할 eVar를 선택합니다.
1. (선택 사항) 더 많은 prop을 설정하려면 **[!UICONTROL prop 추가]**&#x200B;를 선택하십시오.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

#### 이벤트

[이벤트](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html)를 한 개 이상 설정합니다.

1. 드롭다운에서 이벤트를 선택합니다.
1. (선택 사항) [이벤트 일련화](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html)에 사용되는 데이터 요소를 선택하거나 지정합니다.
1. (선택 사항) 더 많은 이벤트를 설정하려면 **[!UICONTROL 이벤트 추가]**&#x200B;를 선택하십시오.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

#### 계층

Analytics [계층](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html) 변수를 설정합니다.

계층에서 각 수준을 지정합니다.

원하는 경우 추가 계층을 구성합니다.

#### 페이지 이름

이 값은 지정된 페이지의 이름을 참조하며 Analytics의 [`pageName` 변수](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/pagename.html)에 해당합니다.

>[!IMPORTANT]
>
>Adobe Experience Manager 구현에서 이 변수는 AEM에 가져온 Analytics 보고서를 저장할 위치를 알려줍니다. 보고서가 제대로 유지되도록 하려면 페이지 이름 문자열 형식을 사이트에 대한 콜론으로 구분된 경로로 지정해야 합니다.
>
>예를 들어 `content/we-retail/language-masters/en/men.html`의 웹 페이지는 `content:we-retail:language-masters:en:men`의 페이지 이름 값을 가져야 합니다.

#### 기타 정보

페이지에서 사용하는 기타 정보를 지정합니다.

이러한 설정은 다음과 같습니다.

* 페이지 URL
* 서버
* 채널
* 레퍼러
* 캠페인
* 구매 ID

  값 또는 쿼리 매개 변수 지정

* 주/도
* Zip
* 거래 ID

이러한 설정은 &quot;추가 설정&quot; 확인란을 선택하여 &quot;전역 변수&quot; 메뉴에서 찾을 수 있습니다.

#### 사용자 지정 페이지 코드

**설명**

편집기를 사용하여 사용자 지정 페이지 코드를 지정합니다.

**설정**

1. **[!UICONTROL 편집기 열기]**&#x200B;를 선택합니다.
1. 사용자 지정 코드를 입력합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### 비콘 보내기 {#send-beacon}

#### Increment a pageview - s.t()

페이지 보기를 증가시키려는 경우 선택합니다.

#### 페이지 보기 - s.tl()을 증가시키지 마십시오.

페이지 보기를 증가시키지 않으려는 경우 선택합니다.

**설정**

1. 링크 유형을 선택합니다.

   다음 중 하나를 선택할 수 있습니다.

   * 사용자 지정 링크
   * 다운로드 링크
   * 종료 링크

1. 선택한 링크에 대한 매개 변수를 설정합니다.
   * Custom Link: 링크 이름을 지정합니다.
   * Download Link: 파일 이름을 지정합니다.
   * Exit Link: 대상 URL를 지정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

### 변수 지우기 {#clear-variables}

변수 지우기 작업 유형을 선택한 경우 구성 옵션이 없습니다.
