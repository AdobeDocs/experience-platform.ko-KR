---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트(2021년 1월 27일)
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: cf70b21f3a8c02b25e5acd3be8c8feaa3f52a5e3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 8%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 1월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변형 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 정규 표현식 함수 | [!DNL Data Prep] 이제 매퍼가 일반 표현식을 기반으로 입력 필드의 일부를 일치 및 추출할 수 있습니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 한편, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Audience Manager 소스 커넥터 개선 사항 | 이제 Audience Manager에서 인제스트까지 개별 자사 세그먼트를 필터링하고 선택할 수 있을 뿐만 아니라 자사 트레이트를 필터링할 수 있습니다. 자세한 내용은 [Audience Manager 소스 커넥터 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)의 자습서를 참조하십시오. |
| [!DNL Google BigQuery] 소스 커넥터 개선 사항 | 이제 [!DNL BigQuery] 소스 커넥터를 사용하여 하나의 흐름 실행에서 10GB 이상의 파일을 인제스트할 수 있습니다. 자세한 내용은 [[!DNL BigQuery] 소스 커넥터 개요](../../sources/connectors/databases/bigquery.md)를 참조하십시오. |
| 클라우드 스토리지를 위한 복잡한 데이터 유형 지원 | 이제 클라우드 스토리지 소스 커넥터를 사용할 때 JSON 파일의 배열과 같은 복잡한 데이터 유형을 인제스트할 수 있습니다. 자세한 내용은 UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 또는 [API](../../sources/tutorials/api/collect/cloud-storage.md)를 사용하여 클라우드 저장소 데이터 흐름 [을 만드는 방법에 대한 자습서를 참조하십시오. [!DNL Flow Service]  |
| [!DNL Microsoft Dynamics] 소스에 대한 서비스 주 키 기반 인증 지원 | 이제 서비스 인증 키를 사용하여 암호 기반 인증에 대한 대안으로 [!DNL Dynamics] 계정에 인증할 수 있습니다. 자세한 내용은 [[!DNL Dynamics] 소스 커넥터 개요](../../sources/connectors/crm/ms-dynamics.md)를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
