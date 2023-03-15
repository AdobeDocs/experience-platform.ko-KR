---
title: Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항
description: Adobe Experience Platform Web SDK를 사용하기 위한 사전 요구 사항에 대해 알아봅니다.
keywords: 자사 도메인;CNAME;스키마;스키마 만들기;launch;aep web sdk 확장;확장;구성 id;구성 도구;데이터 요소;데이터 요소 만들기;XDM 개체;sendEvent;이벤트 보내기;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항

Adobe Experience Platform Web SDK를 사용하려면 먼저 다음을 수행해야 합니다.

- 조직의 사용자에 대해 올바른 권한을 구성하십시오. 모든 Experience Cloud 고객은 데이터 수집 도구에 액세스할 수 있으며 조직의 각 사용자는 스키마, ID 및 데이터스트림에 대한 권한만 있으면 됩니다. 이러한 권한을 설정하는 방법에 대한 자세한 내용은 다음 문서에서 확인할 수 있습니다. [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- 자사 도메인(CNAME)을 활성화하는 것이 좋습니다. Adobe Analytics용 CNAME이 이미 있는 경우 해당 CNAME을 사용해야 합니다. 개발의 테스트는 CNAME 없이 작동하지만 Adobe은 프로덕션으로 이동하기 전에 테스트를 수행할 것을 권장합니다. CNAME 구현은 쿠키 수명 측면에서는 어떠한 이점도 제공하지 않지만, 특정 광고 차단기 및 덜 일반적인 브라우저가 SDK 요청을 차단하는 것을 방지할 수 있습니다. 이러한 경우 CNAME을 사용하면 이러한 도구를 사용하는 사용자의 데이터 수집이 중단되는 것을 방지할 수 있습니다.

>[!IMPORTANT]
>
>**2020년 11월 10일부터 자사 CNAME 구현은 모든 Safari 브라우저 및 모바일 iOS 장치에서 7일 만료됩니다.**

- 웹 사이트에서 이미 를 사용 중인 경우 [Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 웹 사이트(Adobe Experience Platform Launch 내 방문자 API 또는 Experience Cloud ID 서비스 확장 사용)에서 Adobe Experience Platform Web SDK로 마이그레이션하는 동안 계속 사용하려면 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 확장을 사용해야 합니다. 다음을 참조하십시오 [ID 마이그레이션](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 추가 정보.
