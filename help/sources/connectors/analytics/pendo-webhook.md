---
title: 보류 소스 개요
description: 웹 후크를 활용하여 API 또는 사용자 인터페이스를 사용하여 Pendo를 Adobe Experience Platform에 연결하는 방법을 알아봅니다
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>다음 [!DNL Pendo] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 analytics 애플리케이션에서 데이터를 수집하도록 지원합니다. 분석 공급자를 지원하는 기능에는 다음이 포함됩니다 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 는 소프트웨어 회사가 고객에게 공감하는 제품을 개발할 수 있도록 만들어진 제품 분석 앱입니다. 이 앱을 사용하면 소프트웨어 제조업체는 제품을 다양한 도구로 포함하여 사용자를 위한 제품 경험과 제품 팀을 위한 새로운 통찰력을 얻을 수 있습니다.

다음 [!DNL Pendo] 소스를 사용하면 지원되는 웹 후크 이벤트 스키마와 관련 이벤트 데이터를 [!DNL Pendo.io] 사용 [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 다음 [!DNL Pendo] 소스 작동 [!DNL Pendo] URL 웹 후크.

지원되는 웹 후크는 다음과 같습니다.

* [안내서](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 표시
* [투표](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 표시/제출됨
* [네트 프로모터 점수](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 표시/제출됨

## 사전 요구 사항 {#prerequisites}

만들기 전에 [!DNL Pendo] 소스 연결에서 먼저 다음을 확인해야 합니다.

A [!DNL Pendo] 계정이 필요합니다. 아직 표시되지 않은 경우 [[!DNL Pendo] 등록](https://app.pendo.io/register) 페이지를 사용하여 계정을 등록하고 만듭니다.

### 설정 [!DNL Pendo] Webhook {#set-up-webhook}

데이터 흐름을 성공적으로 만든 후에는 웹 후크를 설정하여 Platform에 [!DNL Pendo] events. [!DNL Pendo] Webhooks에서는 특정 이벤트가 발생할 때 실시간 알림을 다른 서비스에 푸시하고 이 정보를 [!DNL Pendo] 소스. 자세한 내용은 [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 연결 중 [!DNL Pendo] 플랫폼 {#connect-to-platform}

아래 설명서에서는 [!DNL Pendo] 연결할 스트리밍 커넥터 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### Connect [!DNL Pendo] API를 사용하여 플랫폼 구현 {#connect-to-platform-using-api}

* [가져올 소스 연결 만들기 [!DNL Pendo] api를 사용하여 Platform에 데이터를 추가합니다.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connect [!DNL Pendo] UI를 사용하여 플랫폼 구현 {#connect-to-platform-using-ui}

* [가져올 소스 연결 만들기 [!DNL Pendo] 사용자 인터페이스를 사용하여 Platform에 데이터 추가](../../tutorials/ui/create/analytics/pendo-webhook.md)
