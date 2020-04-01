---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 데이터 통합 개요
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 데이터 통합 개요

Adobe Experience Platform은 마케터가 고객의 행동을 보다 효과적으로 파악할 수 있도록 다양한 소스의 데이터를 취합합니다. Adobe Experience Platform 데이터 수집은 플랫폼이 이러한 소스의 데이터를 수집하는 여러 방법뿐만 아니라 다운스트림 플랫폼 서비스에서 사용하기 위해 Data Lake 내에서 데이터가 지속되는 방식을 나타냅니다.

이 문서에서는 데이터를 플랫폼으로 인제스트하는 세 가지 주요 방법과 자세한 내용은 해당 개요 설명서에 대한 링크를 소개합니다.

## 일괄 처리

일괄 처리 처리를 사용하면 데이터를 Experience Platform에 일괄 처리 파일로 인제스트할 수 있습니다. 일괄 처리는 하나의 단위로 인제스트할 하나 이상의 파일로 구성된 데이터 단위입니다. 한 번 인제스트되면 일괄 처리에서는 성공적으로 인제스트된 레코드 수, 실패한 레코드 및 관련 오류 메시지 등을 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑됨)과 같은 수동으로 업로드된 데이터 파일 및 이 방법을 사용하여 쪽모이 세공 데이터 프레임을 인제스트해야 합니다.

자세한 내용은 [일괄 처리 통합 개요를](./batch-ingestion/overview.md) 참조하십시오.

## 스트리밍 통합

스트리밍 통합 기능을 사용하면 클라이언트 및 서버측 디바이스에서 Experience Platform으로 데이터를 실시간으로 전송할 수 있습니다. 플랫폼은 데이터 Inlet을 사용하여 들어오는 경험 데이터를 스트리밍할 수 있도록 지원합니다. 이 데이터는 Data Lake 내에서 스트리밍이 활성화된 데이터 세트에 유지됩니다. 데이터 수신기를 구성하여 수집한 데이터를 자동으로 인증할 수 있으므로 데이터가 신뢰할 수 있는 소스에서 오고 있습니다.

자세한 내용은 [스트리밍 통합 개요를](./streaming-ingestion/overview.md) 참조하십시오.

## 소스

경험 플랫폼을 사용하면 다양한 데이터 공급자에 대한 소스 연결을 설정할 수 있습니다. 이러한 연결을 통해 외부 데이터 소스에 대한 인증, 통합 실행 시간 설정, 통합 처리량 관리 등을 수행할 수 있습니다.

소스 연결은 다른 Adobe 응용 프로그램(예: Adobe Analytics 및 Adobe Audience Manager), 타사 클라우드 스토리지 소스(예: Azure Blob, Amazon S3, FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예: Microsoft Dynamics 및 Salesforce)에서 데이터를 수집하도록 구성할 수 있습니다.

자세한 내용은 [소스 개요를](../source-connectors/home.md) 참조하십시오.

## 다음 단계

이 문서에서는 경험 플랫폼의 데이터 수집의 다양한 측면을 간략하게 소개합니다. 다양한 기능, 사용 사례 및 모범 사례에 익숙해지려면 각 통합 방법에 대한 개요 설명서를 계속 읽어 보시기 바랍니다. Experience Platform에서 인제스트된 레코드에 대한 메타데이터를 추적하는 방법에 대한 자세한 내용은 카탈로그 [서비스 개요를](../catalog/home.md)참조하십시오.