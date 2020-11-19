---
title: Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항
seo-title: Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항
description: Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항
seo-description: Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항

이 SDK를 사용하려면 먼저 다음을 수행해야 합니다.

- 조직에 이 기능을 제공합니다. 대기 목록에 오르고자 하는 경우 CSM(Certified Software Manager)에 문의하십시오.
- 자사 도메인(CNAME)이 활성화되어 있어야 합니다. 이미 Adobe Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 테스트에서는 CNAME이 없어도 되지만 프로덕션으로 이동하려면 먼저 테스트가 필요합니다.

>[!IMPORTANT]
>
>**2020년 11월 10일 현재 자사 CNAME 구현은 모든 Safari 브라우저와 모바일 iOS 장치에서 7일 만료됩니다.**

- Adobe Experience Platform에 대한 자격 부여 Adobe Experience Platform을 구매하지 않은 경우 Adobe은 추가 비용 없이 SDK와 함께 제한된 방식으로 사용할 수 있는 Experience Platform 데이터 서비스 재단을 귀하에게 제공합니다.
- 웹 사이트에서 방문자 API 또는 Adobe Experience Platform Launch 내 Experience Cloud ID 서비스 [확장을 통해 웹 사이트에서](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) Experience Cloud ID 서비스를 이미 사용하고 있고 Adobe Experience Platform 웹 SDK로 마이그레이션하는 동안 계속 사용하고자 하는 경우 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 확장을 사용해야 합니다. 자세한 내용은 [ID 마이그레이션을](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 참조하십시오.
