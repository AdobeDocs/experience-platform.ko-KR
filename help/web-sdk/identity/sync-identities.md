---
title: Platform Web SDK를 사용하여 Audience Manager과 Adobe Experience Platform 간에 Id 동기화
description: Platform Web SDK를 사용하여 Audience Manager과 Adobe Experience Platform 간에 ID를 동기화하는 방법에 대해 알아봅니다
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;id;동기화 id;네임스페이스;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Audience Manager과 Experience Platform 간 ID 동기화

Adobe Experience Platform Web SDK는 [sendEvent](./overview.md#syncing-identities) 명령을 통해 고객 ID와 해당 인증 상태를 선언하는 기능을 지원합니다.

ID 기호 열의 값을 사용하여 ID와 관련된 컨텍스트를 나타내려면 [ID 서비스 네임스페이스](../../identity/../identity-service/features/namespaces.md)에서 네임스페이스를 선택하십시오.

![네임스페이스 UI 보기](../assets/identity/edge_namespaceUI_identity-symbol.png)

Audience Manager 고객은 ID 유형: 크로스 디바이스를 사용하는 모든 기존 데이터 소스에 해당 ID 네임스페이스가 자동으로 부여됩니다. Audience Manager 데이터 Source에 해당하는 ID 네임스페이스를 찾으려면 Adobe Experience Platform에 로그인하여 ID 섹션으로 이동합니다.

ID 유형: 교차 장치를 사용하는 새 [!DNL Audience Manager] Data Source은 해당 ID 네임스페이스를 생성합니다. Data Source ID Types 쿠키 및 Device Advertising ID는 현재 지원되지 않습니다. 또한 Adobe Experience Platform에서 만든 모든 ID 네임스페이스는 해당 [!DNL Audience Manager] Data Source을 생성하지만 syncIdentity 메서드는 네임스페이스 ID 기호만 지원합니다.
