---
title: Adobe Experience Platform 웹 SDK 도움말
seo-title: Adobe Experience Platform 웹 SDK 도움말
description: Adobe Experience Platform 웹 SDK의 정의와 사용 방법을 살펴보십시오.
seo-description: Adobe Experience Cloud 고객은 Experience Cloud의 다양한 서비스와 상호 작용할 수 있습니다.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Adobe Experience Platform 웹 SDK 소개

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network를 통해 Experience Cloud의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

## Adobe Experience Platform 웹 SDK로 대체된 SDK

Adobe Experience Platform Web SDK는 다음 SDK를 대체합니다.

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

기존 라이브러리 주위에 있는 래퍼만이 아닙니다. 완전히 다시 쓴 거야 이 솔루션의 목적은 올바른 순서로 태그 실행, 라이브러리 버전 관리 문제와 불일치, 향상된 종속성 관리 등의 문제를 해결하는 것입니다. Experience Cloud를 구현하는 새로운 방법이며 [오픈 소스입니다](https://github.com/adobe/alloy)

새로운 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새로운 종점이 있습니다. 이전에 Visitor.js는 방문자 ID 서비스에 차단 호출을 전송한 다음 AT.js가 Adobe Target에 호출을 전송하고, DIL.js는 Adobe Audience Manager에 호출을 전송했으며, 마지막으로 AppMeasurement.js가 Adobe Analytics에 호출을 전송했습니다. 이 새 라이브러리와 종단점은 ID를 검색하고, Target 경험을 가져오고, 데이터를 Audience Manager에 보내고, 데이터를 한 번의 클릭으로 Adobe Experience Platform에 전달할 수 있습니다.

## 시작하기

시작 사용 방법에 대한 빠른 자습서를 보려면 [시작 가이드를](getting-started/quick-start-with-launch.md) 확인해 보는 것이 좋습니다.

이 제품은 점점 더 많은 사용 사례를 지원하기 위해 끊임없이 진화하고 증가하고 있습니다. 최신 상태를 유지하기 위해 [지원되는 사용 사례 보드를](https://github.com/adobe/alloy/projects/5)체크아웃합니다. Adobe는 Adobe가 현재 지원하는 사용 사례와 귀하가 최선의 결정을 내릴 수 있도록 노력하고 있는 사례에 대해 이러한 최신 정보를 제공합니다.

* __아직 지원되지__ 않는 사용 사례 - 향후 제공될 예정인 사용 사례입니다.
* __활용 사례__ - 팀이 현재 릴리스를 위해 완료하고 있는 사용 사례입니다.
* __지원되는 사용 사례__ - 현재 지원되고 작동하는 사용 사례입니다.
* __Adobe가 지원하지__ 않는 사용 사례 - 지원하지 않기로 결정한 사용 사례입니다.
