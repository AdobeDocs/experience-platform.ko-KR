---
keywords: id rtcdp;rtcdp ID;실시간 cdp ID
title: 실시간 고객 데이터 플랫폼의 ID
description: Adobe Experience Platform Identity Service를 사용하면 다양한 디바이스와 시스템에서 ID를 결합함으로써 고객과 고객의 행동을 보다 정확하게 파악할 수 있습니다.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# 실시간 고객 데이터 플랫폼의 ID

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 여러 디바이스 및 시스템에 걸쳐 ID를 연결함으로써 고객과 고객의 행동을 보다 정확하게 파악할 수 있습니다. 일반적으로 고객은 여러 채널에서 브랜드와 인터랙션할 수 있습니다. 이러한 방법에는 웹 사이트를 온라인으로 탐색, 스토어에서 구입, 로열티 프로그램 가입, 지원 헬프데스크 요청 등이 포함됩니다. 이러한 여러 시스템에서 해당 고객에 대해 만들어진 ID가 있으며, [!DNL Identity Service]을 사용하면 이러한 ID를 결합하여 전체 상황을 확인할 수 있습니다.

5개의 서로 다른 채널을 통해 상호 작용하는 5개의 개별 고객이 아니라 동일한 고객임을 확인할 수 있으므로 각 상호 작용을 통해 일관되고 개인화된 경험을 일관되게 제공할 수 있습니다. 고객에 대한 추가 정보가 알려지면(예: 웹 사이트의 익명 브라우저는 계정 및 로그인 등록) 해당 정보가 함께 결합되어 고객의 모습이 점점 더 명확해집니다.

## ID 네임스페이스

ID 네임스페이스는 [!DNL Identity Service]의 구성 요소이며 고객 ID에 대한 추가 컨텍스트를 제공하는 표시기 역할을 합니다. 일반적으로 사용되는 ID 네임스페이스의 예로는 &quot;이메일&quot;이 있습니다. 여기서 여러 웹 사이트에서 동일한 이메일 주소를 사용하면 동일한 고객에 실제로 속하는 고유한 고객 ID로 여러 개의 다른 ID를 연결할 수 있습니다. [!DNL Experience Platform] ID 네임스페이스를 사용하여 사용자 인터페이스 내에서 개별 프로파일을 검색할 수 있습니다. 프로필 보기에 대한 자세한 내용은 [프로필 뷰어 개요](/help/rtcdp/profile/profile-viewer.md)를 참조하십시오. ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/namespaces.md)를 참조하십시오.

## ID 그래프

ID 그래프는 서로 다른 ID 네임스페이스 간의 관계를 보여주는 지도로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여줍니다. 모든 고객 ID 그래프는 고객 활동에 대한 응답으로 거의 실시간으로 [!DNL Identity Service]에 의해 종합적으로 관리 및 업데이트됩니다.

[!DNL Identity Service] 개인 그래프라고 하는 데이터를 기반으로 작성되고 조직만 볼 수 있는 ID 그래프를 관리합니다. [!DNL Identity Service] 인제스트된 데이터 레코드에 둘 이상의 ID가 포함되어 있는 경우 개인 그래프를 늘립니다. 검색된 ID 간의 관계를 추가합니다.

## 다음 단계

ID 및 그 사이의 관계는 [!DNL Identity Service]에 의해 정의 및 유지되며 [!DNL Real-time Customer Profile]에 의해 활용되어 각 개별 고객과 상호 작용에 대한 전체 그림을 만듭니다. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md)를 참조하십시오.