---
title: Customer.io 소스 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Customer.io를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
badge: 베타
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>다음 [!DNL Customer.io] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. 스트리밍 공급자에 대한 지원은 다음과 같습니다 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 는 데이터 기반의 이메일, 푸시 알림, 인앱 메시지 및 SMS를 만들고 전송하기 위해 더 많은 제어와 유연성을 원하는 마케터를 위한 자동화된 메시징 플랫폼입니다.

다음 [!DNL Customer.io] 소스에서 지원되는 웹후크 이벤트 스키마 및 관련 이벤트 데이터를 수집할 수 있습니다. [!DNL Customer.io] 사용 [[!DNL Customer.io] 웹후크 보고](https://customer.io/docs/api/webhooks/).

지원되는 Webhook 이벤트 스키마는 다음과 같습니다.

* 고객 이벤트
* 이메일 이벤트
* SMS 이벤트
* 푸시 알림 이벤트
* 앱 내 메시지 이벤트
* Slack 이벤트
* Webhook 이벤트

웹 후크를 통해 사용할 수 있는 이벤트 목록은 다음을 참조하십시오. [[!DNL Customer.io] Webhook 이벤트 보고](https://customer.io/docs/webhooks/#events) 설명서를 참조하십시오.

## 사전 요구 사항 {#prerequisites}

다음을 만들기 전에 [!DNL Customer.io] 소스 연결에서 먼저 다음을 확인해야 합니다.

* A [!DNL Customer.io] 계정입니다. 읽지 않은 경우 [[!DNL Customer.io] 등록 페이지](https://fly.customer.io/signup) 을 클릭하여 계정을 등록하고 만듭니다.
* 계정을 만든 후에는 계정의 유효성을 검사해야 합니다. 다음에 설명된 단계를 수행합니다. [[!DNL Customer.io] 계정 확인](https://customer.io/docs/account-verification/) 페이지를 클릭하여 프로세스를 완료합니다.

### 설정 [!DNL Customer.io] Webhook {#set-up-webhook}

데이터 흐름을 성공적으로 생성한 후에는 플랫폼에 알릴 보고 웹후크를 설정해야 합니다 [!DNL Customer.io] 이벤트. 웹후크는 고객 특성이 변경되거나 사람들이 메시지를 열 때 즉시 알리고 이 정보를 사용자에게 보낼 수 있습니다. [!DNL Customer.io] 소스. 자세한 내용은 의 자습서를 참조하십시오. [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 연결 중 [!DNL Customer.io] 대상 플랫폼 {#connect-to-platform}

아래 설명서에서는 를 만드는 방법에 대한 정보를 제공합니다 [!DNL Customer.io] 연결할 스트리밍 연결 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### 연결 [!DNL Customer.io] API를 사용하여 플랫폼으로 {#connect-to-platform-using-api}

* [소스 연결 및 데이터 흐름을 만들어 가져오기 [!DNL Customer.io] API를 사용하여 데이터를 플랫폼에 전송합니다.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### 연결 [!DNL Customer.io] UI를 사용하여 플랫폼에 연결 {#connect-to-platform-using-ui}

* [소스 연결 및 데이터 흐름을 만들어 가져오기 [!DNL Customer.io] 사용자 인터페이스를 사용하여 Platform에 데이터 전송](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
