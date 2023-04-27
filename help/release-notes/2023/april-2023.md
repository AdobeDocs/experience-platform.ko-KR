---
title: Adobe Experience Platform 릴리스 노트 - 2023년 4월
description: Adobe Experience Platform에 대한 2023년 4월 릴리스 노트입니다.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 8b77b3a91d8724591ec389aa214c81c4bef6baf8
workflow-type: tm+mt
source-wordcount: '1373'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2023년 4월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 준비](#data-prep)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 개의 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 다음을 수행할 수 있습니다 **내역 데이터 필터링** 위젯 인사이트에서 최근 데이터 또는 사용자 지정 분석 기간을 사용합니다.<br>이제 다음을 수행할 수도 있습니다 **기존 위젯 복제**. 복제를 사용자 지정하고 해당 속성을 편집함으로써 고유한 새 위젯을 만들 때 처음부터 다시 시작하지 않도록 할 수 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 지정 위젯을 만드는 방법 등 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md).

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어가 XDM(Experience Data Model) 간 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간 업데이트 | 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간이 3개월로 줄었습니다. 프로덕션 샌드박스의 채우기 기능은 13개월에서 동일하게 유지됩니다. 이 변경 사항은 새 흐름에만 적용되며 기존 흐름에 영향을 주지 않습니다. 자세한 내용은 [Adobe Analytics 개요](../../sources/connectors/adobe-applications/analytics.md). |
| FPID 문자열을 ECID로 변환하는 새 매퍼 함수 | 를 사용하십시오 `fpid_to_ecid` Experience Platform 및 Experience Cloud 애플리케이션에서 사용할 FPID 문자열을 ECID로 변환하는 함수입니다. 자세한 내용은 [데이터 준비 함수 안내서](../../data-prep/functions.md). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트에 대한 IP 주소 난독화 | 이제 에서 부분 또는 전체 데이터 스트림 수준 IP 난독화 옵션을 정의할 수 있습니다 [데이터 스트림 구성 UI](../../edge/datastreams/configure.md). <br><br>데이터 스트림 수준 IP 난독화 설정은 Adobe Target 및 Audience Manager에 구성된 모든 IP 난독화보다 우선합니다. <br><br>Adobe Analytics으로 전송된 데이터는 데이터 스트림 수준의 영향을 받지 않습니다 [!UICONTROL IP 난독화] 설정 Adobe Analytics이 현재 난독화되지 않은 IP 주소를 수신합니다. Analytics에서 난독화된 IP 주소를 수신하려면 Adobe Analytics에서 별도로 IP 난독화를 구성해야 합니다. 이 동작은 향후 릴리스에서 업데이트됩니다.<br><br> IP 난독화에 대한 자세한 내용과 구성 방법에 대한 지침은 를 참조하십시오. [데이터 스트림 구성 설명서](../../edge/datastreams/configure.md#advanced-options). |
| [데이터 스트림 구성 무시](../../edge/datastreams/overrides.md) | 이제 이벤트 데이터 세트, Target 속성 토큰, ID 동기화 컨테이너 및 Analytics 보고서 세트와 같은 특정 설정을 재정의하는 데 사용할 수 있는 데이터 세트에 대한 추가 구성 옵션을 정의할 수 있습니다. <br><br>데이터 스트림 구성을 재정의하는 것은 두 단계로 구성됩니다. <ol><li>먼저, [데이터 스트림 구성 페이지](../../edge/datastreams/configure.md).</li><li>그런 다음 웹 SDK 명령을 통해 또는 웹 SDK를 사용하여 Edge Network에 무시를 보내야 합니다 [태그 확장](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 연결](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Salesforce Marketing Cloud 계정 참여(이전의 Pardot) 대상을 사용하여 리드를 캡처, 추적, 점수 및 등급화합니다. 판매 및 의사 결정 주기를 더 오래 필요로 하는 여러 부서 및 의사 결정자와 관련된 B2B 사용 사례에 대해 이 대상을 사용합니다. |

{style="table-layout:auto"}

**새 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 데이터 흐름 모니터링 [!DNL Custom Personalization] 및 [!DNL Adobe Commerce] 대상 | <p> 이제 에 대한 활성화 지표를 볼 수 있습니다. [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 그리고 [속성을 사용한 사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결. </p> <p>![Adobe Commerce 이미지](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce 지표"){width="100" zoomable="yes"}</p>  자세한 내용은 [대상 작업 공간에서 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 자세한 내용 |
| 새로 만들기 **[!UICONTROL 세그먼트 이름에 세그먼트 ID 추가]** 에 대한 필드 [!DNL Google Ad Manager] 및 [!DNL Google Ad Manager 360] 대상 | <p>이제 세그먼트 이름을에 사용할 수 있습니다. [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 및 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 다음과 같이 Experience Platform의 세그먼트 ID를 포함합니다. `Segment Name (Segment ID)`.</p><p>![세그먼트 ID 이미지 추가](/help/destinations/assets/common/append-segment-id-to-segment-name.png "새 세그먼트 이름 필드에 세그먼트 ID 추가 "){width="100" zoomable="yes"}</p> |
| 예약된 대상 채우기 | <p>대상 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 대상, 세그먼트가 대상 연결에 처음 매핑되면 24-48시간 후에 대상에 대한 대상 채우기 활성화가 수행되도록 예약되었습니다. 이 업데이트는 데이터를 수집할 때까지 24시간을 대기하는 Google의 정책에 응답하며 실시간 CDP와 [!DNL Google Display & Video 360].</p> <p>이 구성은 이 대상에만 적용할 수 있는 백엔드 구성이며 UI의 고객 구성 가능한 예약 옵션과 관련이 없습니다.</p> |

{style="table-layout:auto"}

**수정 사항 및 향상된 기능** {#destinations-fixes-and-enhancements}

- 에서 문제가 해결되었습니다. **제외된 ID** 파일 기반 대상 내보내기에 대한 보고 지표. 고객은 예상대로 활성화된 내보내기에서 내보낸 모든 ID를 수신했습니다. 하지만, **제외된 ID** 내보내지 않아야 하는 ID를 잘못 계산하여 UI의 보고 지표가 제외된 높은 ID를 잘못 표시했습니다. (PLAT-149774)
- 에서 문제가 해결되었습니다. **예약** 활성화 워크플로우의 단계입니다. 매핑 ID가 필요한 대상의 경우, 고객은 기존 대상 연결에 추가된 세그먼트에 대한 매핑 ID를 추가할 수 없었습니다. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 이름 표시 전환 | 이제 스키마 편집기에서 원래 필드 이름과 더 사람이 읽을 수 있는 표시 이름 간에 전환할 수 있습니다. 이러한 유연성을 통해 필드 검색 및 스키마 편집을 향상시킬 수 있습니다. 표준 필드 그룹의 표시 이름은 시스템에서 생성되지만 필요한 경우 UI를 통해 사용자 지정할 수도 있습니다. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 익명의 프로필 데이터 만료 | 일반적으로 익명의 프로필 데이터 만료 기능을 사용할 수 있습니다. 이 릴리스는 활성화되면 Experience Platform 인스턴스에서 오래된 익명의 프로필을 계속 제거합니다. 이 기능 및 익명의 프로필에 대한 자세한 내용은 [익명의 프로필 데이터 만료 안내서](../../profile/pseudonymous-profiles.md). |

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud에 대한 행 수준 데이터 필터링을 위한 API 지원 | 논리 및 비교 연산자를 사용하여 Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud 소스에 대한 행 수준 데이터를 필터링합니다. 안내서 읽기 [API를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md) 추가 정보. |
| Shopify 스트리밍 베타 가용성 | 다음 [Shopify 스트리밍 소스](../../sources/connectors/ecommerce/shopify-streaming.md) 이제 베타로 제공됩니다. Shopify 스트리밍 소스를 사용하여 Shopify 파트너 계정의 데이터를 Experience Platform으로 스트리밍합니다. |
| OneTrust 통합의 일반 공급 | 다음 [OneTrust 통합 소스](../../sources/connectors/consent-and-preferences/onetrust.md) 은 현재 GA입니다. OneTrust 통합 소스를 사용하여 OneTrust 통합 계정의 동의 및 환경 설정 데이터를 Experience Platform으로 가져옵니다. |
| oracle 서비스 클라우드의 일반 공급 | 다음 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md) 은 현재 GA입니다. oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 데이터를 Experience Platform으로 가져옵니다. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
