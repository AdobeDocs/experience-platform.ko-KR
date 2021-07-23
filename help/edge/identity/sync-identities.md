---
title: Platform Web SDK를 사용하여 Audience Manager과 Adobe Experience Platform 간 Id 동기화
description: Platform Web SDK를 사용하여 Audience Manager과 Adobe Experience Platform 간에 ID를 동기화하는 방법을 알아봅니다
seo-description: Adobe Audience Manager과 Experience Platform Web SDK를 동기화하는 방법을 알아봅니다
keywords: audience manager;aam;id;ID 동기화;네임스페이스
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Audience Manager과 Experience Platform 간 ID 동기화

Adobe Experience Platform Web SDK는 [sendEvent](./overview.md#syncing-identities) 명령을 통해 고객 ID 및 인증 상태를 선언할 수 있는 기능을 지원합니다.

ID 기호 열의 값을 사용하여 [ID 서비스 네임스페이스](../../identity/../identity-service/namespaces.md)에서 네임스페이스를 선택하여 ID와 관련된 컨텍스트를 나타냅니다.

![네임스페이스 UI 보기](../images/identity/edge_namespaceUI_identity-symbol.png)

Audience Manager 고객으로서 ID 유형을 사용하는 모든 기존 데이터 소스: 교차 장치에는 자동으로 해당 ID 네임스페이스가 있습니다. Audience Manager 데이터 소스에 대한 해당 ID 네임스페이스를 찾으려면 Adobe Experience Platform에 로그인하고 ID 섹션으로 이동합니다.

ID 유형을 사용하는 모든 새 [!DNL Audience Manager] 데이터 소스: 교차 장치는 해당 ID 네임스페이스를 생성합니다. 데이터 소스 ID 유형 쿠키 및 장치 광고 ID는 현재 지원되지 않습니다. 또한 Adobe Experience Platform에서 만든 모든 ID 네임스페이스는 해당 [!DNL Audience Manager] 데이터 소스를 생성하지만 syncIdentity 메서드는 네임스페이스 ID 기호만 지원합니다.
