---
title: Adobe Experience Platform 릴리스 정보 2022년 1월
description: Adobe Experience Platform의 2022년 1월 릴리스 정보입니다.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 20%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 1월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 다음을 통해 다양한 경고 규칙에 가입할 수 있습니다. [!UICONTROL 경고] Platform 사용자 인터페이스의 탭으로, UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 새로운 기능 경고 규칙 | 이제 데이터 수집, ID, 프로필, 세분화 및 활성화와 관련된 워크플로우에 여러 가지 새로운 경고 규칙을 사용할 수 있습니다. 의 개요 보기 [경고 규칙](../../observability/alerts/rules.md) 경고 유형 업데이트 목록. |
| 소스 데이터 흐름에 대한 컨텍스트 내 경고 | 이제 을(를) 구독하여 수집 워크플로우 동안 데이터 흐름 상태와 관련된 경고 메시지를 받을 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [UI에서 소스 경고에 구독](../../sources/tutorials/ui/alerts.md). |

플랫폼의 경고에 대한 자세한 내용은 [경고 개요](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 지능형 캡션 | 머신 러닝 알고리즘은 프로필 및 대상 데이터에 대한 통찰력을 자동으로 제공하며 30~90일 또는 12개월 동안의 패턴 및 트렌드를 보여 줍니다. 캡션에는 다음에 대한 정보가 포함되어 있습니다. <ul><li>전체 모양 및 통계</li><li>트렌드 및 갑작스러운 변경</li><li>계절별 패턴</li><li>예기치 않은 예외 항목</li></ul> 자세한 내용은 [프로필 대시보드](../../dashboards/guides/profiles.md#profiles-count-trend) 및 [세그먼트 대시보드](../../dashboards/guides/audiences.md#audience-size-trend) 설명서를 참조하십시오. |
| 대시보드 인벤토리 | 중앙 위치에서 PowerBI와 같은 설치된 통합을 포함하여 프로필, 세그먼트 및 대상 대시보드에 대한 사전 구성된 보고서에 액세스합니다. 자세한 내용은 [[!DNL Dashboards] 인벤토리 설명서](../../dashboards/inventory.md). |
| PowerBI 보고서 템플릿 | 새 PowerBI 차트를 사용하여 프로필, 세그먼트 및 대상 보고 데이터 모델에서 지표를 빌드, 사용자 지정 또는 확장합니다. 자동 설치 작업 과정을 통해 PowerBI 환경 내에서 조직 전체에 마케팅 인사이트를 공유할 수 있습니다. 자세한 내용은 [PowerBI 보고서 템플릿 설명서](../../dashboards/integrations/power-bi.md). |

에 대한 자세한 내용 [!DNL Dashboards], 다음을 참조하십시오. [[!DNL Dashboards] 개요](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 통합 매핑 경험 | Platform UI의 새 매핑 인터페이스는 일관된 매핑 환경을 제공하여 지능형 매핑 권장 사항을 활용하고, 매핑 규칙을 수동으로 구성하며, 매핑 세트에 발생하는 모든 오류를 디버깅합니다. 자세한 내용은 [[!DNL Data Prep] UI 안내서](../../data-prep/ui/mapping.md). |

에 대한 자세한 내용 [!DNL Data Prep], 다음을 참조하십시오. [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 동일 페이지 및 다음 페이지 개인화 | 다음 [동일 페이지 및 다음 페이지 개인화 기능](../../destinations/ui/activate-edge-personalization-destinations.md) 는 마케팅과 고객 채널 간의 일관성을 위해 Edge Network의 애플리케이션에 대한 사용자를 공유 및 타깃팅할 수 있는 보기를 제공합니다. 이 개인화는 다음을 통해 가능합니다. [Adobe Target 연결](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md). 동일 페이지 또는 다음 페이지 개인화 캠페인을 구성하려면 다음을 참조하십시오. [전용 자습서](../../destinations/ui/activate-edge-personalization-destinations.md). |
| 배치 대상 모니터링 및 세그먼트 수준 지표 | 이제 대상 모니터링 기능이 스트리밍 대상에서 활성화 데이터 흐름에 대한 배치 대상 및 세그먼트 수준 지표도 포함하도록 확장되었습니다. 자세한 내용은 다음을 참조하십시오 [모니터링 대상 대시보드](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [세그먼트 작업 대시보드 모니터링](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), 및 [세그먼트 수준 보기](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| 기존 일괄 처리 활성화 데이터 흐름에 대한 UI의 편집 예약 | 이 릴리스에서는 배치 대상에 대한 기존 활성화 데이터 흐름의 일정을 편집하는 옵션이 도입되었습니다. 자세한 내용은 다음을 참조하십시오 [프로필 데이터를 프로필 대상 일괄 처리에 활성화](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo 대상 개선 사항 | Marketo Engage을 사용하는 Experience Platform 고객은 를 통해 새로운 개인 레코드를 Experience Platform에서 Marketo Engage으로 푸시하는 새로운 기능을 통해 Marketo 데이터베이스를 극대화할 수 있습니다. [Marketo 대상 커넥터](/help/destinations/catalog/adobe/marketo-engage.md). <br> Experience Platform에서 Marketo Engage으로 대상 세그먼트를 보낼 때 Marketo Engage 데이터베이스에 아직 존재하지 않는 세그먼트 내의 사람도 자동으로 추가할 수 있습니다. 자세한 내용은 다음을 참조하십시오 [Adobe Experience Platform 세그먼트를 Marketo 정적 목록에 푸시](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html) (자습서의 9단계는 순-신규 개인 레코드를 Marketo에 푸시하는 방법을 나타냅니다.) |

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [Adobe Target 연결](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험을 제공하는 애플리케이션입니다. Adobe Target은 Adobe Experience Platform의 개인화 연결입니다. |
| [사용자 지정 개인화 연결](../../destinations/catalog/personalization/custom-personalization.md) | 이 개인화 연결은 Adobe Experience Platform에서 외부 개인화 플랫폼, 콘텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행 중인 기타 애플리케이션으로 세그먼트 정보를 검색하는 방법을 제공합니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

[!DNL Query Service] 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]. 에서 모든 데이터 세트를 결합할 수 있습니다. [!DNL Data Lake] 보고, Data Science Workspace에 사용하거나 실시간 고객 프로필로 수집하기 위한 새 데이터 세트로 쿼리 결과를 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 익명 블록 | 익명 블록 SQL 구성을 사용하면 쿼리 서비스의 대규모 데이터 준비 작업을 더 작은 작업으로 분류한 다음 증분 데이터 로드를 위해 순서대로 재사용하고 실행할 수 있습니다. 자세한 내용은 [익명 블록 설명서에 대한 샘플 쿼리](../../query-service/essential-concepts/anonymous-block.md). |
| 데이터 세트 조직 | 샌드박스 내의 데이터 에셋 양이 증가할 때 쿼리 서비스와 함께 사용할 데이터 에셋을 구성할 수 있도록 일관성 있고 논리적인 데이터 구조를 제공합니다. 자세한 내용은 [데이터 에셋 구성 설명서](../../query-service/best-practices/organize-data-assets.md). |

에 대한 자세한 내용 [!DNL Query Service], 다음을 참조하십시오. [[!DNL Query Service] 개요](../../query-service/home.md).

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 글로벌 규모로 디지털 경험 애플리케이션을 강화하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 샌드박스를 제공합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 UI 개선 사항 | 이제 샌드박스 표시기가 모든 Platform UI 애플리케이션의 헤더에 통합되었습니다. 샌드박스 표시기에는 샌드박스 이름, 영역 및 유형이 표시되며 드롭다운 메뉴에 액세스하여 샌드박스 간을 전환할 수 있습니다. 자세한 내용은 [샌드박스 UI 안내서](../../sandboxes/ui/user-guide.md). |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 세그먼트 일치 | 세그먼트 일치는 두 명 이상의 플랫폼 사용자가 안전하고 관리되며 개인정보 보호에 친화적인 방식으로 공통 식별자를 기반으로 데이터를 교환할 수 있는 데이터 공동 작업 서비스입니다. 세그먼트 일치는 Platform 개인 정보 보호 표준과 해시된 이메일, 해시된 전화번호 및 IDFA 및 GAID와 같은 장치 식별자와 같은 개인 식별자를 사용합니다. 자세한 내용은 [세그먼트 일치 개요](../../segmentation/ui/segment-match/overview.md). |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| GA로 이동하는 Beta 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 소스 개선 사항 | 다음 [!DNL Event Hubs] 소스는 이제 소스 연결을 연결하고 만들기 위해 루트가 아닌 SAS 키 유형의 인증을 지원합니다. 자세한 내용은 [[!DNL Event Hubs] 개요](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] 소스 개선 사항 | 다음 [!DNL SFTP] 이제 소스를 사용하여 데이터 흐름이 SFTP 서버에 연결하는 데 사용할 수 있는 최대 동시 연결 수를 설정할 수 있습니다. 자세한 내용은 [[!DNL SFTP] 개요](../../sources/connectors/cloud-storage/sftp.md). |
