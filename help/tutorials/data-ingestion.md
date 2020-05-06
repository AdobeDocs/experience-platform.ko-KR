---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 통합 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 경험 플랫폼에 데이터 인제스트

Adobe Experience Platform을 사용하면 마케터가 고객의 행동을 보다 효과적으로 파악할 수 있도록 다양한 소스의 데이터를 취합할 수 있습니다. Adobe Experience Platform Data Injection은 다운스트림 플랫폼 서비스에서 사용하기 위해 플랫폼이 이러한 소스의 데이터를 수집하는 방법뿐만 아니라 해당 데이터가 Data Lake 내에 어떻게 유지되는지를 나타냅니다. 데이터 수집에는 일괄 처리, 스트리밍 통합 및 소스 커넥터를 사용한 습득 등이 포함됩니다. 자세한 내용은 [데이터 수집 개요를](../ingestion/home.md) 참조하거나 [소스 문서로 직접 진행하십시오](../sources/home.md).

## UI 및 API에서 소스 커넥터 만들기

소스 커넥터를 사용하면 여러 소스에서 데이터를 인제스트할 수 있으며, 여기에서 플랫폼 서비스를 사용하여 레이블 지정, 구성 및 개선할 수 있습니다. 소스 커넥터를 만들려면 [소스 개요를 참조하십시오](../sources/home.md).

## 일괄 처리 데이터 인제스트

Adobe Experience Platform을 사용하면 데이터를 일괄 처리 파일로 플랫폼에 손쉽게 가져올 수 있습니다. 인제스트할 데이터의 예로는 CRM 시스템의 플랫 파일의 프로필 데이터(예: 쪽모이 세공 파일)나 스키마 레지스트리에서 알려진 XDM(Experience Data Model) 스키마를 준수하는 데이터가 포함될 수 있습니다. 시작하려면 Platform(플랫폼)에 [데이터 수집 자습서를 참조하십시오](../ingestion/tutorials/ingest-batch-data.md).

## XDM 스키마에 CSV 파일 매핑

CSV 데이터를 Adobe Experience Platform으로 인제스트하려면 데이터를 XDM(Experience Data Model) 스키마에 매핑해야 합니다. Experience Platform 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 보여주는 단계는 CSV 파일을 XDM 스키마 자습서에 [매핑하십시오](../ingestion/tutorials/map-a-csv-file.md).

## 스트리밍 연결 만들기

Experience Platform에 대한 데이터 스트리밍을 시작하려면 먼저 HTTP 끝점을 요청해야 합니다. 인증된 동작을 적용하도록 이 끝점을 구성하는 옵션이 있습니다. 플랫폼 사용자 인터페이스 또는 경험 플랫폼 API를 사용하여 수행할 수 있습니다. 자세한 내용은 튜토리얼을 따라 UI를 사용하여 스트리밍 연결 [을 만들거나 API를 사용하여 스트리밍 연결](../ingestion/tutorials/create-streaming-connection-ui.md)[을 만듭니다](../ingestion/tutorials/create-streaming-connection.md).

## 인증된 스트리밍 연결 만들기

인증된 데이터 수집을 사용하면 실시간 고객 프로필 및 ID와 같은 Adobe Experience Platform 서비스를 통해 신뢰할 수 있는 출처의 레코드와 신뢰할 수 없는 출처의 레코드를 구별할 수 있습니다. 시작하려면 튜토리얼에 따라 인증된 스트리밍 연결 [을 만듭니다](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## 스트림 레코드 및 시간 시리즈 데이터

데이터 세트 및 스트리밍 연결을 적절히 사용하여 레코드 또는 시간 시리즈 데이터를 플랫폼에 스트리밍할 수 있습니다. 레코드 데이터 스트리밍을 시작하려면 플랫폼 자습서에 [스트림 레코드 데이터를 따릅니다](../ingestion/tutorials/streaming-record-data.md). 스트리밍 시간 시리즈 데이터를 시작하려면 [스트림 시간 시리즈 데이터를 Platform에 따르십시오](../ingestion/tutorials/streaming-time-series-data.md).

## 하나의 HTTP 요청으로 여러 메시지 스트리밍

데이터를 Adobe Experience Platform으로 스트리밍하면 많은 HTTP 호출을 처리하는 데 비용이 들 수 있습니다. 예를 들어 1KB 페이로드로 200개의 HTTP 요청을 만드는 대신 200KB의 단일 페이로드를 사용하여 각각 1KB의 200개의 메시지를 포함하는 1개의 HTTP 요청을 만드는 것이 훨씬 효율적입니다. 올바르게 사용할 경우 단일 요청 내에서 여러 메시지를 그룹화하는 것은 Experience Platform으로 전송되는 데이터를 최적화하는 좋은 방법입니다. 스트리밍 통합 기능을 사용하여 단일 HTTP 요청 내에서 여러 메시지를 Experience Platform으로 전송하는 방법을 알아보려면 여러 메시지 [전송 튜토리얼을 따르십시오](../ingestion/tutorials/streaming-multiple-messages.md).



