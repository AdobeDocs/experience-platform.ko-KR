---
title: Adobe Experience Platform 릴리스 정보 2024년 2월
description: Adobe Experience Platform의 2024년 2월 릴리스 정보.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 91%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 2월 21일**

Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 Experience Platform 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며 UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고 내역 탭 | Experience Platform 관리자는 경고 구독자 관리 기능을 사용하여 Adobe 사용자 ID, 외부 이메일 주소 또는 이메일 그룹 목록에 경고를 할당할 수 있습니다. [경고 UI 설명서](../../observability/alerts/ui.md)에서 내역 탭에 대한 자세한 내용을 확인할 수 있습니다. |

{style="table-layout:auto"}

경고에 대해 자세히 알아보려면 [[!DNL Observability Insights] 개요 ](../../observability/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [Web SDK에서 웹 인앱 메시지 지원](../../web-sdk/personalization/web-in-app-messaging.md) | 이제 Adobe Experience Platform Web SDK는 Adobe Journey Optimizer 캠페인을 위한 웹 인앱 메시지 구성을 지원합니다. |

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

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [Gainsight PX 연결](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX는 제품 팀이 사용자가 제품을 어떻게 사용하는지 파악하고, 피드백을 수집하며, 제품 안내와 같은 인앱 참여를 만들어 사용자 온보딩 및 제품 채택을 촉진할 수 있는 제품 경험 플랫폼입니다. |
| [Mailchimp 태그 연결](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp는 널리 사용되는 마케팅 자동화 플랫폼이자 이메일 마케팅 서비스입니다. Mailchimp 태그 커넥터를 사용하여 연락처를 구조화, 라벨링 또는 분류할 수 있습니다. |
| [SAP Commerce 연결](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce는 B2B 및 B2C 기업을 위한 클라우드 기반 전자 상거래 플랫폼 솔루션으로, SAP 고객 경험 포트폴리오의 일부로 제공됩니다. 이 대상을 사용하여 기존 Experience Platform 대상자의 SAP Commerce 내 고객 세부 정보를 업데이트할 수 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 일반적으로 사용 가능한 계정 대상자 활성화 | 특정 대상에 대한 계정 대상자 활성화 기능은 이제 일반적으로 Real-Time CDP의 [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) 버전을 구매하는 기업에서 사용할 수 있습니다. [계정 대상자 활성화](/help/destinations/ui/activate-account-audiences.md)에 대한 튜토리얼을 읽고 지원 대상을 포함한 전체 정보를 확인하십시오. |
| Google 대상을 위한 디지털 시장법 동의 시행 도구 | Google은 유럽연합에서 [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en)&#x200B;(DMA)에 정의된 규정 준수 및 동의 관련 요구 사항을 지원하기 위해 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치 타겟팅](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)에 대한 변경 사항을 출시합니다([EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/)). 이러한 동의 요구 사항 변경 사항은 2024년 3월 6일부터 시행될 예정입니다. <br/><br/> EU 사용자 동의 정책을 준수하고 유럽 경제 지역(EEA) 사용자를 위한 대상자 목록을 계속 생성하려면 광고주와 파트너가 대상자 데이터를 업로드할 때 최종 사용자 동의를 전달해야 합니다. Google 파트너로서 Adobe는 유럽연합의 DMA에 따른 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.<br/><br/>Adobe Privacy &amp; Security Shield를 구매하고 동의하지 않은 프로필을 필터링하는 [동의 정책](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)을 구성한 고객은 별다른 조치를 취할 필요가 없습니다.<br/><br/>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용하려면 [세그먼트 빌더](../../segmentation/ui/segment-builder.md) 내에서 [세그먼트 정의](../../segmentation/home.md#segment-definitions) 기능을 사용하여 동의하지 않는 프로필을 필터링해야 합니다. |
| [!BADGE Beta]{type=Informative} 배치 대상에 대한 매핑 필드 재정렬 | 이제 [매핑](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 단계에서 매핑 필드를 드래그 앤 드롭하여 CSV 내보내기의 열의 순서를 변경할 수 있습니다. UI에서 매핑된 필드의 순서는 내보낸 CSV 파일의 열 순서를 위에서 아래로 반영하며, 맨 위 행은 CSV 파일에서 가장 왼쪽에 있는 열입니다. <br/><br/> 이 기능은 Beta 버전으로 일부 고객만 사용할 수 있습니다. 이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE Beta]{type=Informative} 배치 대상에 대해 미리 선택된 기본 내보내기 예약 | 이제 Experience Platform은 각 파일 내보내기에 대한 기본 일정을 자동으로 설정합니다. 기본 일정을 수정하는 방법은 [대상자 내보내기 예약](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)에 대한 설명서를 참조하십시오. <br/><br/> 이 기능은 Beta 버전으로 일부 고객만 사용할 수 있습니다. 이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE Beta]{type=Informative} 배치 대상에 대한 대상자 활성화 예약 일괄 편집 | 이제 [활성화 데이터](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) 페이지에서 여러 대상자의 활성화 예약을 일괄로 편집할 수 있습니다. <br/><br/> 이 기능은 Beta 버전으로 일부 고객만 사용할 수 있습니다. 이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE Beta]{type=Informative} 배치 대상으로 온디맨드 파일 일괄 내보내기 | 이제 [온디맨드 파일 내보내기](../../destinations/ui/export-file-now.md) 기능을 통해 대상자를 배치 대상으로 일괄 내보낼 수 있습니다. <br/><br/> 이 기능은 Beta 버전으로 일부 고객만 사용할 수 있습니다. 이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오. |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 | 이제 동의 및 거버넌스 규칙을 위해 오브젝트 유형을 지원하는 것 외에도 샌드박스 도구를 사용하여 통합 프로필이 활성화되지 않은 상태에서 스키마를 가져오고, 세그먼트를 가져올 때 대상 샌드박스에서 누락된 속성이 있는지 확인한 다음 기존 병합 정책을 사용하도록 기본 설정할 수 있습니다. 이들 기능에 대한 자세한 내용은 [샌드박스 도구 UI 안내서](../../sandboxes/ui/sandbox-tooling.md)를 참조하십시오. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Experience Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계정 대상자 | 이제 계정 대상자를 일반적으로 사용할 수 있습니다! 이제 계정 세분화를 사용하여 Real-Time Customer Experience Platform의 B2B 및 B2P 에디션 모두에서 사람 기반 대상자에서 계정 기반 대상자로 마케팅 세분화 환경을 완전히 용이하고 정교하게 만들 수 있습니다. 이 릴리스를 통해 사람 기반 대상자를 계정 기반 대상자에 대한 예측 기준으로 사용할 수 있고, 검색 기능을 추가하고, 사용자 정의 엔티티의 사용을 지원하며, 데이터 거버넌스를 준수할 수 있습니다. 이 기능에 대한 자세한 내용은 [계정 대상자 개요](../../segmentation/types/account-audiences.md)를 참조하십시오. |

{style="table-layout:auto"}

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] 소스 | [[!DNL Acxiom Prospecting Data Import] 소스](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)를 사용하여 [!DNL Acxiom] 잠재 고객 서비스에서 데이터를 검색하고 Experience Platform에 매핑합니다. |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
