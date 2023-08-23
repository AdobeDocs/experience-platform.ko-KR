---
title: Chatlio 소스 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Chatlio를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: ce1e6c08d1e53346c11f9746cea524689f402031
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# [!DNL Chatlio]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 스트리밍 공급자에 대한 지원은 다음과 같습니다 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 는 과 완전히 통합된 라이브 채팅 앱입니다. [!DNL Slack] 및 는 여러 지원 에이전트가 동시에 개별 사이트 방문자를 지원할 수 있도록 합니다. [!DNL Chatlio] 를 사용합니다. [!DNL Chatio Zapier App] 연결하려면 [!DNL Chatlio] 2000개 이상의 다양한 앱과 서비스를 제공합니다.

다음 [!DNL Chatlio] 소스에서 지원되는 웹후크 이벤트 스키마 및 관련 이벤트 데이터를 수집할 수 있습니다. [!DNL Chatlio.com] 사용 [[!DNL Chatlio] 웹훅](https://chatlio.com/docs/webhooks/).

지원되는 웹 후크는 다음과 같습니다.

* 채팅 성적 증명서 내보내기
* 오프라인 메시지 내보내기
* 새 대화가 시작됨
* 방문자가 제시간에 답변을 받지 못했습니다.
* 방문자가 채팅 후 피드백을 남겼습니다

## 전제 조건 {#prerequisites}

다음을 만들기 전에 [!DNL Chatlio] 소스 연결에서 먼저 다음을 확인해야 합니다.

* A [!DNL Chatlio] 계정입니다. 아직 계정이 없는 경우 [[!DNL Chatlio] 등록 페이지](https://chatlio.com/app/#/signup) 을 클릭하여 계정을 등록하고 만듭니다.
* 계정을 등록했으면 다음을 따르십시오. [[!DNL Chatlio] 설치 설명서](https://chatlio.com/docs/setup/) 계정 설정을 완료합니다.

### 설정 [!DNL Chatlio] 웹후크 {#set-up-webhook}

데이터 흐름을 성공적으로 만들었으면 Platform에 알릴 웹후크를 설정해야 합니다 [!DNL Chatlio] 이벤트. 웹후크는 고객 특성이 변경되거나 사람들이 메시지를 열고 이 정보를 사용자에게 보낼 때 즉시 알릴 수 있습니다. [!DNL Chatlio] 소스.

자세한 내용은 의 자습서를 참조하십시오. [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## 연결 [!DNL Chatlio] 대상 플랫폼 {#connect-to-platform}

아래 설명서에서는 를 만드는 방법에 대한 정보를 제공합니다 [!DNL Chatlio] 연결할 스트리밍 커넥터 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### 연결 [!DNL Chatlio] API를 사용하여 플랫폼으로 {#connect-to-platform-using-api}

* [가져올 소스 연결 만들기 [!DNL Chatlio] API를 사용하여 데이터를 플랫폼에 전송합니다.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### 연결 [!DNL Chatlio] UI를 사용하여 플랫폼에 연결 {#connect-to-platform-using-ui}

* [가져올 소스 연결 만들기 [!DNL Chatlio] 사용자 인터페이스를 사용하여 Platform에 데이터 전송](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
