---
description: Adobe Experience Platform의 대상 서비스는 대상 기능을 구성하는 여러 구성 요소에 대해 구성 템플릿을 사용합니다. 이러한 구성 요소를 결합하면 Experience Platform이 대상 파트너에 연결하고, 사용자 지정 메시지를 보내고, 디지털 에코시스템에서 프로필 데이터를 활성화할 수 있습니다.
title: Destination SDK의 구성 옵션
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Destination SDK의 구성 옵션

## 개요 {#overview}

Adobe Experience Platform의 대상 서비스는 대상 기능을 구성하는 여러 구성 요소에 대해 구성 템플릿을 사용합니다. 이러한 구성 요소를 결합하면 Experience Platform이 대상 파트너에 연결하고, 사용자 지정 메시지를 보내고, 디지털 에코시스템에서 프로필 데이터를 활성화할 수 있습니다. Adobe Experience Platform에 사용되는 템플릿은 다음과 같습니다.

* **대상 구성**: 대상에 대한 기본 정보를 포함합니다. 이 구성에는 대상이 지원할 수 있는 ID 유형과 Adobe Experience Platform 사용자 인터페이스의 대상 카드에 대한 다양한 UI 속성이 포함됩니다.
* **서버 및 템플릿 사양**: 서버 사양 및 Adobe에서 사용하는 템플릿에 대한 정보를 연결하여 페이로드를 대상에 전달합니다.
   * **서버 사양**: 엔드포인트 세부 사항을 저장하는 템플릿입니다.
   * **템플릿 사양**: 이 템플릿에서 XDM 스키마와 플랫폼에서 지원하는 형식 간에 프로필 속성 필드를 변형하는 방법을 정의할 수 있습니다. 지원되는 템플릿 언어, 메시지 형식 및 플랫폼과의 통합을 설정하는 데 Adobe이 필요한 정보에 대한 자세한 내용은 다음을 참조하십시오 [메시지 포맷](./message-format.md).
* **인증 구성**: 이러한 설정은 Adobe Experience Platform 사용자가 대상에 연결하는 방식을 정의합니다.
* **대상 메타데이터 구성**: 이 템플릿을 사용하면 대상에서 대상/세그먼트를 프로그래밍 방식으로 만들기, 업데이트 또는 삭제하는 방법을 구성할 수 있습니다.

![Destination SDK 템플릿 및 구성](./assets/self-service-configuration.png)

## 관련 링크 {#related-links}

아래 페이지에서는 Destination SDK에서 사용할 수 있는 기능 및 구성 옵션과 수행할 수 있는 해당 API 작업에 대해 자세히 설명합니다.

| 기능 설명 | API 참조 |
|--- |--- |
| [대상 구성](./destination-configuration.md) | [대상 API 끝점 작업](./destination-configuration-api.md) |
| [서버 및 템플릿 사양](./server-and-template-configuration.md) | [대상 서버 API 끝점 작업](./destination-server-api.md) |
| [인증 구성](./authentication-configuration.md) | [자격 증명 끝점 API 작업](./credentials-configuration-api.md) |
| [대상 메타데이터 관리](./audience-metadata-management.md) | [대상 메타데이터 끝점 API 작업](./audience-metadata-api.md) |
| [OAuth 2 구성](./oauth2-authentication.md) | 을 사용하여 를 구성합니다 `customerAuthenticationConfigurations` 의 매개 변수 [/destinations API 엔드포인트](./destination-configuration-api.md). |
| [메시지 포맷](./message-format.md) | - |
| [대상 테스트](./test-destination.md) | [대상 테스트 API 작업](./destination-testing-api.md) |
| [대상 게시](./configure-destination-instructions.md#publish-destination) | [대상 게시 API 작업](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
