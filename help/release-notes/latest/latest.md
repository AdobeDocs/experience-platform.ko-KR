---
title: Adobe Experience Platform 릴리스 노트 2025년 6월
description: Adobe Experience Platform의 2025년 6월 릴리스 노트.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fb34e033c90c269742a2045025bf0c964b513679
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 44%

---


# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 구성](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 6월 18일 목요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [액세스 제어](#access-control)
- [고급 데이터 라이프사이클 관리](#advanced-data-lifecycle-management)
- [카탈로그 서비스](#catalog-service)
- [대시보드](#dashboards)
- [데이터 거버넌스](#data-governance)
- [대상](#destinations)
- [페더레이션된 대상자 컴포지션](#fac)
- [Privacy Service](#privacy-service)
- [샌드박스](#sandboxes)
- [세그먼테이션](#segmentation-service)
- [소스](#sources)

## 액세스 제어 {#access-control}

Experience Platform은 [Adobe Admin Console](https://adminconsole.adobe.com) 제품 프로필을 활용하여 사용 권한 및 샌드박스를 사용자와 연결합니다. 권한은 데이터 모델링, 프로필 관리 및 샌드박스 관리를 포함하여 다양한 Experience Platform 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대시보드 데이터 내보내기 권한 | 이제 대시보드의 **[!UICONTROL CSV 다운로드]** 및 **[!UICONTROL 이메일로 보내기]** 옵션에는 **[!UICONTROL 대시보드 데이터 내보내기]** 권한이 필요합니다. 이 권한을 사용하면 권한이 있는 사용자만 탭으로 작성된 insight 데이터를 내보낼 수 있으므로 보다 엄격한 거버넌스 및 데이터 액세스 제어 정책을 지원할 수 있습니다. 자세한 내용은 액세스 제어 가이드의 [권한 섹션](../../access-control/home.md#permissions)을 참조하십시오. |

자세한 내용은 [액세스 제어 개요](../../access-control/home.md)를 참조하십시오.

## 고급 데이터 라이프사이클 관리 {#advanced-data-lifecycle-management}

Experience Platform은 프로그램 수준에서 소비자 기록 및 데이터 세트를 삭제함으로써 저장 데이터를 관리할 수 있도록 해 주는 데이터 위생 기능 세트를 제공합니다. UI의 데이터 라이프사이클 작업 영역을 사용하거나 데이터 위생 API 호출을 통해 데이터 저장소를 효과적으로 관리할 수 있습니다. 이들 기능을 사용하면 정보를 의도대로 사용하고 정확하지 않은 데이터를 수정해야 할 때 업데이트하며 조직 정책에 따라 필요한 경우 삭제할 수 있습니다.

**새 설명서**

| 새 설명서 | 설명 |
| --- | --- |
| 레코드 삭제 일반 가용성 | 이제 UI 또는 API를 사용하여 ID 필드를 기반으로 개별 레코드를 삭제할 수 있습니다. 이 기능을 사용하면 단일 데이터 세트 또는 모든 데이터 세트에서 삭제할 수 있으므로 스토리지를 줄이고 거버넌스를 적용하며 데이터 위생 상태를 개선할 수 있습니다. 볼륨 제한 및 자격 요구 사항이 적용됩니다. 자세한 내용은 [레코드 삭제 가이드](../../hygiene/ui/record-delete.md)를 참조하세요. |

자세한 내용은 [고급 데이터 라이프사이클 관리 개요](../../hygiene/home.md)를 참조하십시오.

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 미리보기 개선: 더 빠른 탐색 및 더 명확한 통찰력 | 익숙한 데이터 세트 미리보기 환경 내에서 데이터 세트 데이터를 빠르게 미리 보고, 기본 SQL 쿼리를 보고, 향상된 필터링과 더 명확한 구조 가시성으로 최대 100개의 행을 탐색할 수 있습니다. 자세한 내용은 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#preview)를 참조하십시오. |

{style="table-layout:auto"}

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 전자 메일로 보내기 내보내기 옵션 | 이제 **[!UICONTROL 자세히 보기]** 메뉴에서 **[!UICONTROL 이메일로 보내기]**&#x200B;를 선택하여 Query Pro 모드 대시보드에서 최대 10,000개의 레코드를 내보낼 수 있습니다. 이 옵션은 더 큰 내보내기를 위해 Adobe 관련 이메일에 다운로드 링크를 안전하게 보냅니다. 자세한 내용은 [추가 가이드 보기](../../dashboards/sql-insights-query-pro-mode/view-more.md#export)를 참조하십시오. |

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 거버넌스 {#data-governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 이 기능은 [!DNL Experience Platform] 내 카탈로그 작성, 데이터 계통 확인, 데이터 사용 라벨링, 데이터 액세스 정책, 마케팅 액션을 위한 데이터 액세스 제어 등 다양한 수준에서 주요 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Azure CMK 경고 및 IP 허용 목록 구성 | 이제 Azure Key에서 Adobe의 고정 IP 주소를 허용 목록 하여 네트워크 제한이 계속 액세스되도록 할 수 있습니다. 이렇게 하면 제한된 키 액세스로 인한 Platform 서비스 중단을 방지할 수 있습니다. |
| CMK 구성 경고 및 해결 방법 | 이제 Experience Platform에서 Adobe 서비스가 Azure 키 자격 증명 모음에 대한 액세스 권한을 상실하면(예: 제거된 IP 허용 목록 항목이나 비활성화된 키로 인해) 경고를 트리거합니다. 새로운 안내서는 각 경고를 이해하고 수정 조치를 취하는 데 도움이 됩니다. |

자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) 연결 | [!DNL Algolia] 대상을 사용하여 홈페이지에서 검색할 사이트 간에 일관된 개인화를 제공합니다. 타겟팅 전략 및 캠페인 개인화를 개선하기 위해 여러 데이터 소스에서 풍부한 대상을 작성하고 다양한 채널에서 공유합니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) 일반 공급 | 이제 모든 Experience Platform 사용자가 Google Customer Match + DV360 대상을 사용할 수 있습니다. 이제 설명서에는 [!DNL Adobe]에서 [!DNL Google]개의 광고 계정 사이의 [계정 연결](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking)에 대한 자세한 지침이 포함되어 있습니다. |
| 스트리밍 대상에 대한 [대상 수준 모니터링](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 이제 다음 대상에 대해 대상자 수준 모니터링을 사용할 수 있습니다. <ul><li>[[!DNL (API) Oracle Eloqua] 연결](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) 대상에 대한 추가 식별자 지원 | [!DNL Facebook] 대상은 이제 개선된 타깃팅 및 Facebook 속성의 프로필과 일치하기 위해 새 주소 관련 필드의 매핑을 지원합니다. 새 주소 관련 필드에 대한 자세한 내용은 [지원되는 ID](../../destinations/catalog/social/facebook.md#supported-identities) 섹션을 참조하십시오. <br> Facebook의 추가 필드를 표시하는 ![플랫폼 UI 이미지입니다.](../2025/assets/june/facebook-destination-fields.png "Facebook에 대한 추가 필드를 표시하는 플랫폼 UI 이미지입니다."){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) 대상 업그레이드 | 2025년 6월 19일부터 대상 카탈로그에서 두 개의 **[!DNL Braze]** 카드를 나란히 볼 수 있습니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. 기존 [!DNL Braze] 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) 동기화]**(으)로 변경되었으며 이제 이름이 **[!UICONTROL 동기화]**&#x200B;인 새 카드를 사용할 수 있습니다. <br> 카탈로그에서 **[!UICONTROL 중단]** 연결을 사용하여 새 활성화 데이터 흐름을 만드십시오. **[!UICONTROL (더 이상 사용되지 않음) 중단]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br> [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 생성하는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]를 다음 값으로 업데이트해야 합니다. <ul><li>흐름 사양 ID: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>연결 사양 ID: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 페더레이션된 대상자 컴포지션 {#fac}

페더레이션된 대상자 컴포지션을 통해 기업은 다양한 사용 사례에서 데이터를 더 잘 적용할 수 있습니다. 이 새로운 접근 방식을 사용하면 Adobe Real-Time CDP 및/또는 Adobe Journey Optimizer 사용자로서 기존 데이터 웨어하우스에서 직접 데이터 세트를 페더레이션하여 Adobe Experience Platform 대상자와 속성을 모두 하나의 시스템에 만들고 강화할 수 있습니다.

| 새로운 기능 | 설명 |
| ----------- | ----------- |
| Adobe Healthcare Shield 고객을 위한 일반 가용성 | 연합 대상 구성은 Adobe Healthcare Shield 고객이 6월 말까지 대상 생성, 강화 및 프로필 강화 사용 사례를 사용할 수 있습니다. Federated Audience Composition의 개인 정보 및 보안 조치에 대한 자세한 내용은 Federated Audience Composition 개요[&#128279;](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/start/privacy-security)의 개인 정보 및 보안을 참조하십시오. 일반적으로 Experience Platform 제품에 대한 HIPAA 준수에 대한 자세한 내용은 [HIPAA 및 Adobe 제품 및 서비스 개요](https://www.adobe.com/trust/compliance/hipaa-ready.html)를 참조하십시오. |

자세한 내용은 [페더레이션된 대상자 컴포지션 설명서](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/home)를 참조하십시오.

## [!DNL Privacy Service] {#privacy}

일부 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service]는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]를 사용하면 Adobe Experience Cloud 애플리케이션에서 비공개 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | ---|
| 테네시 및 미네소타 개인 정보 보호 법 지원 | Privacy Service은 이제 테네시 정보 보호법(`tipa_tn_usa`) 및 미네소타 소비자 데이터 개인정보 보호법(`mcdpa_mn_usa`)을 지원합니다. 이러한 새로운 주 수준 규정을 준수하여 액세스 및 삭제 요청을 처리할 수 있습니다. 자세한 내용은 [규정 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/privacy/regulations/overview)를 참조하세요. |

서비스에 대한 자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 개체 구성 업데이트 마이그레이션 | 이제 초기 복제 후 샌드박스 간에 반복적인 객체 구성 업데이트를 마이그레이션할 수 있습니다. 이 개선 사항은 전체 샌드박스 설정을 다시 생성하지 않고 환경 간에 구성을 업데이트하고 전파해야 하는 개발 워크플로를 지원합니다. 자세한 내용은 [샌드박스 간 구성 업데이트 전송](../../sandboxes/ui/sandbox-tooling.md#move-configs)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 유사 인사이트 가용성 업데이트 | 사용량이 적은 환경에 대해 유사 인사이트 및 유사 대상이 자동으로 비활성화됩니다. 낮은 사용량은 지난 3개월 동안 유사 인사이트를 보지 못하거나 지난 6개월 동안 새로운 유사 대상을 만들지 않은 것으로 정의됩니다. 이 변경 사항에 대한 자세한 내용은 [유사 대상 안내서](../../segmentation/types/lookalike-audiences.md)를 참조하십시오. |

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Azure Databricks]에 대한 [!BADGE Beta]{type=Informative} UI 지원 | 이제 UI의 소스 작업 영역을 사용하여 [!DNL Azure Databricks] 계정을 Experience Platform에 연결할 수 있습니다. 자세한 내용은 UI의 [Experience Platform에 연결 [!DNL Databricks] 하기](../../sources/connectors/databases/databricks.md)에 대한 안내서를 참조하십시오. |
| [!DNL Azure Synapse Analytics]에 대한 새 인증 유형 지원 | 이제 [!DNL Azure Synapse Analytics]은(는) 기존 연결 문자열 인증 외에 서비스 사용자 인증도 지원합니다. 자세한 내용은 [[!DNL Azure Synapse Analytics] 인증 개요](../../sources/connectors/databases/synapse-analytics.md)를 참조하세요. |
| [!DNL Salesforce] 기본 인증 사용 중단 | [Salesforce CRM](../../sources/connectors/crm/salesforce.md) 및 [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md)에 대한 기본 인증은 2026년 1월까지 더 이상 사용되지 않습니다. 고객은 OAuth 2.0 인증으로 마이그레이션해야 연결을 유지할 수 있습니다. 이 변경 사항은 소스 커넥터 모두에 영향을 미치며 향상된 보안과 Salesforce 인증 표준 준수를 보장합니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
