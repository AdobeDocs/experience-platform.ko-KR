---
title: Adobe Experience Platform 릴리스 노트 2022년 8월
description: Adobe Experience Platform에 대한 2022년 8월 릴리스 정보입니다.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 25697d341b2970eeb20d9f2507ee701ade8046d3
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 26%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 8월 24일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [실시간 고객 프로필](#profile)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능과 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준의 구성을 사용하여 기업의 요구 사항에 맞는 모델을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 개인 정보 보호 지원 | <ul><li> 이제 Attribution AI는 제품 애플리케이션 내의 기능 및 개체에 대한 [권한](../../../help/access-control/abac/ui/permissions.md)을(를) 관리하기 위한 사용자 역할 및 액세스 정책 정의를 지원합니다. </li><li>감사 로그 리소스는 활동이 발생하면 자동으로 기록됩니다.</li><li> [특성 기반 액세스 제어](../../access-control/abac/overview.md)를 통해 관리자는 특정 특성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다. 특정 특성은 레이블과 같이 개체에 추가된 메타데이터일 수 있습니다. 또한 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.</li><li>기여도 AI는 Experience Platform 데이터 세트를 활용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하기 위해 브랜드는 Experience Platform Privacy Service을 사용하여 액세스 및 삭제에 대한 소비자 요청을 제출하고 데이터 레이크, ID 서비스 및 실시간 고객 프로필에서 데이터를 제거해야 합니다.  </li><li>모델의 입력/출력에 사용되는 모든 데이터 세트는 Experience Platform 지침을 따릅니다. Experience Platform 데이터 암호화는 사용되지 않는 데이터 및 전송 중인 데이터에 적용됩니다. [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md)에 대한 자세한 내용은 설명서를 참조하세요.</li></ul> |

{style="table-layout:auto"}

**참고**: 추가 통지가 있을 때까지 기존 Healthcare Shield 고객은 Attribution AI를 사용할 수 없습니다.

기여도 AI에 대한 자세한 내용은 [기여도 AI](../../intelligent-services/attribution-ai/overview.md) 개요를 참조하십시오.

### 고객 AI

Real-Time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 개인 정보 보호 지원 | <ul><li> 이제 Customer AI는 제품 응용 프로그램 내의 기능 및 개체에 대한 [권한](../../../help/access-control/abac/ui/permissions.md)을(를) 관리하기 위한 사용자 역할 및 액세스 정책 정의를 지원합니다. </li><li>감사 로그 리소스는 활동이 발생하면 자동으로 기록됩니다.</li><li> [특성 기반 액세스 제어](../../access-control/abac/overview.md)를 통해 관리자는 특정 특성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다. 이러한 속성은 레이블과 같은 객체에 추가된 메타데이터일 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수도 있습니다.</li><li>고객 AI는 Experience Platform 데이터 세트를 활용합니다. 브랜드가 수신할 수 있는 소비자 권한 요청을 지원하기 위해 브랜드는 Experience Platform Privacy Service을 사용하여 액세스 및 삭제에 대한 소비자 요청을 제출하고 데이터 레이크, ID 서비스 및 실시간 고객 프로필에서 데이터를 제거해야 합니다. </li><li>모델의 입력/출력에 사용되는 모든 데이터 세트는 Experience Platform 지침을 따릅니다. Experience Platform 데이터 암호화는 사용되지 않는 데이터 및 전송 중인 데이터에 적용됩니다. [데이터 암호화](../../../help/landing/governance-privacy-security/encryption.md)에 대한 자세한 내용은 설명서를 참조하세요.</li></ul> |

{style="table-layout:auto"}

**참고**: Customer AI는 추가 통지가 있을 때까지 기존 Healthcare Shield 고객에서 사용할 수 없습니다.

Customer AI에 대한 자세한 내용은 [Customer AI](../../intelligent-services/customer-ai/overview.md) 개요를 참조하십시오.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform에서는 매일 스냅숏 중에 캡처된 조직 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 [!DNL dashboards]을(를) 제공합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 예약된 활성화 위젯 | [!UICONTROL 예약된 활성화] 위젯은 가장 최근에 활성화된 대상을 표로 정리한 보기를 제공합니다. 각 세그먼트에 대한 이름, 대상 플랫폼 및 활성화 시작 및 종료 날짜가 포함됩니다. 이 위젯을 사용하면 대상이 활성화되는 위치와 시기를 한 눈에 파악할 수 있으며 중복되거나 불필요한 활성화를 더 투명하게 만듭니다. 이렇게 축적된 정보에서는 활성화가 제외된 위치도 강조합니다. |

[!DNL Dashboards]에 대한 자세한 내용은 [[!DNL Dashboards] 개요](../../dashboards/home.md)를 참조하십시오.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]을(를) 사용하면 데이터 엔지니어가 XDM(Experience Data Model)에서 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고가 있는 레코드 수집 지원 | 이제 데이터 준비에서 필드에 대한 경고(중요하지 않은 오류)를 현지화하고 나머지 행을 수집할 수 있습니다. 이제 모든 매퍼 변환 오류가 경고로 보고되며, 부분적으로 수집된 행은 경고와 함께 성공한 것으로 간주됩니다.  경고 및 진단 세부 정보가 있는 레코드에서도 모니터링이 지원됩니다. 경고가 있는 레코드의 일부 수집은 현재 데이터 스트리밍에만 사용할 수 있습니다. 자세한 내용은 [경고가 있는 레코드 수집](../../sources/tutorials/ui/monitor-streaming.md)에 대한 설명서를 검토하십시오. |

