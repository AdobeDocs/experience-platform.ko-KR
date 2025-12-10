---
title: Adobe Experience Platform Web SDK FAQ
description: Adobe Experience Platform 웹 SDK에 대해 자주 묻는 질문에 대한 답변을 얻으십시오.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# 자주 묻는 질문

이 안내서에서는 Adobe Experience Platform 웹 SDK과 관련하여 자주 묻는 질문에 대한 답변을 제공합니다.

## Adobe Experience Platform Web SDK은 이전 솔루션과 어떻게 다릅니까?

### Experience Platform Web SDK 이전

현재 각 개별 솔루션을 기반으로 서로 다른 JavaScript 라이브러리를 배포해야 합니다.

* 각 솔루션에는 자체 JavaScript 라이브러리, 스키마 및 도메인이 있습니다.
* 이러한 라이브러리는 서로 작동하도록 빌드되지 않았습니다.
* 솔루션 간 및 Adobe Experience Platform 사용 사례에서는 이러한 서로 다른 라이브러리가 상호 종속되어 배포 마찰을 일으킵니다.

Experience Platform의 태그를 사용하여 이러한 라이브러리를 최대한 쉽게 배포하고 관리할 수 있지만 여전히 다음과 같은 문제가 있습니다.

* 라이브러리 크기(페이지에 Adobe 코드가 너무 많음)
* 성능(사이트 로드 시간이 너무 오래 걸림)
* 단일 사용 사례에 대한 여러 호출
* 개인화 호출 전에 ECID 반환 대기 중(지연 발생)
* 분리된 데이터 수집(evar란 무엇입니까?)
* 솔루션 간 스키마 혼동(A4T)
* 다른 덜 최적의 많은 것들

또한 현재 Adobe Experience Platform으로 데이터를 직접 전송하는 JavaScript 라이브러리는 없습니다.

### Experience Platform Web SDK 사용

새로운 웹 SDK은 다음 솔루션에 대한 데이터를 단일 대상(Experience Platform Edge Network)으로 보내고 앞서 언급한 가장 일반적인 솔루션 사용 사례를 해결합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 방문자 ID
* Adobe Experience Platform

다른 해결 방법도 함께 제공됩니다.

Adobe Experience Platform Web SDK에서 데이터를 Adobe Experience Platform으로 직접 전송할 수도 있습니다. 이 데이터는 XDM 형식이며 서버측 솔루션 스키마에 매핑됩니다.

## 이 새로운 웹 SDK의 가치는 얼마입니까?

**성능:** 웹 SDK은 현재 Adobe 라이브러리를 모두 사용하는 것보다 작고 훨씬 빠른 페이지 로드를 제공합니다.

**단순성:** XDM, Web SDK, 태그, Edge Network, Adobe Experience Cloud 솔루션 및 Adobe Experience Platform의 조합은 이해하기 쉽고 따라하기 쉬운 데이터 수집 스토리를 만듭니다.

* **XDM:** Adobe으로 데이터를 보내는 데 사용하는 솔루션과 관계없는 스키마입니다. evar 또는 mbox에 대해 더 이상 태깅하지 않습니다.
* **웹 SDK:** Adobe Experience Platform Edge Network으로 데이터를 쉽게 보내고 받을 수 있습니다.
* **태그:** 사이트에서 웹 SDK(및 기타 JavaScript 태그)의 배포 및 구성을 간소화합니다.
* **Edge Network:** 데이터를 필요한 형식으로 Adobe Experience Platform 및 솔루션에 쉽게 라우팅합니다.
* **Adobe Experience Platform 및 Adobe 솔루션:** 가치 제안을 사용하도록 설정합니다.

**제어:** 모든 데이터는 연결된 단일 데이터 스트림을 사용하므로 응용 프로그램과 여정의 매 밀리초 단위로 데이터의 모양을 논리적으로 추적하고 제어할 수 있습니다.

**현대적이고 미래 지향적:** 웹 SDK과 Edge Network에 대한 연결을 통해 AdobeAdobe 는 데이터 수집, 개인화, 동의 및 서드파티 쿠키의 미래를 처리하는 방법을 현대화할 수 있습니다. (Adobe에서 관리하는 자사 도메인을 활성화합니다.)

**가치 창출 시간:** Adobe은 태그를 통해 웹 SDK을 배포하고 클라이언트측 데이터를 XDM에 매핑하기 위해 최대한 노력했습니다(및 계속 진행할 예정). 이 작업이 완료되면 다른 모든 Adobe 솔루션 및 Adobe Experience Platform 서비스를 서버측에서 켜거나 끌 수 있습니다. 예를 들어, Adobe Analytics에 대해 이 기능을 사용 중이며 Target 또는 Experience Platform을 켜려는 경우 데이터 스트림 구성에 대한 토글을 전환하고 해당 사용 사례를 켤 수 있습니다.

