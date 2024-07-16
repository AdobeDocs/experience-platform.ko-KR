---
title: Adobe Experience Platform 릴리스 노트 2022년 4월
description: Adobe Experience Platform에 대한 2022년 4월 릴리스 정보입니다.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2670'
ht-degree: 18%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 4월 27일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [데이터 흐름](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B 에디션](#B2B)
- [소스](#sources)

## [!DNL Dashboards] {#dashboards}

Platform은 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 정보를 볼 수 있는 여러 대시보드를 제공합니다.

대시보드는 조직의 데이터에 대해 사전 구성된 보고 옵션을 제공하며 Platform 내의 마케터 워크플로우에 직접 빌드됩니다. 이러한 대시보드는 추가적인 IT 지원이나 추가적인 데이터 웨어하우징 설계 및 구현으로 데이터를 내보내고 처리하는 데 소요되는 시간과 노력 없이 사용할 수 있습니다.

다음 위젯은 해당 대시보드의 위젯 라이브러리를 통해 사용할 수 있습니다. [위젯 라이브러리를 통해 위젯을 추가하는 방법](../../dashboards/customize/widget-library.md)에 대한 자세한 내용은 설명서를 참조하세요.

**새 위젯**

| 위젯 | 대시보드 | 설명 |
| ------ | --------- | ----------- |
| [!UICONTROL 추가된 프로필 트렌드] | 프로필 | 이 위젯은 선 그래프를 사용하여 지난 30일, 90일 또는 12개월 동안 매일 프로필 스토어에 추가된 총 병합 프로필 수를 보여 줍니다. |
| [!UICONTROL 대상 상태에 매핑된 대상자] | 프로필 | 이 위젯은 매핑된 대상자와 매핑되지 않은 대상자의 총 수를 단일 지표로 표시하며, 도넛형 차트를 사용하여 합계의 비례 차이를 보여 줍니다. |
| [!UICONTROL 대상 크기] | 프로필 | 이 위젯은 최대 20개의 세그먼트와 각 세그먼트에 포함된 총 대상 수를 나열하는 2열 테이블을 제공합니다. 목록은 적용된 병합 정책에 따라 다르며, 전체 대상 수에 따라 높음에서 낮음 순으로 정렬됩니다. |
| [!UICONTROL 프로필 개수 트렌드] | 프로필 | 이 위젯은 선 그래프를 사용하여 시간에 따른 시스템에 포함된 총 프로필 수의 트렌드를 보여 줍니다. 데이터는 30일, 90일, 12개월 기간에 시각화할 수 있습니다. |
| [!UICONTROL ID별 단일 ID 프로필] | 프로필 | 이 위젯은 막대 차트를 사용하여 하나의 고유 식별자로만 식별되는 총 프로필 수를 보여줍니다. 위젯은 가장 일반적으로 발생하는 ID 중 최대 5개를 지원합니다. |
| [!UICONTROL 대상 상태] | 대상 | 이 위젯은 활성화된 대상의 총 수를 단일 지표로 표시하고 도넛형 차트를 사용하여 활성화된 대상과 비활성화된 대상 간의 비례 차이를 보여 줍니다. |
| 대상 플랫폼별 [!UICONTROL 활성 대상] | 대상 | 이 위젯은 2열 테이블을 사용하여 활성 대상 플랫폼 목록과 각 대상 플랫폼에 대한 총 활성 대상 수를 표시합니다. |
| [!UICONTROL 모든 대상에 대해 활성화된 대상자] | 대상 | 이 위젯은 단일 지표의 모든 대상에 대해 활성화된 총 대상자 수를 제공합니다. |
| [!UICONTROL 대상자 활성화 순서] | 세그먼트 | 이 위젯은 대상 이름, 플랫폼 및 대상의 활성화 날짜를 나열하는 3열 테이블을 제공합니다. |
| [!UICONTROL 대상자 크기 트렌드] | 세그먼트 | 이 위젯에서는 30일, 90일 및 12개월 기간 동안 세그먼트 정의의 기준을 충족하는 총 프로필 수에 대한 선 그래프 일러스트레이션을 제공합니다. |
| [!UICONTROL 대상 크기 변경 트렌드] | 세그먼트 | 이 위젯에서는 가장 최근의 일별 스냅샷 간 주어진 세그먼트에 적합한 총 프로필 수 차이를 선 그래프로 보여 줍니다. 추세 분석 기간은 30일, 90일, 12개월 기간으로 시각화할 수 있다. |
| ID별 [!UICONTROL 대상 크기 트렌드] | 세그먼트 | 이 위젯은 선택한 ID 유형을 기반으로 특정 세그먼트에 대한 대상 크기 트렌드를 보여 줍니다. 추세 분석 기간은 30일, 90일, 12개월 기간으로 시각화할 수 있다. |

**새로운 기능** {#new-features}

| 기능 | 대시보드 | 설명 |
| ------- | --------- | ----------- |
| 분리된 프로필 세그먼트 멤버십 정리 | 프로필 및 라이선스 사용 | 이제 프로필 서비스는 매일 남은 세그먼트 구성원을 제거하여 시스템에 있는 프로필을 보다 정확하게 표시할 수 있습니다. 이 정리는 주어진 프로필에 대한 프로필 조각이 모두 삭제된 후에 수행됩니다. 이는 라이선스 사용 대시보드의 &quot;대응 가능 대상&quot; 지표가 감소할 수 있으며, 프로필 대시보드의 &quot;프로필 수&quot; 지표가 감소할 수 있습니다. 이는 이 릴리스 이전에 이들 지표가 남은 세그먼트 조각을 포함했기 때문입니다. |

{style="table-layout:auto"}

[[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md) 및 [[!DNL Segments]](../../dashboards/guides/audiences.md) 대시보드에 대한 자세한 내용은 설명서를 참조하세요.

## 데이터 흐름 {#dataflows}

플랫폼에서 데이터는 다양한 소스에서 수집되고, 시스템 내에서 분석되며, 다양한 대상으로 활성화됩니다. Platform은 데이터 흐름과 함께 투명성을 제공하여 이 잠재적으로 비선형적인 데이터 흐름을 추적하는 프로세스를 보다 쉽게 만듭니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하는 데 도움이 되며, 이 데이터 흐름은 최종적으로 대상에 활성화되기 전에 ID 서비스 및 실시간 고객 프로필에 의해 사용됩니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 대시보드 | 이제 모니터링 대시보드를 사용하여 세그먼트에 대한 데이터 흐름을 모니터링할 수 있습니다. 자세한 내용은 [UI에서 세그먼트 모니터링](../../dataflows/ui/monitor-audiences.md)에 대한 안내서를 참조하십시오. |

데이터 흐름에 대한 일반적인 정보는 [데이터 흐름 개요](../../dataflows/home.md)를 참조하세요. 세그먼테이션에 대한 자세한 내용은 [세그먼테이션 개요](../../segmentation/home.md)를 참조하세요.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]을(를) 사용하면 데이터 엔지니어가 XDM(Experience Data Model)에서 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 소스 지원 | 이제 Adobe Analytics 소스가 데이터 준비 기능을 지원하므로, 데이터 흐름을 생성할 때 Analytics 보고서 세트 데이터를 대상 XDM 스키마에 매핑할 수 있습니다. 자세한 내용은 [Analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md)에 대한 자습서를 참조하십시오. |
| 기존 매핑 규칙 가져오기 지원 | 이제 기존 데이터 흐름에서 매핑 규칙을 가져와서 데이터 흐름 구성을 가속화하고 오류를 제한할 수 있습니다. 자세한 내용은 [기존 매핑 규칙 가져오기](../../data-prep/ui/mapping.md)에 대한 자습서를 참조하십시오. |

[!DNL Data Prep]에 대한 자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하세요.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 고급 엔터프라이즈 대상 커넥터 | 이제 세 개의 Enterprise 대상 커넥터를 일반적으로 사용할 수 있습니다. [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) 및 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> Enterprise 대상 커넥터의 일반 가용성에는 이전에 Beta 단계에서 제공된 모든 기능 등이 포함됩니다. <ul><li>Azure Event Hubs의 [공유 액세스 서명](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 및 HTTP API 대상에 있는 더 많은 [인증 유형](../../destinations/catalog/streaming/http-destination.md#authentication-information)(전달자 토큰, OAuth 2)을 포함한 새로운 인증 기능</li><li>[내역 프로필 데이터 다시 채우기](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill)(처음 활성화될 때 세그먼트에 적합한 내역 프로필 전송);</li><li>이제 이러한 대상에 대해 데이터 흐름 실행 지표가 지원됩니다.</li><li>[세그먼트 이름 및 세그먼트 타임스탬프를 포함하여 데이터 페이로드에 포함된 추가 세그먼트 메타데이터](../../destinations/catalog/streaming/http-destination.md#destination-details);</li><li>허용 목록에 추가하다 Experience Platform이 필요한 고객을 위해 [고정 IP 주소](/help/destinations/catalog/streaming/ip-address-allow-list.md)를 지원합니다.</li></ul> |
| 대상 데이터 흐름에 대한 컨텍스트 내 경고 | 이제 대상 데이터 흐름을 만들 때 [경고에 가입](../../destinations/ui/alerts.md)하여 데이터 흐름 실행의 상태, 성공 또는 실패에 대한 경고 메시지를 받을 수 있습니다. Experience Platform UI에서 또는 이메일을 통해 경고를 수신하도록 선택할 수 있습니다. |

### 고급 엔터프라이즈 대상 커넥터의 릴리스 프로세스 {#release-process-enterprise-destinations}

Amazon Kinesis, Azure 이벤트 허브 및 HTTP API 대상의 경우, 릴리스 프로세스(4월 27일부터) 중에 이전 Beta 대상 카드와 대상 카탈로그에 새로 사용 가능한 GA(일반 출시) 대상 카드가 모두 표시됩니다. Beta 대상을 사용하는 고객이 구성한 모든 데이터 흐름은 다음 며칠 내에 동일한 대상의 GA 버전으로 마이그레이션됩니다. 이 마이그레이션은 궁극적으로 4월 29일 금요일까지 완료되어야 합니다. Beta 대상은 이 짧은 기간 동안 계속 표시되며 **사용되지 않음**(으)로 표시됩니다.

Beta 단계에서 이러한 대상을 활용하고 있는 경우 다음 사항에 유의하십시오.

- 이전에 Beta에 3개의 대상 중 하나가 있었던 경우에는 조치가 필요하지 않습니다. Beta의 일부로 설정된 모든 데이터 흐름은 계속 작동하며 GA 버전으로 마이그레이션됩니다.
- 4월 27일부터 이러한 대상을 설정하려면 대상의 새 GA 버전으로 설정하십시오.
- 릴리스 작업이 완료되면 더 이상 사용되지 않는 것으로 표시된 베타 카드는 4월 29일 금요일까지 제거됩니다. Experience Platform 엔지니어링 팀은 성공적인 릴리스 작업을 위해 면밀히 모니터링하고 있습니다.

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [!DNL Criteo] | [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 광고 플랫폼에 데이터를 연결하고 활성화하십시오. |
| [!DNL Sendgrid] | 트랜잭션 및 마케팅 전자 메일을 위해 데이터를 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 플랫폼에 연결하고 활성화합니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 대한 개별 표준 필드 추가 또는 제거 | 이제 스키마 편집기 UI를 통해 표준 필드 그룹의 일부를 스키마에 추가할 수 있으므로, 사용자 지정 리소스를 처음부터 빌드할 필요 없이 포함하기로 선택한 필드에 더 많은 유연성을 제공할 수 있습니다.<br><br>이제 미리 필드 그룹을 만들거나 편집할 필요 없이 스키마 구조 내에서 임시 사용자 정의 필드를 직접 정의하고 새 사용자 정의 필드 그룹이나 기존 사용자 정의 필드 그룹에 할당할 수도 있습니다.<br><br>새 워크플로에 대한 자세한 내용은 [UI에서 스키마 만들기 및 편집](../../xdm/ui/resources/schemas.md)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 데이터 위생 작업 요청]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 지정된 데이터 세트 또는 샌드박스의 레코드를 삭제하거나 수정하기 위한 데이터 정리 요청의 세부 정보를 캡처합니다. |
| 설명자 | [[!UICONTROL 시계열 세부 기간 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 시계열 및 요약 데이터의 세부 기간을 나타냅니다. 스키마에 적용되면 스키마의 `timestamp` 필드가 이 세부 기간의 첫 번째 타임스탬프입니다. |
| 클래스 | [[!UICONTROL XDM 요약 지표]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | GROUP BY가 있는 SQL SELECT의 결과와 같은 그룹화 차원과 함께 미리 요약된 지표를 제공합니다. |
| 필드 그룹 | [[!UICONTROL 동의 정책 평가 결과 맵]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 개인에 대한 동의 정책 평가 결과를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 검색 쿼리, 필터링 및 순서 지정 등 사이트 검색 관련 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 리드 병합]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 두 개 이상의 리드가 병합되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 보낸 전자 메일]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 수신자에게 이메일이 전송되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 필드 결합]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 이벤트에 대한 ID 결합 프로세스를 통해 계산된 값을 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 감사를 위한 보조 받는 사람 세부 정보]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 감사의 보조 수신자 세부 정보를 캡처하는 Adobe Journey Optimizer 필드 그룹입니다. |
| 필드 그룹 | [[!UICONTROL XDM 비즈니스 계정 사용자 관계 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-사용자 관계와 관련된 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 계정 사용자 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-사용자 관계와 관련된 세부 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 장바구니]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 전자 상거래 장바구니에 대한 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 하나 이상의 제품에 대한 배송 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 사이트 검색 활동에 대한 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 운영 작업과 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 Portfolio 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 작업 포트폴리오 관련 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로그램 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 작업 프로그램 관련 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로젝트 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 작업 프로젝트 관련 세부 정보를 캡처합니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 업데이트 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 대상]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | `destinationCategory`에 대한 새 열거형 값입니다. |
| 설명자 | [[!UICONTROL 알기 쉬운 이름 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 표준 필드에서 필요하지 않은 제안 값(`meta:enum`)을 제거하는 지원이 추가되었습니다. |
| 필드 그룹 | [[!UICONTROL 사용자 로그인 프로세스]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 필드가 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 상거래]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 장바구니 관련 필드가 몇 개 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 선택한 옵션 및 할인 금액에 대해 새 필드가 추가되었습니다. |
| 확장(Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI 전송 시간 최적화]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 전송 시간 점수를 위해 저장소 형식을 최적화합니다. |
| 확장(Workfront) | [[!UICONTROL Workfront 변경 이벤트]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 여러 필드가 사용자 정의 양식 필드에 대한 `workfront:customData` 필드로 대체되었습니다. |
| 확장(Workfront) | [[!UICONTROL 작업 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 여러 필드가 추가되었습니다. |
| 확장(Workfront) | [[!UICONTROL 작업 개체]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 상위 오브젝트 유형 및 사용자 정의 양식 필드에 대한 새 필드입니다. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능과 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가가 데이터 과학에 대한 전문 지식 없이도 비즈니스 수준의 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

### 기여도 AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 다중 데이터 세트 지원 | 다중 데이터 세트 기능은 이제 모든 경험 이벤트 데이터 세트와 ID 맵의 ID 선택을 지원합니다. 데이터 세트 간에 공통 ID 네임스페이스가 있는 한 고객은 ID 맵 및 연결된 ID를 선택할 수 있습니다. Attribution AI은 Adobe Analytics, 경험 이벤트, 소비자 경험 이벤트 스키마를 지원합니다. Attribution AI의 다중 데이터 세트 지원에 대한 자세한 내용은 [Attribution AI 사용 안내서](../../intelligent-services/attribution-ai/user-guide.md)를 참조하세요. |

[!DNL Intelligent Services]에 대한 자세한 내용은 [[!DNL Intelligent Services] 개요](../../intelligent-services/home.md)를 참조하세요.

### 고객 AI

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 다중 데이터 세트 지원 | 다중 데이터 세트 기능은 이제 모든 경험 이벤트 데이터 세트와 ID 맵의 ID 선택을 지원합니다. 데이터 세트 간에 공통 ID 네임스페이스가 있는 한 고객은 ID 맵 및 연결된 ID를 선택할 수 있습니다. 고객 AI는 Adobe Analytics, 경험 이벤트, 소비자 경험 이벤트 및 Adobe Audience Manager 스키마를 지원합니다. Customer AI의 다중 데이터 세트 지원에 대한 자세한 내용은 [Customer AI 사용 안내서](../../intelligent-services/customer-ai/user-guide/configure.md)를 참조하십시오. |
| Customer AI의 새로운 모델 평가 지표 | Customer AI의 새로운 이익 차트를 통해 마케터는 예산 및 ROI 목표를 기반으로 타깃팅할 그룹 크기를 결정할 수 있습니다. 새로운 상승도 차트는 모델의 품질을 측정하므로 무작위 타깃팅을 통해 얻을 수 있는 상승도에 대한 가시성을 향상시킵니다. 자세한 내용은 [고객 AI를 통해 인사이트 검색](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 문서를 참조하십시오. |

[!DNL Intelligent Services]에 대한 자세한 내용은 [[!DNL Intelligent Services] 개요](../../intelligent-services/home.md)를 참조하세요.

## Real-Time Customer Data Platform B2B 에디션 {#B2B}

Real-Time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 business-to-business 서비스 모델에서 운영하는 마케터를 위해 특별히 설계되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `isDeleted` 기능 지원 | 이제 `Activities`을(를) 제외한 모든 [!DNL Marketo] 데이터 세트가 `isDeleted` 매핑을 지원합니다. 새 매핑은 기존 B2B 데이터 흐름에 자동으로 추가됩니다. `isDeleted` 매핑을 사용하여 [!DNL Data Lake]의 데이터가 원본 데이터와 일치하도록 삭제된 레코드를 필터링할 수 있습니다. `isDeleted`에 대한 자세한 내용은 [[!DNL Marketo] 매핑 필드 가이드](../../sources/connectors/adobe-applications/mapping/marketo.md)를 참조하십시오. |

Real-time Customer Data Platform B2B 에디션에 대한 자세한 내용은 [B2B 개요](../../rtcdp/b2b-overview.md)를 참조하세요.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL OneTrust Integration] 지원 | 이제 [!DNL OneTrust Integration] 소스를 사용하여 [!DNL OneTrust] 계정의 동의 및 환경 설정 데이터를 플랫폼으로 수집할 수 있습니다. 자세한 내용은 [소스 연결 만들기 [!DNL OneTrust Integration] 에 대한 설명서를 참조하십시오.](../../sources/connectors/consent-and-preferences/onetrust.md) |
| [!DNL Square] 지원 | 이제 [!DNL Square] 소스를 사용하여 [!DNL Square] 계정에서 플랫폼으로 결제 데이터를 수집할 수 있습니다. |
| 고객 속성 데이터 흐름 삭제 지원 | 이제 고객 속성 소스 커넥터로 만든 데이터 흐름을 삭제할 수 있습니다. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
