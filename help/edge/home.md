---
title: Adobe Experience Platform 웹 SDK 도움말
seo-title: Adobe Experience Platform 웹 SDK 도움말
description: Adobe Experience Platform Web SDK의 정의와 사용 방법을 살펴볼 수 있습니다.
seo-description: adobe Experience Cloud 고객이 Experience Cloud의 다양한 서비스와 상호 작용할 수 있도록 허용
translation-type: tm+mt
source-git-commit: 68361835437026c86af2402cc8400a3b3f32cb81

---


# (베타) Adobe Experience Platform Web SDK 소개

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform Web SDK는 Adobe Experience Cloud 고객이 Adobe Experience Platform Edge Network를 통해 Experience Cloud의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다.

## Adobe Experience Platform 웹 SDK로 대체된 SDK

Adobe Experience Platform Web SDK는 다음 SDK를 대체합니다.

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

이는 기존 라이브러리 주위의 래퍼만이 아닙니다. 이것은 완전히 다시 쓴 것이다. 이 솔루션은 올바른 순서로 태그 실행, 라이브러리 버전 관리 문제와 불일치, 향상된 종속성 관리 등의 문제를 해결하는 데 목적이 있습니다. Experience Cloud를 구현하는 새로운 방법입니다.

새로운 라이브러리 외에도 Adobe 솔루션에 대한 HTTP 요청을 간소화하는 새로운 종점이 있습니다. 이전에는 Visitor.js가 방문자 ID 서비스로 차단 호출을 전송한 다음 AT.js가 Adobe Target으로 호출을 전송하고 DIL.js가 Adobe Audience Manager로 호출을 전송했으며 마지막으로 AppMeasurement.js가 Adobe Analytics에 대한 호출을 전송했습니다. 이 새 라이브러리 및 종단점은 ID를 검색하고, Target 경험을 가져오고, Audience Manager로 데이터를 보내고, 한 번의 호출로 데이터를 Adobe Experience Platform에 전달할 수 있습니다.