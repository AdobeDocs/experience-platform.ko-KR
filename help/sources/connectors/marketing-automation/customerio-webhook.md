---
title: Customer.io 소스 개요
description: 웹 후크를 활용하여 API 또는 사용자 인터페이스를 사용하여 Customer.io를 Adobe Experience Platform에 연결하는 방법을 알아봅니다
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>다음 [!DNL Customer.io] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 응용 프로그램에서 데이터를 수집하도록 지원합니다. 스트리밍 공급자를 지원하는 내용은 다음과 같습니다 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 는 데이터 기반 이메일, 푸시 알림, 인앱 메시지 및 SMS를 만들고 전송하기 위한 보다 효과적인 제어 및 유연성을 원하는 마케터를 위한 자동화된 메시징 플랫폼입니다.

다음 [!DNL Customer.io] 소스를 사용하면 지원되는 웹 후크 이벤트 스키마와 관련 이벤트 데이터를 [!DNL Customer.io] 사용 [[!DNL Customer.io] 보고 Webhooks](https://customer.io/docs/api/webhooks/).

지원되는 웹 후크 이벤트 스키마는 다음과 같습니다.

* 고객 이벤트
* 이메일 이벤트
* SMS 이벤트
* 푸시 알림 이벤트
* 인앱 메시지 이벤트
* Slack 이벤트
* Webhook 이벤트

웹 후크를 통해 사용할 수 있는 이벤트 목록은 다음을 참조하십시오. [[!DNL Customer.io] Webhook 이벤트 보고](https://customer.io/docs/webhooks/#events) 설명서.

## 사전 요구 사항 {#prerequisites}

만들기 전에 [!DNL Customer.io] 소스 연결에서 먼저 다음을 확인해야 합니다.

* A [!DNL Customer.io] 계정이 필요합니다. 책을 읽지 않은 경우 [[!DNL Customer.io] 등록 페이지](https://fly.customer.io/signup) 계정을 등록하고 만들려면
* 계정을 만든 후에는 계정의 유효성을 검사해야 합니다. 다음에 설명된 단계를 따릅니다. [[!DNL Customer.io] 계정 확인](https://customer.io/docs/account-verification/) 페이지를 클릭하여 프로세스를 완료합니다.

### 설정 [!DNL Customer.io] Webhook {#set-up-webhook}

데이터 흐름을 성공적으로 만든 후에는 Platform에 다음 정보를 알려주기 위해 보고 웹 후크를 설정해야 합니다 [!DNL Customer.io] events. Webhooks는 고객 특성이 변경되거나 사용자가 메시지를 열 때 즉시 알리고 이 정보를 사용자에게 보낼 수 있습니다 [!DNL Customer.io] 소스. 자세한 내용은 [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 연결 중 [!DNL Customer.io] 플랫폼 {#connect-to-platform}

아래 설명서에서는 [!DNL Customer.io] 연결할 스트리밍 연결 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### Connect [!DNL Customer.io] API를 사용하여 플랫폼 구현 {#connect-to-platform-using-api}

* [가져올 소스 연결 및 데이터 흐름 만들기 [!DNL Customer.io] api를 사용하여 Platform에 데이터를 추가합니다.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] UI를 사용하여 플랫폼 구현 {#connect-to-platform-using-ui}

* [가져올 소스 연결 및 데이터 흐름 만들기 [!DNL Customer.io] 사용자 인터페이스를 사용하여 Platform에 데이터 추가](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

