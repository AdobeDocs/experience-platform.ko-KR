---
title: Adobe Experience Platform 릴리스 노트 - 2021년 9월
description: Adobe Experience Platform에 대한 2021년 9월 릴리스 노트입니다.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 9월 29일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [소스](#sources)

## 데이터 수집 {#ingestion}

Adobe Experience Platform 데이터 섭취는 플랫폼이 다양한 소스에서 데이터를 수집하는 여러 메서드와 다운스트림 플랫폼 서비스에서 사용하기 위해 Data Lake 내에서 해당 데이터가 지속되는 방법을 나타냅니다.

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 배치 수집을 사용하여 프로필 레코드 업데이트 또는 패치 | 이제 실시간 고객 프로필을 사용하면 배치 섭취 를 통해 개별 프로필 레코드 데이터의 프로필 속성을 업데이트할 수 있습니다. 자세한 내용은 [배치 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md). |

Platform으로 데이터를 수집하는 방법에 대한 자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 스트리밍 데이터 흐름 지원 | 이제 스트리밍 데이터 흐름을 만들 때 데이터 준비 함수를 사용할 수 있습니다. [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], 및 [!DNL Google PubSub]. 다음에서 자습서를 참조하십시오. [클라우드 스토리지 소스를 위한 스트리밍 데이터 흐름 만들기](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) 추가 정보. |

에 대해 자세히 알아보려면 [!DNL Data Prep] 참조 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| [!DNL Data Landing Zone] | 이제 다음을 만들 수 있습니다 [!DNL Data Landing Zone] 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] is [!DNL Azure Blob] Platform에서 프로비저닝한 스토리지 인터페이스로, 파일을 플랫폼으로 가져올 수 있도록 클라우드 기반의 보안 파일 스토리지 기능을 이용할 수 있습니다. 자세한 내용은 [[!DNL Data Landing Zone] 개요](../../sources/connectors/cloud-storage/data-landing-zone.md) 추가 정보. |
| [!DNL Snowflake] | 이제 다음을 만들 수 있습니다 [!DNL Snowflake] 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/databases/snowflake.md) 데이터를에서 [!DNL Snowflake] Platform으로 데이터베이스를 전환합니다. 자세한 내용은 [[!DNL Snowflake] 개요](../../sources/connectors/databases/snowflake.md) 추가 정보. |
| [!DNL SFTP] 소스 개선 사항 | 사용자 정의 포트 번호는 수동으로 설정할 수 있습니다 [!DNL SFTP] 소스 연결. 자세한 내용은 [[!DNL SFTP] 개요](../../sources/connectors/cloud-storage/sftp.md) 추가 정보. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
