---
keywords: Experience Platform;홈;인기 주제;카탈로그 서비스;카탈로그;카탈로그 서비스;데이터 위치;데이터 위치;데이터 관리;데이터 관리;계보;계보;카탈로그;데이터 세트 활성화
solution: Experience Platform
title: 카탈로그 서비스 개요
description: 카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 보유합니다.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 8%

---

# [!DNL Catalog Service] 개요

[!DNL Catalog Service]은(는) Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. [!DNL Experience Platform]에 수집된 모든 데이터는 [!DNL Data Lake]에 파일 및 디렉터리로 저장되지만 [!DNL Catalog]에는 조회 및 모니터링을 위해 해당 파일 및 디렉터리의 메타데이터와 설명이 들어 있습니다.

간단히 말해, [!DNL Catalog]은(는) [!DNL Experience Platform] 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot; 역할을 합니다. [!DNL Catalog]을(를) 사용하여 다음 질문에 답변할 수 있습니다.

* 내 데이터는 어디에 있습니까?
* 이 데이터는 어떤 처리 단계에서 처리됩니까?
* 내 데이터에 어떤 시스템 또는 프로세스가 적용되었습니까?
* 얼마나 많은 데이터가 성공적으로 처리되었습니까?
* 처리 도중 발생한 오류

[!DNL Catalog]은(는) 기본 CRUD 작업을 사용하여 [!DNL Experience Platform] 메타데이터를 프로그래밍 방식으로 관리할 수 있는 RESTful API를 제공합니다. 자세한 내용은 [카탈로그 개발자 안내서](api/getting-started.md)를 참조하세요.

## [!DNL Catalog] 및 [!DNL Experience Platform] 서비스

[!DNL Catalog Service]개 트랙이 있는 리소스를 여러 [!DNL Experience Platform] 서비스에서 사용하고 있습니다. [!DNL Catalog's] 기능을 최대한 활용하려면 이러한 서비스와 [!DNL Catalog]과(와) 상호 작용하는 방법에 익숙해지는 것이 좋습니다.

### [!DNL Experience Data Model]&#x200B;(XDM) 시스템

[!DNL Experience Data Model]&#x200B;(XDM) 시스템은 [!DNL Experience Platform]이(가) 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. [!DNL Experience Platform]은(는) XDM 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다.

데이터를 [!DNL Experience Platform]에 수집하면 해당 데이터의 구조가 XDM 스키마에 매핑되고 데이터 집합의 일부로 [!DNL Data Lake] 내에 저장됩니다. 각 데이터 세트에 대한 메타데이터는 [!DNL Catalog Service]에 의해 추적되며, 여기에는 데이터 세트가 준수하는 XDM 스키마에 대한 참조가 포함됩니다.

XDM 시스템에 대한 일반적인 정보는 [XDM 시스템 개요](../xdm/home.md)를 참조하십시오.

### [!DNL Data Ingestion]

[!DNL Experience Platform]은(는) 여러 소스에서 데이터를 수집하고 [!DNL Data Lake] 내의 데이터 세트로 레코드를 유지합니다. [!DNL Catalog]은(는) 해당 데이터 세트의 소스 또는 수집 방법과 관계없이 해당 데이터 세트에 대한 메타데이터를 추적합니다.

일괄 처리 수집 방법을 사용하는 경우 [!DNL Catalog]은(는) 일괄 처리 파일에 대한 추가 메타데이터도 추적합니다. 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog]은(는) 이러한 배치 파일과 수집 후 지속되는 데이터 세트에 대한 메타데이터를 추적합니다. 일괄 처리 메타데이터에는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지에 대한 정보가 포함됩니다.

자세한 내용은 [데이터 수집 개요](../ingestion/home.md)를 참조하십시오.

## 개체 [!DNL Catalog]개

이전 섹션에 설명된 대로 [!DNL Catalog]은(는) 다른 [!DNL Experience Platform] 서비스에서 사용하는 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다. [!DNL Catalog]은(는) 이 메타데이터를 캡슐화하는 &quot;개체&quot;의 자체 저장소를 유지 관리합니다. [!DNL Catalog] 개체는 데이터 자체에 액세스하지 않고도 데이터를 검색, 모니터링 및 레이블을 지정할 수 있도록 해주는 [!DNL Experience Platform] 데이터를 쿼리할 수 있는 표현입니다.

다음 표에서는 [!DNL Catalog]에서 지원하는 다양한 개체 유형에 대해 설명합니다.

| 오브젝트 | API 엔드포인트 | 정의 |
|---|---|---|
| 배치 | `/batches` | 배치는 단일 단위로 수집할 하나 이상의 파일로 구성된 데이터 단위입니다. [!DNL Catalog]의 일괄 처리 개체는 일괄 처리의 수집 지표(예: 처리된 레코드 수 또는 디스크 크기)에 대한 개요를 제공하며, 일괄 처리 작업의 영향을 받은 데이터 세트, 보기 및 기타 리소스에 대한 링크도 포함할 수 있습니다. |
| 데이터 세트 | `/dataSets` | 데이터 집합은 스키마(열) 및 필드(행)를 포함하는 데이터(일반적으로 테이블) 수집에 사용되는 저장소 및 관리 구성입니다. 자세한 내용은 [데이터 세트 개요](./datasets/overview.md)를 참조하십시오. |
| 데이터 세트 파일 | `/datasetFiles` | 데이터 집합 파일은 [!DNL Experience Platform]에 저장된 데이터 블록을 나타냅니다. 리터럴 파일의 레코드로 파일의 크기, 파일에 포함된 레코드 수 및 파일을 수집한 일괄 처리에 대한 참조를 찾을 수 있습니다. |

## 다음 단계

이 문서에서는 [!DNL Catalog Service]에 대한 소개와 [!DNL Experience Platform]의 더 큰 범위 내에서 작동하는 방식을 제공했습니다. 해당 [!DNL Catalog] API의 다양한 끝점과 상호 작용하는 방법에 대한 단계는 [[!DNL Catalog] 개발자 안내서](api/getting-started.md)를 참조하십시오. API 응답에서 반환되는 데이터를 제한하는 모범 사례를 따르려면 [카탈로그 데이터 필터링](api/filter-data.md)에 대한 안내서를 참조하는 것이 좋습니다.
