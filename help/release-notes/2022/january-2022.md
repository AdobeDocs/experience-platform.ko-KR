---
title: Adobe Experience Platform 릴리스 노트 - 2022년 1월
description: Adobe Experience Platform에 대한 2022년 1월 릴리스 노트입니다.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 3%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 1월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
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
| 대시보드 인벤토리 | 중앙 위치에서 PowerBI와 같은 설치된 통합을 포함하여 프로필, 세그먼트 및 대상 대시보드에 대해 사전 구성된 보고서에 액세스합니다. 자세한 내용은 [[!DNL Dashboards] 인벤토리 설명서](../../dashboards/inventory.md). |
| PowerBI 보고서 템플릿 | 새로운 PowerBI 차트를 사용하여 프로필, 세그먼트 및 대상 보고 데이터 모델에서 지표를 작성하고 사용자 지정하거나 확장합니다. 자동 설치 워크플로우를 사용하면 PowerBI 환경 내에서 조직 전체에서 마케팅 통찰력을 공유할 수 있습니다. 자세한 내용은 [PowerBI 보고서 템플릿 설명서](../../dashboards/integrations/power-bi.md). |

자세한 내용은 [!DNL Dashboards]를 보려면 [[!DNL Dashboards] 개요](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 통합 매핑 경험 | Platform UI의 새로운 매핑 인터페이스는 지능형 매핑 권장 사항을 활용하고, 매핑 규칙을 수동으로 구성하고, 매핑 세트에 발생하는 모든 오류를 디버깅하는 일관된 매핑 경험을 제공합니다. 자세한 내용은 [[!DNL Data Prep] UI 안내서](../../data-prep/ui/mapping.md). |

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 동일 페이지 및 다음 페이지 개인화 | 다음 [동일한 페이지 및 다음 페이지 개인화 기능](../../destinations/ui/configure-personalization-destinations.md) 마케팅 채널과 고객 채널 간의 일관성을 위해 Experience Edge에서 애플리케이션을 위한 공유 타겟팅할 수 있는 사용자 보기를 제공합니다. 이러한 개인화는 [Adobe Target 연결](../../destinations/catalog/personalization/adobe-target-connection.md) 그리고 [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md). 동일한 페이지 또는 다음 페이지 개인화 캠페인을 구성하려면 다음을 참조하십시오. [전용 자습서](../../destinations/ui/configure-personalization-destinations.md). |
| 배치 대상 모니터링 및 세그먼트 수준 지표 | 이제 대상 모니터링 기능이 스트리밍 대상에서 활성화 데이터 흐름에 대한 배치 대상 및 세그먼트 수준 지표도 포함하도록 확장되었습니다. 자세한 내용은 [대상 대시보드 모니터링](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [세그먼트 작업 대시보드 모니터링](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), 및 [세그먼트 수준 보기](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| 기존 배치 활성화 데이터 흐름에 대한 UI에서 편집 예약 | 이 릴리스에서는 기존 활성화 데이터 흐름의 일정을 일괄 처리 대상으로 편집하는 옵션이 제공됩니다. 자세한 내용은 [프로필 데이터를 배치 프로필 대상에 활성화](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo 대상 개선 사항 | Marketo Engage을 사용하는 Experience Platform 고객은 Marketo 데이터베이스를 통해 를 통해 Experience Platform에서 Marketo Engage으로 net-new person 레코드를 푸시할 수 있는 새로운 기능으로 극대화할 수 있습니다 [Marketo 대상 커넥터](/help/destinations/catalog/adobe/marketo-engage.md). <br> Experience Platform에서 Marketo Engage으로 대상 세그먼트를 보낼 때 Marketo Engage 데이터베이스에 아직 존재하지 않는 세그먼트 내의 사람을 자동으로 해당 세그먼트에 추가할 수 있습니다. 자세한 내용은 [Marketo 정적 목록에 Adobe Experience Platform 세그먼트 푸시](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (자습서의 9단계는 net-new person 레코드를 Marketo에 푸시하는 방법을 나타냅니다.) |

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [Adobe Target 연결](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target은 웹 사이트, 모바일 앱 등에서 모든 인바운드 고객 상호 작용에서 실시간 AI 기반의 개인화 및 실험을 제공하는 애플리케이션입니다. Adobe Target은 Adobe Experience Platform의 개인화 연결입니다. |
| [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md) | 이 개인화 연결은 Adobe Experience Platform에서 외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 응용 프로그램으로 세그먼트 정보를 검색하는 방법을 제공합니다. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## 쿼리 서비스 {#query-service}

[!DNL Query Service] 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 익명 블록 | 익명 블록 SQL 구성을 사용하면 Query Service의 대규모 데이터 준비 작업을 작은 작업으로 분류한 다음 증분 데이터 로드를 위해 다시 사용하고 순서대로 실행할 수 있습니다. 자세한 내용은 [익명 블록 설명서에 대한 샘플 쿼리](../../query-service/best-practices/anonymous-block.md). |
| 데이터 집합 조직 | 샌드박스 내의 데이터 자산 양이 증가함에 따라 Query Service에서 사용할 데이터 자산을 정리하기 위한 일관된 논리 데이터 구조를 제공합니다. 자세한 내용은 [데이터 자산 설명서 구성](../../query-service/best-practices/organize-data-assets.md). |

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
