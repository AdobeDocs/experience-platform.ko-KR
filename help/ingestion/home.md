---
keywords: Experience Platform;홈;인기 항목;데이터 수집;데이터 위치;데이터 위치;데이터 관리;데이터 관리;계보;계보;배치;일괄 처리;수집된 데이터
solution: Experience Platform
title: 데이터 수집 개요
description: 이 문서에서는 보다 자세한 정보를 보려면 해당 개요 설명서에 대한 링크와 함께 Experience Platform으로 데이터를 수집하는 세 가지 주요 방법을 소개합니다.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 데이터 수집 개요

Adobe Experience Platform은 마케터가 고객의 행동을 더 잘 이해할 수 있도록 여러 소스의 데이터를 함께 가져옵니다. Adobe Experience Platform 데이터 수집은 Experience Platform이 이러한 소스에서 데이터를 수집하는 여러 방법과 다운스트림 Experience Platform 서비스에서 사용하기 위해 데이터 레이크 내에서 데이터가 지속되는 방법을 나타냅니다.

이 문서에서는 보다 자세한 정보를 보려면 해당 개요 설명서에 대한 링크와 함께 Experience Platform으로 데이터를 수집하는 세 가지 주요 방법을 소개합니다.

## 일괄 처리 수집

일괄 처리 수집을 사용하면 데이터를 [!DNL Experience Platform]에 일괄 처리 파일로 수집할 수 있습니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 배치가 수집되면 배치는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지를 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑됨) 및 Parquet 데이터 프레임처럼 수동으로 업로드한 데이터 파일은 이 방법을 사용하여 수집해야 합니다.

자세한 내용은 [일괄 처리 수집 개요](./batch-ingestion/overview.md)를 참조하십시오.

>[!TIP]
>
>일괄 처리 수집을 위한 입력으로 다중 라인 JSON 대신 단일 라인 JSON을 사용합니다. 한 줄 JSON을 사용하면 시스템에서 하나의 입력 파일을 여러 청크로 분할하여 병렬로 처리할 수 있으므로 성능이 향상되지만 여러 줄 JSON은 분할할 수 없습니다. 이를 통해 데이터 처리 비용을 크게 줄이고 일괄 처리 지연 시간을 개선할 수 있습니다.

## 스트리밍 수집

스트리밍 수집을 사용하면 클라이언트측 및 서버측 장치에서 실시간으로 [!DNL Experience Platform]&#x200B;(으)로 데이터를 보낼 수 있습니다. Experience Platform은 데이터 입력 기능을 사용하여 들어오는 경험 데이터를 스트리밍할 수 있도록 지원하며, 이는 데이터 레이크 내의 스트리밍 지원 데이터 세트에서 유지됩니다. 데이터 입력 기능은 수집된 데이터를 자동으로 인증하도록 구성하여 신뢰할 수 있는 소스에서 데이터가 오는지 확인할 수 있습니다.

자세한 내용은 [스트리밍 수집 개요](./streaming-ingestion/overview.md)를 참조하십시오.

## 소스

[!DNL Experience Platform]을(를) 사용하면 다양한 데이터 공급자에 대한 소스 연결을 설정할 수 있습니다. 이러한 연결을 통해 외부 데이터 소스를 인증하고, 수집 실행 시간을 설정하고, 수집 처리량을 관리할 수 있습니다.

Source 연결은 다른 Adobe 애플리케이션(Adobe Analytics 및 Adobe Audience Manager 등), 타사 클라우드 저장소 소스(예: [!DNL Azure Blob], [!DNL Amazon] S3, FTP 서버 및 SFTP 서버), 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce])에서 데이터를 수집하도록 구성할 수 있습니다.

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

### ML 지원 스키마 만들기 {#ml-assisted-schema-creation}

이제 새로운 데이터 소스를 빠르게 통합하기 위해 머신 러닝 알고리즘을 사용하여 샘플 데이터에서 스키마를 생성할 수 있습니다. 이러한 자동화는 정확한 스키마 생성을 단순화하고 오류를 줄이며 데이터 수집에서 분석 및 통찰력에 이르는 프로세스의 속도를 높입니다.

이 워크플로에 대한 자세한 내용은 [ML 지원 스키마 만들기 안내서](../xdm/ui/ml-assisted-schema-creation.md)를 참조하십시오.

## 다음 단계 및 추가 리소스

이 문서에서는 [!DNL Experience Platform]의 [!DNL Data Ingestion]에 대한 다양한 측면을 간략하게 소개합니다. 각 수집 방법에 대한 개요 설명서 를 계속 읽으면서 다양한 기능, 사용 사례 및 모범 사례를 숙지하십시오. 또한 아래 수집 개요 비디오를 시청하여 학습을 보완할 수도 있습니다. [!DNL Experience Platform]이(가) 수집된 레코드의 메타데이터를 추적하는 방법에 대한 자세한 내용은 [카탈로그 서비스 개요](../catalog/home.md)를 참조하십시오.

>[!WARNING]
>
>다음 비디오에 사용된 &quot;통합 프로필&quot;이라는 용어가 최신 상태가 아닙니다. [!DNL "Profile"] 또는 [!DNL "Real-Time Customer Profile"] 용어는 [!DNL Experience Platform] 설명서에 사용된 올바른 용어입니다. 최신 기능은 설명서 를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
