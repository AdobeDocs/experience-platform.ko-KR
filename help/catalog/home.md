---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그;카탈로그 서비스;데이터 위치;데이터 위치;데이터 관리;데이터 관리;계보;계보;카탈로그;데이터 세트 활성화
solution: Experience Platform
title: 카탈로그 서비스 개요
description: 카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치와 계보를 위한 기록 시스템입니다. Experience Platform에 수집되는 모든 데이터는 파일 및 디렉터리로 데이터 레이크에 저장되지만, 카탈로그는 조회 및 모니터링을 위해 이러한 파일 및 디렉터리에 대한 메타데이터 및 설명을 포함합니다.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 개요

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치와 계보를 위한 기록 시스템입니다. 로 수집되는 모든 데이터 [!DNL Experience Platform] 에 저장됩니다. [!DNL Data Lake] 파일 및 디렉터리로, [!DNL Catalog] 조회 및 모니터링을 위해 이러한 파일 및 디렉터리의 메타데이터 및 설명을 보유합니다.

간단히 말해서 [!DNL Catalog] 는 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot; 역할을 합니다. [!DNL Experience Platform]. 다음을 사용할 수 있습니다. [!DNL Catalog] 다음 질문에 답변할 수 있습니다.

* 내 데이터는 어디에 있습니까?
* 이 데이터는 어떤 처리 단계에서 처리됩니까?
* 내 데이터에 어떤 시스템 또는 프로세스가 적용되었습니까?
* 얼마나 많은 데이터가 성공적으로 처리되었습니까?
* 처리 도중 발생한 오류

[!DNL Catalog] 는 프로그래밍 방식으로 관리할 수 있는 RESTful API를 제공합니다 [!DNL Platform] 기본 CRUD 작업을 사용하는 메타데이터. 다음을 참조하십시오. [카탈로그 개발자 안내서](api/getting-started.md) 추가 정보.

## [!DNL Catalog] 및 [!DNL Experience Platform] 서비스

리소스 [!DNL Catalog Service] 트랙이 여러 곳에서 사용됨 [!DNL Experience Platform] 서비스. 을 최대한 활용하기 위해 [!DNL Catalog's] 기능, 이러한 서비스와 상호 작용 방식을 숙지하는 것이 좋습니다 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) 시스템

[!DNL Experience Data Model] (XDM) 시스템은 표준화된 프레임워크로서 [!DNL Platform] 고객 경험 데이터를 구성합니다. [!DNL Experience Platform] 는 XDM 스키마를 활용하여 일관되고 재사용 가능한 방식으로 데이터 구조를 설명합니다.

데이터를에 수집할 때 [!DNL Platform]: 해당 데이터의 구조가 XDM 스키마에 매핑되고 [!DNL Data Lake] 을 데이터 세트의 일부로 사용하십시오. 각 데이터 세트에 대한 메타데이터는에 의해 추적됩니다. [!DNL Catalog Service]: 데이터 세트가 준수하는 XDM 스키마에 대한 참조가 포함됩니다.

XDM 시스템에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 여러 소스에서 데이터를 수집하고 내의 데이터 세트로 레코드를 유지합니다. [!DNL Data Lake]. [!DNL Catalog] 소스 또는 수집 방법에 관계없이 이러한 데이터 세트에 대한 메타데이터를 추적합니다.

일괄 처리 수집 방법을 사용하는 경우 [!DNL Catalog] 또한 배치 파일에 대한 추가 메타데이터를 추적합니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog] 는 이러한 배치 파일과 수집 후 지속되는 데이터 세트에 대한 메타데이터를 추적합니다. 일괄 처리 메타데이터에는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지에 대한 정보가 포함됩니다.

다음을 참조하십시오. [데이터 수집 개요](../ingestion/home.md) 추가 정보.

## [!DNL Catalog] 오브젝트

이전 섹션에 설명된 대로 [!DNL Catalog] 다른 항목에서 사용하는 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다 [!DNL Platform] 서비스. [!DNL Catalog] 는 이 메타데이터를 캡슐화하는 &quot;오브젝트&quot;의 자체 저장소를 유지 관리합니다. [!DNL Catalog] 객체는 다음과 같은 쿼리 가능한 표현입니다. [!DNL Platform] 데이터 자체에 액세스하지 않고도 데이터를 검색, 모니터링 및 레이블을 지정할 수 있는 데이터입니다.

다음 표에서 지원되는 다양한 객체 유형을 간략하게 설명합니다. [!DNL Catalog]:

| 오브젝트 | API 엔드포인트 | 정의 |
|---|---|---|
| 계정 | `/accounts` | 소스 연결을 만들 때 인증 자격 증명을 제공해야 합니다. 계정은 특정 유형의 연결을 만드는 데 사용된 인증 자격 증명의 컬렉션을 나타냅니다. 각 연결에는 가 지속하는 고유한 매개 변수 세트가 있습니다. [!DNL Catalog] 및 보안 유지 [!DNL Azure Key Vault]. |
| 일괄 처리 | `/batches` | 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 의 배치 객체 [!DNL Catalog] 배치의 수집 지표(예: 처리된 레코드 수 또는 디스크 크기)에 대한 개요를 제공하며 데이터 세트, 보기 및 배치 작업의 영향을 받은 기타 리소스에 대한 링크도 포함할 수 있습니다. |
| Connection | `/connections` | 연결은 조직에 고유하고 커넥터 유형에 대한 적절한 인증 자격 증명을 사용하여 구성된 소스 커넥터의 단일 인스턴스입니다. |
| 커넥터 | `/connectors` | 커넥터는 소스 연결이 다른 Adobe 애플리케이션(예: Adobe Analytics 및 Adobe Audience Manager), 서드파티 클라우드 스토리지 소스(예: [!DNL Azure Blob], [!DNL Amazon S3], FTP 서버 및 SFTP 서버), 타사 CRM 시스템(예: [!DNL Microsoft Dynamics] 및 [!DNL Salesforce]). |
| 데이터 세트 | `/dataSets` | 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터(일반적으로 테이블) 수집에 사용되는 저장소 및 관리 구성입니다. 다음을 참조하십시오. [데이터 세트 개요](./datasets/overview.md) 추가 정보. |
| 데이터 세트 파일 | `/datasetFiles` | 데이터 세트 파일은에 저장된 데이터 블록을 나타냅니다 [!DNL Platform]. 리터럴 파일의 레코드로 파일의 크기, 파일에 포함된 레코드 수 및 파일을 수집한 일괄 처리에 대한 참조를 찾을 수 있습니다. |

## 다음 단계

이 문서는에 대한 소개를 제공합니다. [!DNL Catalog Service] 및 의 광범위한 범위 내에서 작동하는 방식 [!DNL Experience Platform]. 다음을 참조하십시오. [[!DNL Catalog] 개발자 안내서](api/getting-started.md) 의 다양한 끝점과 상호 작용하는 단계 [!DNL Catalog] API. 다음 안내서도 참조하는 것이 좋습니다. [카탈로그 데이터 필터링](api/filter-data.md) API 응답에서 반환되는 데이터를 제한하는 모범 사례를 따르십시오.
