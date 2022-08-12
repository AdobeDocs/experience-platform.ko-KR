---
title: Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항
description: Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항에 대해 알아봅니다.
keywords: 자사 도메인;CNAME;스키마;스키마 만들기;launch;aep 웹 sdk 확장;확장;구성 id;구성 도구;데이터 요소;데이터 요소 만들기;XDM 개체;이벤트 보내기;이벤트 보내기;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 853c0a662592939c280c7e7ede8235d1b6155b2f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항

Adobe Experience Platform Web SDK를 사용하려면 먼저 다음을 수행해야 합니다.

- 조직에 이 기능이 프로비저닝되어 있는지 확인합니다. 액세스 권한을 얻으려면 다음 사항을 기입하십시오 [양식](https://adobe.ly/websdkaccess) 및 Adobe은 데이터 스트림 및 Adobe Experience Platform에 대한 액세스 권한을 제공합니다(필요한 경우). Adobe은 추가 비용 없이 SDK를 사용하여 제한된 방식으로 사용할 수 있는 필요한 액세스 권한을 제공합니다.
- 자사 도메인(CNAME)이 활성화되어 있는 것이 좋습니다. 이미 Adobe Analytics용 CNAME이 있는 경우 해당 CNAME을 사용해야 합니다. 개발 상태에서 테스트는 CNAME 없이 작동하지만 Adobe은 프로덕션으로 이동하기 전에 포함하는 것을 권장합니다. CNAME 구현은 쿠키 수명 측면에서 이점이 없지만 특정 광고 차단기와 덜 일반적인 브라우저가 SDK 요청을 차단하지 못하도록 할 수 있습니다. 이러한 경우 CNAME을 사용하면 이러한 도구를 사용하는 사용자에게 데이터 수집이 중단되지 않을 수 있습니다.

>[!IMPORTANT]
>
>**11/10/20 현재, 자사 CNAME 구현에는 모든 Safari 브라우저 및 모바일 iOS 장치에서 7일 만료 기간이 있습니다.**

- 웹 사이트에서 이미 [Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 웹 사이트에서 방문자 API 또는 Adobe Experience Platform Launch 내의 Experience Cloud ID 서비스 확장을 통해 Adobe Experience Platform Web SDK로 마이그레이션하는 동안 계속 사용하려면 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 확장을 사용해야 합니다. 자세한 내용은 [ID 마이그레이션](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 추가 정보.

## Adobe Experience Platform Web SDK에 대한 권한 관리

Adobe Experience Platform Web SDK 사용을 시작하려면 올바른 권한이 구성되어 있어야 합니다. 구성을 설정하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오. [데이터 수집 권한 관리](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
