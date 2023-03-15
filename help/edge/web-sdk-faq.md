---
title: Adobe Experience Platform 웹 SDK FAQ
description: Adobe Experience Platform Web SDK에 대해 자주 묻는 질문에 대한 답변을 받아 보십시오.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5586c788f4ae5c61b3b94f93b4180fc293d7e179
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 2%

---

# 자주 묻는 질문

이 안내서에서는 Adobe Experience Platform 웹 SDK에 대해 자주 묻는 질문에 대한 답변을 제공합니다.

## Adobe Experience Platform 웹 SDK란 무엇입니까?

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Experience Cloud에서 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

솔루션과 관계없는 방식(XDM)으로 데이터를 Adobe Experience Platform Edge Network로 전송한 다음, 해당 데이터를 솔루션별 형식 및 대상에 매핑하고 실시간으로 전송합니다.

**추가 정보**
[Adobe Summit 표시](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform 웹 SDK는 이전 솔루션과 어떻게 다릅니까?

### Adobe Experience Platform SDK 이전

현재 각 개별 솔루션을 기반으로 다른 JavaScript 라이브러리를 배포해야 합니다.

* 각 솔루션에는 자체 JavaScript 라이브러리, 스키마 및 도메인이 있습니다.
* 이러한 라이브러리는 서로 작동하도록 빌드되지 않았습니다.
* 솔루션 간 및 Adobe Experience Platform 사용 사례에서는 이러한 서로 다른 라이브러리가 상호 종속되어 배포 마찰을 일으킵니다.

Platform의 태그를 사용하여 이러한 라이브러리를 최대한 쉽게 배포 및 관리할 수 있지만 여전히 다음과 같은 문제가 있습니다.

* 라이브러리 크기(페이지에 Adobe 코드가 너무 많음)
* 성능(사이트 로드 시간이 너무 오래 걸림)
* 단일 사용 사례에 대한 여러 호출
* 개인화 호출 전에 ECID 반환 대기 중(지연 발생)
* 분리된 데이터 수집(evar란 무엇입니까?)
* 솔루션 간 스키마 혼동(A4T)
* 다른 덜 최적의 많은 것들

또한 현재 Adobe Experience Platform으로 데이터를 직접 전송하는 JavaScript 라이브러리가 없습니다.

### Adobe Experience Platform Web SDK 사용

새로운 웹 SDK는 다음 솔루션에 대한 데이터를 단일 대상(Adobe Experience Platform Edge Network)으로 전송하고 위에서 언급한 가장 일반적인 솔루션 사용 사례를 해결합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 방문자 ID
* Adobe Experience Platform

다른 해결책들은 올해 말에 뒤따를 것입니다.

Adobe Experience Platform Web SDK는 Adobe Experience Platform으로 직접 데이터를 전송할 수도 있습니다. 이 데이터는 XDM으로 이루어지며 서버측 솔루션 스키마에 매핑됩니다.

## 이 새로운 웹 SDK의 가치는 무엇입니까?

**성능:** 웹 SDK는 현재 Adobe 라이브러리를 모두 사용하는 것보다 크기가 작고 훨씬 빠른 페이지 로드를 제공합니다.

**단순성:** XDM, Web SDK, 태그, Experience Edge, Adobe Experience Cloud 솔루션 및 Adobe Experience Platform의 조합은 이해하기 쉽고 따라하기 쉬운 데이터 수집 스토리를 만듭니다.

* **XDM:** 데이터를 Adobe으로 전송하는 데 사용하는 솔루션과 관계없는 스키마. evar 또는 mbox에 대해 더 이상 태깅하지 않습니다.
* **Adobe Experience Platform 웹 SDK:** Adobe Experience Platform Edge Network로 데이터를 쉽게 보내고 받을 수 있습니다.
* **태그:** 사이트에서 Web SDK(및 기타 JavaScript 태그)의 배포 및 구성을 간소화합니다.
* **경험 에지:** 필요한 형식으로 Adobe Experience Platform 및 솔루션에 데이터를 쉽게 라우팅할 수 있습니다.
* **Adobe Experience Platform 및 Adobe 솔루션:** 해당 가치 제안을 활성화합니다.

**제어:** 모든 데이터는 연결된 단일 데이터 스트림을 사용하므로 여정의 밀리초 단위로 데이터가 어떻게 보이는지 논리적으로 추적하고 제어할 수 있습니다.

**현대적이고 미래를 위한 준비:** Web SDK와 Experience Edge Network의 연결을 통해 Adobe은 Adobe에서 데이터 수집, 개인화, 동의 및 향후 서드파티 쿠키를 처리하는 방법을 현대화할 수 있습니다. (Adobe에서 관리하는 자사 도메인을 활성화합니다.)

**가치 창출 시간:** Adobe은 태그를 통해 웹 SDK를 배포하고 클라이언트측 데이터를 XDM에 매핑하기 위해 최대한 열심히 노력했습니다(및 계속 진행할 예정). 이 작업이 완료되면 다른 모든 Adobe 솔루션 및 Adobe Experience Platform 서비스를 서버측에서 켜거나 끌 수 있습니다. 예를 들어, Adobe Analytics에 대해 이 기능을 사용 중이며 Target 또는 Experience Platform을 켜려는 경우 데이터 스트림 구성에 대한 토글을 전환하고 해당 사용 사례를 켤 수 있습니다.

## Alloy란?

Alloy는 Adobe Experience Platform 웹 SDK의 코드 이름입니다. Adobe Experience Platform Web SDK가 공식 이름이지만 SDK의 소스 코드 및 파일 이름 내에서 사용됩니다.

## 고객이 Adobe Experience Platform을 구입하여 [!DNL Web SDK]?

아니요. 모든 Adobe Digital Experience 고객은 Adobe Experience Platform Web SDK를 무료로 사용할 수 있습니다. 를 사용하려는 고객 [!DNL Web SDK] 데이터 수집 UI 또는 Experience Platform UI에서 스키마, 데이터 세트, ID 네임스페이스 및 데이터스트림을 생성할 수 있는 올바른 권한을 구성해야 합니다.

이러한 권한 구성에 대한 자세한 내용은 다음 문서를에 참조하십시오. [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## 웹 SDK는 누가 사용해야 합니까?

Adobe Experience Platform Web SDK는 다음 사용자를 위해 개발되었습니다.

* Adobe Experience Platform 사용자
   * 장치에서 Adobe Experience Platform으로 직접 데이터를 전송해야 하는 경우 이렇게 하는 것이 좋습니다.
   * Adobe은 고객이 이미 Adobe Analytics을 보유하고 있는 경우 Adobe Analytics 커넥터를 사용하는 것이 더 빠르다는 것을 알고 있지만, 데이터 수집을 위한 장기적인 전략은 아닙니다.

* Adobe Experience Cloud 솔루션 고객
   * 새 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 고객은 기존 라이브러리를 사용하지 말고 새 Web SDK로 시작해야 합니다.
   * 최대한 최적화된 구현을 얻고자 하는 기존 고객은 새로운 웹 SDK를 사용해야 합니다.


## Adobe Experience Platform Web SDK를 사용하기 시작하려면 어떻게 해야 합니까?

Web SDK는 현재 일반 사용자가 사용할 수 있으며 Adobe Experience Cloud 제품으로 데이터를 전송하는 데 사용할 수 있습니다. 데이터를 서드파티 솔루션으로 보낼 수 있는 기능은 가까운 미래에 제공될 예정입니다. SDK는 무료이며, Adobe에서 무료로 호스팅합니다. 다운로드할 수 있으므로 원하는 경우 자체 서버에 무료로 호스팅할 수 있습니다. Platform Web SDK는 Adobe 서버가 SDK에서 오는 인바운드 데이터를 제대로 처리하기 위해 데이터 스트림 구성 및 Adobe Experience Platform XDM 스키마 빌더에 대한 액세스가 필요합니다. 액세스 권한을 얻으려면 CSM(고객 성공 관리자)에 문의하여 요청 프로세스를 시작하십시오.

## 현재 웹 SDK에서 지원되는 사용 사례는 무엇입니까?

Web SDK는 빠르게 발전하고 있습니다. 더 많은 사용 사례가 진행 중입니다. 다음을 찾을 수 있습니다. [현재 여기에서 지원되는 사용 사례 목록입니다.](https://github.com/adobe/alloy/projects/5)

## 현재 고객은 사이트에 태그를 다시 지정해야 합니까?

상황에 따라 다릅니다. Adobe Experience Platform Web SDK는 두 가지 스타일로 배포할 수 있습니다. 향후 마이그레이션 문서에서는 추가 세부 정보가 제공됩니다.

* **다른 태그입니다.** 사이트에 솔루션에 대한 태그가 이미 지정되어 있지만 다시 태깅할 수 없는 경우 Experience Platform 사용 사례 또는 예정된 이벤트 전달 기능(아래 참조)을 위해 Adobe Experience Platform Edge Network에 데이터를 전송하려면 다음을 추가할 수 있습니다. `alloy.js` 태그로 지정됩니다. 여기서 태그는 &quot;다른 태그&quot;로 작동합니다.

* **유일한 태그:** Experience Cloud 솔루션에 Web SDK를 사용하려면 다음을 위해 사용해야 합니다. _모두_ 을 참조하십시오. 예를 들어 사이트에 Adobe Analytics이 이미 태그가 지정되어 있고 Target에 사용하려는 경우 두 사이트뿐만 아니라 향후 다른 사이트에도 태그를 사용해야 합니다.

즉, 솔루션이 아닌 사용 사례에 Adobe Experience Platform Web SDK를 사용하려는 경우 `alloy.js` 새로운 솔루션인 것처럼 계속 진행하십시오. Adobe Analytics, Target 또는 Audience Manager에 사용하거나 애플리케이션 사용 사례에 사용하려는 경우 페이지에서 기존 코드를 제거해야 할 수 있습니다.

## 웹 사이트 방문자가 새 방문자로 표시되지 않도록 Alloy를 사용할 때 ECID를 마이그레이션할 수 있습니까?

예. Adobe Experience Platform Web SDK는 ID 마이그레이션 기능을 제공합니다. 에서 ID 마이그레이션에 대한 지침을 따르십시오. [Platform Web SDK ID 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 을 참조하십시오.

## 웹 SDK는 태그와 어떻게 다릅니까?

* **Experience Platform의 태그** 장치 코드를 관리합니다. 이를 사용하여 코드를 보다 쉽게 배포할 수 있습니다. 그것들은 자유롭고 강력합니다.

* **Adobe Experience Platform 웹 SDK** 는 Adobe 사용 사례에 대해 태그로 배포할 새 코드의 공식 이름입니다. 또한 자유롭고 강력합니다.

* **`alloy.js`** 는 Adobe Experience Platform 웹 SDK 코드의 파일 이름입니다.

## Web SDK를 배포하려면 태그를 사용해야 합니까?

아니요. 다음을 다운로드할 수 있습니다. `alloy.js` 직접 정리하십시오.

하지만

* Adobe Experience Platform Web SDK에는 Edge Network가 스트림을 식별하고 데이터로 수행할 작업을 결정할 수 있도록 데이터 스트림 ID라는 것이 필요합니다. 이 ID는 Experience Platform 내에 만들어집니다. 즉, UI를 사용하여 속성을 만들거나 JavaScript 코드를 배포해야 하는 것은 아니지만, 태그를 사용하여 구성 ID를 만들어야 합니다.

* 태그는 최고의 사용 가능한 태그와 SDK 관리자일 뿐만 아니라 배포도 매우 간편합니다 `alloy.js` 데이터를 XDM 스키마에 매핑합니다. 태그를 사용하지 않기로 결정한 경우 배포를 관리해야 합니다 `alloy.js`, 이벤트 및 데이터를 보내기 전에 XDM에 매핑합니다. (이)는 _많이_ 태그를 사용하는 것보다 더 어려운 프로세스입니다.

* 태그를 사용하여 배포하는 것이 좋습니다 `alloy.js`를 설정하는 데 사용하는 유일한 태그라고 가정해 보겠습니다.

## 이벤트 전달이란?

SDK를 사용하고 XDM을 Experience Edge로 전송하는 경우 이러한 새로운 기능 이벤트 전달을 사용하여 새로운 서버측 확장을 설치하고 데이터를 Edge 네트워크의 어디에나 매핑하여 전송할 수 있습니다. 이를 &quot;서비스로서의 데이터 수집&quot;으로 간주합니다. 이 기능은 Adobe Experience Platform의 일부로 번들로 제공될 뿐 아니라, 추가 비용으로 사용할 수 있습니다.

## CNAME 또는 자사 도메인이란 무엇이며 이것이 중요한 이유는 무엇입니까?

CNAME에 대한 자세한 내용은 [Adobe 설명서](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform 웹 SDK에서 쿠키를 사용합니까? 그렇다면 어떤 쿠키를 사용합니까?

예. 현재 Web SDK는 구현에 따라 1개에서 7개 사이의 쿠키를 사용합니다. 다음은 웹 SDK에서 볼 수 있는 쿠키와 쿠키 사용 방법의 목록입니다.

| **이름** | **maxAge** | **우호적인 나이** | **설명** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395일 | ID 쿠키는 ECID와 ECID와 관련된 기타 정보를 저장합니다. |
| **kndctr_orgid_consent_check** | 7200 | 2시간 | 이 쿠키는 웹 사이트에 대한 사용자의 동의 기본 설정을 저장합니다. |
| **kndctr_orgid_consent** | 15552000 | 180일 | 이 세션 기반 쿠키는 서버에서 동의 환경 설정 서버측을 조회하도록 신호를 보냅니다. |
| **kndctr_orgid_cluster** | 1800 | 30분 | 이 쿠키는 현재 사용자의 요청을 제공하는 Experience Edge 영역을 저장합니다. 영역은 Experience Edge가 요청을 올바른 영역으로 라우팅할 수 있도록 URL 경로에 사용됩니다. 이 쿠키에는 30분의 라이프타임이 있으므로 사용자가 다른 IP 주소와 연결하는 경우 요청을 가장 가까운 영역으로 라우팅할 수 있습니다. |
| **mbox** | 63072000 | 2년 | 이 쿠키는 Target 마이그레이션 설정이 true로 설정된 경우에 나타납니다. 이렇게 하면 Target이 허용됩니다. [mbox 쿠키](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 웹 SDK에서 설정합니다. |
| **mboxEdgeCluster** | 1800 | 30분 | 이 쿠키는 Target 마이그레이션 설정이 true로 설정된 경우에 나타납니다. 이 쿠키를 사용하면 Web SDK가 올바른 Edge 클러스터를 at.js에 전달할 수 있으므로, 사용자가 사이트를 탐색할 때 Target 프로필이 동기화 상태를 유지할 수 있습니다. |
| **AMCV_###@AdobeOrg** | 34128000 | 395일 | 이 쿠키는 Adobe Experience Platform Web SDK에서 ID 마이그레이션을 사용하는 경우에만 나타납니다. 이 쿠키는 사이트의 일부가 여전히 visitor.js를 사용하는 동안 Web SDK로 전환할 때 도움이 됩니다. 다음을 참조하십시오. [idMigrationEnabled 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 이 설정에 대해 자세히 알아보십시오. |

Web SDK를 사용하는 경우 Edge Network는 위의 쿠키 중 하나 이상을 설정합니다. Edge Network는 `secure` 및 `sameSite="none"` 속성.

현재 웹 사이트에 보안 섹션과 비보안 섹션이 모두 있는 경우 이로 인해 사용자 식별이 방해될 수 있습니다. 사용자가 사이트의 보안 섹션에서 비보안 섹션으로 이동하면 Edge Network가 새 항목을 생성합니다 `ECID` (요청 포함)

## Adobe Experience Platform Web SDK는 어떤 브라우저를 지원합니까?

Adobe Experience Platform Web SDK는 최신 버전의 Google Chrome, Safari, Firefox, Internet Explorer 11 및 Microsoft Edge Chromium에서 최적으로 작동되도록 설계되었습니다. 이전 버전의 브라우저에서 특정 기능을 사용하는 데 문제가 있을 수 있습니다.

## Adobe Experience Platform Web SDK에 대한 자세한 내용은 어디에서 확인할 수 있습니까?

* [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko-KR)
* [소스 코드](https://github.com/adobe/alloy)