{style="table-layout:auto"}

[!DNL Data Prep]에 대한 자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하세요.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| (Beta) 개인화 대상에 대한 속성 기반 개인화 지원 | 특성 기반 개인화의 베타 릴리스에서는 [대상 카탈로그](../../destinations/catalog/overview.md)에 두 개의 새 카드가 표시됩니다. <ul><li>**[!UICONTROL Adobe Target V2]**: 이 커넥터는 현재 Beta 버전이며 일부 고객만 사용할 수 있습니다. Adobe Target V1 카드에서 제공하는 기능 외에도 Target V2 커넥터는 활성화 워크플로에 [매핑 단계](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes)를 추가합니다. 이를 통해 프로필 속성을 Adobe Target에 매핑할 수 있으므로 속성 기반의 동일 페이지 및 다음 페이지 개인화를 수행할 수 있습니다.</li><li>**[!UICONTROL 특성이 있는 사용자 지정 Personalization]**: 이 커넥터는 현재 Beta 상태이며 일부 고객만 사용할 수 있습니다. **[!UICONTROL 사용자 지정 Personalization]**&#x200B;에서 제공하는 기능 외에 **[!UICONTROL 특성을 가진 사용자 지정 Personalization]** 커넥터는 활성화 워크플로에 선택적 [매핑 단계](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes)를 추가합니다. 이를 통해 프로필 특성을 사용자 지정 개인화 대상에 매핑하여 특성을 기반으로 한 동일 페이지 및 다음 페이지 개인화를 활성화할 수 있습니다.</li></ul> <br> 프로필 특성에 중요한 데이터가 포함되어 있을 수 있습니다. 이 데이터를 보호하려면 **[!UICONTROL 특성을 가진 사용자 지정 Personalization]** 대상을 사용하려면 데이터 수집에 [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/)를 사용해야 합니다. 또한 모든 Edge Network API 호출은 [인증된 컨텍스트](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication)에서 수행되어야 합니다. |

