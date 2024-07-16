---
title: Chatlio Source 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Chatlio를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>[!DNL Chatlio] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 스트리밍 공급자에 대한 지원에는 [!DNL Chatlio]이(가) 포함됩니다.

[[!DNL Chatlio]](https://chatlio.com/)은(는) [!DNL Slack]과(와) 완전히 통합되고 여러 지원 에이전트가 동시에 개별 사이트 방문자를 지원할 수 있도록 해주는 라이브 채팅 앱입니다. [!DNL Chatlio]은(는) [!DNL Chatio Zapier App]을(를) 사용하여 [!DNL Chatlio]을(를) 2000개 이상의 다른 앱 및 서비스와 연결합니다.

[!DNL Chatlio] 원본을 사용하면 [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/)을(를) 사용하여 [!DNL Chatlio.com]에서 지원되는 Webhook 이벤트 스키마와 관련 이벤트 데이터를 수집할 수 있습니다.

지원되는 웹 후크는 다음과 같습니다.

* 채팅 성적 증명서 내보내기
* 오프라인 메시지 내보내기
* 새 대화가 시작됨
* 방문자가 제시간에 답변을 받지 못했습니다.
* 방문자가 채팅 후 피드백을 남겼습니다

## 전제 조건 {#prerequisites}

[!DNL Chatlio] 원본 연결을 만들려면 먼저 다음 내용이 있는지 확인해야 합니다.

* [!DNL Chatlio] 계정입니다. 아직 등록하지 않은 경우 [[!DNL Chatlio] 등록 페이지](https://chatlio.com/app/#/signup)를 방문하여 계정을 등록하고 만드십시오.
* 계정을 등록했으면 [[!DNL Chatlio] 설치 설명서](https://chatlio.com/docs/setup/)에 따라 계정 설정을 완료하십시오.

### [!DNL Chatlio] 웹후크 설정 {#set-up-webhook}

데이터 흐름을 성공적으로 만든 후에는 [!DNL Chatlio]개의 이벤트에 대해 플랫폼에 알리도록 웹후크를 설정해야 합니다. Webhooks는 고객 특성이 변경되거나 사람들이 메시지를 열어 이 정보를 [!DNL Chatlio] 소스로 보낼 때 즉시 알릴 수 있습니다.

자세한 내용은 [스트리밍 끝점 URL 가져오기](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 및 [Webhook 설정 [!DNL Chatlio] 에 대한 자습서를 참조하십시오.](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook)

## [!DNL Chatlio]을(를) 플랫폼에 연결 {#connect-to-platform}

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Platform]과(와) 연결할 [!DNL Chatlio] 스트리밍 커넥터를 만드는 방법에 대한 정보를 제공합니다.

### API를 사용하여 [!DNL Chatlio]을(를) 플랫폼에 연결 {#connect-to-platform-using-api}

* [API를 사용하여  [!DNL Chatlio] 데이터를 플랫폼으로 가져오려면 소스 연결을 만드십시오.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### UI를 사용하여 [!DNL Chatlio]을(를) 플랫폼에 연결 {#connect-to-platform-using-ui}

* [사용자 인터페이스를 사용하여  [!DNL Chatlio] 데이터를 플랫폼으로 가져오려면 소스 연결을 만드십시오.](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