## `alloy.js` 소개

`alloy.js`은(는) 웹 SDK JavaScript 라이브러리의 이름입니다. SDK 소스 코드 및 파일 이름 내에서 참조됩니다.

## 고객이 [!DNL Web SDK]을(를) 사용하려면 Adobe Experience Platform을 구입해야 합니까?

아니요. 모든 Adobe Digital Experience 고객은 Adobe Experience Platform Web SDK을 무료로 사용할 수 있습니다.

* *없음*&#x200B;이(가) Experience Platform 또는 Real-Time CDP에 액세스할 수 있고 [!DNL Web SDK]을(를) 사용하려는 고객은 데이터 수집 UI 또는 Experience Platform UI에서 스키마 및 데이터스트림을 만드는 올바른 권한을 구성해야 합니다.
* Experience Platform 또는 Real-time CDP에 액세스할 수 있으며 [!DNL Web SDK]을(를) 사용하려는 고객은 데이터 수집 UI 또는 Experience Platform UI에서 스키마, 데이터 세트, ID 네임스페이스 및 데이터스트림을 만드는 올바른 권한을 구성해야 합니다.

이러한 권한을 구성하는 방법에 대한 자세한 내용은 [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)에 대한 설명서를 참조하십시오.

## 웹 SDK을 사용해야 하는 사용자

Adobe Experience Platform Web SDK은 다음 고객을 위해 개발되었습니다.

* Adobe Experience Platform 사용자
   * 장치에서 Adobe Experience Platform으로 직접 데이터를 전송해야 하는 경우 이렇게 하는 것이 좋습니다.
   * Adobe은 이미 Adobe Analytics이 있는 경우 Adobe Analytics 커넥터를 사용하는 것이 더 빠르다는 것을 알고 있지만 데이터 수집을 위한 장기적인 전략은 아닙니다.

* Adobe Experience Cloud 솔루션 고객
   * 새 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 고객은 새 웹 SDK으로 시작하고 기존 라이브러리를 사용하지 않아야 합니다.
   * 최대한 최적화된 구현을 얻고자 하는 기존 고객은 새로운 웹 SDK을 사용해야 합니다.

## 웹 SDK에 액세스하려면 어떻게 합니까?

웹 SDK은 현재 일반 사용자가 사용할 수 있으며 Adobe Experience Cloud 제품으로 데이터를 전송하는 데 사용할 수 있습니다. 데이터를 서드파티 솔루션으로 보낼 수 있는 기능은 가까운 미래에 제공될 예정입니다.

SDK에 대한 요금은 없으며 Adobe에서 무료로 호스팅합니다. 필요한 경우 무료로 다운로드하여 자체 서버에 호스팅할 수 있습니다.

Adobe 서버가 SDK에서 오는 인바운드 데이터를 제대로 처리하려면 웹 SDK에서 [데이터스트림 구성](/help/datastreams/overview.md) 및 Experience Platform [XDM 스키마 빌더](/help/xdm/tutorials/create-schema-ui.md)에 액세스해야 합니다. 액세스 권한을 얻으려면 Adobe 계정 팀에 연락하여 요청 프로세스를 시작하십시오.

## 현재 웹 SDK에서 지원하는 사용 사례는 무엇입니까?

