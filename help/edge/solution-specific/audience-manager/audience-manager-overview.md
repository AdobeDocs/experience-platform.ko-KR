---
title: Adobe Audience Manager으로 데이터 보내기
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Audience Manager으로 데이터 보내기
description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Audience Manager으로 전송하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Audience Manager으로 전송하는 방법 살펴보기
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Experience Platform 에지 네트워크의 Audience Manager

Adobe Experience Platform 웹 SDK는 Adobe Audience Manager과 통합되어 Audience Manager, 쿠키 및 URL 대상 및 ID 동기화에서 데이터 전송 및 수신을 지원합니다.

## Audience Manager 활성화

Audience Manager을 활성화하려면 다음을 수행해야 합니다.

- 에지 구성에서 Audience Manager을 [활성화합니다](../../fundamentals/edge-configuration.md).
- 쿠키 및 URL 대상을 활성화하거나 비활성화합니다.
- 외부 파트너 동기화용 ID 동기화 컨테이너 지정(선택 사항)

## ID 동기화

Adobe Experience Platform 웹 SDK는 [SyncIdentity](../../fundamentals/identity.md) 명령을 통해 고객 ID와 인증 상태를 선언할 수 있는 기능을 지원합니다.

syncIdentity 메서드는 ID [서비스 네임스페이스를](../../../identity/../identity-service/namespaces.md) 사용하여 ID와 관련된 컨텍스트를 나타냅니다. Audience Manager 고객으로서, ID 유형을 사용하는 모든 기존 데이터 소스: 크로스 장치에는 해당 ID 네임스페이스가 자동으로 포함됩니다. Audience Manager 데이터 소스에 해당하는 ID 네임스페이스를 찾으려면 Adobe Experience Platform에 로그인하고 ID 섹션으로 이동합니다.

![네임스페이스 UI 보기](../../../assets/edge_configuration_identity.png)

Audience Manager 데이터 소스를 이름별로 검색할 수 있습니다. syncIdentity 메서드는 네임스페이스의 상태를 표시하기 위해 ID 기호를 사용합니다.

ID 유형을 사용하는 모든 새 Audience Manager 데이터 소스: 상호 장치는 해당 ID 네임스페이스를 생성합니다. 데이터 소스 ID 유형 쿠키 및 장치 광고 ID는 현재 지원되지 않습니다. 또한 Adobe Experience Platform에서 만들어진 ID 네임스페이스는 해당 Audience Manager 데이터 소스를 생성하지만 syncIdentity 메서드는 네임스페이스 ID 심볼만 지원합니다.
