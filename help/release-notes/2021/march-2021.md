---
title: Adobe Experience Platform 릴리스 노트 2021년 3월
description: Adobe Experience Platform의 2021년 3월 릴리스 정보.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2021년 3월 31일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| `add_to_array` 함수 위에 있어야 합니다 | 매개 변수로 배열을 지원하도록 기능이 업데이트되었습니다. |
| `to_array` 함수 위에 있어야 합니다 | 개체를 매개 변수로 지원하도록 기능이 업데이트되었습니다. |

자세한 내용은 다음을 참조하십시오. [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 세분화 서비스 {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 빌드하고 대상에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. [!DNL Real-Time Customer Profile] 데이터. 이러한 세그먼트는에서 중앙 집중식으로 구성 및 유지 관리됩니다. [!DNL Platform]를 사용하여 모든 Adobe 애플리케이션에서 간편하게 액세스할 수 있습니다.

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| (베타) 에지 세분화 | Edge 세그멘테이션은 세그먼트를 실시간으로 평가하므로 동일한 페이지 및 다음 페이지 개인화 사용 사례를 사용할 수 있습니다. 에지 세분화에 대한 자세한 내용은 [세그멘테이션 UI 개요](../../segmentation/ui/overview.md). |
| (Beta) 증분 세분화 | 일괄 처리 세분화에서 평가되는 기존 세그먼트 정의의 신선도를 최대 1시간까지 늘립니다. |

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| GA로 이동하는 Beta 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 압축 파일 수집을 위한 API 지원 | 이제 클라우드 저장소 소스를 사용하여 압축된 JSON 또는 구분된 파일을 미리 보고 수집할 수 있습니다. 자세한 내용은 다음 자습서를 참조하십시오. [api를 사용하여 클라우드 스토리지 데이터 수집](../../sources/tutorials/api/collect/cloud-storage.md). |
| 재귀 파일 업로드에 대한 UI 지원 | 이제 클라우드 스토리지 소스를 사용할 때 전체 폴더를 재귀적으로 수집할 수 있습니다. 전체 폴더를 수집할 때 해당 콘텐츠가 동일한 스키마를 공유하는지 확인해야 합니다. 자세한 내용은 다음 자습서를 참조하십시오. [ui에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
