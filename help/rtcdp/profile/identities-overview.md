---
keywords: id rtcdp;rtcdp id;실시간 cdp ID
title: Real-time Customer Data Platform의 ID
description: Adobe Experience Platform Identity Service를 사용하면 여러 장치 및 시스템에서 ID를 함께 결합함으로써 고객 및 해당 행동을 보다 잘 파악할 수 있습니다.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ID 개요

Adobe Experience Platform [!DNL Identity Service] 은 여러 장치 및 시스템에서 ID를 결합하여 고객 및 해당 행동을 더 잘 볼 수 있도록 지원합니다. 일반적으로 고객은 여러 채널에서 브랜드와 상호 작용할 수 있으며, 여기에는 웹 사이트를 온라인으로 탐색, 매장 내 구매, 충성도 프로그램에 참여 또는 지원을 위한 헬프 데스크 호출이 포함될 수 있습니다. 여러 시스템에 걸쳐 해당 고객을 위해 만들어진 ID가 있습니다. [!DNL Identity Service] 이 모든 ID를 함께 가져와서 전체 사진을 볼 수 있습니다.

5개의 서로 다른 채널에서 브랜드와 상호 작용하는 5개의 개별 고객 대신 이 고객이 동일한 고객임을 인식하고 각 상호 작용을 통해 일관되고 개인화된 적절한 경험을 제공받을 수 있습니다. 고객에 대해 더 많은 정보가 알려지면(예: 웹 사이트의 익명의 브라우저는 계정 및 로그인 등록) 해당 정보가 함께 결합되고 고객의 그림이 더 명확해집니다.

## ID 네임스페이스

ID 네임스페이스는 [!DNL Identity Service] 고객 ID에 추가적인 컨텍스트를 제공하는 지표 역할을 합니다. 일반적으로 사용되는 ID 네임스페이스의 예로는 &quot;이메일&quot;이 있습니다. 이 경우 여러 웹 사이트에서 동일한 이메일 주소를 사용하면 각각 고유한 고객 ID와 동일한 고객에 속한 여러 개의 서로 다른 ID를 결합할 수 있습니다. [!DNL Experience Platform] 네임스페이스 를 사용하여 사용자 인터페이스 내에서 개별 프로필을 검색할 수 있습니다. 프로필 보기에 대한 자세한 내용은 [프로필 찾아보기 개요](profile-browse.md). ID 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md).

## ID 그래프

ID 그래프는 서로 다른 ID 네임스페이스 간의 관계 맵으로, 고객이 다른 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여줍니다. 모든 고객 ID 그래프는 다음을 통해 종합적으로 관리 및 업데이트됩니다. [!DNL Identity Service] 거의 실시간으로, 고객 활동에 대한 응답으로 제공됩니다.

[!DNL Identity Service] 조직만 볼 수 있고 비공개 그래프라고 하는 데이터를 기반으로 구축된 id 그래프를 관리합니다. [!DNL Identity Service] 수집된 데이터 레코드에 두 개 이상의 ID가 포함되어 있는 경우 개인 그래프를 늘립니다. 검색된 ID 간에 관계를 추가합니다.

## 다음 단계

ID와 그 사이의 관계는 [!DNL Identity Service] 및 [!DNL Real-time Customer Profile] 각 개별 고객 및 상호 작용에 대한 전체 그림을 작성하기 위해. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md).
