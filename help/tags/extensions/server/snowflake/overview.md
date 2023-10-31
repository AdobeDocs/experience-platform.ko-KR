---
title: Snowflake 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Snowflake에 대해 알아봅니다.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Snowflake] 개요

[[!DNL Snowflake]](https://www.snowflake.com/en/) 는 모든 데이터 레코드를 한 곳에 저장하고 분석할 수 있는 클라우드 데이터 웨어하우스입니다. 데이터 웨어하우징, 데이터 레이크, 데이터 엔지니어링, 데이터 과학, 데이터 애플리케이션 개발, 실시간 또는 공유 데이터의 안전한 공유 및 소비에 사용할 수 있습니다.

[!DNL Snowflake] 은(는) Amazon Web Services(AWS), Microsoft Azure(Azure) 및 Google 클라우드 플랫폼(GCP) 위에 구축됩니다.

![다음을 보여 주는 다이어그램 [!DNL Snowflake] 데이터 아키텍처.](../../../images/extensions/server/snowflake/snowflake.png)

## Snowflake 통합

Snowflake 계정은 다음 클라우드 플랫폼 중 하나에서 호스팅할 수 있습니다.

- [AMAZON WEB SERVICES ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] 은 분산 컴퓨팅, 데이터베이스 스토리지, 컨텐츠 전달, CRM(고객 관계 관리) 및 ERP(전사적 자원 관리)를 위한 SaaS(Software-as-a-Service) 통합 서비스 등 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

다음을 참조하십시오. [[!DNL AWS] 개요](../aws/overview.md) 확장 설치 및 이벤트 전달 규칙 구성에 대한 자세한 내용을 참조하십시오.

- [Microsoft Azure([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] 는 Microsoft에서 제공하는 클라우드 서비스 및 리소스에 액세스하고 관리할 수 있는 클라우드 컴퓨팅 플랫폼이자 온라인 포털입니다.

다음을 참조하십시오. [[!DNL Azure] 개요](../azure/overview.md) 확장 설치 및 이벤트 전달 규칙 구성에 대한 자세한 내용을 참조하십시오.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] 은 분산 컴퓨팅, 데이터베이스 스토리지, 컨텐츠 전달, CRM(고객 관계 관리) 및 ERP(전사적 자원 관리)를 위한 SaaS(Software-as-a-Service) 통합 서비스 등 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

다음을 참조하십시오. [[!DNL Google Cloud Platform] 개요](../google-cloud-platform/overview.md) 확장 설치 및 이벤트 전달 규칙 구성에 대한 자세한 내용을 참조하십시오.

우리 모국어 [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md), 및 [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) 이벤트 전달 확장을 사용하면 고객이 이벤트 데이터를 실시간으로 서버측에서 수집하여 보강하고, 사용할 클라우드 서비스로 전달할 수 있습니다 [!DNL Snowflake]. 아래를 참조하십시오.

![다음 [!DNL Snowflake] 다음 사이의 링크를 보여주는 보고 다이어그램 [!DNL AWS] 및 [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## 다음 단계

이 안내서에서는 다음에 대한 개요를 제공합니다. [!DNL Snowflake] 및 사용 [!DNL AWS] 및 [!DNL Azure] 이벤트 전달 확장.

에 대한 자세한 내용은 [!DNL AWS] 및 [!DNL Azure] Experience Platform의 이벤트 전달 기능은 [[!DNL AWS] 확장 개요](../aws/overview.md) 및 [[!DNL Azure] 확장 개요](../azure/overview.md).
