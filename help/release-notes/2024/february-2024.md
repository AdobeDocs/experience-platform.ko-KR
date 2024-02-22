---
title: Adobe Experience Platform 릴리스 노트 2024년 2월
description: Adobe Experience Platform의 2024년 2월 릴리스 정보.
source-git-commit: b41a69244c7eb1111759b2af5c1ae6a0fb90be32
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 20%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 2월 21일 목요일**

Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [데이터 수집](#data-collection)
<!-- - [Data Prep](#data-prep) -->
- [대상](#destinations)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 다음을 통해 다양한 경고 규칙에 가입할 수 있습니다. [!UICONTROL 경고] Platform 사용자 인터페이스의 탭으로, UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.
**새 기능 또는 업데이트된 기능**
| 기능 | 설명 | | — | — | | 경고 내역 탭 | Experience Platform 관리자는 경고 구독자 관리 기능을 사용하여 Adobe 사용자 ID, 외부 이메일 주소 또는 이메일 그룹 목록에 경고를 할당할 수 있습니다. 자세한 내용은 [경고 UI 설명서](../../observability/alerts/ui.md) 기록 탭에 대한 자세한 내용은 |

{style="table-layout:auto"}

경고에 대해 자세히 알아보려면 [[!DNL Observability Insights] 개요](../../observability/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [Web SDK의 웹 인앱 메시지 지원](../../edge/personalization/web-in-app-messaging.md) | 이제 Adobe Experience Platform Web SDK가 Adobe Journey Optimizer 캠페인에 대한 웹 인앱 메시지 구성을 지원합니다. |

{style="table-layout:auto"}

데이터 수집에 대해 자세히 알아보려면 [데이터 수집 개요](../../tags/home.md)를 참조하십시오.

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [Gainsight PX 연결](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX는 제품 팀이 사용자가 제품을 사용하는 방법을 이해하고 피드백을 수집하며 제품 연습과 같은 인앱 참여를 만들어 사용자 온보딩 및 제품 채택을 유도할 수 있는 제품 경험 플랫폼입니다. |
| [Mailchimp 태그 연결](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp는 인기 있는 마케팅 자동화 플랫폼 및 이메일 마케팅 서비스입니다. Mailchimp 태그 커넥터를 사용하여 연락처를 구성, 레이블 지정 또는 분류할 수 있습니다. |
| [SAP Commerce 연결](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce는 B2B 및 B2C 기업을 위한 클라우드 기반의 전자 상거래 플랫폼 솔루션으로 SAP Customer Experience 포트폴리오의 일부로 제공됩니다. 이 대상을 사용하여 기존 Experience Platform 대상에서 SAP Commerce 내의 고객 세부 정보를 업데이트할 수 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 일반적으로 사용할 수 있는 계정 대상자 활성화 | 이제 를 구매하는 회사에서 특정 대상에 대해 계정 대상을 활성화하는 기능을 일반적으로 사용할 수 있습니다. [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2b) Real-time Customer Data Platform 에디션. 다음에 대한 자습서 읽기: [계정 대상자 활성화](/help/destinations/ui/activate-account-audiences.md) 지원되는 대상을 포함하여 전체 정보를 얻습니다. |
| Google 대상에 대한 Digital Markets Act 동의 시행 도구 | Google은 의 변경 사항을 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)및 [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 아래에 정의된 준수 및 동의 관련 요구 사항을 지원하기 위해 [디지털 시장법](https://digital-markets-act.ec.europa.eu/index_en) 유럽 연합의 (DMA)[EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/)). 이러한 동의 요건 변경의 시행은 2024년 3월 6일부터 시행될 예정이다. <br/><br/> EU 사용자 동의 정책을 준수하고 유럽 경제 영역(EEA)의 사용자에 대한 대상 목록을 계속 만들려면 광고주와 파트너는 대상 데이터를 업로드할 때 최종 사용자 동의를 전달하는지 확인해야 합니다. Google 파트너인 Adobe은 유럽 연합의 DMA에 따라 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.<br/><br/>Adobe 개인 정보 보호 및 보안 쉴드를 구매하고 [동의 정책](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 동의하지 않은 프로필을 필터링하려면 별도의 조치를 취할 필요가 없습니다.<br/><br/>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 [세그먼트 정의](../../segmentation/home.md#segment-definitions) 내 기능 [세그먼트 빌더](../../segmentation/ui/segment-builder.md) 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용할 수 있도록 동의하지 않은 프로필을 필터링합니다. |
| [!BADGE 베타]{type=Informative} 배치 대상에 대한 매핑 필드 순서 바꾸기 | 이제 의 매핑 필드를 드래그 앤 드롭하여 CSV 내보내기의 열 순서를 변경할 수 있습니다. [매핑](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 단계. UI에서 매핑된 필드의 순서는 내보낸 CSV 파일의 열 순서에 따라 위에서 아래로 반영되며, 맨 위 행은 CSV 파일의 가장 왼쪽 열입니다. <br/><br/> 이 기능은 베타 버전이며 일부 고객만 사용할 수 있습니다. 이 기능에 대한 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE 베타]배치 대상에 대해 미리 선택된 기본 내보내기 일정 {type=Informative} | 이제 Experience Platform이 각 파일 내보내기에 대한 기본 일정을 자동으로 설정합니다. 다음에서 설명서를 참조하십시오. [대상자 내보내기 예약](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) 기본 일정을 수정하는 방법을 알아봅니다. <br/><br/> 이 기능은 베타 버전이며 일부 고객만 사용할 수 있습니다. 이 기능에 대한 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE 베타]{type=Informative} 배치 대상에 대한 대상자 활성화 일정 벌크 편집 | 이제 다음에서 여러 대상에 대한 활성화 일정을 일괄적으로 편집할 수 있습니다. [활성화 데이터](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) 페이지를 가리키도록 업데이트하는 중입니다. <br/><br/> 이 기능은 베타 버전이며 일부 고객만 사용할 수 있습니다. 이 기능에 대한 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE 베타]{type=Informative} 주문형 파일을 일괄 처리 대상으로 내보내기 | 이제 다음을 통해 대상자를 일괄 배치 대상으로 내보낼 수 있습니다. [요청 시 파일 내보내기](../../destinations/ui/export-file-now.md) 기능. <br/><br/> 이 기능은 베타 버전이며 일부 고객만 사용할 수 있습니다. 이 기능에 대한 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 글로벌 규모로 디지털 경험 애플리케이션을 강화하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 | 이제 동의 및 거버넌스 규칙에 대한 오브젝트 유형을 지원하는 것 외에도 샌드박스 도구를 사용하여 통합 프로필이 활성화되지 않은 스키마를 가져오고, 세그먼트를 가져올 때 타겟 샌드박스에서 누락된 속성이 있는지 확인하고, 기본적으로 기존 병합 정책을 사용합니다. 이러한 기능에 대한 자세한 내용은 [샌드박스 도구 UI 안내서](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계정 대상자 | 이제 계정 대상을 일반적으로 사용할 수 있습니다! 이제 계정 세분화를 사용하여 Real-Time Customer Platform의 B2B 및 B2P 에디션 모두에서 사람 기반 대상자에서 계정 기반 대상자로 마케팅 세분화 환경을 완전히 쉽고 정교하게 만들 수 있습니다. 이 릴리스에서는 사용자 기반 대상을 계정 기반 대상의 술어로 사용하고, 검색 기능을 추가하고, 사용자 지정 엔티티의 사용을 지원하고, 데이터 거버넌스를 준수할 수 있습니다. 이 기능에 대한 자세한 내용은 [계정 대상자 개요](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE 베타]{type=Informative} [!DNL Acxiom] 소스 | 사용 [[!DNL Acxiom Prospecting Data Import] 소스](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) 에서 데이터 검색 및 매핑 [!DNL Acxiom] Experience Platform 대상 Prospect Service |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).
