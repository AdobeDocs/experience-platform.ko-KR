---
title: Adobe Experience Platform 릴리스 노트 - 2022년 8월
description: Adobe Experience Platform에 대한 2022년 8월 릴리스 노트입니다.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 8월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [실시간 고객 프로필](#profile)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

마케팅 분석가 및 전문가가 AI/ML 서비스를 통해 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 모델을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 개인 정보 지원 | <ul><li> 이제 Attribution AI은 사용자 역할 정의 및 관리 액세스 정책 을 지원합니다 [권한](../../../help/access-control/abac/ui/permissions.md) 제품 애플리케이션 내의 기능 및 개체 </li><li>활동이 발생하면 감사 로그 리소스가 자동으로 기록됩니다.</li><li> 사용 [속성 기반 액세스 제어](../../access-control/abac/overview.md)를 설정하는 경우, 관리자는 특정 속성에 따라 특정 객체 및/또는 기능에 대한 액세스를 제어할 수 있습니다. 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수도 있습니다</li><li>Attribution AI은 Platform 데이터 세트를 사용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하려면 브랜드는 Platform Privacy Service을 사용하여 소비자 액세스 및 삭제 요청을 제출하여 데이터 레이크, Identity Service 및 실시간 고객 프로필에서 데이터를 제거해야 합니다.  </li><li>모델의 입출력 작업에 사용되는 모든 데이터 세트는 플랫폼 지침을 따릅니다. Platform 데이터 암호화는 전송 중인 데이터를 위해 적용됩니다. 자세한 내용은 설명서 를 참조하십시오 [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**참고**: 추가 통지가 있을 때까지는 기존 Healthcare Shield 고객에게는 Attribution AI을 제공하지 않습니다.

Attribution AI에 대한 자세한 내용은 [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 개요.

### 고객 AI

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 개인 정보 지원 | <ul><li> Customer AI는 이제 관리를 위한 사용자 역할 및 액세스 정책 정의를 지원합니다 [권한](../../../help/access-control/abac/ui/permissions.md) 제품 애플리케이션 내의 기능 및 개체 </li><li>활동이 발생하면 감사 로그 리소스가 자동으로 기록됩니다.</li><li> 사용 [속성 기반 액세스 제어](../../access-control/abac/overview.md), 관리자는 특정 속성에 따라 특정 객체 및/또는 기능에 대한 액세스를 제어할 수 있습니다. 이러한 속성은 레이블과 같은 객체에 추가된 메타데이터일 수 있습니다. 또한 관리자는 해당 필드에 해당하는 특정 필드 및 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.</li><li>고객 AI는 플랫폼 데이터 세트를 활용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하려면 브랜드는 Platform Privacy Service을 사용하여 소비자 액세스 및 삭제 요청을 제출하여 데이터 레이크, Identity Service 및 실시간 고객 프로필에서 데이터를 제거해야 합니다. </li><li>모델의 입출력 작업에 사용되는 모든 데이터 세트는 플랫폼 지침을 따릅니다. Platform 데이터 암호화는 전송 중인 데이터를 위해 적용됩니다. 자세한 내용은 설명서 를 참조하십시오 [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**참고**: 고객 AI는 추가 통지가 있을 때까지 기존 Healthcare Shield 고객에게 제공되지 않습니다.

Customer AI에 대한 자세한 내용은 [고객 AI](../../intelligent-services/customer-ai/overview.md) 개요.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 여러 기능을 제공합니다 [!DNL dashboards] 을 통해 일일 스냅샷 동안 캡처된 조직 데이터에 대한 중요한 통찰력을 볼 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 예약된 활동 위젯 | 다음 [!UICONTROL 예약된 활동] 위젯은 가장 최근에 활성화된 대상에 대해 표 형식으로 된 보기를 제공합니다. 각 세그먼트에 대해 이름, 대상 플랫폼, 활성화 시작 및 종료 날짜가 포함됩니다. 이 위젯을 사용하면 대상이 활성화된 위치와 시점을 한눈에 파악할 수 있으며, 중복되거나 불필요한 활동을 보다 투명하게 만들 수 있습니다. 이렇게 축적된 정보에서도 활동이 중지된 위치를 강조 표시합니다. |

자세한 내용은 [!DNL Dashboards]를 보려면 [[!DNL Dashboards] 개요](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고가 있는 레코드 수집 지원 | 이제 데이터 준비에서 경고(중요하지 않은 오류)를 필드에 현지화하고 나머지 행을 수집할 수 있습니다. 이제 모든 매퍼 변환 오류는 경고 및 부분적으로 수집된 행으로 보고되며, 경고 메시지가 표시됩니다.  경고 및 진단 세부 정보가 있는 레코드에서도 모니터링이 지원됩니다. 경고가 있는 레코드의 일부 섭취는 현재 스트리밍 데이터만 사용할 수 있습니다. 다음 문서를 검토하십시오. [경고가 있는 레코드 수집](../../sources/tutorials/ui/monitor-streaming.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

에 대해 자세히 알아보려면 [!DNL Data Prep]를 참조하고 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| (베타) 개인화 대상에 대한 속성 기반 개인화 지원 | 특성 기반 개인화의 베타 릴리스를 사용하면 [대상 카탈로그](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: 이 커넥터는 현재 베타에 있으며 일부 고객만 사용할 수 있습니다. Adobe Target V1 카드에서 제공하는 기능 외에도 Target V2 커넥터는 [매핑 단계](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 프로필 속성을 Adobe Target에 매핑할 수 있는 활성화 워크플로우에 속성 기반의 동일 페이지 및 다음 페이지 개인화를 활성화합니다.</li><li>**[!UICONTROL 속성을 사용한 사용자 지정 개인화]**: 이 커넥터는 현재 베타에 있으며 일부 고객만 사용할 수 있습니다. 에서 제공하는 기능 추가 **[!UICONTROL 사용자 지정 개인화]**, **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 커넥터가 옵션 추가 [매핑 단계](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) 프로필 속성을 사용자 지정 개인화 대상에 매핑하고 속성 기반의 동일 페이지 및 다음 페이지 개인화를 활성화할 수 있는 활성화 워크플로우에 대한 것입니다.</li></ul> <br> 프로필 속성에는 중요한 데이터가 포함될 수 있습니다. 이 데이터를 보호하려면 **[!UICONTROL 속성을 사용한 사용자 지정 개인화]** 대상을 사용하려면 [Edge Network Server API](../../server-api/overview.md) 참조하십시오. 또한 모든 서버 API 호출은 [인증된 컨텍스트](../../server-api/authentication.md). |

{style=&quot;table-layout:auto&quot;}

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) 는 전 세계에서 가장 많은 B2B 구매자 상호 작용 데이터와 독점 AI 기술에 대한 상당한 투자를 보유한 판매 실행 플랫폼으로서 판매 데이터를 인텔리전스로 변환합니다. [!DNL Outreach] 영업 참여를 자동화하고 수익 인텔리전스를 활용하여 효율성, 예측 가능성 및 성장을 향상시킬 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL AJO 엔터티 클래스]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Adobe Journey Optimizer에 대한 조회 스키마를 만들기 위한 레코드 기반 클래스입니다. |
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

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 병합 정책 하드 제한 | 이제 플랫폼에서는 **5개** 샌드박스당 정책 병합 샌드박스에 현재 5개 이상의 병합 정책이 있는 경우 다음을 수행합니다 **not** 샌드박스에 5개 미만의 병합 정책이 있을 때까지 새 병합 정책을 만들 수 있습니다. |
| 분리된 프로필 에지 특성 정리 | 이제 모든 조직의 경우 프로필 서비스에서 사용자 활동 영역의 남은 에지 속성을 매일 제거하여 시스템에서 프로필을 보다 정확하게 표현합니다. 이 정리는 주어진 프로필에 대한 모든 프로필 조각이 삭제된 후 발생하며 다음 데이터 세트에서 병합되는 프로필에 영향을 주어야 합니다. `com_adobe_aep_profile_region_dataset` 으로 표시됨 `true`. 이 지표들은 이번 릴리스 전에 남은 에지 특성 조각을 포함했으므로 라이선스 사용 대시보드의 &quot;주소 지정 가능 대상&quot; 지표에 감소가 표시될 수 있으며, 프로필 대시보드의 &quot;프로필 수&quot; 지표에 이 릴리스 전의 남은 에지 특성 조각이 포함되어 있을 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

프로필 데이터 작업에 대한 자습서 및 모범 사례 등 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 4000개 세그먼트 지원 | 이제 Platform을 사용하는 모든 조직이 최대 4000개의 세그먼트 정의를 지원할 수 있습니다. 이 변경 사항이 세그먼트 작업 API에 미치는 영향에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../../segmentation/api/segment-jobs.md) |

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).

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

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
