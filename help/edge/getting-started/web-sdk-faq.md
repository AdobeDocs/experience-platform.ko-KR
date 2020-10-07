---
title: 웹 SDK FAQ
seo-title: Adobe Experience Platform 웹 SDK FAQ
description: Adobe Experience Platform 웹 SDK에 대한 FAQ
seo-description: Adobe Experience Platform 웹 SDK에 대한 FAQ
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 2%

---


# Experience Cloud 핵심 서비스에 대한

이 FAQ에는 Adobe 웹 SDK에 대해 자주 묻는 질문이 포함되어 있습니다.

## Adobe Experience Platform 웹 SDK란?

Adobe Experience Platform 웹 SDK는 Adobe Experience Cloud 고객이 Experience Cloud의 다양한 서비스와 상호 작용할 수 있는 클라이언트측 JavaScript 라이브러리입니다.

XDM(솔루션 독립적인 방식)의 데이터를 Adobe Experience Platform Edge Network로 전송하여 데이터를 특정 포맷 및 대상으로 매핑하고 실시간으로 전송합니다.

**자세한 정보**[Adobe Summit 프레젠테이션](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform 웹 SDK는 이전 솔루션과 어떻게 다릅니까?

### Adobe Experience Platform SDK 이전

현재 각 개별 솔루션을 기반으로 다른 JavaScript 라이브러리를 배포해야 합니다.

* 각 솔루션에는 자체 JavaScript 라이브러리, 스키마 및 도메인이 있습니다.
* 이러한 라이브러리는 서로 연동되도록 만들어지지 않았습니다.
* 크로스 솔루션 및 Adobe Experience Platform 사용 사례에서는 이러한 서로 다른 라이브러리가 상호 종속되어 배포 마찰이 발생했습니다.

Adobe Experience Platform Launch을 통해 이러한 라이브러리를 최대한 쉽게 배포 및 관리할 수 있지만 다음과 같은 문제에 여전히 직면합니다.

* 라이브러리 크기(페이지의 Adobe 코드가 너무 많음)
* 성능(사이트를 로드하는 데 시간이 너무 오래 소요됨)
* 단일 사용 사례에 대한 여러 호출
* 개인화 호출 전 ECID 반환 대기(지연 발생)
* 분리된 데이터 수집(evar 소개)
* 솔루션(A4T) 간 스키마 혼동
* 차선책이 없는 많은 것들

또한 현재 Adobe Experience Platform으로 직접 데이터를 보내는 JavaScript 라이브러리가 없습니다.

### Adobe Experience Platform 웹 SDK 사용

새로운 웹 SDK는 다음 솔루션에 대한 데이터를 단일 대상(AEP Edge Network)으로 전송하고 앞에서 언급한 가장 일반적인 솔루션 사용 사례를 해결합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

다른 솔루션들은 올해 말에 제공될 것이다.

또한 Adobe Experience Platform 웹 SDK는 데이터를 Adobe Experience Platform으로 직접 전송할 수 있습니다. 이 데이터는 XDM에 있으며 서버측 솔루션 스키마에 매핑됩니다.

## 이 새로운 웹 SDK의 가치는 무엇입니까?

**성능:** 웹 SDK가 현재 Adobe 라이브러리를 모두 사용하는 것보다 작고 페이지 로드 속도가 상당히 빨라졌습니다.

**간단한 기능:** XDM, Web SDK, Launch, Experience Edge, Adobe Experience Cloud 솔루션 및 Adobe Experience Platform이 결합되어 이해하기 쉽고 이해하기 쉬운 데이터 수집 스토리가 만들어집니다.

* **XDM:** 데이터를 Adobe으로 전송하는 데 사용하는 솔루션에 관계없이 사용되는 스키마입니다. evar 또는 mbox에 더 이상 태깅하지 않습니다.
* **웹 SDK:** 데이터를 손쉽게 Adobe Experience Platform Edge Network로 전송하고 받을 수 있습니다.
* **론치:** 사이트에서 웹 SDK(및 기타 JavaScript 태그)의 배포 및 구성을 단순화합니다.
* **경험 에지:** 데이터를 필요한 형식으로 Adobe Experience Platform 및 솔루션에 손쉽게 전달할 수 있습니다.
* **Adobe Experience Platform 및 Adobe 솔루션:** 가치 제안을 활성화합니다.

**컨트롤:** 모든 데이터는 하나의 연결된 데이터 스트림을 사용하므로, 데이터의 매 밀리초마다 데이터를 순서대로, 애플리케이션과 연계하여 데이터를 논리적으로 제어할 수 있습니다.

**미래를 위한 최신 솔루션:** 웹 SDK와 Experience Edge Network와의 연결을 통해 Adobe은 Adobe이 데이터 수집, 개인화, 동의 및 타사 쿠키의 미래를 처리하는 방식을 대폭 현대화할 수 있게 되었습니다. (Adobe에서 관리하는 퍼스트 파티 도메인을 활성화합니다.)

**가치 실현 시간:** Adobe은 Launch를 통해 웹 SDK를 가능한 한 쉽게 배포하고 클라이언트측 데이터를 XDM에 매핑하기 위해 많은 노력을 기울였습니다.  이러한 작업이 완료되면 다른 모든 Adobe 솔루션과 Adobe Experience Platform 서비스를 서버측에서 켜거나 끌 수 있습니다. 예를 들어 Adobe Analytics에 이 옵션을 사용하고 Target 또는 Experience Platform을 켜려는 경우 경험 에지 구성을 전환하여 이러한 사용 사례를 활성화하면 됩니다.

##  `alloy.js`?

`Alloy.js` 는 Adobe Experience Platform 웹 SDK의 파일 이름입니다. Adobe Experience Platform 웹 SDK는 공식 이름이지만 개발자는 이를 합금으로 부른다.

## 웹 SDK를 사용하려면 Adobe Experience Platform을 구입해야 합니까?

아니요. 모든 Adobe Digital Experience 고객은 이를 사용할 수 있습니다. 자유로워 웹 SDK를 사용하려는 모든 고객은 Adobe Experience Platform UI에서 스키마 및 데이터 세트를 만드는 액세스 권한을 받게 됩니다.

## 웹 SDK는 누가 사용해야 합니까?

Adobe Experience Platform 웹 SDK는 다음과 같은 사용자를 위해 개발되었습니다.

* Adobe Experience Platform 사용자

   장치에서 Adobe Experience Platform으로 직접 데이터를 보내야 하는 경우, 이는 공식적으로 권장되는 방법입니다.

   Adobe은 고객이 이미 Adobe Analytics을 보유하고 있는 경우 Adobe Analytics 커넥터를 사용하는 것이 더 빠른다는 점을 알고 있지만 데이터 수집에 대한 장기적인 전략은 아닙니다.

* Adobe Experience Cloud 솔루션 고객

   새로운 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 고객은 새로운 웹 SDK로 시작해야 하며 기존 라이브러리를 사용하지 않아야 합니다.

   가장 최적화된 구현을 원하는 기존 고객은 새로운 웹 SDK를 사용해야 합니다.


## Adobe Experience Platform 웹 SDK를 사용하려면 어떻게 해야 합니까?

웹 SDK는 현재 일반 사용자가 사용할 수 있으며 데이터를 Adobe Experience Cloud 제품으로 전송하는 데 사용할 수 있습니다. 제3자 솔루션으로 데이터를 전송할 수 있는 기능은 곧 제공될 예정입니다. 웹 SDK에 액세스하려면 CSM(Certified Software Manager)에 연락하여 요청 프로세스를 시작하십시오.

## 현재 웹 SDK에서 지원되는 사용 사례는 무엇입니까?

웹 SDK는 빠르게 진화하고 있습니다. 더 많은 활용 사례가 진행 중입니다. 여기에서 현재 지원되는 사용 사례 [목록을 확인할 수 있습니다.](https://github.com/adobe/alloy/projects/5)

## 현 고객은 사이트에 태그를 다시 지정해야 합니까?

상황에 따라 다릅니다. Adobe Experience Platform 웹 SDK는 두 가지 스타일로 배포할 수 있습니다. 향후 마이그레이션 문서는 추가 정보를 제공합니다.

* **다른 태그만:** 사이트에 솔루션에 대해 태그를 이미 지정했는데 태그를 다시 지정할 수는 없지만 Experience Platform 사용 사례 또는 예정된 Launch 서버측 기능(아래 참조)을 위해 데이터를 Adobe Experience Platform 에지 네트워크에 전송하려는 경우 사이트에 태그를 추가할 수 있습니다. 이 태그는 &quot;그저 다른 태그&quot;로 작동합니다. `alloy.js`

* **유일한 태그:** Experience Cloud 솔루션에 웹 SDK를 사용하려면 해당 페이지의 모든 솔루션에 사용해야 합니다. 예를 들어, 사이트에 Analytics 태그가 이미 지정되어 있고 Target에 사용하려는 경우, 이 태그를 향후 다른 사이트뿐만 아니라 둘 다에 사용해야 합니다.

즉, 비솔루션 사용 사례에 Adobe Experience Platform 웹 SDK를 사용하려는 경우 사이트에 태그를 지정하고 새 솔루션인 것처럼 이동할 수 `alloy.js` 있습니다. Adobe Analytics, Target 또는 Audience Manager에 사용하거나 애플리케이션 사용 사례에 사용하려면 페이지에서 기존 코드를 제거해야 할 수 있습니다.

## 합금 사용을 시작할 때 ECID를 마이그레이션하여 웹 사이트 방문자가 새로운 방문자로 표시되지 않도록 할 수 있습니까?

예. Adobe Experience Platform 웹 SDK는 ID 마이그레이션 기능을 제공합니다. 자세한 내용은 [이 문서의](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) 지침을 따르십시오.

## 웹 SDK는 Adobe Experience Platform Launch과 어떻게 다릅니까?

* **론치가** 장치 코드 관리자입니다. 코드를 보다 손쉽게 배포할 수 있습니다. 그것은 자유롭고 강력하다.

* **Adobe Experience Platform 웹 SDK는** Launch for Adobe 사용 사례를 통해 배포되는 새로운 코드의 공식 이름입니다. 또한 자유롭고 강력합니다.

* **`alloy.js`** 는 Adobe Experience Platform 웹 SDK 코드의 파일 이름입니다.

## 웹 SDK를 배포하려면 Adobe Experience Platform Launch을 사용해야 합니까?

아니요. 직접 `alloy.js` 파일을 다운로드할 수 있습니다.

그러나:

* Adobe Experience Platform 웹 SDK에는 Experience Edge 구성 ID라는 것이 필요합니다. 따라서 Edge Network가 스트림을 식별하고 데이터를 사용하여 수행할 작업을 결정할 수 있습니다. 이 ID는 론치 내에 만들어집니다. Launch를 사용하여 속성을 만들거나 JavaScript 코드를 배포해야 하는 것은 아니지만 Launch를 사용하여 구성 ID를 만들어야 합니다.

* Adobe Experience Platform Launch은 사용 가능한 최고의 태그 및 SDK 관리자일 뿐만 아니라 XDM 스키마에 데이터를 손쉽게 배포 `alloy.js` 및 매핑할 수 있습니다. Launch를 사용하지 않기로 결정한 경우 데이터를 보내기 전에 XDM에 배포, 이벤트 `alloy.js`및 매핑을 관리해야 합니다. Launch를 사용하는 것보다 훨씬 더 어려운 과정입니다.

* Launch를 사용하여 배포하는 `alloy.js`것이 좋습니다.

## XDM이란 무엇이며 웹 SDK에 사용해야 합니까?

XDM은 Adobe Experience Platform 및 웹 SDK로 데이터를 전송하는 데 사용되는 데이터 형식입니다. 웹 [SDK 설명서는](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) 특정 요구 사항에 맞게 사용자 정의할 수 있는 스키마를 쉽게 설정하는 방법을 설명합니다.

## &quot;Adobe Experience Platform Launch 서버측&quot;이란?

2020년 후반에 Launch는 서버측 전달 기능을 출시합니다. Adobe의 SDK를 사용하고 XDM을 Experience Edge로 전송하는 경우, 이러한 새로운 기능을 통해 새로운 서버측 익스텐션을 설치하고 Edge Network에서 해당 데이터를 아무데나 매핑하고 전송할 수 있습니다. 이를 &quot;서비스로 데이터 수집&quot;으로 간주합니다.  이 번들 제품은 Adobe Experience Platform의 일부로 번들로 제공되거나, 비용이 부과됩니다.

**자세한 정보**[Adobe Summit 프레젠테이션](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## CNAME 또는 퍼스트 파티 도메인이란 무엇이며, 이것이 중요한 이유는 무엇입니까?

CNAME에 대한 자세한 내용은 [Adobe 설명서를 참조하십시오.](https://docs.adobe.com/content/help/ko-KR/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform 웹 SDK에 대한 자세한 정보는 어디에서 얻을 수 있습니까?

* [설명서](https://docs.adobe.com/content/help/ko-KR/experience-platform/edge/home.html)
* [소스 코드](https://github.com/adobe/alloy)
