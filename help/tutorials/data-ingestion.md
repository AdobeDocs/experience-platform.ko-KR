---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 통합 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: 2020f4b88f81f2d4fe3cfbd91cd18119ae580f4f

---


# 경험 플랫폼으로 데이터 인제스트

Adobe Experience Platform은 마케터가 고객의 행동을 보다 효과적으로 파악할 수 있도록 다양한 소스의 데이터를 취합합니다. Adobe Experience Platform 데이터 수집은 플랫폼이 이러한 소스의 데이터를 수집하는 여러 방법뿐만 아니라 다운스트림 플랫폼 서비스에서 사용하기 위해 Data Lake 내에서 데이터가 지속되는 방식을 나타냅니다. 데이터 통합에는 일괄 처리, 스트리밍 통합 및 소스 커넥터를 사용한 통합 기능이 포함됩니다. 자세한 내용은 데이터 통합 [개요를](../ingestion/home.md) 참조하거나 소스 [문서로](../source-connectors/home.md)직접 진행하십시오.

## UI 및 API에서 소스 커넥터 만들기

소스 커넥터를 사용하면 여러 소스에서 데이터를 인제스트할 수 있으며, 여기에서 플랫폼 서비스를 사용하여 레이블 지정, 구조 지정 및 개선할 수 있습니다. UI를 사용하여 커넥터를 만들려면 UI 개요에서 [소스 커넥터](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md)만들기를 참조하십시오. API를 사용하여 소스 커넥터를 만들려면 흐름 서비스 API 개요를 [사용하여 소스 커넥터를](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)만듭니다.

## 일괄 처리 데이터 인제스트

Adobe Experience Platform을 사용하면 데이터를 Platform에 일괄 파일로 손쉽게 가져올 수 있습니다. 인제스트할 데이터의 예로는 CRM 시스템의 플랫 파일에서 프로파일 데이터(예: 쪽모이 세공 파일)나 스키마 레지스트리에서 알려진 XDM(Experience Data Model) 스키마를 따르는 데이터가 포함될 수 있습니다. 시작하려면, 통합 [데이터를 플랫폼용 자습서를](../ingestion/tutorials/ingest-batch-data.md)참조하십시오.

## XDM 스키마에 CSV 파일 매핑

CSV 데이터를 Adobe Experience Platform으로 인제스트하려면 데이터를 XDM(Experience Data Model) 스키마에 매핑해야 합니다. Experience Platform 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 보여주는 단계는 CSV 파일을 XDM 스키마 자습서에 [](../ingestion/tutorials/map-a-csv-file.md)매핑합니다.

## 스트리밍 연결 만들기

Experience Platform에 대한 스트리밍 데이터를 시작하려면 먼저 스트리밍 HTTP 연결을 만들어야 합니다. 스트리밍 연결을 만들 때 스트리밍 데이터의 소스, 신뢰할 수 있는(인증된) 소스 또는 신뢰할 수 없는(인증되지 않은) 소스에서 데이터를 전송할지 여부와 같은 주요 세부 정보를 제공해야 합니다. 플랫폼 사용자 인터페이스 또는 경험 플랫폼 API를 사용하여 수행할 수 있습니다. 자세한 내용은 UI를 사용하여 스트리밍 연결을 [만들거나 API를 사용하여 스트리밍 연결을](../ingestion/tutorials/create-streaming-connection-ui.md) 만드는 [자습서를](../ingestion/tutorials/create-streaming-connection.md)따르십시오.

## 인증된 스트리밍 연결 만들기

Authenticated Data Collection을 사용하면 실시간 고객 프로필 및 ID와 같은 Adobe Experience Platform 서비스를 통해 신뢰할 수 있는 출처의 기록들과 신뢰할 수 없는 출처의 기록들을 구별할 수 있습니다. 시작하려면 튜토리얼을 따라 인증된 스트리밍 연결을 [만듭니다](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## 스트림 레코드 및 시계열 데이터

데이터 세트 및 스트리밍 연결을 적절히 사용하여 레코드 또는 시간 시리즈 데이터를 플랫폼에 스트리밍할 수 있습니다. 레코드 데이터 스트리밍을 시작하려면 [스트림 레코드 데이터를 플랫폼 자습서로](../ingestion/tutorials/streaming-record-data.md)따르십시오. Time Series 데이터를 스트리밍하려면 [스트림 시간 시리즈 데이터를 Platform으로 팔로우하십시오](../ingestion/tutorials/streaming-time-series-data.md).

## 하나의 HTTP 요청으로 여러 메시지 스트리밍

Adobe Experience Platform으로 데이터를 스트리밍할 때 많은 HTTP 호출을 하는 것은 비용이 들 수 있습니다. 예를 들어, 1KB 페이로드로 200개의 HTTP 요청을 만드는 대신 200KB의 단일 페이로드를 사용하여 각각 1KB의 200개의 메시지를 포함하는 1개의 HTTP 요청을 만드는 것이 훨씬 효율적입니다. 올바르게 사용할 경우 단일 요청 내에서 여러 메시지를 그룹화하는 것은 Experience Platform으로 전송되는 데이터를 최적화하는 좋은 방법입니다. 스트리밍 통합 기능을 사용하여 하나의 HTTP 요청 내에서 여러 메시지를 Experience Platform으로 전송하는 방법을 알아보려면 여러 메시지 [보내기 자습서를](../ingestion/tutorials/streaming-multiple-messages.md)따르십시오.



