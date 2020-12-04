---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: February 14, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 15%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 2월 12일**

Adobe Experience Platform의 기존 기능 업데이트:

* [소스](#sources)

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| SaaS - 서비스 시스템에 대한 API 지원 | API 및 API에 대한 새 소스 커넥터 [!DNL Salesforce Service Cloud] [!DNL ServiceNow] 가 있습니다. |
| SaaS - 마케팅 시스템에 대한 API 지원 | API용 새 소스 [!DNL HubSpot] 커넥터. |
| 데이터베이스 시스템에 대한 API [!DNL NoSQL] 지원 | 새 소스 커넥터 [!DNL AWS Redshift], [!DNL Google BigQuery][!DNL MariaDB], [!DNL MySQL]및 [!DNL PostgreSQL]API를 [!DNL SQL Server] 만듭니다. |
| 클라우드 스토리지 시스템에 대한 API 지원 | API 및 API에 대한 새 소스 커넥터 [!DNL Azure Data Lake Service Gen 2] [!DNL Google Cloud Storage] 가 있습니다. |
| 클라우드 스토리지 시스템에 대한 UI 지원 | UI에 대한 새 소스 커넥터 [!DNL Google Cloud Storage] 가 있습니다. |

**알려진 문제**

* None

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).