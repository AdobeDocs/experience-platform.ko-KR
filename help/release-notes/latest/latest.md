---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 78f9b8434d577909ccb1c62211a802e05c8291e1
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 1월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 을 통해 다른 경고 규칙에 가입할 수 있습니다 [!UICONTROL 경고] 플랫폼 사용자 인터페이스의 탭. 및 UI 자체 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 경고 규칙 | 이제 데이터 수집, ID, 프로필, 세그멘테이션 및 활성화와 관련된 워크플로우에 여러 가지 새로운 경고 규칙을 사용할 수 있습니다. 다음 사항에 대한 개요를 참조하십시오. [경고 규칙](../../observability/alerts/rules.md) 를 참조하십시오. |
| 소스 데이터 흐름에 대한 컨텍스트 내 경고 | 이제 구독하여 수집 워크플로우 중 데이터 흐름의 상태에 대한 경고 메시지를 받을 수 있습니다. 자세한 내용은 [UI에서 소스 경고 구독](../../sources/tutorials/ui/alerts.md). |

Platform의 경고에 대한 자세한 내용은 [경고 개요](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 개의 대시보드를 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 지능형 캡션 | 기계 학습 알고리즘은 프로필 및 대상 데이터에 대한 인사이트를 자동으로 제공하고 30~90일 또는 12개월 기간 동안의 패턴 및 트렌드를 보여줍니다. 캡션에는 다음 정보가 포함됩니다 <ul><li>전체 모양 및 통계</li><li>트렌드 및 갑작스러운 변경</li><li>계절별 패턴</li><li>예기치 않은 예외 항목</li></ul> 자세한 내용은 [프로필 대시보드](../../dashboards/guides/profiles.md#profiles-count-trend) 및 [세그먼트 대시보드](../../dashboards/guides/segments.md#audience-size-trend) 설명서. |
| 대시보드 인벤토리 | 중앙 위치에서 PowerBI와 같은 설치된 통합을 포함하여 프로필, 세그먼트 및 대상 대시보드에 대해 사전 구성된 보고서에 액세스합니다. 자세한 내용은 [[!DNL Dashboards] 개요](../../dashboards/home.md). |
| PowerBI 보고서 템플릿 | 새로운 PowerBI 차트를 사용하여 프로필, 세그먼트 및 대상 보고 데이터 모델에서 지표를 작성하고 사용자 지정하거나 확장합니다. 자동 설치 워크플로우를 사용하면 PowerBI 환경 내에서 조직 전체에서 마케팅 통찰력을 공유할 수 있습니다. 자세한 내용은 [[!DNL Dashboards] 개요](../../dashboards/home.md). |

자세한 내용은 [!DNL Dashboards]를 보려면 [[!DNL Dashboards] 개요](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 통합 매핑 경험 | Platform UI의 새로운 매핑 인터페이스는 지능형 매핑 권장 사항을 활용하고, 매핑 규칙을 수동으로 구성하고, 매핑 세트에 발생하는 모든 오류를 디버깅하는 일관된 매핑 경험을 제공합니다. 자세한 내용은 [[!DNL Data Prep] UI 안내서](../../data-prep/ui/mapping.md). |

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

<!--

## [!DNL Destinations] {#destinations}

[!DNL Destinations] are pre-built integrations with destination platforms that allow for the seamless activation of data from Adobe Experience Platform. You can use destinations to activate your known and unknown data for cross-channel marketing campaigns, email campaigns, targeted advertising, and many other use cases.

| Feature | Description |
| ----------- | ----------- |
| Placeholder for next-hit personalization | Description |
| Placeholder for batch monitoring | Description |
| Placeholder for re-introducing scheduling in the UI | Description |
| Placeholder for Marketo destination update | Description |


**New destinations**

| Destination | Description |
| ----------- | ----------- |
| Placeholder for Target | Description |
| Placeholder for Custom Personalization | Description |

For more general information on destinations, refer to the [destinations overview](../../destinations/home.md).

-->

## 쿼리 서비스 {#query-service}

[!DNL Query Service] 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 익명 블록 | 익명 블록 SQL 구성을 사용하면 Query Service의 대규모 데이터 준비 작업을 작은 작업으로 분류한 다음 증분 데이터 로드를 위해 다시 사용하고 순서대로 실행할 수 있습니다. 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md). |
| 데이터 집합 조직 | 샌드박스 내의 데이터 자산 양이 증가함에 따라 Query Service에서 사용할 데이터 자산을 정리하기 위한 일관된 논리 데이터 구조를 제공합니다. 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md). |

자세한 내용은 [!DNL Query Service]를 보려면 [[!DNL Query Service] 개요](../../query-service/home.md).

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 디지털 경험 애플리케이션을 전 세계에 맞게 보강하기 위해 제작되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 운영하고 있으며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 충족해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스 를 제공합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 UI 개선 사항 | 이제 샌드박스 표시기가 모든 Platform UI 애플리케이션의 헤더 내에 통합됩니다. 샌드박스 표시기에는 샌드박스 이름, 영역 및 유형이 표시되며, 드롭다운 메뉴에 액세스하여 샌드박스 간을 전환할 수도 있습니다. 자세한 내용은 [sandbox UI 안내서](../../sandboxes/ui/user-guide.md). |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 세그먼트 일치 | 세그먼트 일치 는 두 명 이상의 플랫폼 사용자가 공통 식별자를 기반으로 데이터를 안전하고 제어되며 개인 정보를 보호하는 방식으로 교환할 수 있도록 해주는 데이터 공동 작업 서비스입니다. 세그먼트 일치 는 해시된 이메일, 해시된 전화번호 및 IDFA 및 GAID와 같은 장치 식별자 등의 플랫폼 개인 정보 표준 및 개인 식별자를 사용합니다. 자세한 내용은 [세그먼트 일치 개요](../../segmentation/ui/segment-match/overview.md). |

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| GA로 이동하는 베타 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 소스 개선 사항 | 다음 [!DNL Event Hubs] 이제 원본에서 비루트 SAS 키 유형의 인증을 지원하여 소스 연결을 연결하고 만듭니다. 자세한 내용은 [[!DNL Event Hubs] 개요](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] 소스 개선 사항 | 다음 [!DNL SFTP] 이제 소스를 통해 데이터 양이 SFTP 서버에 연결하는 데 사용할 수 있는 최대 동시 연결 수를 설정할 수 있습니다. 자세한 내용은 [[!DNL SFTP] 개요](../../sources/connectors/cloud-storage/sftp.md). |
