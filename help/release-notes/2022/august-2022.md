---
title: Adobe Experience Platform 릴리스 노트 - 2022년 8월
description: Adobe Experience Platform에 대한 2022년 8월 릴리스 노트입니다.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 9%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 8월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 준비](#data-prep)
- [소스](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고가 있는 레코드 수집 지원 | 이제 데이터 준비에서 경고(중요하지 않은 오류)를 필드에 현지화하고 나머지 행을 수집할 수 있습니다. 이제 모든 매퍼 변환 오류는 경고 및 부분적으로 수집된 행으로 보고되며, 경고 메시지가 표시됩니다.  경고 및 진단 세부 정보가 있는 레코드에서도 모니터링이 지원됩니다. 경고가 있는 레코드의 일부 섭취는 현재 스트리밍 데이터만 사용할 수 있습니다. 다음 문서를 검토하십시오. [경고가 있는 레코드 수집](../../sources/tutorials/ui/monitor-streaming.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

에 대해 자세히 알아보려면 [!DNL Data Prep]를 참조하고 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 셀프 서비스 소스(배치 SDK)의 일반 가용성 | REST API 기반 데이터 소스를 개발, 테스트 및 통합하여 소스 사양을 쉽게 구성하여 Experience Platform으로 배치 데이터를 수집할 수 있습니다. 소스 SDK를 사용하여 다음을 수행할 수 있습니다. <ul><li>Experience Platform 카탈로그에 대한 새 소스를 구성합니다.</li><li>지원되는 인증 유형, 일정 및 리소스 데이터 가져오기 방법과 관련된 정보를 포함하여 소스에 대한 사양을 정의합니다.</li><li>새 소스에 대한 사용자 관련 설명서를 만듭니다.</li></ul> 자세한 내용은 [셀프 서비스 소스(배치 SDK)](../../sources/sources-sdk/overview.md). |
| 의 일반 공급 [!DNL Google BigQuery] 소스 | 를 사용하십시오 [!DNL Google BigQuery] 소스에서 데이터 수집 [!DNL Google BigQuery] data warehouse에서 Experience Platform으로 자세한 내용은 [[!DNL Google BigQuery] 소스](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] 소스(베타) | 를 사용하십시오 [!DNL Teradata Vantage] 하이브리드 다중 클라우드 환경에서 Experience Platform으로 데이터를 수집할 소스입니다. 자세한 내용은 [[!DNL Teradata Vantage] 소스](../../sources/connectors/databases/teradata-vantage.md). |
| Adobe Analytics 소스에 대한 지역 간 지원 | 이제 모든 지역(미국, 영국 또는 싱가포르)에서 보고서 세트를 수집할 수 있습니다. 보고서 세트는 소스 연결을 만들고 있는 Experience Platform 샌드박스 인스턴스와 동일한 조직에 매핑되어야 합니다. 자세한 내용은 다음 안내서를 참조하십시오. [UI에서 Adobe Analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| 온디맨드 수집을 위한 API 지원 | 온디맨드 수집 기능을 사용하여 [!DNL Flow Service] API. 생성된 흐름 실행은 1회 수집으로 설정해야 합니다. 자세한 내용은 다음 안내서를 참조하십시오. [api를 사용하여 온디맨드 통합에 대한 흐름 실행 만들기](../../sources/tutorials/api/on-demand-ingestion.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
