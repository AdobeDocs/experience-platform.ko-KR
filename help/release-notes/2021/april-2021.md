---
title: Adobe Experience Platform 릴리스 노트 2021년 4월
description: Adobe Experience Platform에 대한 2021년 4월 릴리스 정보입니다.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2021년 4월 21일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 기존 데이터 흐름에 대한 매핑 편집 지원 | 이제 기존 데이터 흐름의 매핑 세트를 업데이트할 수 있습니다. 1회 수집으로 예약된 데이터 흐름에 대해서는 매핑 세트를 업데이트할 수 없습니다. 이 기능은 HTTP API, Adobe Analytics, Adobe Audience Manager 및 [!DNL Marketo Engage]. 자세한 내용은 다음 자습서를 참조하십시오. [ui에서 소스 데이터 흐름 업데이트](../../sources/tutorials/ui/update-dataflows.md). |
| 스트리밍 수집 지원 | 이제 스트리밍 소스 연결을 만들 때 데이터 준비 기능을 사용할 수 있습니다. 자세한 내용은 다음 자습서를 참조하십시오. [ui에서 스트리밍 소스 연결 만들기](../../sources/tutorials/ui/create/streaming/http.md). |

자세한 내용은 다음을 참조하십시오. [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

XDM(경험 데이터 모델)은 디지털 경험의 성능을 개선하기 위해 설계된 오픈 소스 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 산업별 스키마 권장 사항 | 스키마 편집기 UI에서 클래스 및 스키마 필드 그룹을 선택할 때 새 필터를 사용하여 특정 산업을 기반으로 권장되는 표준 구성 요소를 볼 수 있습니다. 다음에서 설명서를 참조하십시오. [업계 데이터 모델](https://www.adobe.com/go/xdm-industry-erds-en) 다양한 산업 사용 사례에서 이러한 구성 요소가 서로 관련되는 방식에 대한 자세한 정보. |

## [!DNL Intelligent Services] {#intelligent-services}

인텔리전트 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준의 전문 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

### 고객 AI

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Analytics 데이터 지원 | CEE(소비자 경험 이벤트) 스키마를 준수하도록 데이터를 ETL할 필요 없이 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터 세트를 지원하도록 기능이 업데이트되었습니다. |
| Adobe Audience Manager 데이터 지원 | CEE(소비자 경험 이벤트) 스키마를 준수하도록 데이터를 ETL할 필요 없이 Audience Manager 소스 커넥터를 통해 Adobe Audience Manager 데이터 세트를 지원하도록 기능이 업데이트되었습니다. |
| 모델 성능 요약 | 이제 고객 AI에 [모델 성능 요약 탭](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) service instance insights 페이지 내에서 참조할 수 있습니다. 모델 성능 탭에는 모든 실제 전환율과 이탈률이 표시됩니다. 이를 통해 각 성향 버킷에서 무슨 일이 일어나고 있는지 해독하고 이해할 수 있습니다. |

지원되는 데이터 세트에 대한 자세한 내용은 [[!DNL Intelligent Services] 데이터 준비 설명서](../../intelligent-services/data-preparation.md).

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Analytics 데이터 지원 | CEE(소비자 경험 이벤트) 스키마를 준수하도록 데이터를 ETL할 필요 없이 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터 세트를 지원하도록 기능이 업데이트되었습니다. |

지원되는 데이터 세트에 대한 자세한 내용은 [[!DNL Intelligent Services] 데이터 준비 설명서](../../intelligent-services/data-preparation.md).

## 세분화 서비스 {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 빌드하고 대상에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. [!DNL Real-Time Customer Profile] 데이터. 이러한 세그먼트는 플랫폼에서 중앙에서 구성 및 유지 관리되므로 모든 Adobe 애플리케이션에서 쉽게 액세스할 수 있습니다.

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 추가 집계 함수 | 세그먼트 빌더에 카운트 함수가 추가되었습니다. 카운트 함수를 사용하면 지정된 이벤트가 수행된 횟수를 카운트할 수 있습니다. count 함수에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#count-functions) |

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL Marketo Engage] (베타) | 이제 다음을 만들 수 있습니다 [!DNL Marketo Engage] UI를 사용하여 소스 연결을 통해 B2B 데이터를 플랫폼으로 가져오고 플랫폼 연결 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지합니다. 자세한 내용은 [[!DNL Marketo Engage] 소스 커넥터 설명서](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| GA로 이동하는 Beta 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
