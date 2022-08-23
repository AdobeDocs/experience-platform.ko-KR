---
title: Adobe Experience Platform 릴리스 노트 - 2022년 8월
description: Adobe Experience Platform에 대한 2022년 8월 릴리스 노트입니다.
source-git-commit: 925991d58c3cdd84e13b12a095e9681b8f4b254b
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 8%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 8월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 준비](#data-prep)
- [XDM(경험 데이터 모델)](#xdm)
- [소스](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고가 있는 레코드 수집 지원 | 이제 데이터 준비에서 경고(중요하지 않은 오류)를 필드에 현지화하고 나머지 행을 수집할 수 있습니다. 이제 모든 매퍼 변환 오류는 경고 및 부분적으로 수집된 행으로 보고되며, 경고 메시지가 표시됩니다.  경고 및 진단 세부 정보가 있는 레코드에서도 모니터링이 지원됩니다. 경고가 있는 레코드의 일부 섭취는 현재 스트리밍 데이터만 사용할 수 있습니다. 다음 문서를 검토하십시오. [경고가 있는 레코드 수집](../../sources/tutorials/ui/monitor-streaming.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

에 대해 자세히 알아보려면 [!DNL Data Prep]를 참조하고 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL AJO 엔티티 스키마]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Adobe Journey Optimizer의 비정규화된 엔터티에 대해 설명합니다. |
| 클래스 | [[!UICONTROL AJO 실행 엔티티]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | 세그멘테이션에 사용할 Adobe Journey Optimizer 실행 엔티티에 대해 설명합니다. |
| 필드 그룹 | [[!UICONTROL Workfront 작업 개체]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Adobe Workfront의 모든 하위 수준 개체 특정 필드 그룹을 참조하는 래퍼 필드 그룹입니다. |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 두 개의 새 속성이 추가되었습니다. `origTimeStamp` 및 `experienceID`. |
| 필드 그룹 | [[!UICONTROL 세그먼트 멤버십 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 추가 [!UICONTROL XDM 개별 프로필]이렇게 하면 이제 XDM 비즈니스 계정 클래스를 기반으로 한 스키마에서도 이 필드 그룹을 사용할 수 있습니다. |
| 필드 그룹 | (복수) | Marketo B2B 활동과 관련된 여러 필드 그룹이 안정적인 상태로 업데이트되었습니다. 다음을 참조하십시오 [가져오기 요청](https://github.com/adobe/xdm/pull/1593/files) 자세한 내용 |
| 필드 그룹 | (복수) | 몇 가지 날씨 관련 필드 그룹이 에 대해 발생한 오류를 수정하도록 업데이트되었습니다 `uvIndex` 및 `sunsetTime`. 다음을 참조하십시오 [가져오기 요청](https://github.com/adobe/xdm/pull/1602/files) 자세한 내용 |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 새 속성 `productImageUrl` 이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 새 속성 `framesPerSecond` 이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion`의 이름이 `appVersion`로 변경되었습니다. `meta:enum` 및 `description` 필드도 업데이트되었습니다. |
| 데이터 유형 및 필드 그룹 | (복수) | 여러 미디어 데이터 유형과 필드 그룹에는 새 필드와 업데이트된 설명이 있습니다. 다음을 참조하십시오 [가져오기 요청](https://github.com/adobe/xdm/pull/1582/files) 자세한 내용 |
| (모두) | (복수) | 를 포함하는 모든 스키마 개체 `enum` 이제 필드에 해당 필드도 포함됩니다 `meta:enum` 각 제약 조건에 대한 표시 값을 나타내는 필드입니다. 다음을 참조하십시오 [가져오기 요청](https://github.com/adobe/xdm/pull/1601/files) 자세한 내용 |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

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
