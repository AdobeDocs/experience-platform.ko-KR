---
keywords: Experience Platform;홈;인기 항목;데이터 수집;데이터 위치;데이터 관리;데이터 관리;계보;계보;배치;일괄 처리;수집된 데이터
solution: Experience Platform
title: 데이터 수집 개요
description: 이 문서에서는 Platform으로 데이터를 수집하는 세 가지 주요 방법과 각 개요 설명서에 대한 링크를 통해 자세한 정보를 설명합니다.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 14%

---

# 데이터 수집 개요

Adobe Experience Platform은 마케터가 고객의 행동을 더 잘 이해할 수 있도록 여러 소스의 데이터를 함께 가져옵니다. Adobe Experience Platform 데이터 수집은 [!DNL Platform] 는 이러한 소스의 데이터와 해당 데이터가 다운스트림으로 사용하기 위해 Data Lake 내에서 지속되는 방법을 설정합니다. [!DNL Platform] 서비스.

이 문서에서는 데이터를 수집하는 세 가지 주요 방법을 소개합니다 [!DNL Platform]자세한 내용은 해당 개요 설명서에 대한 링크를 참조하십시오.

## 일괄 처리 수집

배치 수집 기능을 사용하면 데이터를 수집 [!DNL Experience Platform] 를 배치 파일로 추가할 수 있습니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 배치가 수집되면 배치는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지를 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑됨) 및 Parquet 데이터 프레임처럼 수동으로 업로드한 데이터 파일은 이 방법을 사용하여 수집해야 합니다.

자세한 내용은 [배치 수집 개요](./batch-ingestion/overview.md) 추가 정보.

## 스트리밍 수집

스트리밍 수집 기능을 사용하여 클라이언트 및 서버측 장치에서 다음으로 데이터를 보낼 수 있습니다 [!DNL Experience Platform] 실시간으로 [!DNL Platform] 에서는 데이터 레이크 내에서 스트리밍이 가능한 데이터 세트에 지속되는 수신 경험 데이터를 스트리밍하기 위해 데이터 inlet을 사용할 수 있도록 지원합니다. 신뢰할 수 있는 소스에서 데이터가 전달되도록 하여 수집하는 데이터를 자동으로 인증하도록 데이터 입력기를 구성할 수 있습니다.

자세한 내용은 [스트리밍 수집 개요](./streaming-ingestion/overview.md) 추가 정보.

## 소스

[!DNL Experience Platform] 다양한 데이터 공급자에 대한 소스 연결을 설정할 수 있습니다. 이러한 연결을 통해 외부 데이터 소스를 인증하고 수집 실행 시간을 설정하고 수집 처리량을 관리할 수 있습니다.

소스 연결은 다른 Adobe 애플리케이션(예: Adobe Analytics 및 Adobe Audience Manager), 타사 클라우드 스토리지 소스(예: [!DNL Azure Blob], [!DNL Amazon] S3, FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예 [!DNL Microsoft Dynamics] 및 [!DNL Salesforce]).

자세한 내용은 [소스 개요](../sources/home.md) 추가 정보.

## 다음 단계 및 추가 리소스

이 문서에서는 [!DNL Data Ingestion] in [!DNL Experience Platform]. 각 수집 방법에 대한 개요 설명서를 계속 읽어 다른 기능, 사용 사례 및 우수 사례를 숙지하십시오. 아래의 수집 개요 비디오를 시청하여 학습을 보완할 수도 있습니다. 방법에 대한 자세한 정보 [!DNL Experience Platform] 수집된 레코드에 대한 메타데이터를 추적합니다. 자세한 내용은 [카탈로그 서비스 개요](../catalog/home.md).

>[!WARNING]
>
>다음 비디오에서 사용되는 &quot;통합 프로필&quot;은 최신 상태가 아닙니다. 용어 [!DNL "Profile"] 또는 [!DNL "Real-Time Customer Profile"] 에서 사용하는 올바른 용어입니다. [!DNL Experience Platform] 설명서. 최신 기능에 대해서는 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
