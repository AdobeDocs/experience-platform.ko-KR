---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그 서비스;카탈로그 서비스;데이터 위치;데이터 위치;데이터 관리;계보;계보;계보;카탈로그;데이터 집합 활성화
solution: Experience Platform
title: 카탈로그 서비스 개요
description: 카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 파일 및 디렉터리로 데이터 레이크에 저장되지만 카탈로그에는 조회 및 모니터링을 위해 해당 파일 및 디렉토리의 메타데이터와 설명이 저장됩니다.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 개요

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. 에 수집되는 모든 데이터 [!DNL Experience Platform] 에 저장됩니다. [!DNL Data Lake] 파일 및 디렉터리로 사용 [!DNL Catalog] 조회 및 모니터링을 위해 해당 파일 및 디렉토리에 대한 메타데이터와 설명을 포함합니다.

간단히 말해서 [!DNL Catalog] 는 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot;로 작동합니다 [!DNL Experience Platform]. 다음을 사용할 수 있습니다 [!DNL Catalog] 다음과 같은 질문에 답변합니다.

* 내 데이터가 어디에 있습니까?
* 이 데이터는 처리 단계에서 무엇입니까?
* 데이터에 대해 어떤 시스템 또는 프로세스가 수행되었습니까?
* 성공적으로 처리된 데이터의 양은 얼마입니까?
* 처리하는 동안 어떤 오류가 발생합니까?

[!DNL Catalog] 는 프로그래밍 방식으로 관리할 수 있는 RESTful API를 제공합니다 [!DNL Platform] 기본 CRUD 작업을 사용하는 메타데이터. 자세한 내용은 [카탈로그 개발자 안내서](api/getting-started.md) 추가 정보.

## [!DNL Catalog] 및 [!DNL Experience Platform] 서비스

이 리소스를 [!DNL Catalog Service] 트랙은 여러 곳에서 사용됩니다 [!DNL Experience Platform] 서비스. 다음을 최대한 활용하려면 [!DNL Catalog's] 기능, 이러한 서비스와 상호 작용하는 방법을 잘 알고 있는 것이 좋습니다 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) 시스템

[!DNL Experience Data Model] (XDM) 시스템은 [!DNL Platform] 고객 경험 데이터를 구성합니다. [!DNL Experience Platform] 은 XDM 스키마를 활용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다.

데이터를에 수집할 때 [!DNL Platform]로 지정하는 경우 해당 데이터의 구조가 XDM 스키마에 매핑되고 내에 저장됩니다 [!DNL Data Lake] 데이터 집합의 일부로 사용됩니다. 각 데이터 세트에 대한 메타데이터는 [!DNL Catalog Service]에는 데이터 세트가 준수하는 XDM 스키마 참조가 포함되어 있습니다.

XDM 시스템에 대한 일반적인 정보는 [XDM 시스템 개요](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 여러 소스의 데이터를 수집하여 레코드를 내의 데이터 세트로 유지합니다 [!DNL Data Lake]. [!DNL Catalog] 소스 또는 수집 방법에 관계없이 이러한 데이터 세트에 대한 메타데이터를 추적합니다.

일괄 처리 수집 방법을 사용할 때 [!DNL Catalog] 또한 배치 파일에 대한 추가 메타데이터도 추적합니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog] 이 배치 파일에 대한 메타데이터와 수집 후 유지되는 데이터 세트를 추적합니다. 배치 메타데이터에는 성공적으로 수집된 레코드 수와 실패한 레코드 및 관련 오류 메시지에 대한 정보가 포함됩니다.

자세한 내용은 [데이터 수집 개요](../ingestion/home.md) 추가 정보.

## [!DNL Catalog] 개체

이전 섹션에 설명된 대로, [!DNL Catalog] 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다( 다른 항목에서 사용). [!DNL Platform] 서비스. [!DNL Catalog] 은 이 메타데이터를 캡슐화하는 &quot;개체&quot;의 자체 저장소를 유지합니다. [!DNL Catalog] 객체는 [!DNL Platform] 데이터 자체에 액세스할 필요 없이 데이터를 검색, 모니터링 및 레이블을 지정할 수 있는 데이터입니다.

다음 표에서는 지원되는 다양한 객체 유형에 대해 설명합니다 [!DNL Catalog]:

| 오브젝트 | API 엔드포인트 | 정의 |
|---|---|---|
| 계정 | `/accounts` | 소스 연결을 만들 때 인증 자격 증명을 제공해야 합니다. 계정은 특정 유형의 연결을 만드는 데 사용된 인증 자격 증명 모음을 나타냅니다. 각 연결에는 다음과 같이 지속되는 고유한 매개 변수 세트가 있습니다 [!DNL Catalog] 그리고 [!DNL Azure Key Vault]. |
| 일괄 처리 | `/batches` | 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. 의 배치 개체 [!DNL Catalog] 일괄 처리의 수집 측정 단위(처리된 레코드 수 또는 디스크의 크기 등)를 간략하게 설명하고 배치 작업의 영향을 받은 데이터 세트, 보기 및 기타 리소스에 대한 링크도 포함할 수 있습니다. |
| Connection | `/connections` | 연결은 조직에 고유한 소스 커넥터의 단일 인스턴스이며, 커넥터 유형에 대한 적절한 인증 자격 증명을 사용하여 구성됩니다. |
| 커넥터 | `/connectors` | 커넥터는 소스 연결이 다른 Adobe 애플리케이션(예: Adobe Analytics 및 Adobe Audience Manager)과 타사 클라우드 스토리지 소스(예: [!DNL Azure Blob], [!DNL Amazon S3], FTP 서버 및 SFTP 서버) 및 타사 CRM 시스템(예 [!DNL Microsoft Dynamics] 및 [!DNL Salesforce]). |
| 데이터 세트 | `/dataSets` | 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터 수집(일반적으로 테이블)에 사용되는 저장 및 관리 구성입니다. 자세한 내용은 [데이터 세트 개요](./datasets/overview.md) 추가 정보. |
| 데이터 집합 파일 | `/datasetFiles` | 데이터 세트 파일은 저장된 데이터 블록을 나타냅니다 [!DNL Platform]. 리터럴 파일의 레코드로서 파일의 크기, 포함된 레코드 수 및 파일을 수집한 배치에 대한 참조를 찾을 수 있는 위치입니다. |

## 다음 단계

이 문서에서는 [!DNL Catalog Service] 그리고 더 큰 범위 내에서 작동 [!DNL Experience Platform]. 자세한 내용은 [[!DNL Catalog] 개발자 안내서](api/getting-started.md) 의 다른 종단점과 상호 작용하는 절차 [!DNL Catalog] API. 또한 다음 안내서를 참조하는 것이 좋습니다 [카탈로그 데이터 필터링](api/filter-data.md) 를 사용하여 API 응답으로 반환되는 데이터를 제한하는 우수 사례를 따를 수 있습니다.
