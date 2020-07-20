---
title: Adobe Audience Manager으로 데이터 보내기
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Audience Manager으로 데이터 보내기
description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Audience Manager으로 전송하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Audience Manager으로 전송하는 방법 살펴보기
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] on [!DNL Experience Platform Edge Network]

Adobe Experience Platform [!DNL Web SDK] 는 Adobe Audience Manager과 통합되며, 쿠키 및 URL 대상 및 ID 동기화에서 데이터 전송 및 받기 [!DNL Audience Manager]를 지원합니다.

## 활성화 [!DNL Audience Manager]

이를 활성화하려면 [!DNL Audience Manager] 다음을 수행해야 합니다.

- Edge 구성 [!DNL Audience Manager] 에서 [활성화합니다](../../fundamentals/edge-configuration.md).
- 쿠키 및 URL 대상을 활성화하거나 비활성화합니다.
- 외부 파트너 동기화용 ID 동기화 컨테이너 지정(선택 사항)

## ID 동기화

Adobe Experience Platform은 SyncIdentity [!DNL Web SDK] [](../../fundamentals/identity.md) 명령을 통해 고객 ID와 인증 상태를 선언할 수 있는 기능을 지원합니다.

syncIdentity 메서드는 ID [서비스 네임스페이스를](../../../identity/../identity-service/namespaces.md) 사용하여 ID와 관련된 컨텍스트를 나타냅니다. 고객으로서, ID 유형을 사용하는 모든 기존 데이터 소스: [!DNL Audience Manager] 상호 장치에는 해당 항목이 자동으로 포함됩니다 [!DNL Identity Namespace]. 해당 Adobe Experience Platform [!DNL Identity Namespace] 에 [!DNL Audience Manager Data Source]로그인하여 섹션으로 [!DNL Identities] 이동합니다.

![네임스페이스 UI 보기](../../../assets/edge_configuration_identity.png)

여기에서 이름별로 [!DNL Audience Manager] 데이터 소스를 검색할 수 있습니다. syncIdentity 메서드는 네임스페이스의 상태를 표시하기 위해 ID 기호를 사용합니다.

ID 유형을 사용하는 모든 새 [!DNL Audience Manager] 데이터 소스: 상호 장치는 해당 ID 네임스페이스를 생성합니다. 데이터 소스 ID 유형 쿠키 및 장치 광고 ID는 현재 지원되지 않습니다. 또한 Adobe Experience Platform에서 만들어진 ID 네임스페이스는 해당 [!DNL Audience Manager] 데이터 소스를 생성하지만 syncIdentity 메서드는 네임스페이스 ID 심볼만 지원합니다.
