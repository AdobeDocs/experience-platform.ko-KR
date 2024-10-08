---
keywords: id rtcdp;rtcdp id;실시간 cdp id
title: Real-time Customer Data Platform의 ID
description: Adobe Experience Platform Identity Service를 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객과 고객의 행동을 더 잘 볼 수 있습니다.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ID 개요

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스와 시스템 간에 id를 연결하여 고객과 고객의 행동을 더 잘 파악할 수 있습니다. 일반적으로 고객은 여러 채널에서 귀하의 브랜드와 상호 작용하며, 여기에는 웹 사이트 온라인 탐색, 매장 내 구매, 충성도 프로그램 가입 또는 지원을 위해 헬프 데스크에 문의 전화하는 것이 포함될 수 있습니다. 이러한 여러 시스템에 해당 고객을 위해 만들어진 ID가 있으며 [!DNL Identity Service]을(를) 통해 이러한 ID를 함께 가져와서 전체 그림을 볼 수 있습니다.

이제 5개의 서로 다른 채널에서 브랜드와 상호 작용하는 5개의 개별 고객 대신, 동일한 고객임을 확인할 수 있으며 각 상호 작용을 통해 일관되고 개인화된 관련 경험을 받을 수 있습니다. 고객에 대해 더 많은 정보가 알려지면(예: 웹 사이트의 익명 브라우저가 계정에 등록하고 로그인하기로 결정하는 경우) 정보가 함께 결합되어 고객의 사진이 점점 더 명확해집니다.

## ID 네임스페이스

ID 네임스페이스는 [!DNL Identity Service]의 구성 요소이며 고객 ID에 추가 컨텍스트를 제공하는 표시기 역할을 합니다. 일반적으로 사용되는 ID 네임스페이스의 예로는 &quot;이메일&quot;이 있습니다. 여러 웹 사이트에서 동일한 이메일 주소를 사용하면 실제로 동일한 고객에 속하면서 각각 고유한 고객 ID를 가진 여러 다른 ID를 함께 결합할 수 있습니다. [!DNL Experience Platform]을(를) 사용하면 ID 네임스페이스를 사용하여 사용자 인터페이스 내에서 개별 프로필을 검색할 수 있습니다. 프로필 보기에 대한 자세한 내용은 [프로필 찾아보기 개요](profile-browse.md)를 참조하십시오. ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/features/namespaces.md)를 참조하세요.

## ID 그래프

ID 그래프는 서로 다른 ID 간의 관계 맵으로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여 줍니다. 모든 고객 ID 그래프는 고객 활동에 대한 응답으로 ID 서비스에서 총괄적으로 관리 및 업데이트됩니다.

[!DNL Identity Service]은(는) 조직에만 표시되고 데이터를 기반으로 빌드된 ID 그래프를 관리합니다. [!DNL Identity Service]은(는) 수집된 데이터 레코드에 둘 이상의 ID가 포함되어 있는 경우 그래프를 확장하여 찾은 ID 간의 관계를 추가합니다.

## 다음 단계

ID 및 ID 간의 관계는 [!DNL Identity Service]에서 정의 및 유지 관리되고 [!DNL Real-Time Customer Profile]에서 활용하여 각 개별 고객 및 해당 상호 작용에 대한 전체 그림을 만듭니다. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md)를 참조하세요.
