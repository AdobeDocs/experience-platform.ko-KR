---
title: Adobe Experience Platform 릴리스 노트 2024년 4월
description: Adobe Experience Platform에 대한 2024년 4월 릴리스 정보입니다.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: fea62a2aa3c7d175afbfa808f392c3a93a0d31a0
workflow-type: tm+mt
source-wordcount: '1843'
ht-degree: 16%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 4월 30일 수요일**

>[!TIP]
>
>사용 [Adobe Experience Platform 용어](/help/landing/glossary.md) Real-time Customer Data Platform 및 Adobe Experience Platform에 사용되는 용어를 숙지합니다. 찾고 있는 특정 용어를 찾을 수 없는 경우 페이지의 피드백 옵션을 사용하여 용어집에 새 용어를 추가하도록 요청합니다.

Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [ID 서비스](#identity-service)
- [모니터링](#monitoring)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Real-time Customer Data Platform B2B 인사이트 | 계정 및 기회에 대해 사전 구성된 Real-Time CDP B2B 데이터 인사이트를 탐색하여 데이터를 이해하고 비즈니스 의사 결정을 알리는 데 도움이 됩니다. 또한 Real-Time CDP B2B 데이터 모델을 사용하여 나만의 통찰력을 구축하여 데이터를 시각화 및 탐색하고 대시보드에 사용자 지정 시각화를 저장할 수 있습니다. |

{style=“table-layout:auto”}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Experience Platform Edge Network으로 전송할 수 있는 기술 제품군을 제공합니다. 여기서 데이터 보강 및 변환, Adobe 또는 비 Adobe 대상으로 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 확장 | [!DNL Acxiom Anonymous Visitor Insights] 태그 확장 | 로 웹 사이트 방문자를 검색하는 방법 [!DNL Acxiom's Visitor Insights]. Acxiom은 지역 IP 조회 기술을 활용하여 익명 브라우저의 위치를 정확하게 파악할 수 있습니다. 식별되면 구성된 데이터베이스에서 검색하면 다시 브라우저로 전송되는 추가 인사이트가 생성됩니다. 따라서 콘텐츠 작성자는 낯선 사람으로 시작한 경우에도 방문자에게 보다 개인화되고 흥미로운 경험을 제공하는 이러한 데이터 포인트에 맞게 콘텐츠를 조정할 수 있습니다. |
| 데이터스트림 | [Edge Network 봇 탐지](../../datastreams/bot-detection.md) | 자동화된 프로그램, 웹 스크레이퍼, 스파이더, 스크립팅된 스캐너와 같은 비인간 엔티티에서 발생하는 트래픽은 인간 방문자에서 발생하는 이벤트를 식별하는 것을 더 어렵게 할 수 있습니다. 이 유형의 트래픽은 중요한 비즈니스 지표에 부정적인 영향을 주어 잘못된 트래픽 보고를 초래할 수 있습니다. <br>보트 감지를 사용하면 [웹 SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) 및 [[!DNL Server API]](../../server-api/overview.md) 알려진 스파이더 및 보트에서 생성됨. 데이터스트림에 대한 보트 감지를 구성하여 보트 이벤트로 분류하려는 특정 IP 주소, IP 범위 및 요청 헤더를 식별할 수 있습니다. <br> 보트 트래픽을 식별하면 사이트 또는 모바일 애플리케이션에서 사용자 활동을 보다 정확하게 측정할 수 있습니다. |
| Mobile SDK | 주요 버전 릴리스 | iOS Mobile Core 5.x 및 호환 iOS 확장, Android Mobile Core 3.x 및 호환 Android 확장, React Native Core 6.x 및 호환 React Native 확장, Flutter Core 4.x 및 호환 Flutter 확장에 대한 Mobile SDK의 새 주요 버전이 출시되었습니다. 이러한 릴리스는 Jetpack Compose용 Android SDK의 지원, Adobe Journey Optimizer 코드 기반 경험의 지원, Flutter용 Adobe Journey Optimizer Messaging 확장의 일반 가용성을 포함하여 몇 가지 새로운 기능과 개선 사항을 제공합니다. 릴리스 노트에 대한 자세한 내용은 [모바일 SDK 릴리스 노트](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | 개인정보 보호 | 2024년 5월 1일부터 Apple의 정책 업데이트로 인해 개발자가 App Store에 제출하려면 새로운 개인 정보 보호 기능을 구현해야 합니다. Mobile SDK를 사용하는 모든 Adobe 고객이 5월 1일 이후에 App Store 승인을 받으려면 SDK 버전 5.x로 업그레이드해야 합니다. |
| Roku SDK | Roku SDK | Platform Edge Network용 Streaming Media에 대한 지원과 함께 Roku SDK의 첫 번째 주요 버전이 출시되었습니다. |
| 태그 및 이벤트 전달 | 제품 내 지침 | Experience Platform [태그](../../tags/home.md) 및 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 는 빠르게 시작하고 빠른 가치 창출 시간을 실현하는 데 도움이 되는 새로운 경험을 제공합니다. 이러한 경험에는 새로운 온보딩 화면, 제품 내 튜토리얼 및 도구 팁이 포함됩니다. <br>![제품 내 지침이 강조 표시된 이벤트 전달.](../2024/assets/april/event-forwarding.png "유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기."){width="100" zoomable="yes"}<br> |
| Web SDK | Audience Manager 고객을 위한 간소화된 웹 SDK 채택 | 이제 여러 웹 SDK 업데이트를 통해 Audience Manager, 분석 및 타겟과 같은 Experience Cloud 솔루션에 XDM(Experience Data Model)을 사용하지 않고 웹 SDK를 간편하게 사용할 수 있습니다. 다음 안내서에서 웹 SDK 채택 Audience Manager에 대해 자세히 알아보십시오. <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Audience Manager 태그 확장에서 웹 SDK 태그 확장으로 Audience Manager을 위한 데이터 수집 라이브러리 업데이트</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">AppMeasurement JavaScript 라이브러리에서 웹 SDK JavaScript 라이브러리로의 Audience Manager을 위해 데이터 수집 라이브러리 업데이트</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

데이터 수집에 대해 자세히 알아보려면 [데이터 수집 개요](../../collection/home.md).

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| `isRequired` 이제 Destination SDK의 중첩된 고객 데이터 필드에 매개 변수를 사용할 수 있습니다. | 이제 Destination SDK에서 대상을 구성할 때 다음 작업을 수행할 수 있습니다 [필요에 따라 중첩된 고객 데이터 필드 설정](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). 이렇게 하면 대상을 설정하는 사용자는 해당 필드에 대한 값을 선택할 때까지 활성화 플로우를 진행할 수 없습니다. |
| Web SDK를 사용하여 Adobe Target 대상을 설정할 때 Edge 세그멘테이션은 더 이상 필수 요구 사항이 아닙니다 | 이전에는 을 구성할 때 [Adobe Target 대상](/help/destinations/catalog/personalization/adobe-target-connection.md) web SDK를 사용하면 데이터 스트림을 개인화 및 에지 세분화에 사용할 수 있어야 합니다. 에지 세그멘테이션에 대해 데이터 스트림을 활성화해야 하는 요구 사항 [이(가) 이제 제거되었습니다.](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). 이 통합 패턴은 Real-Time CDP에서 Adobe Target을 사용할 때 개인화 사용 사례의 하위 집합에서만 혜택을 받을 수 있습니다. 자세한 내용 [통합 유형별로 활성화된 사용 사례](/help/destinations/catalog/personalization/adobe-target-connection.md#parameters). |
| [!BADGE 베타]{type=Informative} 활성화 플로우에서 여러 대상자 및 데이터 세트 제거 | 이제 대상 활성화 플로우에서 여러 대상 및 데이터 세트를 선택하고 제거할 수 있습니다. 다음을 참조하십시오. [대상 세부 사항](../../destinations/ui/destination-details-page.md#bulk-remove) 및 [데이터 세트 내보내기](../../destinations/ui/export-datasets.md) 자세한 내용은 설명서 를 참조하십시오. |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

Adobe Experience Platform Identity Service를 사용하여 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 만들고, 이를 통해 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 사용 중단 `/orgs/{ORG}/` API의 엔드포인트 | 의 다음 엔드포인트 [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 더 이상 사용되지 않음:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> 다음을 사용할 수 있습니다. `/idnamespace/identities` 및 `/idnamespace/identities/{ID}` 동일한 작업을 수행하고 조직의 모든 네임스페이스 또는 조직의 특정 네임스페이스를 검색하는 엔드포인트. |

{style="table-layout:auto"}

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).

## 모니터링 {#monitoring}

Experience Platform UI의 여정 대시보드를 사용하여 소스, ID 서비스, 실시간 고객 프로필, 대상 및 대상에서 데이터 모니터링을 모니터링합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대시보드 확장 모니터링 | 이제 비즈니스 사용 사례에 따라 다양한 데이터 유형에 모니터링 대시보드를 사용할 수 있습니다. 모니터링 대시보드를 사용하여 소스, 대상 및 대상에서 개인, 계정 및 잠재 고객 데이터 유형 활동을 모니터링합니다. |

{style="table-layout:auto"}

자세한 내용은 의 안내서를 참조하십시오. [모니터링 대시보드 사용](../../dataflows/ui/monitor.md).

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. 에서 모든 데이터 세트를 결합할 수 있습니다. [!DNL Data Lake] 보고, Data Science Workspace에 사용하거나 실시간 고객 프로필로 수집하기 위한 새 데이터 세트로 쿼리 결과를 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 쿼리 격리 | 장애가 발생한 쿼리 실행을 자동으로 격리하여 중단을 방지하고 일관된 성능을 유지합니다. |
| 쿼리 취소 | 쿼리 실행을 제어하고 오래 실행되는 쿼리를 취소하여 생산성을 향상시킵니다. |
| 예약된 쿼리 경고 | 사전 알림을 통해 정보를 지속적으로 확인하고 쿼리를 스케줄링하여 효율적이고 시기 적절한 작업 관리를 보장합니다. 쿼리를 만들거나 기존 예약된 쿼리에 대한 인라인 작업을 사용하여 경고를 구독할 수 있습니다. |
| 향상된 예약된 쿼리 탐색 | 쿼리 템플릿과 예약된 실행 사이를 쉽게 탐색하여 생산성을 높일 수 있습니다. |
| 확장 쿼리 출력 | 콘솔 내에서 최대 500개의 쿼리 결과 행에 액세스하여 데이터를 보다 심층적으로 분석할 수 있습니다. |
| 이전 쿼리 편집기 종료 | 2024년 4월 30일부터 고급 쿼리 편집기가 모든 사용자의 기본 편집기가 되었습니다. 레거시 편집기는 2024년 5월 30일에 사용이 중단되며 더 이상 사용할 수 없습니다. |

{style=“table-layout:auto”}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 글로벌 규모로 디지털 경험 애플리케이션을 강화하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [샌드박스 도구](../../sandboxes/ui/sandbox-tooling.md) | 샌드박스 도구 사용 [내보내기](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) 지원되는 모든 객체 유형을 전체 샌드박스 패키지로 만든 다음 [가져오기](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) 다양한 샌드박스에 걸쳐 개체 구성을 복제하는 패키지입니다. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상 라이프사이클 상태 | 대상 라이프사이클 상태가 간소화되어 라이프사이클 관리가 간소화되었습니다. 이러한 라이프사이클 상태에 대해 자세히 알아보려면 [세그먼테이션 서비스 FAQ](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션이나 타사 데이터 소스에서 데이터를 수집합니다.

**새 소스**

| 새 소스 | 설명 |
| --- | --- |
| [!BADGE 베타]{type=Informative} [!DNL PathFactory] | 사용 [[!DNL PathFactory] 소스](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) 에서 방문자, 세션 및 페이지 보기 데이터를 통합하려면 [!DNL PathFactory] Experience Platform. 읽기 [[!DNL PathFactory] 개요](../../sources/connectors/marketing-automation/pathfactory.md) 을 참조하십시오. |
| [!DNL Teradata Vantage] | 사용 [[!DNL Teradata Vantage] 소스](../../sources/tutorials/ui/create/databases/teradata-vantage.md) 하이브리드 멀티 클라우드 환경에서 Experience Platform으로 데이터를 수집합니다. 읽기 [[!DNL Teradata Vantage] 개요](../../sources/connectors/databases/teradata-vantage.md) 을 참조하십시오. |

{style="table-layout:auto"}

**새로운 기능 및 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| VA7에 허용 목록에 대한 IP 주소 업데이트 | VA7(북미) 허용 목록에 추가할 IP 주소 목록에 다음 IP 주소가 추가되었습니다. <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> 허용 목록에 추가할 IP 주소의 전체 목록을 보려면 [IP 주소 허용 목록 문서](../../sources/ip-address-allow-list.md). |
| 를 사용한 새 인증 유형 지원 [!DNL Azure Event Hubs] 소스 | 이제 다음을 연결할 수 있습니다. [!DNL Event Hubs] 다음 중 하나를 사용하여 소스-Experience Platform [!DNL Azure Active Directory Authentication] 또는 [!DNL Scoped Azure Active Directory Authentication]. 의 안내서 읽기 [연결 중 [!DNL Event Hubs] 대상 Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) 추가 정보. |
| 업데이트 대상: [!DNL Data Landing Zone] 자격 증명 검색 | 이제 소스 작업 영역에서 올바른 레일을 사용하여 [!DNL Data Landing Zone] 자격 증명. 이제 올바른 레일을 사용하여 자격 증명을 새로 고칠 수도 있습니다. 읽기 [[!DNL Data Landing Zone] UI 안내서](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) 추가 정보. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).
