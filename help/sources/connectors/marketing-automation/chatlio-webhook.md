---
title: Chatlio 소스 개요
description: 웹 후크를 활용하여 API 또는 사용자 인터페이스를 사용하여 Chatlio를 Adobe Experience Platform에 연결하는 방법을 알아봅니다
badge: "Beta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>다음 [!DNL Chatlio] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 응용 프로그램에서 데이터를 수집하도록 지원합니다. 스트리밍 공급자를 지원하는 내용은 다음과 같습니다 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 는 와 완전히 통합된 라이브 채팅 앱입니다 [!DNL Slack] 및 에서는 여러 지원 에이전트를 활성화하여 개별 사이트 방문자를 동시에 지원합니다. [!DNL Chatlio] 사용 [!DNL Chatio Zapier App] 연결 [!DNL Chatlio] 2000개가 넘는 다양한 앱 및 서비스를 통해

다음 [!DNL Chatlio] 소스를 사용하면 지원되는 웹 후크 이벤트 스키마와 관련 이벤트 데이터를 [!DNL Chatlio.com] 사용 [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

지원되는 웹 후크는 다음과 같습니다.

* 채팅 스크립트 내보내기
* 오프라인 메시지 내보내기
* 새 대화가 시작되었습니다.
* 방문자가 제 시간에 답변을 받지 못했습니다
* 방문자가 채팅 후 피드백을 남겼습니다.

## 전제 조건 {#prerequisites}

만들기 전에 [!DNL Chatlio] 소스 연결에서 먼저 다음을 확인해야 합니다.

* A [!DNL Chatlio] 계정이 필요합니다. 아직 방문이 없는 경우 [[!DNL Chatlio] 등록 페이지](https://chatlio.com/app/#/signup) 계정을 등록하고 만들려면
* 계정을 성공적으로 등록했으면 [[!DNL Chatlio] 설정 설명서](https://chatlio.com/docs/setup/) 계정 설정을 완료하려면

### 설정 [!DNL Chatlio] webhook {#set-up-webhook}

데이터 흐름을 성공적으로 만든 후에는 웹 후크를 설정하여 Platform에 [!DNL Chatlio] events. Webhooks는 고객 특성이 변경될 때 또는 사람들이 메시지를 열고 이 정보를 사용자에게 보낼 때 즉시 알려줍니다 [!DNL Chatlio] 소스.

자세한 내용은 [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] 플랫폼 {#connect-to-platform}

아래 설명서에서는 [!DNL Chatlio] 연결할 스트리밍 커넥터 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### Connect [!DNL Chatlio] API를 사용하여 플랫폼 구현 {#connect-to-platform-using-api}

* [가져올 소스 연결 만들기 [!DNL Chatlio] api를 사용하여 Platform에 데이터를 추가합니다.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] UI를 사용하여 플랫폼 구현 {#connect-to-platform-using-ui}

* [가져올 소스 연결 만들기 [!DNL Chatlio] 사용자 인터페이스를 사용하여 Platform에 데이터 추가](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

