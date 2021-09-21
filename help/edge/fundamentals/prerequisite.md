---
title: Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항
description: Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항에 대해 알아봅니다.
keywords: 자사 도메인;CNAME;스키마;스키마 만들기;launch;aep 웹 sdk 확장;확장;구성 id;구성 도구;데이터 요소;데이터 요소 만들기;XDM 개체;이벤트 보내기;이벤트 보내기;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 9d3965be1956de754f0d2a82178bf5dcd871e239
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK 사용을 위한 사전 요구 사항

Platform Web SDK를 사용하려면 먼저 다음을 수행해야 합니다.

- 조직에 이 기능이 프로비저닝되어 있는지 확인합니다. (Platform Web SDK에 대한 액세스 권한은 무료이며, 액세스 권한을 얻으려면 CSM(Customer Success Manager)에게 문의하십시오.)
- 자사 도메인(CNAME)이 활성화되어 있는 것이 좋습니다. 이미 Adobe Analytics용 CNAME이 있는 경우 해당 CNAME을 사용해야 합니다. 개발 상태에서 테스트는 CNAME 없이 작동하지만 Adobe은 프로덕션으로 이동하기 전에 포함하는 것을 권장합니다. CNAME 구현은 쿠키 수명 측면에서 이점이 없지만 특정 광고 차단기와 덜 일반적인 브라우저가 SDK 요청을 차단하지 못하도록 할 수 있습니다. 이러한 경우 CNAME을 사용하면 이러한 도구를 사용하는 사용자에게 데이터 수집이 중단되지 않을 수 있습니다.

>[!IMPORTANT]
>
>**11/10/20 현재, 퍼스트 파티 CNAME 구현에는 모든 Safari 브라우저 및 모바일 iOS 장치에서 7일 만료 기간이 있습니다.**

- Adobe Experience Platform에 대한 권한 얻기. Adobe Experience Platform을 구매하지 않은 경우, Adobe은 추가 비용 없이 SDK를 사용하여 제한된 방식으로 사용할 수 있는 필수 액세스 권한을 제공합니다.
- 웹 사이트에서 방문자 API 또는 Adobe Experience Platform Launch 내의 Experience Cloud ID 서비스 확장을 통해 웹 사이트에서 [Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)를 이미 사용하고 있는데 Adobe Experience Platform Web SDK로 마이그레이션하는 동안 계속 사용하려면 최신 버전의 방문자 API 또는 Experience Cloud ID 서비스 확장을 사용해야 합니다. 자세한 내용은 [ID 마이그레이션](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)을 참조하십시오.

## Adobe Experience Platform Web SDK에 대한 권한 관리

Adobe Experience Platform을 사용하면 특별한 권한이 필요하지 않지만 Adobe Experience Platform에서 스키마를 만들려면 권한 [권한](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=kr)이 있어야 합니다. 필요한 최소 권한은 데이터 모델링 및 ID 카테고리에서 찾을 수 있습니다.

![](../images/AEP-permission-categories.png)

데이터 모델링 카테고리 내에서 사용자에게 스키마 관리 및 스키마 보기 권한을 부여합니다.

![](../images/data-modeling-permissions.png)

Identity Management 카테고리 내에서 사용자에게 ID 네임스페이스 관리 및 ID 네임스페이스 보기 권한을 부여합니다.

![](../images/identity-management-permissions.png)
