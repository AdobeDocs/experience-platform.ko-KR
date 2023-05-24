---
title: Pendo 소스 개요
description: API 또는 웹 후크를 활용하여 사용자 인터페이스를 사용하여 Pendo를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다
badge: 베타
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
>다음 [!DNL Pendo] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 분석 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. Analytics 공급자에 대한 지원은 다음과 같습니다 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 는 소프트웨어 회사가 고객에게 공감하는 제품을 개발할 수 있도록 지원하기 위해 구축된 제품 분석 앱입니다. 이 앱을 통해 소프트웨어 제조업체는 사용자의 제품 경험과 제품 팀의 새로운 통찰력을 향상시킬 수 있는 다양한 도구를 제품에 포함할 수 있습니다.

다음 [!DNL Pendo] 소스에서 지원되는 웹후크 이벤트 스키마 및 관련 이벤트 데이터를 수집할 수 있습니다. [!DNL Pendo.io] 사용 [[!DNL Pendo] 웹훅](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 다음 [!DNL Pendo] 소스는 [!DNL Pendo] URL 웹훅.

지원되는 웹 후크는 다음과 같습니다.

* [안내서](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 표시됨
* [투표](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 표시됨 / 제출됨
* [Net Promoter 점수](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 표시됨 / 제출됨

## 사전 요구 사항 {#prerequisites}

다음을 만들기 전에 [!DNL Pendo] 소스 연결에서 먼저 다음을 확인해야 합니다.

A [!DNL Pendo] 계정입니다. 아직 없는 경우 [[!DNL Pendo] 레지스터](https://app.pendo.io/register) 계정을 등록하고 만들 페이지입니다.

### 설정 [!DNL Pendo] Webhook {#set-up-webhook}

데이터 흐름을 성공적으로 만들었으면 Platform에 알릴 웹후크를 설정해야 합니다 [!DNL Pendo] 이벤트. [!DNL Pendo] 웹후크는 특정 이벤트가 발생할 때 다른 서비스에 실시간 알림을 푸시하고 이 정보를 [!DNL Pendo] 소스. 자세한 내용은 의 자습서를 참조하십시오. [스트리밍 끝점 URL을 가져오는 중](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 및 [설정 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 연결 중 [!DNL Pendo] 대상 플랫폼 {#connect-to-platform}

아래 설명서에서는 를 만드는 방법에 대한 정보를 제공합니다 [!DNL Pendo] 연결할 스트리밍 커넥터 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### 연결 [!DNL Pendo] API를 사용하여 플랫폼으로 {#connect-to-platform-using-api}

* [가져올 소스 연결 만들기 [!DNL Pendo] API를 사용하여 데이터를 플랫폼에 전송합니다.](../../tutorials/api/create/analytics/pendo-webhook.md)

### 연결 [!DNL Pendo] UI를 사용하여 플랫폼에 연결 {#connect-to-platform-using-ui}

* [가져올 소스 연결 만들기 [!DNL Pendo] 사용자 인터페이스를 사용하여 Platform에 데이터 전송](../../tutorials/ui/create/analytics/pendo-webhook.md)
