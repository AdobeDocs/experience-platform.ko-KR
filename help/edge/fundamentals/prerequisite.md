---
title: Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항
description: Adobe Experience Platform 웹 SDK 사용에 필요한 사전 요구 사항에 대해 알아봅니다.
keywords: 1차 도메인;CNAME;스키마;만들기;스키마;시작;aep 웹 sdk 확장;구성 ID;구성 도구;데이터 요소;데이터 요소 만들기;데이터 요소 만들기;XDM 개체;sendEvent;send Event;send Event;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Adobe Experience Platform 웹 SDK 사용을 위한 사전 요구 사항

플랫폼 웹 SDK를 사용하려면 먼저 다음을 수행해야 합니다.

- 조직에서 이 기능을 사용하도록 프로비저닝했습니다. (Platform Web SDK에 대한 액세스 권한은 무료이며, 액세스 권한을 받으려면 CSM(Customer Success Manager)에 문의하십시오.)
- 자사 도메인(CNAME)이 활성화되어 있어야 합니다. 이미 Adobe Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 테스트에서는 CNAME 없이도 사용할 수 있지만 제작 과정에는 CNAME이 있어야 합니다.

>[!IMPORTANT]
>
>**11/10/20 현재, 1차 CNAME 구현은 모든 Safari 브라우저와 모바일 iOS 장치에서 7일 만료됩니다.**

- Adobe Experience Platform 이용 권한 부여 Adobe Experience Platform을 구매하지 않은 경우, Adobe은 추가 비용 없이 SDK와 함께 제한된 방식으로 사용할 수 있도록 필요한 액세스 권한을 제공합니다.
- 웹 사이트에서 방문자 API 또는 Adobe Experience Platform Launch 내의 Experience Cloud ID 서비스 확장을 통해 웹 사이트에서 [Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)를 이미 사용하고 있고 Adobe Experience Platform 웹 SDK로 마이그레이션하는 동안 계속 사용하고자 하는 경우 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 확장을 사용해야 합니다. 자세한 내용은 [ID 마이그레이션](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)을 참조하십시오.
