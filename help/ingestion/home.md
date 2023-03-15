---
keywords: Experience Platform;홈;인기 항목;데이터 수집;데이터 위치;데이터 위치;데이터 관리;데이터 관리;계보;계보;배치;배치;수집된 데이터
solution: Experience Platform
title: 데이터 수집 개요
description: 이 문서에서는 각 개요 설명서에 대한 링크를 통해 데이터를 Platform에 수집하는 3가지 주요 방법을 소개합니다.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# 데이터 수집 개요

Adobe Experience Platform은 마케터가 고객의 행동을 더 잘 이해할 수 있도록 여러 소스의 데이터를 함께 가져옵니다. Adobe Experience Platform 데이터 수집은 다음과 같은 여러 가지 방법을 나타냅니다. [!DNL Platform] 는 이러한 소스에서 데이터를 수집하고 다운스트림에서 사용하기 위해 데이터가 데이터 레이크 내에서 지속되는 방식을 수집합니다 [!DNL Platform] 서비스.

이 문서에서는 데이터를 섭취하는 세 가지 주요 방법을 소개합니다 [!DNL Platform]자세한 내용은 해당 개요 설명서 링크를 참조하십시오.

## 일괄 처리 수집

일괄 처리 수집을 통해 데이터를에 수집할 수 있습니다. [!DNL Experience Platform] 배치 파일로. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 배치가 수집되면 배치는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지를 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑됨) 및 Parquet 데이터 프레임처럼 수동으로 업로드한 데이터 파일은 이 방법을 사용하여 수집해야 합니다.

다음을 참조하십시오. [일괄 처리 수집 개요](./batch-ingestion/overview.md) 추가 정보.

## 스트리밍 수집

스트리밍 수집을 사용하면 클라이언트측 및 서버측 장치에서 로 데이터를 보낼 수 있습니다. [!DNL Experience Platform] 실시간으로. [!DNL Platform] 는 데이터 입구를 사용하여 들어오는 경험 데이터를 스트리밍할 수 있도록 지원하며, 이는 데이터 레이크 내의 스트리밍 지원 데이터 세트에서 지속됩니다. 데이터 입력 기능은 수집된 데이터를 자동으로 인증하도록 구성하여 신뢰할 수 있는 소스에서 데이터가 오는지 확인할 수 있습니다.

다음을 참조하십시오. [스트리밍 수집 개요](./streaming-ingestion/overview.md) 추가 정보.

## 소스

[!DNL Experience Platform] 다양한 데이터 공급자에 대한 소스 연결을 설정할 수 있습니다. 이러한 연결을 통해 외부 데이터 소스를 인증하고, 수집 실행 시간을 설정하고, 수집 처리량을 관리할 수 있습니다.

다른 Adobe 애플리케이션(예: Adobe Analytics 및 Adobe Audience Manager), 서드파티 클라우드 스토리지 소스(예: [!DNL Azure Blob], [!DNL Amazon] S3, FTP 서버 및 SFTP 서버), 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce]).

다음을 참조하십시오. [소스 개요](../sources/home.md) 추가 정보.

## 다음 단계 및 추가 리소스

이 문서는 의 다양한 측면에 대한 간략한 소개를 제공했습니다 [!DNL Data Ingestion] 위치: [!DNL Experience Platform]. 각 수집 방법에 대한 개요 설명서 를 계속 읽으면서 다양한 기능, 사용 사례 및 모범 사례를 숙지하십시오. 또한 아래 수집 개요 비디오를 시청하여 학습을 보완할 수도 있습니다. 자세한 내용 [!DNL Experience Platform] 수집된 레코드의 메타데이터를 추적합니다. 다음을 참조하십시오. [카탈로그 서비스 개요](../catalog/home.md).

>[!WARNING]
>
>다음 비디오에 사용된 &quot;통합 프로필&quot;이라는 용어가 최신 상태가 아닙니다. 용어 [!DNL "Profile"] 또는 [!DNL "Real-Time Customer Profile"] 은(는) 다음에 사용되는 올바른 용어입니다. [!DNL Experience Platform] 설명서를 참조하십시오. 최신 기능은 설명서 를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
