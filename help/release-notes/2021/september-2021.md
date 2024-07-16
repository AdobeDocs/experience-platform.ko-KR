---
title: Adobe Experience Platform 릴리스 노트 2021년 9월
description: Adobe Experience Platform에 대한 2021년 9월 릴리스 정보입니다.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 26%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2021년 9월 29일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [소스](#sources)

## 데이터 수집 {#ingestion}

Adobe Experience Platform 데이터 수집은 플랫폼이 다양한 소스에서 데이터를 수집하는 여러 방법과 다운스트림 플랫폼 서비스에서 사용하기 위해 데이터 레이크 내에서 데이터가 지속되는 방법을 나타냅니다.

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 일괄 처리 수집을 사용하여 프로필 레코드 업데이트 또는 패치 | 이제 실시간 고객 프로필을 통해 일괄 처리 수집을 통해 개별 프로필 레코드 데이터의 프로필 속성을 업데이트할 수 있습니다. 자세한 내용은 [일괄 처리 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md)를 참조하세요. |

플랫폼으로 데이터 수집에 대한 자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md)를 참조하세요.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]을(를) 사용하면 데이터 엔지니어가 XDM(Experience Data Model)에서 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 스트리밍 데이터 흐름 지원 | 이제 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] 및 [!DNL Google PubSub]에 대한 스트리밍 데이터 흐름을 만들 때 데이터 준비 기능을 사용할 수 있습니다. 자세한 내용은 [클라우드 저장소 소스의 스트리밍 데이터 흐름 만들기](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)에 대한 자습서를 참조하십시오. |

[!DNL Data Prep]에 대한 자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하세요.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| [!DNL Data Landing Zone] | 이제 [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)를 사용하여 [!DNL Data Landing Zone] 원본 연결을 만들 수 있습니다. [!DNL Data Landing Zone]은(는) 플랫폼에서 프로비저닝한 [!DNL Azure Blob] 스토리지 인터페이스로서, 파일을 플랫폼으로 가져올 수 있는 안전한 클라우드 기반 파일 스토리지 기능에 액세스할 수 있도록 허용합니다. 자세한 내용은 [[!DNL Data Landing Zone] 개요](../../sources/connectors/cloud-storage/data-landing-zone.md)를 참조하세요. |
| [!DNL Snowflake] | 이제 [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/databases/snowflake.md)를 사용하여 [!DNL Snowflake] 원본 연결을 만들어 [!DNL Snowflake] 데이터베이스에서 플랫폼으로 데이터를 가져올 수 있습니다. 자세한 내용은 [[!DNL Snowflake] 개요](../../sources/connectors/databases/snowflake.md)를 참조하세요. |
| [!DNL SFTP] 소스 개선 사항 | [!DNL SFTP] 원본 연결을 만들 때 사용자 지정 포트 번호를 수동으로 설정할 수 있습니다. 자세한 내용은 [[!DNL SFTP] 개요](../../sources/connectors/cloud-storage/sftp.md)를 참조하세요. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