웹 SDK은 빠르게 발전하고 있습니다. 더 많은 사용 사례가 진행 중입니다. 여기에서 현재 지원되는 사용 사례 [목록을 찾을 수 있습니다.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## 현재 고객은 사이트에 태그를 다시 지정해야 합니까?

상황에 따라 다릅니다. Adobe Experience Platform Web SDK은 두 가지 다른 스타일로 배포할 수 있습니다. 향후 마이그레이션 문서에서는 추가 세부 정보가 제공됩니다.

* **다른 태그만 추가:** 사이트에 이미 솔루션에 대한 태그가 지정되어 있고 다시 태그를 지정할 수 없지만 Experience Platform 사용 사례 또는 예정된 이벤트 전달 기능을 위해 Adobe Experience Platform Edge Network에 데이터를 전송하려는 경우(아래 참조), 사이트에 `alloy.js` 태그를 추가할 수 있습니다. 이 태그가 &quot;다른 태그만 사용&quot;됩니다.

* **유일한 태그:** Experience Cloud 솔루션에 웹 SDK을 사용하려면 해당 페이지의 솔루션 _전체_&#x200B;에 사용해야 합니다. 예를 들어 사이트에 이미 Adobe Analytics에 대한 태그가 지정되어 있고 이 태그를 Target에 사용하려면 두 사이트뿐만 아니라 향후 다른 사이트에도 태그를 사용해야 합니다.

즉, 솔루션이 아닌 사용 사례에 Adobe Experience Platform Web SDK을 사용하기로 결정한 경우 `alloy.js`을(를) 사용하여 사이트에 태그를 지정하고 새로운 솔루션인 것처럼 진행할 수 있습니다. Adobe Analytics, Target 또는 Audience Manager에 사용하거나 애플리케이션 사용 사례에 사용하려는 경우 페이지에서 기존 코드를 제거해야 할 수 있습니다.

## 웹 SDK 사용을 시작할 때 웹 사이트 방문자가 새 방문자로 표시되지 않도록 ECID를 마이그레이션할 수 있습니까?

예. Adobe Experience Platform Web SDK은 ID 마이그레이션 기능을 제공합니다. 자세한 내용은 [Experience Platform Web SDK ID 설명서](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid)의 ID 마이그레이션에 대한 지침을 따르십시오.

## 웹 SDK은 태그와 어떻게 다릅니까?

* **Experience Platform의 태그**&#x200B;에서 장치 코드를 관리합니다. 이를 사용하여 코드를 보다 쉽게 배포할 수 있습니다. 그것들은 자유롭고 강력합니다.

* **Adobe Experience Platform Web SDK**&#x200B;은(는) Adobe 사용 사례에 대해 태그에 의해 배포되는 새 코드의 공식 이름입니다. 또한 자유롭고 강력합니다.

* **`alloy.js`**&#x200B;은(는) Adobe Experience Platform Web SDK 코드의 파일 이름입니다.

## 웹 SDK을 배포하려면 태그를 사용해야 합니까?

아니요. `alloy.js` 파일을 직접 다운로드할 수 있습니다.

그러나:

* Adobe Experience Platform Web SDK에는 에지 네트워크가 스트림을 식별하고 데이터로 수행할 작업을 결정할 수 있도록 데이터 스트림 ID라는 것이 필요합니다. 이 ID는 Experience Platform 내에서 만들어집니다. 즉, UI를 사용하여 속성을 만들거나 JavaScript 코드를 배포해야 하는 것은 아니지만, 태그를 사용하여 구성 ID를 만들어야 합니다.

* 태그는 최고의 사용 가능한 태그와 SDK 관리자일 뿐만 아니라 `alloy.js`을(를) 배포하고 데이터를 XDM 스키마에 매핑하는 것도 매우 쉽습니다. 태그를 사용하지 않기로 결정한 경우 전송하기 전에 배포 `alloy.js`, 이벤트 및 XDM에 대한 데이터 매핑을 관리해야 합니다. 태그를 사용하는 것보다 _훨씬_ 더 어려운 프로세스입니다.

* `alloy.js`을(를) 배포하는 데 태그를 사용하는 것이 좋습니다.

## 이벤트 전달이란?

SDK를 사용하고 XDM을 Edge Network으로 전송하는 경우 이러한 새로운 기능 이벤트 전달을 사용하여 새로운 서버측 확장을 설치하고 데이터를 Edge Network의 어디에나 매핑하고 전송할 수 있습니다. 이를 &quot;서비스로서의 데이터 수집&quot;으로 간주합니다. 이 기능은 Adobe Experience Platform의 일부로 번들로 제공될 뿐 아니라, 추가 비용으로 사용할 수 있습니다.

## CNAME 또는 자사 도메인이란 무엇이며 이것이 중요한 이유는 무엇입니까?

핵심 서비스 안내서에서 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)을 참조하세요.

## Adobe Experience Platform Web SDK에서 쿠키를 사용합니까? 그렇다면 어떤 쿠키를 사용합니까?

핵심 서비스 안내서에서 [Adobe Experience Platform Web SDK 쿠키](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)를 참조하십시오.

## Adobe Experience Platform Web SDK은 어떤 브라우저를 지원합니까?

Adobe Experience Platform Web SDK은 최신 버전의 Google Chrome, Safari, Firefox 및 Microsoft Edge Chromium에서 최적으로 작동하도록 설계되었습니다. 이전 버전의 브라우저나 더 이상 사용되지 않는 브라우저(예: Internet Explorer)에서 특정 기능을 사용하는 데 문제가 있을 수 있습니다.

## 웹 SDK의 소스 코드는 어디에서 가져올 수 있습니까?

GitHub에서 [Alloy](https://github.com/adobe/alloy) 리포지토리를 참조하십시오.
