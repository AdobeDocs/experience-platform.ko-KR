---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a80f011dc8a6e10d1d311bc85029fa9f57d8b4ab
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 3%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2022년 4월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Dashboards]](#dashboards)
- [데이터 흐름](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [대상](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [Real-time Customer Data Platform B2B 에디션](#B2B)
- [소스](#sources)

## [!DNL Dashboards] {#dashboards}

플랫폼은 일일 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 정보를 볼 수 있는 여러 개의 대시보드를 제공합니다.

대시보드는 조직의 데이터에 대해 사전 구성된 보고 옵션을 제공하며 플랫폼 내의 마케터 워크플로우에 직접 구축됩니다. 이러한 대시보드는 추가 IT 지원이 필요하거나 추가적인 데이터 웨어하우징 설계 및 구현을 통해 데이터를 내보내고 처리하는 데 소요되는 시간과 노력 없이 사용할 수 있습니다.

다음 위젯은 해당 대시보드의 위젯 라이브러리를 통해 사용할 수 있습니다. 자세한 내용은 설명서 를 참조하십시오 [위젯 라이브러리를 통해 위젯을 추가하는 방법](../../dashboards/customize/widget-library.md).

**새 위젯**

| 위젯 | 대시보드 | 설명 |
| ------ | --------- | ----------- |
| [!UICONTROL 프로필이 트렌드를 추가했습니다.] | 프로필 | 이 위젯은 선 그래프를 사용하여 지난 30일, 90일 또는 12개월 동안 매일 프로필 저장소에 추가된 병합된 프로필의 총 수를 보여줍니다. |
| [!UICONTROL 대상 상태에 매핑된 대상] | 프로필 | 이 위젯은 단일 지표에 매핑되고 매핑되지 않은 대상의 총 수를 표시하고 도넛 차트를 사용하여 해당 합계의 비례 차이를 보여줍니다. |
| [!UICONTROL 대상 크기] | 프로필 | 이 위젯은 각 세그먼트에 포함된 최대 20개의 세그먼트와 총 대상 수를 나열하는 2열 테이블을 제공합니다. 목록은 총 대상 수에 따라 높은 값에서 낮은 순서로 적용되는 병합 정책에 따라 다릅니다. |
| [!UICONTROL 프로필 수 트렌드] | 프로필 | 이 위젯은 선 그래프를 사용하여 시간에 따라 시스템에 포함된 총 프로필 수의 트렌드를 보여줍니다. 데이터는 30일, 90일 및 12개월 동안 시각화할 수 있습니다. |
| [!UICONTROL ID별 단일 ID 프로필] | 프로필 | 이 위젯에서는 막대 차트를 사용하여 하나의 고유 식별자만 사용하여 식별되는 프로필의 총 수를 보여줍니다. 위젯은 가장 일반적으로 발생하는 ID 중 최대 5개를 지원합니다. |
| [!UICONTROL 대상 상태] | 대상 | 이 위젯은 활성화된 총 대상 수를 단일 지표로 표시하며, 도넛형 차트를 사용하여 활성화된 대상과 비활성화된 대상 간의 비례 차이를 보여줍니다. |
| [!UICONTROL 대상 플랫폼별 활성 대상] | 대상 | 이 위젯은 두 열 테이블을 사용하여 활성 대상 플랫폼 목록과 각 대상 플랫폼에 대한 총 활성 대상 수를 표시합니다. |
| [!UICONTROL 모든 대상에서 활성화된 대상] | 대상 | 이 위젯은 단일 지표의 모든 대상에서 활성화된 총 대상 수를 제공합니다. |
| [!UICONTROL Audience Activation 순서] | 세그먼트 | 이 위젯은 대상의 대상 이름, 플랫폼 및 활성화 날짜를 나열하는 3열 테이블을 제공합니다. |
| [!UICONTROL 대상 크기 트렌드] | 세그먼트 | 이 위젯은 30일, 90일 및 12개월 기간 동안의 세그먼트 정의 기준을 충족하는 총 프로필 수에 대한 선 그래프 그림을 제공합니다. |
| [!UICONTROL 대상 크기 변경 트렌드] | 세그먼트 | 이 위젯은 가장 최근 일별 스냅샷 간 주어진 세그먼트에 자격을 부여받은 프로필의 총 수 차이에 대한 선 그래프 그림을 제공합니다. 트렌드 분석 기간은 30일, 90일 및 12개월 기간으로 시각화할 수 있습니다. |
| [!UICONTROL ID별 대상 크기 트렌드] | 세그먼트 | 이 위젯은 선택한 ID 유형을 기반으로 한 특정 세그먼트의 대상 크기 트렌드를 보여줍니다. 트렌드 분석 기간은 30일, 90일 및 12개월 기간으로 시각화할 수 있습니다. |

**새로운 기능**

| 기능 | 대시보드 | 설명 |
| ------- | --------- | ----------- |
| 분리된 프로필 세그먼트 멤버십 정리 | 프로필 및 라이선스 사용 | 이제 프로필 서비스에서 나머지 세그먼트 구성원을 매일 제거하여 시스템에서 프로필을 보다 정확하게 표현합니다. 이 정리 작업은 주어진 프로필에 대한 모든 프로필 조각이 삭제된 후에 발생합니다. 이 지표들은 이번 릴리스 전에 남은 세그먼트 조각을 포함했으므로, 라이선스 사용 대시보드의 &quot;대응 가능 대상&quot; 지표에 한 방울이 표시될 수 있으며, 프로필 대시보드의 &quot;프로필 수&quot; 지표에 이 릴리스 전의 남은 세그먼트 조각이 포함되어 있을 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

자세한 내용은 설명서 를 참조하십시오 [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md), 및 [[!DNL Segments]](../../dashboards/guides/segments.md) 대시보드 .

## 데이터 흐름 {#dataflows}

Platform에서 데이터는 다양한 소스에서 수집되고 시스템 내에서 분석되며 다양한 대상으로 활성화됩니다. 플랫폼 을 사용하면 데이터 흐름에 투명성을 제공하여 비선형 이외의 데이터 흐름을 쉽게 추적할 수 있습니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어, 데이터를 소스 커넥터에서 타겟 데이터 세트로 이동하는 데 도움이 되며, 이 데이터 흐름은 최종적으로 대상으로 활성화하기 전에 Identity 서비스 및 실시간 고객 프로필에서 활용합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 대시보드 | 이제 모니터링 대시보드를 사용하여 세그먼트의 데이터 흐름을 모니터링할 수 있습니다. 자세한 내용은 [UI에서 세그먼트 모니터링](../../dataflows/ui/monitor-segments.md) |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md). 세그멘테이션에 대해 자세히 알아보려면 [세분화 개요](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 소스 지원 | 이제 Adobe Analytics 소스가 데이터 준비 기능을 지원하므로 데이터 스트림을 만들 때 Analytics 보고서 세트 데이터를 대상 XDM 스키마에 매핑할 수 있습니다. 다음에서 자습서를 참조하십시오. [analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 추가 정보. |
| 기존 매핑 규칙 가져오기 지원 | 이제 기존 데이터 흐름에서 매핑 규칙을 가져와 데이터 흐름 구성을 가속화하고 오류를 제한할 수 있습니다. 다음에서 자습서를 참조하십시오. [기존 매핑 규칙 가져오기](../../data-prep/ui/mapping.md) 추가 정보. |

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 고급 엔터프라이즈 대상 커넥터 | 이제 3개의 엔터프라이즈 대상 커넥터를 일반적으로 사용할 수 있습니다. [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md), 및 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> 엔터프라이즈 대상 커넥터의 일반 가용성에는 베타 단계에서 이전에 제공되는 모든 기능 등이 포함되어 있습니다. <ul><li>다음을 포함한 새로운 인증 기능 [Azure 이벤트 허브의 공유 액세스 서명](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 및 기타 [인증 유형](../../destinations/catalog/streaming/http-destination.md#authentication-information) (HTTP API 대상의 베어러 토큰, OAuth 2);</li><li>[내역 프로필 데이터 채우기](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (처음 활성화되었을 때 세그먼트에 적합한 내역 프로필 전송)</li><li>이제 데이터 흐름 실행 지표가 이러한 대상에 대해 지원됩니다.</li><li>[추가 세그먼트 메타데이터](../../destinations/catalog/streaming/http-destination.md#destination-details) 세그먼트 이름 및 세그먼트 타임스탬프를 포함한 데이터 페이로드에 포함됨</li><li>지원 대상 [정적 IP 주소](/help/destinations/catalog/streaming/ip-address-allow-list.md) Experience Platform을 방문해야 하는 고객허용 목록에 추가하다의 경우.</li></ul> |
| 대상 데이터 흐름에 대한 컨텍스트 내 경고 | 이제 다음을 수행할 수 있습니다 [경고 구독](../../destinations/ui/alerts.md) 대상 데이터 흐름을 만들 때 데이터 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 수신합니다. Experience Platform UI나 이메일을 통해 경고를 수신하도록 선택할 수 있습니다. |

### 고급 엔터프라이즈 대상 커넥터에 대한 릴리스 프로세스 {#release-process-enterprise-destinations}

Amazon Kinesis, Azure 이벤트 허브 및 HTTP API 대상의 경우 릴리스 프로세스(4월 27일부터)에서 이전 베타 대상 카드와 대상 카탈로그에서 새로운 GA(General Available) 대상 카드를 모두 볼 수 있습니다. 베타 대상을 사용하는 고객이 구성한 모든 데이터 흐름은 다음 며칠 내에 동일한 대상의 GA 버전으로 마이그레이션됩니다. 이 마이그레이션은 궁극적으로 4월 29일 금요일 말까지 완료되어야 합니다. 베타 대상은 이 짧은 시간 동안 계속 표시되며 **사용되지 않음**.

베타 단계에서 이러한 대상을 활용하는 경우 다음을 참고하십시오.

- 이전에 3개의 대상 중 하나를 사용하여 Beta에 도착한 적이 있는 경우 아무 작업도 필요하지 않습니다. Beta의 일부로 설정된 모든 데이터 흐름은 계속 작동하며 GA 버전으로 마이그레이션됩니다.
- 4월 27일부터 이러한 대상을 설정하려면 새 GA 버전의 대상으로 설정하십시오.
- 더 이상 사용되지 않음으로 표시된 베타 카드는 릴리스 작업이 완료되면 제거되며, 이는 4월 29일 금요일 말까지 예상됩니다. Experience Platform 엔지니어링 팀은 성공적인 릴리스 작업을 위해 면밀히 모니터링하고 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [!DNL Criteo] | 데이터에 연결 및 활성화 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 광고 플랫폼. |
| [!DNL Sendgrid] | 데이터에 연결 및 활성화 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 트랜잭션 및 마케팅 이메일을 위한 플랫폼. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 대한 개별 표준 필드 추가 또는 제거 | 이제 스키마 편집기 UI를 사용하여 스키마에 표준 필드 그룹 부분을 추가할 수 있으므로, 사용자 지정 리소스를 처음부터 빌드하지 않아도 포함하도록 선택한 필드에 더 유연하게 대처할 수 있습니다.<br><br>이제 스키마 구조 내에서 직접 임시 사용자 지정 필드를 정의하고 필드 그룹을 미리 만들거나 편집할 필요 없이 새 사용자 지정 필드 그룹에 할당할 수도 있습니다.<br><br>다음 안내서를 참조하십시오. [UI에서 스키마 만들기 및 편집](../../xdm/ui/resources/schemas.md) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 데이터 위생 작업 요청]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 지정된 데이터 세트 또는 샌드박스에서 레코드를 삭제하거나 수정하기 위한 데이터 정리 요청의 세부 정보를 캡처합니다. |
| 설명자 | [[!UICONTROL 시계열 세부기간 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 시계열 및 요약 데이터의 세부기간을 나타냅니다. 스키마에 적용할 경우 스키마는 `timestamp` 필드는 이 세부 기간 동안의 첫 번째 타임스탬프입니다. |
| 클래스 | [[!UICONTROL XDM 요약 지표]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | SQL SELECT를 GROUP BY로 사용한 결과와 같은 그룹 차원과 함께 사전 요약된 지표를 제공합니다. |
| 필드 그룹 | [[!UICONTROL 동의 정책 평가 결과 맵]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 개인에게 대한 동의 정책 평가 결과를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 검색 쿼리, 필터링 및 순서 지정과 같은 사이트 검색 관련 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 리드 병합]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 두 개 이상의 리드가 병합되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 이메일 전송됨]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 수신자에게 이메일이 전송되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 결합 필드]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 이벤트에 대한 ID 결합 프로세스를 통해 계산된 값을 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 감사를 위한 보조 수신자 세부 정보]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 감사에 대한 보조 수신자 세부 정보를 캡처하는 Adobe Journey Optimizer 필드 그룹입니다. |
| 필드 그룹 | [[!UICONTROL XDM 비즈니스 계정 개인 관계 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-개인 관계와 관련된 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 계정 개인 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-개인 관계와 관련된 세부 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 장바구니]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 전자 상거래 장바구니에 대한 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 하나 이상의 제품에 대한 배송 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 사이트 검색 활동에 대한 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 작업 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 작업 작업과 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 Portfolio 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 작업 포트폴리오와 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로그램 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 작업 프로그램과 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로젝트 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 작업 프로젝트와 관련된 세부 정보를 캡처합니다. |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 업데이트 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 대상]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 에 대한 새 열거형 값 `destinationCategory`. |
| 설명자 | [[!UICONTROL 이름 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 추천 값(`meta:enum`) 포함되어 있어야 합니다. |
| 필드 그룹 | [[!UICONTROL 사용자 로그인 프로세스]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 필드가 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 상거래]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 장바구니 관련 필드가 몇 개 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 선택한 옵션 및 할인 금액에 대해 새 필드가 추가되었습니다. |
| 확장(Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI 전송 시간 최적화]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 전송 시간 점수를 위한 스토리지 형식을 최적화합니다. |
| 확장(Workfront) | [[!UICONTROL Workfront 변경 이벤트]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 여러 필드가 `workfront:customData` 사용자 지정 양식 필드에 대한 필드입니다. |
| 확장(Workfront) | [[!UICONTROL 작업 작업 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 여러 필드가 추가되었습니다. |
| 확장(Workfront) | [[!UICONTROL 작업 개체]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 상위 개체 유형 및 사용자 지정 양식 필드에 대한 새 필드입니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있는 Intelligent Services를 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

Attribution AI 및 Customer AI를 통해 고객은 마케팅 기여도 분석 및 고객 성향에 대한 고급 AI/ML 모델을 구성할 수 있습니다. 다중 데이터 세트 기능은 고객이 데이터를 미리 결합하고 준비할 필요 없이 모델 구성 시 여러 데이터 세트를 가져올 수 있도록 지원합니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 다중 데이터 집합 지원 | 이제 다중 데이터 세트 기능이 모든 경험 이벤트 데이터 세트와 ID 맵을 ID로 선택할 수 있습니다. 데이터 세트 간에 공통 ID 네임스페이스가 있는 한 고객은 ID 맵 및 관련 ID를 선택할 수 있습니다. Attribution AI은 다음 스키마를 지원합니다. Adobe Analytics, 경험 이벤트, 소비자 경험 이벤트 등을 참조하십시오. Customer AI는 이러한 모든 스키마와 Adobe Audience Manager 스키마를 지원합니다. Attribution AI 및 고객 AI의 다중 데이터 세트 지원에 대한 자세한 내용은 [Attribution AI 사용 안내서](../../intelligent-services/attribution-ai/user-guide.md) 및 [Customer AI 사용 안내서](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Customer AI의 새로운 모델 평가 지표 | 고객 AI의 새로운 이득 차트를 통해 마케터는 예산과 ROI 목표를 기반으로 타겟팅할 그룹 크기를 결정할 수 있습니다. 새 상승도 차트는 모델의 품질을 측정하여 무작위 타깃팅을 통해 얻을 수 있는 상승도를 더 잘 파악할 수 있도록 합니다. 자세한 내용은 [고객 AI를 통해 인사이트 살펴보기](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 문서. |

자세한 내용은 [!DNL Intelligent Services]를 보려면 [[!DNL Intelligent Services] 개요](../../intelligent-services/home.md).

## Real-time Customer Data Platform B2B 에디션 {#B2B}

Real-time Customer Data Platform(실시간 CDP)를 기반으로 구축된 실시간 CDP B2B Edition은 비즈니스-비즈니스 서비스 모델로 운영되는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 가져와서 사람 및 계정 프로필에 대한 단일 보기로 결합합니다. 이러한 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 그러한 대상을 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 지원 대상 `isDeleted` 기능 | 모두 [!DNL Marketo] 데이터 세트를 제외한 데이터 세트 `Activities` 이제 지원 `isDeleted` 매핑. 새 매핑은 기존 B2B 데이터 흐름에 자동으로 추가됩니다. 를 사용할 수 있습니다 `isDeleted` 매핑 을 사용하여 데이터를 [!DNL Data Lake] 는 소스 데이터와 일치합니다. 자세한 내용은 [[!DNL Marketo] 매핑 필드 안내서](../../sources/connectors/adobe-applications/mapping/marketo.md) 추가 정보 `isDeleted`. |

Real-time Customer Data Platform B2B Edition에 대한 자세한 내용은 다음을 참조하십시오. [B2B 개요](../../rtcdp/b2b-overview.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 지원 대상 [!DNL OneTrust Integration] | 이제 를 사용할 수 있습니다 [!DNL OneTrust Integration] 소스에서 동의 및 환경 설정 데이터를 수집할 수 있습니다. [!DNL OneTrust] Platform에 계정을 설정합니다. 다음 문서를 참조하십시오. [만들기 [!DNL OneTrust Integration] 소스 연결](../../sources/connectors/consent-and-preferences/onetrust.md) 추가 정보. |
| 지원 대상 [!DNL Square] | 이제 를 사용할 수 있습니다 [!DNL Square] 출처: 결제 데이터를 수집하여 [!DNL Square] Platform에 계정을 설정합니다. |
| 고객 속성 데이터 흐름 삭제 지원 | 이제 고객 속성 소스 커넥터로 만든 데이터 흐름을 삭제할 수 있습니다. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
