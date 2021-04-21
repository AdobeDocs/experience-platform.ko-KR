---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 데이터 통합 자습서
topic-legacy: tutorial
type: Tutorial
description: 데이터 통합에는 소스 커넥터를 사용한 일괄 처리, 스트리밍 통합 및 수집이 포함됩니다.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 4%

---

# 데이터를 [!DNL Experience Platform]에 인제스트

Adobe Experience Platform은 마케터가 고객의 행동을 더 잘 이해할 수 있도록 여러 소스의 데이터를 함께 가져옵니다. Adobe [!DNL Experience Platform Data Ingestion]은 [!DNL Platform]이(가) 이러한 소스의 데이터를 수집하는 여러 메서드와 다운스트림 [!DNL Platform services]에서 사용하기 위해 Data Lake 내에서 데이터가 지속되는 방식을 나타냅니다. [!DNL Data Ingestion] 소스 커넥터를 사용한 일괄 통합, 스트리밍 통합 및 섭취 포함 자세한 내용을 보려면 [데이터 통합 개요](../ingestion/home.md)를 읽거나 [소스 설명서](../sources/home.md)로 직접 이동하십시오.

## UI 및 API에서 소스 연결 만들기

소스 커넥터를 사용하면 여러 소스에서 데이터를 인제스트할 수 있습니다. 여기서 [!DNL Platform services]을(를) 사용하여 레이블 지정, 구조 지정 및 개선할 수 있습니다. 소스 커넥터를 만들려면 [소스 개요](../sources/home.md)를 참조하십시오.

## 일괄 처리 데이터 인제스트

Adobe Experience Platform을 사용하면 데이터를 일괄 처리 파일로 [!DNL Platform]에 쉽게 가져올 수 있습니다. 인제스트할 데이터의 예로는 CRM 시스템의 플랫 파일(예: 쪽모이 세공 항목 파일)의 프로필 데이터 또는 스키마 레지스트리에서 알려진 [!DNL Experience Data Model](XDM) 스키마를 따르는 데이터가 포함될 수 있습니다. 시작하려면 플랫폼 자습서](../ingestion/tutorials/ingest-batch-data.md)에 데이터 통합 을 방문하십시오.[

## XDM 스키마에 CSV 파일 매핑

CSV 데이터를 Adobe Experience Platform으로 인제스트하려면 데이터를 [!DNL Experience Data Model](XDM) 스키마에 매핑해야 합니다. [!DNL Experience Platform] 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 보여주는 단계는 [CSV 파일을 XDM 스키마 자습서](../ingestion/tutorials/map-a-csv-file.md)에 매핑하십시오.

## 스트리밍 연결 만들기

[!DNL Experience Platform]에 대한 데이터 스트리밍을 시작하려면 먼저 HTTP 끝점을 요청해야 합니다. 인증된 동작을 적용하도록 이 끝점을 구성하는 옵션이 있습니다. 이 작업은 [!DNL Platform] 사용자 인터페이스 또는 [!DNL Experience Platform] API를 사용하여 수행할 수 있습니다. 자세한 내용을 보려면 UI](../ingestion/tutorials/create-streaming-connection-ui.md) 또는 [API를 사용하여 스트리밍 연결 만들기](../ingestion/tutorials/create-streaming-connection.md)에 대한 자습서를 따르십시오.[

## 인증된 스트리밍 연결 만들기

인증된 데이터 수집을 사용하면 [!DNL Real-time Customer Profile] 및 [!DNL Identity] 등의 Adobe Experience Platform 서비스를 통해 신뢰할 수 있는 출처의 레코드와 신뢰할 수 없는 출처의 레코드를 구별할 수 있습니다. 시작하려면 [인증된 스트리밍 연결 만들기](../ingestion/tutorials/create-authenticated-streaming-connection.md)에 대한 자습서를 따르십시오.

## 스트림 레코드 및 시간 시리즈 데이터

데이터 세트 및 스트리밍 연결을 적절히 사용하여 레코드 또는 시간 시리즈 데이터를 [!DNL Platform]에 스트리밍할 수 있습니다. 레코드 데이터 스트리밍을 시작하려면 [스트림 레코드 데이터를 플랫폼 자습서](../ingestion/tutorials/streaming-record-data.md)에 따르십시오. 시간 시리즈 데이터 스트리밍을 시작하려면 [스트림 시간 시리즈 데이터를 플랫폼](../ingestion/tutorials/streaming-time-series-data.md)에 따르십시오.

## 하나의 HTTP 요청으로 여러 메시지 스트리밍

Adobe Experience Platform으로 데이터를 스트리밍할 때 많은 HTTP 호출을 하는 것은 비용이 많이 들 수 있습니다. 예를 들어 1KB 페이로드로 200개의 HTTP 요청을 만드는 대신 200KB의 단일 페이로드를 사용하여 1KB의 200개 메시지를 포함하는 1개의 HTTP 요청을 만드는 것이 훨씬 효율적입니다. 올바르게 사용할 경우 단일 요청 내에서 여러 메시지를 그룹화하는 것은 [!DNL Experience Platform]으로 전송되는 데이터를 최적화하는 좋은 방법입니다. 스트리밍 통합 기능을 사용하여 단일 HTTP 요청 내에서 여러 메시지를 [!DNL Experience Platform]으로 보내는 방법에 대해 알려면 [여러 메시지 전송 자습서](../ingestion/tutorials/streaming-multiple-messages.md)를 따르십시오.
