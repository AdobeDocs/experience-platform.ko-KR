---
keywords: Experience Platform;home;popular topics;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Adobe Experience Platform 데이터 통합 개요
topic: overview
description: 이 문서에서는 데이터를 플랫폼으로 인제스트하는 세 가지 주요 방법과 각 개요 문서에 대한 링크를 소개합니다.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 9%

---


# 데이터 통합 개요

Adobe Experience Platform은 마케터가 고객의 행동을 더 잘 이해할 수 있도록 여러 소스에서 수집한 데이터를 취합합니다. Adobe Experience Platform 데이터 통합은 다운스트림 [!DNL Platform] [!DNL Platform] 서비스에서 사용하기 위해 Data Lake 내에서 데이터가 지속되는 방법과 이러한 소스의 데이터를 수집하는 여러 방법을 나타냅니다.

이 문서에서는 데이터를 수집하는 세 가지 주요 방법 [!DNL Platform]에 대해 자세히 알아보려면 해당 개요 설명서에 대한 링크를 제공합니다.

## 일괄 처리

일괄 처리 처리를 사용하면 데이터를 일괄 처리 파일 [!DNL Experience Platform] 로 인제스트할 수 있습니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 배치가 수집되면 배치는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지를 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑)과 같은 수동으로 업로드된 데이터 파일 및 이 방법을 사용하여 쪽모이 세공 데이터 프레임을 인제스트해야 합니다.

자세한 내용은 [배치 처리 개요를](./batch-ingestion/overview.md) 참조하십시오.

## 스트리밍 통합

스트리밍 통합 기능을 사용하면 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 전송할 수 [!DNL Experience Platform] 있습니다. [!DNL Platform] 는 데이터 inlet을 사용하여 들어오는 경험 데이터를 스트리밍할 수 있도록 지원합니다. 이 데이터는 데이터 레이크 내의 스트리밍 지원 데이터 세트에 유지됩니다. 데이터 Inlet을 구성하여 수집한 데이터를 자동으로 인증할 수 있으므로 데이터가 신뢰할 수 있는 소스에서 나오고 있습니다.

자세한 내용은 [스트리밍 통합 개요를](./streaming-ingestion/overview.md) 참조하십시오.

## 소스

[!DNL Experience Platform] 다양한 데이터 공급자에 대한 소스 연결을 설정할 수 있습니다. 이러한 연결을 통해 외부 데이터 소스에 인증하고, 통합 실행에 대한 시간을 설정하고, 처리 처리량을 관리할 수 있습니다.

소스 연결은 다른 Adobe 응용 프로그램(Adobe Analytics 및 Adobe Audience Manager 등), 타사 클라우드 스토리지 소스(예: [!DNL Azure Blob]S3, [!DNL Amazon] FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce])의 데이터를 수집하도록 구성할 수 있습니다.

See the [Sources overview](../sources/home.md) for more information.

## 다음 단계 및 추가 리소스

이 문서는 여러 가지 측면을 간략하게 소개하 [!DNL Data Ingestion] 는 내용을 담고 [!DNL Experience Platform]있다. 다양한 기능, 사용 사례 및 모범 사례에 익숙해지려면 각 통합 방법에 대한 개요 설명서를 계속 읽어 보시기 바랍니다. 아래의 통합 개요 비디오를 통해 학습 내용을 보완할 수도 있습니다. 인제스트된 레코드의 메타데이터를 추적하는 방법에 대한 자세한 내용은 [!DNL Experience Platform] 카탈로그 서비스 개요를 참조하십시오 [](../catalog/home.md).

>[!WARNING]
>
>다음 비디오에서 사용되는 &quot;통합 프로필&quot;이 최신 상태가 아닙니다. 용어 [!DNL "Profile"] 또는 [!DNL "Real-time Customer Profile"] 는 설명서에서 사용되는 올바른 [!DNL Experience Platform] 용어입니다. 최신 기능은 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)