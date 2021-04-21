---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그 서비스;카탈로그 서비스;데이터 위치;데이터 관리;리니지;리니지;카탈로그;데이터 집합 사용
solution: Experience Platform
title: 카탈로그 서비스 개요
topic-legacy: overview
description: Catalog Service는 Adobe Experience Platform 내의 데이터 위치 및 리니지에 대한 레코드 시스템입니다. Experience Platform에 인제스트된 모든 데이터가 파일 및 디렉터리로 Data Lake에 저장되지만 카탈로그는 조회 및 모니터링을 위해 해당 파일 및 디렉토리에 대한 메타데이터와 설명을 보관합니다.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 개요

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치 및 리니지에 대한 기록 시스템입니다. [!DNL Experience Platform]에 인제스트된 모든 데이터가 [!DNL Data Lake]에 파일 및 디렉터리로 저장되지만 [!DNL Catalog]에는 조회 및 모니터링을 위해 해당 파일 및 디렉토리의 메타데이터와 설명이 들어 있습니다.

간단히 말해 [!DNL Catalog]은 [!DNL Experience Platform] 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot;로 작동합니다. [!DNL Catalog]을 사용하여 다음 질문에 답변할 수 있습니다.

* 내 데이터는 어디에 있습니까?
* 이 데이터는 어느 단계에서 처리됩니까?
* 데이터에서 어떤 시스템 또는 프로세스가 작용했습니까?
* 성공적으로 처리된 데이터 양은 얼마나 됩니까?
* 처리하는 동안 어떤 오류가 발생합니까?

[!DNL Catalog] 는 기본 CRUD 작업을 사용하여 메타데이터를 프로그래밍 방식으로 관리할 수  [!DNL Platform] 있는 RESTful API를 제공합니다. 자세한 내용은 [카탈로그 개발자 안내서](api/getting-started.md)를 참조하십시오.

## [!DNL Catalog] 및  [!DNL Experience Platform] 서비스

[!DNL Catalog Service]이(가) 추적하는 리소스를 여러 [!DNL Experience Platform] 서비스에서 사용합니다. [!DNL Catalog's] 기능을 최대한 활용하려면 이러한 서비스와 [!DNL Catalog]와의 상호 작용을 잘 아는 것이 좋습니다.

### [!DNL Experience Data Model] (XDM) 시스템

[!DNL Experience Data Model] (XDM) 시스템은 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다. [!DNL Experience Platform] XDM 스키마를 활용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다.

데이터를 [!DNL Platform]으로 인제스트하면 해당 데이터의 구조가 XDM 스키마에 매핑되고 데이터 세트의 일부로 [!DNL Data Lake] 내에 저장됩니다. 각 데이터 세트에 대한 메타데이터는 데이터 세트에 따르는 XDM 스키마에 대한 참조를 포함하는 [!DNL Catalog Service]에 의해 추적됩니다.

XDM 시스템에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md)를 참조하십시오.

### [!DNL Data Ingestion]

[!DNL Experience Platform] 여러 소스의 데이터를 인제스트하고 레코드를 데이터 세트 내의 데이터 세트로  [!DNL Data Lake]유지합니다. [!DNL Catalog] 데이터 세트의 소스 또는 통합 방법에 상관없이 이러한 데이터 세트에 대한 메타데이터를 추적합니다.

일괄 처리 처리 방법을 사용할 때 [!DNL Catalog]도 일괄 처리 파일의 추가 메타데이터를 추적합니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog] 이러한 일괄 처리 파일의 메타데이터와 통합 후 지속되는 데이터 세트를 추적합니다. 배치 메타데이터에는 성공적으로 인제스트한 레코드 수 및 실패한 레코드 및 관련 오류 메시지에 대한 정보가 포함됩니다.

자세한 내용은 [데이터 통합 개요](../ingestion/home.md)를 참조하십시오.

## [!DNL Catalog] 객체

이전 섹션에 요약된 대로 [!DNL Catalog]은 다른 [!DNL Platform] 서비스에서 사용하는 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다. [!DNL Catalog] 이 메타데이터를 캡슐화하는 &quot;객체&quot;의 저장소를 유지합니다. [!DNL Catalog] 객체는 데이터 자체에 액세스할 필요 없이 데이터를 검색, 모니터링 및 레이블을 지정할 수  [!DNL Platform] 있는 데이터에 대해 쿼리할 수 있는 표현입니다.

다음 표에서는 [!DNL Catalog]에서 지원하는 서로 다른 객체 유형에 대해 대략적으로 설명합니다.

| 개체 | API 끝점 | 정의 |
|---|---|---|
| 계정 | `/accounts` | 소스 연결을 만들 때 인증 자격 증명을 제공해야 합니다. 계정은 특정 유형의 연결을 만드는 데 사용된 인증 자격 증명 모음을 나타냅니다. 각 연결에는 [!DNL Catalog]에 의해 지속되고 [!DNL Azure Key Vault]에 보안되는 고유한 매개 변수 집합이 있습니다. |
| 일괄 처리 | `/batches` | 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog]의 일괄 처리 개체는 일괄 처리의 통합 지표(예: 처리된 레코드 수 또는 디스크의 크기 등)에 대한 개요를 설명하고, 일괄 처리 작업으로 인해 영향을 받은 데이터 세트, 보기 및 기타 리소스에 대한 링크도 포함할 수 있습니다. |
| Connection | `/connections` | 연결은 조직 고유의 소스 커넥터의 단일 인스턴스이며 커넥터 유형에 대한 적절한 인증 자격 증명을 사용하여 구성됩니다. |
| 커넥터 | `/connectors` | 커넥터는 소스 연결이 다른 Adobe 응용 프로그램(예: Adobe Analytics 및 Adobe Audience Manager), 타사 클라우드 스토리지 소스(예: [!DNL Azure Blob], [!DNL Amazon S3], FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce])에서 데이터를 수집하는 방법을 정의합니다. |
| 데이터 세트 | `/dataSets` | 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 컬렉션에 사용되는 저장소 및 관리 구조입니다. 자세한 내용은 [데이터 집합 개요](./datasets/overview.md)를 참조하십시오. |
| 데이터 세트 파일 | `/datasetFiles` | 데이터 세트 파일은 [!DNL Platform]에 저장된 데이터 블록을 나타냅니다. 리터럴 파일의 레코드로서 파일의 크기, 파일에 포함된 레코드 수 및 파일을 인제스트한 일괄 처리에 대한 참조를 찾을 수 있는 곳입니다. |

## 다음 단계

이 문서에서는 [!DNL Catalog Service] 및 [!DNL Experience Platform]의 보다 큰 범위 내에서 작동하는 방식을 소개합니다. 해당 [!DNL Catalog] API의 다른 끝점과 상호 작용하는 단계는 [[!DNL Catalog] 개발자 안내서](api/getting-started.md)를 참조하십시오. API 응답으로 반환되는 데이터를 제한하는 모범 사례를 따르려면 [카탈로그 데이터 필터링 안내서](api/filter-data.md)를 참조할 것을 권장합니다.
