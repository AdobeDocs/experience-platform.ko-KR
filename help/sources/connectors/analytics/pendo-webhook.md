---
title: Pendo Source 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Pendo를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>[!DNL Pendo] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 분석 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. 분석 공급자에 대한 지원에는 [!DNL Pendo]이(가) 포함됩니다.

[[!DNL Pendo]](https://pendo.io/)은(는) 소프트웨어 회사가 고객과 공감하는 제품을 개발할 수 있도록 빌드된 제품 분석 앱입니다. 이 앱을 통해 소프트웨어 제조업체는 사용자의 제품 경험과 제품 팀의 새로운 통찰력을 향상시킬 수 있는 다양한 도구를 제품에 포함할 수 있습니다.

[!DNL Pendo] 원본을 사용하면 [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks)을(를) 사용하여 [!DNL Pendo.io]에서 지원되는 Webhook 이벤트 스키마와 관련 이벤트 데이터를 수집할 수 있습니다. [!DNL Pendo] 원본은 [!DNL Pendo] URL 웹후크에서 작동합니다.

지원되는 웹 후크는 다음과 같습니다.

* [안내서](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 표시됨
* [투표](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 표시/제출됨
* [Net Promoter 점수](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 표시/제출됨

## 전제 조건 {#prerequisites}

[!DNL Pendo] 원본 연결을 만들려면 먼저 다음 내용이 있는지 확인해야 합니다.

[!DNL Pendo] 계정입니다. 아직 계정이 없는 경우 [[!DNL Pendo] 등록](https://app.pendo.io/register) 페이지에서 계정을 등록하고 만들 수 있습니다.

### [!DNL Pendo] 웹후크 설정 {#set-up-webhook}

데이터 흐름을 성공적으로 만든 후에는 [!DNL Pendo]개의 이벤트에 대해 플랫폼에 알리도록 웹후크를 설정해야 합니다. [!DNL Pendo] 웹후크는 특정 이벤트가 발생할 때 다른 서비스에 실시간 알림을 푸시하고 이 정보를 [!DNL Pendo] 소스로 보낼 수 있습니다. 자세한 내용은 [스트리밍 끝점 URL 가져오기](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 및 [Webhook 설정 [!DNL Pendo] 에 대한 자습서를 참조하십시오.](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook)

## [!DNL Pendo]을(를) 플랫폼에 연결하는 중 {#connect-to-platform}

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Platform]과(와) 연결할 [!DNL Pendo] 스트리밍 커넥터를 만드는 방법에 대한 정보를 제공합니다.

### API를 사용하여 [!DNL Pendo]을(를) 플랫폼에 연결 {#connect-to-platform-using-api}

* [API를 사용하여  [!DNL Pendo] 데이터를 플랫폼으로 가져오려면 소스 연결을 만드십시오.](../../tutorials/api/create/analytics/pendo-webhook.md)

### UI를 사용하여 [!DNL Pendo]을(를) 플랫폼에 연결 {#connect-to-platform-using-ui}

* [사용자 인터페이스를 사용하여  [!DNL Pendo] 데이터를 플랫폼으로 가져오려면 소스 연결을 만드십시오.](../../tutorials/ui/create/analytics/pendo-webhook.md)
