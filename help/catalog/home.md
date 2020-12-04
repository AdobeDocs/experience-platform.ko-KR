---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: 카탈로그 서비스 개요
topic: overview
description: 카탈로그서비스란 Adobe Experience Platform의 데이터 위치와 혈통에 대한 기록 시스템이다. Experience Platform에 인제스트된 모든 데이터는 파일과 디렉터리로 Data Lake에 저장되지만, 카탈로그는 조회 및 모니터링을 위해 이러한 파일 및 디렉토리의 메타데이터와 설명을 저장합니다.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 5%

---


# [!DNL Catalog Service]개요

[!DNL Catalog Service] adobe experience platform의 데이터 위치와 혈통에 대한 기록 시스템이다. 인제스트된 모든 데이터 [!DNL Experience Platform] 는 파일 및 디렉토리 [!DNL Data Lake] 로 저장되지만, 조회 및 모니터링을 위해 해당 파일 및 디렉토리의 메타데이터와 설명을 [!DNL Catalog] 보관합니다.

간단히 말해, 데이터 내 [!DNL Catalog] 에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 스토어 또는 &quot;카탈로그&quot;로 사용할 수 [!DNL Experience Platform]있습니다. 다음 질문 [!DNL Catalog] 에 응답하는 데 사용할 수 있습니다.

* 데이터가 어디에 있습니까?
* 이 데이터는 어느 단계에서 처리됩니까?
* 내 데이터에 대해 어떤 시스템 또는 프로세스가 작용했습니까?
* 성공적으로 처리된 데이터의 양은 얼마입니까?
* 처리하는 동안 어떤 오류가 발생했습니까?

[!DNL Catalog] 은 기본 CRUD 작업을 사용하여 프로그래밍 방식으로 [!DNL Platform] 메타데이터를 관리할 수 있도록 해주는 RESTful API를 제공합니다. See the [Catalog developer guide](api/getting-started.md) for more information.

## [!DNL Catalog] 및 [!DNL Experience Platform] 서비스

추적하는 리소스 [!DNL Catalog Service] 는 여러 [!DNL Experience Platform] 서비스에서 사용됩니다. 기능을 최대한 활용하려면 이러한 서비스와 서비스 이용 방법에 대해 잘 알고 있어야 합니다 [!DNL Catalog's] [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) 시스템

[!DNL Experience Data Model] (XDM) 시스템은 고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크입니다. [!DNL Experience Platform] XDM 스키마를 활용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다.

데이터를 데이터 [!DNL Platform]로 인제스트하면 해당 데이터의 구조가 XDM 스키마에 매핑되고 데이터 세트의 일부로 해당 데이터 세트 내에 [!DNL Data Lake] 저장됩니다. 각 데이터 세트에 대한 메타데이터는 데이터 세트 [!DNL Catalog Service]가 준수하는 XDM 스키마에 대한 참조를 포함하는

XDM 시스템에 대한 자세한 내용은 [XDM 시스템 개요를 참조하십시오](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 여러 소스의 데이터를 인제스트하고 데이터 세트 내의 데이터 세트로 레코드를 유지합니다 [!DNL Data Lake]. [!DNL Catalog] 데이터 집합의 소스 또는 통합 방법에 관계없이 이러한 데이터 세트에 대한 메타데이터를 추적합니다.

일괄 처리 처리 방법을 사용할 때 일괄 처리 파일에 대한 추가 메타데이터도 [!DNL Catalog] 추적합니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog] 이러한 일괄 처리 파일에 대한 메타데이터와 통합 후 유지되는 데이터 세트를 추적합니다. 배치 메타데이터에는 성공적으로 인제스트한 레코드 수, 실패한 레코드 및 관련 오류 메시지 등에 대한 정보가 포함됩니다.

자세한 내용은 [데이터 수집 개요를](../ingestion/home.md) 참조하십시오.

## [!DNL Catalog] 개체

이전 섹션에 설명된 대로 [!DNL Catalog] 다른 [!DNL Platform] 서비스에서 사용되는 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다. [!DNL Catalog] 은 이 메타데이터를 캡슐화하는 &quot;objects&quot;의 자체 저장소를 유지합니다. [!DNL Catalog] 개체는 데이터 자체에 액세스할 필요 없이 데이터를 검색, 모니터링 및 레이블을 지정할 수 있도록 해주는 [!DNL Platform] 데이터의 쿼리 가능한 표현입니다.

다음 표에서는 지원되는 다양한 객체 유형에 대해 대략적으로 설명합니다 [!DNL Catalog].

| 개체 | API 끝점 | 정의 |
|---|---|---|
| 계정 | `/accounts` | 소스 연결을 만들 때는 인증 자격 증명을 제공해야 합니다. 계정은 특정 유형의 연결을 만드는 데 사용된 인증 자격 증명 모음을 나타냅니다. 각 연결에는 한 연결에 의해 지속되고 보안 상태가 되는 고유한 매개 변수 세트 [!DNL Catalog] 가 있습니다 [!DNL Azure Key Vault]. |
| 일괄 처리 | `/batches` | 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 배치 개체는 배치의 처리 지표(예: 처리된 레코드 수 또는 디스크의 크기 등)에 대한 개요를 [!DNL Catalog] 설명하고, 일괄 처리 작업으로 인해 영향을 받은 데이터 세트, 보기 및 기타 리소스에 대한 링크도 포함할 수 있습니다. |
| 연결 | `/connections` | 연결은 조직 고유의 소스 커넥터 단일 인스턴스이며 커넥터 유형에 적절한 인증 자격 증명을 사용하여 구성됩니다. |
| 커넥터 | `/connectors` | 커넥터는 소스 연결이 다른 Adobe 응용 프로그램(Adobe Analytics 및 Adobe Audience Manager 등), 타사 클라우드 스토리지 소스( [!DNL Azure Blob]예: [!DNL Amazon S3]FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce])에서 데이터를 수집하는 방법을 정의합니다. |
| 데이터 집합 | `/dataSets` | 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 컬렉션에 사용되는 저장소 및 관리 구성체입니다. See the [datasets overview](./datasets/overview.md) for more information. |
| 데이터 집합 파일 | `/datasetFiles` | 데이터 세트 파일은 저장된 데이터 블록을 나타냅니다 [!DNL Platform]. 파일에 대한 기록으로서, 여기에서 파일의 크기, 파일에 포함된 레코드 수 및 파일을 인제스트한 일괄 처리에 대한 참조를 찾을 수 있습니다. |

## 다음 단계

본 문서는 더 큰 범위 내에서 [!DNL Catalog Service] 작동하는 방식과 기능에 대한 소개를 제공합니다 [!DNL Experience Platform]. 해당 API의 다른 끝점과 상호 작용하는 단계는 [[!DNL Catalog] 개발자 안내서를](api/getting-started.md) 참조하십시오 [!DNL Catalog] . 또한 API 응답으로 반환되는 데이터를 제한하는 모범 사례를 따르려면 카탈로그 데이터 [](api/filter-data.md) 필터링 지침을 참조하는 것이 좋습니다.