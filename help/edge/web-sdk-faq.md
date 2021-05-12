---
title: Adobe Experience Platform 웹 SDK FAQ
description: Adobe Experience Platform 웹 SDK에 대한 질문과 답변을 확인할 수 있습니다.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5ead9dc72b8b9fe89e0a1bc8365ceff8affd3c85
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 2%

---

# Experience Cloud 핵심 서비스에 대한

이 안내서에서는 Adobe Experience Platform 웹 SDK에 대해 자주 묻는 질문에 대한 답변을 제공합니다.

## Adobe Experience Platform Web SDK 소개

Adobe Experience Platform 웹 SDK는 Adobe Experience Cloud 고객이 Experience Cloud의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

솔루션에 관계없이 데이터를 Adobe Experience Platform Edge Network(XDM)에 전송하여 데이터를 특정 포맷 및 대상에 매핑하고 실시간으로 전송합니다.

**자세한**
[정보Adobe Summit 프레젠테이션](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK는 이전 솔루션과 어떻게 다릅니까?

### Adobe Experience Platform SDK 이전

현재 각 개별 솔루션을 기반으로 다른 JavaScript 라이브러리를 배포해야 합니다.

* 각 솔루션에는 자체 JavaScript 라이브러리, 스키마 및 도메인이 있습니다.
* 이러한 라이브러리는 서로 연동되도록 만들어지지 않았습니다.
* 크로스 솔루션 및 Adobe Experience Platform 사용 사례를 사용하려면 이러한 서로 다른 라이브러리가 상호 종속되어 배포 마찰이 발생합니다.

Adobe Experience Platform Launch을 사용하면 이러한 라이브러리를 최대한 쉽게 배포하고 관리할 수 있지만 다음과 같은 문제가 남아 있습니다.

* 라이브러리 크기(페이지의 Adobe 코드가 너무 많음)
* 성능(사이트를 로드하는 데 시간이 너무 오래 소요됨)
* 단일 사용 사례에 대한 여러 호출
* 개인화 호출 전 ECID 반환 대기(지연 발생)
* 분리된 데이터 수집(evar 소개)
* 솔루션 간 스키마 혼동(A4T)
* 차선책이 없는 많은 것들

또한 현재 Adobe Experience Platform으로 직접 데이터를 보내는 JavaScript 라이브러리가 없습니다.

### Adobe Experience Platform Web SDK 사용

새로운 웹 SDK는 다음 솔루션에 대한 데이터를 단일 대상(Adobe Experience Platform Edge Network)으로 전송하고 앞서 언급한 가장 일반적인 솔루션 사용 사례를 해결합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 방문자 ID
* Adobe Experience Platform

다른 솔루션들은 올해 말에 제공될 것이다.

또한 Adobe Experience Platform 웹 SDK는 데이터를 Adobe Experience Platform으로 직접 전송할 수 있습니다. 이 데이터는 XDM에 있으며 서버측 솔루션 스키마에 매핑됩니다.

## 이 새로운 웹 SDK의 가치는 어떠한가?

**성능:** 웹 SDK가 현재 Adobe 라이브러리를 모두 사용하는 것보다 작고 페이지 로드가 매우 빨라집니다.

**단순성:** XDM, 웹 SDK, Experience Platform Launch, Experience Edge, Adobe Experience Cloud 솔루션 및 Adobe Experience Platform을 결합하여 이해하기 쉽고 이해하기 쉬운 데이터 수집 스토리를 만듭니다.

* **XDM:** 데이터를 Adobe으로 전송하는 데 사용하는 솔루션에 관계없이 사용되는 스키마입니다. evar 또는 mbox에 대한 태깅이 더 이상 없습니다.
* **Adobe Experience Platform 웹 SDK:** 데이터를 손쉽게 Adobe Experience Platform Edge Network로 전송하고 수신할 수 있습니다.
* **Experience Platform Launch:** 웹 SDK(및 기타 모든 JavaScript 태그)의 배포 및 구성을 간소화합니다.
* **Adobe Experience Edge:** 데이터를 필요한 포맷으로 Adobe Experience Platform 및 솔루션에 손쉽게 전달할 수 있습니다.
* **Adobe Experience Platform 및 Adobe 솔루션:** 가치 제안을 활성화합니다.

**컨트롤:** 모든 데이터는 하나의 연결된 데이터 스트림을 사용하기 때문에 데이터 여정의 매 초, 애플리케이션간, 그리고 모든 데이터를 논리적으로 따르고 제어할 수 있습니다.

**미래 준비: 웹 SDK** 와 Experience Edge Network와의 연결을 통해 Adobe은 Adobe이 데이터 수집, 개인화, 동의 및 제3자 쿠키의 미래를 다루는 방법을 상당히 현대화할 수 있게 되었습니다. (Adobe에서 관리하는 퍼스트 파티 도메인을 활성화합니다.)

**가치 실현 시간:** Adobe은 Experience Platform Launch을 통해 웹 SDK를 간편하게 배포하고 클라이언트측 데이터를 XDM에 매핑하기 위해 열심히(그리고 계속) 작업했습니다.  작업이 완료되면 다른 모든 Adobe 솔루션과 Adobe Experience Platform 서비스를 서버측에서 켜거나 끌 수 있습니다. 예를 들어 Adobe Analytics에 이 옵션을 사용하고 Target 또는 Experience Platform을 켜려는 경우 데이터 스트림 구성을 전환하여 이러한 사용 사례를 켜기만 하면 됩니다.

## 합금 소개

합금은 Adobe Experience Platform Web SDK의 코드 이름입니다. Adobe Experience Platform 웹 SDK가 공식 이름이지만 SDK의 소스 코드와 파일 이름 내에 사용됩니다.

## 고객은 웹 SDK를 사용하기 위해 Adobe Experience Platform을 구입해야 합니까?

아니요. 모든 Adobe Digital Experience 고객이 사용할 수 있습니다. 완전히 자유로워졌습니다. 웹 SDK를 사용하려는 모든 고객은 Adobe Experience Platform UI에서 스키마 및 데이터 세트를 만드는 액세스 권한을 받게 됩니다.

## 누가 웹 SDK를 사용해야 합니까?

Adobe Experience Platform 웹 SDK는 다음 사용자를 위해 개발되었습니다.

* Adobe Experience Platform 사용자

   장치에서 Adobe Experience Platform으로 직접 데이터를 보내야 하는 경우, 이는 공식적으로 권장되는 방법입니다.

   Adobe은 고객에게 이미 Adobe Analytics이 있는 경우 Adobe Analytics 커넥터를 사용하는 것이 더 빠른다는 것을 알고 있지만, 데이터 수집을 위한 장기적인 전략은 아닙니다.

* Adobe Experience Cloud 솔루션 고객

   새로운 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 고객은 새로운 웹 SDK로 시작해야 하며 이전 라이브러리를 사용하지 않아야 합니다.

   가장 최적화된 구현을 원하는 기존 고객은 새로운 웹 SDK를 사용해야 합니다.


## Adobe Experience Platform 웹 SDK를 사용하기 위해 어떻게 액세스할 수 있습니까?

웹 SDK는 현재 일반 사용자가 사용할 수 있으며 Adobe Experience Cloud 제품으로 데이터를 전송하는 데 사용할 수 있습니다. 데이터를 제3자 솔루션으로 보내는 기능은 가까운 시일 내에 제공될 예정입니다. SDK는 무료로 Adobe에서 호스팅되며, 다운로드할 수 있으므로 원하는 경우 자체 서버에서 무료로 호스팅할 수 있습니다. Adobe 서버가 SDK에서 오는 인바운드 데이터를 제대로 처리하려면 플랫폼 웹 SDK에서 데이터 스트림 구성 및 Adobe Experience Platform XDM 스키마 빌더에 대한 액세스 권한이 필요합니다. 액세스 권한을 받으려면 CSM(Customer Success Manager)에 문의하여 요청 프로세스를 시작하십시오.

## 웹 SDK에서 현재 지원되는 사용 사례는 무엇입니까?

웹 SDK는 빠르게 진화하고 있습니다. 더 많은 활용 사례가 진행 중입니다. 여기에서 현재 지원되는 사용 사례 목록을 찾을 수 있습니다.](https://github.com/adobe/alloy/projects/5)[

## 현 고객은 사이트에 태그를 다시 지정해야 합니까?

상황에 따라 다릅니다. Adobe Experience Platform 웹 SDK는 두 가지 스타일로 배포할 수 있습니다. 향후 마이그레이션 문서는 추가 정보를 제공합니다.

* **다른 태그만: 사이트에 이미 솔루션에 대한 태그가 지정되어 있고 태그를 다시 지정할 수 없지만 Experience Platform 사용 사례 또는 예정된 Experience Platform Launch 서버측 기능(아래 참조)을 위해 Adobe Experience Platform Edge Network에 데이터를 전송하려는** 경우  `alloy.js` 태그를 사이트에 추가할 수 있습니다. 이 태그는 사이트에서 &quot;다른 태그&quot;로 작동합니다.

* **유일한 태그:** Experience Cloud 솔루션에 웹 SDK를 사용하려면 해당 페이지의  __ 모든 솔루션에 사용해야 합니다. 예를 들어 사이트에 Adobe Analytics 태그가 이미 지정되어 있고 Target에 사용할 경우, 향후에 다른 사이트뿐만 아니라 둘 다에 사용해야 합니다.

즉, 솔루션 이외의 사용 사례에 Adobe Experience Platform 웹 SDK를 사용하려는 경우 `alloy.js`으로 사이트에 태그를 지정하고 새 솔루션인 것처럼 계속 진행할 수 있습니다. Adobe Analytics, Target, Audience Manager 또는에 사용하거나 애플리케이션 사용 사례용으로 페이지에서 기존 코드를 제거해야 할 수 있습니다.

## 합금 사용을 시작할 때 ECID를 마이그레이션하여 웹 사이트 방문자가 새 방문자로 표시되지 않도록 할 수 있습니까?

예. Adobe Experience Platform 웹 SDK는 ID 마이그레이션 기능을 제공합니다. 자세한 내용은 [플랫폼 웹 SDK ID 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration)의 ID 마이그레이션 지침을 따르십시오.

## 웹 SDK는 Adobe Experience Platform Launch과 어떻게 다릅니까?

* **Experience Platform** 실행장치 코드 관리자입니다. 코드를 보다 손쉽게 배포할 수 있습니다. 그것은 자유롭고 강력하다.

* **Adobe Experience Platform 웹** SDK는 Adobe 사용 사례를 위해 Experience Platform Launch에 의해 배포될 새 코드의 공식 이름입니다. 그것은 또한 자유롭고 강력하다.

* **`alloy.js`** 는 Adobe Experience Platform 웹 SDK 코드의 파일 이름입니다.

## 웹 SDK를 배포하려면 Adobe Experience Platform Launch을 사용해야 합니까?

아니요. `alloy.js` 파일을 직접 다운로드할 수 있습니다.

그러나:

* Adobe Experience Platform 웹 SDK를 사용하려면 Edge 네트워크가 스트림을 식별하고 데이터를 사용하여 수행할 작업을 결정할 수 있도록 데이터 스트림 ID라는 것이 필요합니다. 이 ID는 Experience Platform Launch 내에 만들어집니다. Experience Platform Launch을 사용하여 속성을 만들거나 JavaScript 코드를 배포해야 하는 것은 아니지만, Experience Platform Launch을 사용하여 구성 ID를 만들어야 합니다.

* Adobe Experience Platform Launch은 사용 가능한 최상의 태그 및 SDK 관리자뿐만 아니라 `alloy.js`을(를) 배포하고 데이터를 XDM 스키마에 매핑하는 작업이 매우 쉽습니다. Experience Platform Launch을 사용하지 않기로 결정하면 데이터를 보내기 전에 `alloy.js` 배포, 이벤트 및 XDM에 데이터 매핑을 관리해야 합니다. Experience Platform Launch을 사용하는 것보다 _훨씬_&#x200B;더 어려운 프로세스입니다.

* 사용하는 태그만 사용하더라도 Experience Platform Launch을 사용하여 `alloy.js`을(를) 배포하는 것이 좋습니다.

## &quot;Adobe Experience Platform Launch Server Side&quot;란 무엇입니까?

2020년 후반에, Experience Platform Launch은 서버측 전달 기능을 출시할 예정입니다. Adobe SDK를 사용하고 XDM을 Experience Edge로 전송하는 경우 이러한 새로운 기능을 통해 새로운 서버측 익스텐션을 설치하고 데이터를 Adobe Edge Network에서 아무데나 매핑하고 전송할 수 있습니다. 이를 &quot;서비스로 데이터 수집&quot;이라고 생각해 보십시오.  이 서비스는 Adobe Experience Platform의 일부로 번들할 수 있을 뿐만 아니라 비용이 발생할 수 있습니다.

## CNAME 또는 퍼스트 파티 도메인이란 무엇이며, 이러한 도메인이 중요한 이유는 무엇입니까?

CNAME에 대한 자세한 내용은 [Adobe 설명서](https://docs.adobe.com/content/help/ko-KR/id-service/using/reference/analytics-reference/cname.html)에서 확인할 수 있습니다.

## Adobe Experience Platform 웹 SDK에서 쿠키를 사용합니까? 그렇다면 어떤 쿠키를 사용합니까?

예. 현재 웹 SDK는 구현에 따라 1-4 쿠키 사이의 어느 곳이든 사용합니다. 다음은 웹 SDK에서 볼 수 있는 4개의 쿠키와 쿠키 사용 방법입니다.

**kndct_orgid_id:** ID 쿠키는 ECID와 ECID와 관련된 기타 일부 정보를 저장하는 데 사용됩니다.

**kndctr_orgid_concepts:** 이 쿠키는 웹 사이트에 대한 사용자의 동의 기본 설정을 저장합니다.

**kndctr_orgid_personalization:** 이 쿠키에는 Adobe Target이 웹 페이지를 개인화하기 위해 사용하는 세션 정보가 포함되어 있습니다.

**kndctr_orgid_consentecheck:** 이 세션 기반 쿠키는 서버가 동의 환경 설정 서버측 항목을 찾도록 알립니다.

## Adobe Experience Platform 웹 SDK에서 지원하는 브라우저는 무엇입니까?

Adobe Experience Platform 웹 SDK는 최신 버전의 Google Chrome, Safari, Firefox, Internet Explorer 11 및 Microsoft Edge Chromium에서 최적으로 작동하도록 설계되었습니다. 이전 버전의 브라우저에서 특정 기능을 사용하는 데 문제가 있을 수 있습니다.

## Adobe Experience Platform 웹 SDK에 대한 자세한 내용은 어디에서 확인할 수 있습니까?

* [설명서](https://docs.adobe.com/content/help/ko-KR/experience-platform/edge/home.html)
* [소스 코드](https://github.com/adobe/alloy)
