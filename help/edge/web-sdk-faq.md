---
title: Adobe Experience Platform 웹 SDK FAQ
description: Adobe Experience Platform Web SDK에 대해 자주 묻는 질문에 대한 답변을 얻을 수 있습니다.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 1%

---

# 자주 묻는 질문

이 안내서에서는 Adobe Experience Platform Web SDK에 대해 자주 묻는 질문에 대한 답변을 제공합니다.

## Adobe Experience Platform Web SDK란?

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Experience Cloud의 다양한 서비스와 상호 작용할 수 있는 클라이언트측 JavaScript 라이브러리입니다.

데이터에 대한 XDM(Solution-Agnostic Way)을 사용하여 Adobe Experience Platform Edge Network에 데이터를 보낸 다음, 데이터를 솔루션별 형식 및 대상에 매핑하여 실시간으로 보냅니다.

**추가 정보**
[Adobe Summit 프레젠테이션](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK는 이전 솔루션과 어떻게 다릅니까?

### Adobe Experience Platform SDK 이전

현재 각 개별 솔루션을 기반으로 다른 JavaScript 라이브러리를 배포해야 합니다.

* 각 솔루션에는 자체 JavaScript 라이브러리, 스키마 및 도메인이 있습니다.
* 이러한 라이브러리 중 어느 것도 서로 작동하도록 빌드되지 않았습니다.
* 솔루션 간 및 Adobe Experience Platform 사용 사례에서는 이러한 서로 다른 라이브러리를 상호 종속적으로 사용해야 하므로 배포 마찰이 발생합니다.

Platform의 태그를 사용하면 이러한 라이브러리를 가능한 한 쉽게 배포하고 관리할 수 있지만, 다음과 같은 문제가 여전히 있습니다.

* 라이브러리 크기(페이지에 너무 많은 Adobe 코드)
* 성능(사이트를 로드하는 데 시간이 너무 오래 걸립니다.)
* 단일 사용 사례에 대한 여러 호출
* 개인화 호출 전 ECID 반환 대기 중(지연 발생)
* 분리된 데이터 수집(evar란?)
* 솔루션 간 스키마 혼동(A4T)
* 다른 덜 최적의 것들

또한 현재 Adobe Experience Platform으로 직접 데이터를 전송하는 JavaScript 라이브러리가 없습니다.

### Adobe Experience Platform Web SDK 사용

새 웹 SDK는 다음 솔루션에 대한 데이터를 단일 대상(Adobe Experience Platform Edge Network)에 전송하고 앞서 언급한 가장 일반적인 솔루션 사용 사례를 위해 해결합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 방문자 ID
* Adobe Experience Platform

다른 솔루션도 올해 말에 따를 것이다.

Adobe Experience Platform Web SDK는 데이터를 Adobe Experience Platform으로 직접 전송할 수도 있습니다. 이 데이터는 XDM에 있으며 서버측 솔루션 스키마에 매핑됩니다.

## 이 새로운 웹 SDK의 값은 무엇입니까?

**성능:** 웹 SDK는 현재 모든 Adobe 라이브러리를 사용하는 것보다 작으며, 페이지 로드 속도가 훨씬 빠릅니다.

**단순성:** XDM, Web SDK, 태그, Experience Edge, Adobe Experience Cloud 솔루션 및 Adobe Experience Platform을 조합하면 이해하기 쉽고 이해하기 쉬운 데이터 수집 스토리가 생성됩니다.

* **XDM:** 데이터를 Adobe으로 전송하는 데 사용하는 솔루션과 관계없는 스키마. evar 또는 mbox에 대한 태깅이 더 이상 없습니다.
* **Adobe Experience Platform 웹 SDK:** Adobe Experience Platform Edge Network에 데이터를 쉽게 보내고 받을 수 있도록 해줍니다.
* **태그:** 사이트에서 웹 SDK(및 기타 JavaScript 태그)를 배포하고 구성을 단순화합니다.
* **Experience Edge:** 필요한 형식으로 데이터를 Adobe Experience Platform 및 솔루션에 쉽게 라우팅할 수 있습니다.
* **Adobe Experience Platform 및 Adobe 솔루션:** 가치 제안 활성화

**제어:** 모든 데이터는 하나의 연결된 데이터 스트림을 사용하고 있으므로 데이터 여정의 매 밀리초마다 데이터를 애플리케이션 간 또는 애플리케이션별로 논리적으로 추적하고 제어할 수 있습니다.

**미래를 위한 현대적이며 준비:** 웹 SDK 및 Experience Edge Network에 대한 연결을 통해 Adobe은 Adobe이 데이터 수집, 개인화, 동의 및 타사 쿠키의 미래를 처리하는 방식을 크게 현대화할 수 있습니다. (Adobe에서 관리하는 자사 도메인을 활성화합니다.)

**가치 실현 시간:** Adobe은 태그를 통해 웹 SDK를 쉽게 배포하고 클라이언트측 데이터를 XDM에 매핑할 수 있도록 노력하고, 계속 진행할 것입니다. 작업이 완료되면 다른 모든 Adobe 솔루션 및 Adobe Experience Platform 서비스를 서버측에서 모두 켜거나 끌 수 있습니다. 예를 들어, Adobe Analytics에 이 기능을 사용하고 Target 또는 Experience Platform을 켜려면 데이터 스트림 구성에서 토글을 뒤집고 해당 사용 사례를 켜면 됩니다.

## 합금이란?

Alloy는 Adobe Experience Platform Web SDK의 코드 이름입니다. Adobe Experience Platform Web SDK가 공식 이름이지만 SDK의 소스 코드 및 파일 이름 내에 사용됩니다.

## 고객이 를 사용하려면 Adobe Experience Platform을 구입해야 합니까? [!DNL Web SDK]?

아니요. 모든 Adobe 디지털 경험 고객은 Adobe Experience Platform Web SDK를 무료로 사용할 수 있습니다. 를 사용하려는 고객 [!DNL Web SDK] 는 데이터 수집 UI 또는 Experience Platform UI에서 스키마, 데이터 세트, ID 네임스페이스 및 데이터 세트를 만드는 올바른 권한을 구성해야 합니다.

이러한 권한 구성에 대한 자세한 내용은 [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## 웹 SDK는 누가 사용해야 합니까?

Adobe Experience Platform Web SDK는 다음 사용자를 위해 개발되었습니다.

* Adobe Experience Platform 사용자
   * 장치에서 Adobe Experience Platform으로 직접 데이터를 전송해야 하는 경우에는 이것이 공식적으로 권장되는 방법입니다.
   * Adobe은 고객이 이미 Adobe Analytics을 보유하고 있는 경우 Adobe Analytics 커넥터를 사용하는 것이 더 빠르지만, 데이터 수집을 위한 장기적인 전략은 아닙니다.

* Adobe Experience Cloud 솔루션 고객
   * 새 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 고객은 기존 라이브러리를 사용하지 않고 새 웹 SDK로 시작해야 합니다.
   * 가장 최적화된 구현을 원하는 기존 고객은 새로운 웹 SDK를 사용해야 합니다.


## Adobe Experience Platform Web SDK 사용을 시작하려면 어떻게 해야 합니까?

웹 SDK는 현재 일반 대중에서 사용할 수 있으며 Adobe Experience Cloud 제품으로 데이터를 전송하는 데 사용할 수 있습니다. 타사 솔루션에 데이터를 전송하는 기능은 곧 제공될 예정입니다. SDK는 무료로 Adobe에 의해 호스팅되며 무료로 다운로드할 수 있으므로 원하는 경우 자체 서버에서 호스팅할 수 있습니다. Platform Web SDK를 사용하려면 Adobe 서버가 SDK에서 오는 인바운드 데이터를 제대로 처리할 수 있도록 데이터 스트림 구성 및 Adobe Experience Platform XDM 스키마 빌더에 액세스해야 합니다. 액세스 권한을 얻으려면 CSM(고객 성공 관리자)에 문의하여 요청 프로세스를 시작하십시오.

## 현재 웹 SDK에서 지원하는 사용 사례는 무엇입니까?

웹 SDK가 빠르게 진화하고 있습니다. 더 많은 사용 사례가 진행 중입니다. 다음 항목이 있습니다. [현재 지원되는 사용 사례 목록입니다.](https://github.com/adobe/alloy/projects/5)

## 현재 고객은 사이트에 태그를 다시 지정해야 합니까?

상황에 따라 다릅니다. Adobe Experience Platform Web SDK는 두 가지 다른 스타일로 배포할 수 있습니다. 향후 마이그레이션 문서는 추가 세부 정보를 제공합니다.

* **다른 태그만:** 사이트에 솔루션에 대해 이미 태그가 지정되어 있고 다시 태그를 지정할 수 없지만 Experience Platform 사용 사례 또는 예정된 이벤트 전달 기능을 위해 Adobe Experience Platform Edge Network에 데이터를 전송하려는 경우(아래 참조) `alloy.js` 태그에 다음 코드 행을 추가하여 VisitorAPI를 포함합니다.

* **유일한 태그:** Experience Cloud 솔루션에 Web SDK를 사용하려는 경우 사용해야 합니다 _모두_ 구현합니다. 예를 들어 사이트에 Adobe Analytics에 대해 이미 태그가 지정되어 있고 Target에 사용하려는 경우 향후 다른 사이트뿐만 아니라 둘 다에 사용해야 합니다.

즉, 솔루션 이외의 사용 사례에 Adobe Experience Platform Web SDK를 사용하려는 경우 `alloy.js` 그리고 그것이 새로운 해결책인 것처럼 계속하세요. Adobe Analytics, Target, Audience Manager 또는 애플리케이션 사용 사례에 사용하려는 경우 페이지에서 이전 코드를 제거해야 할 수 있습니다.

## Alloy를 사용하기 시작할 때 웹 사이트 방문자가 새 방문자로 표시되지 않도록 ECID를 마이그레이션할 수 있습니까?

예. Adobe Experience Platform Web SDK는 ID 마이그레이션 기능을 제공합니다. 에서 ID 마이그레이션에 대한 지침을 따르십시오. [Platform Web SDK ID 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 자세한 내용

## 웹 SDK는 태그와 어떻게 다릅니까?

* **Experience Platform의 태그** 장치 코드를 관리합니다. 이러한 코드를 사용하여 코드를 보다 쉽게 배포할 수 있습니다. 그들은 자유롭고 강력하다.

* **Adobe Experience Platform Web SDK** 는 Adobe 사용 사례에 대해 태그로 배포되는 새 코드의 공식 이름입니다. 그것은 또한 자유롭고 강력합니다.

* **`alloy.js`** 는 Adobe Experience Platform 웹 SDK 코드의 파일 이름입니다.

## 웹 SDK를 배포하려면 태그를 사용해야 합니까?

아니요. 을 다운로드할 수 있습니다 `alloy.js` 직접 파일을 작성합니다.

하지만

* Adobe Experience Platform Web SDK를 사용하려면 Edge 네트워크가 스트림을 식별하고 데이터를 사용하여 수행할 작업을 결정할 수 있도록 데이터 스트림 ID라고 하는 것이 필요합니다. 이 ID는 Experience Platform 내에 만들어집니다. 이는 UI를 사용하여 속성을 만들거나 JavaScript 코드를 배포해야 하는 것은 아니지만, 태그를 사용하여 구성 ID를 만들어야 합니다.

* 태그는 사용 가능한 최고의 태그 및 SDK 관리자일 뿐만 아니라 쉽게 배포할 수 있습니다 `alloy.js` 및 데이터를 XDM 스키마에 매핑합니다. 태그를 사용하지 않기로 결정한 경우 배포를 관리해야 합니다 `alloy.js`데이터를 전송하기 전에 XDM에 매핑하고 이벤트에 매핑합니다. 이것은 _많이_ 태그를 사용하는 것보다 더 어려운 프로세스가 있습니다.

* 태그를 사용하여 배포할 것을 권장합니다 `alloy.js`에 사용할 태그만 있는 경우에도 마찬가지입니다.

## 이벤트 전달이란 무엇입니까?

SDK를 사용하고 XDM을 Experience Edge로 전송하는 경우 이러한 새로운 기능 이벤트 전달을 통해 새로운 서버측 확장을 설치하고 해당 데이터를 Adobe Edge Network에서 아무데나 매핑하고 전송할 수 있습니다. 이를 &quot;서비스 로서의 데이터 수집&quot;이라고 생각합니다. 이 서비스는 Adobe Experience Platform의 일부로 번들로 제공될 뿐만 아니라, 비용에 대해서도 사용할 수 있습니다.

## CNAME 또는 퍼스트 파티 도메인이란 무엇이며, 이 도메인이 중요한 이유는 무엇입니까?

CNAME에 대한 자세한 내용은 [Adobe 설명서](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform 웹 SDK에서 쿠키를 사용합니까? 쿠키라면 어떤 쿠키를 사용합니까?

예. 현재 웹 SDK는 구현에 따라 1~4 쿠키 사이의 어느 곳에서든 쿠키를 사용합니다. 다음은 웹 SDK에서 볼 수 있는 4개의 쿠키 및 쿠키 사용 방법입니다.

**ndct_orgid_identity:** ID 쿠키는 ECID와 ECID와 관련된 기타 정보를 저장하는 데 사용됩니다.

**ndctr_orgid_consent:** 이 쿠키는 웹 사이트에 대한 사용자의 동의 기본 설정을 저장합니다.

**ndctr_orgid_cluster:** 이 쿠키는 현재 사용자의 요청을 제공하는 Experience Edge 영역을 저장합니다. 이 영역은 Experience Edge에서 요청을 올바른 영역으로 라우팅할 수 있도록 URL 경로에 사용됩니다. 이 쿠키의 수명은 30분으로, 사용자가 다른 IP 주소와 연결하는 경우 요청을 가장 가까운 영역으로 라우팅할 수 있습니다.

웹 SDK를 사용할 때 Edge Network는 위의 쿠키 중 하나 이상을 설정합니다. Edge Network는 `secure` 및 `sameSite="none"` 속성을 사용합니다.

현재 웹 사이트에 보안 섹션과 비보안 섹션이 모두 있는 경우 사용자 식별을 방해할 수 있습니다. 사용자가 사이트의 보안 섹션에서 비보안 섹션으로 이동하면 Edge Network가 새 보안 섹션을 생성합니다 `ECID` 요청 사용.

## Adobe Experience Platform Web SDK는 어떤 브라우저를 지원합니까?

Adobe Experience Platform Web SDK는 최신 버전의 Google Chrome, Safari, Firefox, Internet Explorer 11 및 Microsoft Edge Chromium에서 최적으로 작동하도록 설계되었습니다. 이전 버전의 브라우저에서 특정 기능을 사용하는 데 문제가 있을 수 있습니다.

## Adobe Experience Platform Web SDK에 대한 자세한 정보는 어디에서 얻을 수 있습니까?

* [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [소스 코드](https://github.com/adobe/alloy)
