---
title: Customer.io Source 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Customer.io를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>[!DNL Customer.io] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. 스트리밍 공급자에 대한 지원에는 [!DNL Customer.io]이(가) 포함됩니다.

[[!DNL Customer.io]](https://customer.io/)은(는) 데이터 기반 이메일, 푸시 알림, 인앱 메시지 및 SMS를 만들고 전송하기 위해 더 많은 제어와 유연성을 원하는 마케터를 위한 자동화된 메시징 플랫폼입니다.

[!DNL Customer.io] 소스를 사용하면 [[!DNL Customer.io] 보고 Webhooks](https://customer.io/docs/api/webhooks/)를 사용하여 [!DNL Customer.io]에서 지원되는 Webhook 이벤트 스키마와 관련 이벤트 데이터를 수집할 수 있습니다.

지원되는 Webhook 이벤트 스키마는 다음과 같습니다.

* 고객 이벤트
* 이메일 이벤트
* SMS 이벤트
* 푸시 알림 이벤트
* 앱 내 메시지 이벤트
* Slack 이벤트
* Webhook 이벤트

웹후크를 통해 사용할 수 있는 이벤트 목록은 [[!DNL Customer.io] 웹후크 이벤트 보고](https://customer.io/docs/webhooks/#events) 설명서를 참조하십시오.

## 전제 조건 {#prerequisites}

[!DNL Customer.io] 원본 연결을 만들려면 먼저 다음 내용이 있는지 확인해야 합니다.

* [!DNL Customer.io] 계정입니다. 계정을 등록하고 만들 [[!DNL Customer.io] 등록 페이지](https://fly.customer.io/signup)를 읽지 않은 경우
* 계정을 만든 후에는 계정의 유효성을 검사해야 합니다. [[!DNL Customer.io] 계정 확인](https://customer.io/docs/account-verification/) 페이지에 설명된 단계에 따라 프로세스를 완료합니다.

### [!DNL Customer.io] 웹후크 설정 {#set-up-webhook}

데이터 흐름을 만들었으면 보고 웹후크를 설정하여 플랫폼에 [!DNL Customer.io]개 이벤트에 대해 알려야 합니다. Webhooks는 고객 특성이 변경되거나 사람들이 메시지를 열 때 즉시 사용자에게 알리고 이 정보를 [!DNL Customer.io] 소스로 보낼 수 있습니다. 자세한 내용은 [스트리밍 끝점 URL 가져오기](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 및 [Webhook 설정 [!DNL Customer.io] 에 대한 자습서를 참조하십시오.](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook)

## [!DNL Customer.io]을(를) 플랫폼에 연결하는 중 {#connect-to-platform}

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Platform]에 연결하기 위해 [!DNL Customer.io] 스트리밍 연결을 만드는 방법에 대한 정보를 제공합니다.

### API를 사용하여 [!DNL Customer.io]을(를) 플랫폼에 연결 {#connect-to-platform-using-api}

* [API를 사용하여  [!DNL Customer.io] 데이터를 플랫폼으로 가져오려면 소스 연결 및 데이터 흐름을 만드십시오.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### UI를 사용하여 [!DNL Customer.io]을(를) 플랫폼에 연결 {#connect-to-platform-using-ui}

* [사용자 인터페이스를 사용하여  [!DNL Customer.io] 데이터를 플랫폼으로 가져올 소스 연결 및 데이터 흐름을 만드십시오.](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