{style="table-layout:auto"}

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/)은(는) 세계에서 가장 많은 B2B 구매자-판매자 상호 작용 데이터와 판매 데이터를 인텔리전스로 변환하기 위한 독점 AI 기술에 대한 상당한 투자가 있는 Sales Execution Experience Platform입니다. [!DNL Outreach]을(를) 사용하면 조직의 효율성, 예측 가능성 및 성장을 향상시키기 위해 영업 참여를 자동화하고 매출 인텔리전스를 수행할 수 있습니다. |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL AJO 엔터티 클래스]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | Adobe Journey Optimizer에 대한 조회 스키마를 만들기 위한 레코드 기반 클래스입니다. |
| 필드 그룹 | [[!UICONTROL Workfront 작업 개체]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Adobe Workfront의 모든 하위 수준 개체별 필드 그룹을 참조하는 래퍼 필드 그룹입니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 두 개의 새 속성이 추가되었습니다. `origTimeStamp` 및 `experienceID`. |
| 필드 그룹 | [[!UICONTROL 세그먼트 멤버십 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 이제 [!UICONTROL XDM 개인 프로필] 외에 XDM 비즈니스 계정 클래스를 기반으로 하는 스키마에서도 이 필드 그룹을 사용할 수 있습니다. |
| 필드 그룹 | (다수) | Marketo B2B 활동과 관련된 여러 필드 그룹이 안정적인 상태로 업데이트되었습니다. 자세한 내용은 다음 [가져오기 요청](https://github.com/adobe/xdm/pull/1593/files)을 참조하십시오. |
| 필드 그룹 | (다수) | `uvIndex` 및 `sunsetTime`에서 발생하는 오류를 수정하기 위해 여러 날씨 관련 필드 그룹이 업데이트되었습니다. 자세한 내용은 다음 [가져오기 요청](https://github.com/adobe/xdm/pull/1602/files)을 참조하십시오. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 새 속성 `productImageUrl`을(를) 추가했습니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 새 속성 `framesPerSecond`을(를) 추가했습니다. |
| 데이터 유형 | [[!UICONTROL 세션 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion`의 이름이 `appVersion`로 변경되었습니다. `meta:enum` 및 `description` 필드도 업데이트되었습니다. |
| 데이터 유형 및 필드 그룹 | (다수) | 일부 미디어 데이터 유형 및 필드 그룹에는 새 필드와 업데이트된 설명이 있습니다. 자세한 내용은 다음 [가져오기 요청](https://github.com/adobe/xdm/pull/1582/files)을 참조하십시오. |
| (모두) | (다수) | 이제 `enum` 필드가 포함된 모든 스키마 개체에는 각 제약 조건의 표시 값을 나타내는 해당 `meta:enum` 필드도 포함됩니다. 자세한 내용은 다음 [가져오기 요청](https://github.com/adobe/xdm/pull/1601/files)을 참조하십시오. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 병합 정책 하드 제한 | 이제 Experience Platform에서 샌드박스당 **5** 병합 정책을 엄격하게 제한합니다. 현재 샌드박스에 5개 이상의 병합 정책이 있는 경우, 샌드박스에 5개 미만의 병합 정책이 있을 때까지 **새 병합 정책을 만들 수 없습니다**. |
| 분리된 프로필 에지 속성 정리 | 이제 모든 조직의 프로필 서비스는 매일 사용자 활동 영역의 남은 가장자리 속성을 제거하여 시스템에서 프로필을 보다 정확하게 표현합니다. 이 정리는 지정된 프로필에 대한 모든 프로필 조각이 삭제된 후 발생하며 `com_adobe_aep_profile_region_dataset`이(가) `true`(으)로 표시된 데이터 세트에서 병합되는 프로필에 영향을 미칩니다. 이 지표에는 이 릴리스 이전에 남은 에지 속성 조각이 포함되었으므로 라이선스 사용 대시보드의 &quot;대응 가능 대상&quot; 지표가 감소할 수 있고 프로필 대시보드의 &quot;프로필 수&quot; 지표가 감소할 수 있습니다. |

{style="table-layout:auto"}

프로필 데이터 작업에 대한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대해 자세히 알아보려면 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 4000개 세그먼트 지원 | Experience Platform을 사용하는 모든 조직은 이제 최대 4000개의 세그먼트 정의를 지원할 수 있습니다. 이 변경 사항이 세그먼트 작업 API에 미치는 영향에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../../segmentation/api/segment-jobs.md)를 참조하십시오. |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 셀프 서비스 소스의 일반 가용성(일괄 SDK) | REST API 기반 데이터 소스를 개발, 테스트 및 통합하여 손쉽게 소스 사양을 구성하여 배치 데이터를 Experience Platform으로 수집할 수 있습니다. Sources SDK을 사용하여 다음과 같은 작업을 수행할 수 있습니다. <ul><li>Experience Platform 카탈로그에 새 소스를 구성합니다.</li><li>지원되는 인증 유형, 예약 및 리소스 데이터를 가져오는 방법에 대한 정보를 포함하여 소스에 대한 사양을 정의합니다.</li><li>새 소스에 대한 사용자 대면 설명서를 만듭니다.</li></ul> 자세한 내용은 [셀프 서비스 원본(일괄 SDK)](../../sources/sources-sdk/overview.md)에 대한 설명서를 참조하십시오. |
| [!DNL Google BigQuery] 소스의 일반 가용성 | [!DNL Google BigQuery] 소스를 사용하여 [!DNL Google BigQuery] 데이터 웨어하우스에서 Experience Platform으로 데이터를 수집합니다. 자세한 내용은 [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md)의 설명서를 참조하십시오. |
| [!DNL Teradata Vantage] 소스(Beta) | [!DNL Teradata Vantage] 소스를 사용하여 하이브리드 멀티 클라우드 환경에서 Experience Platform으로 데이터를 수집합니다. 자세한 내용은 [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md)의 설명서를 참조하십시오. |
| Adobe Analytics 소스에 대한 교차 영역 지원 | 이제 모든 지역(미국, 영국 또는 싱가포르)에서 보고서 세트를 수집할 수 있습니다. 보고서 세트는 소스 연결이 생성되는 Experience Platform Sandbox 인스턴스와 동일한 조직에 매핑되어야 합니다. 자세한 내용은 [UI에서 Adobe Analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
