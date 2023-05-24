---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 2023년 4월 릴리스 정보입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e3fc587d924b2183806918f91e5ae3aa3fee52f3
workflow-type: tm+mt
source-wordcount: '2094'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

>[!IMPORTANT]
>
>2023년 5월 15일부터 `Existing` 상태는 세그먼트 멤버십 라이프사이클에서 중복을 제거하기 위해 세그먼트 멤버십 맵에서 더 이상 사용되지 않습니다. 이 변경 후에는 세그먼트에서 적격한 프로필이 다음과 같이 표시됩니다. `Realized` 및 부적격 프로필은 계속 다음과 같이 표시됩니다. `Exited`. 이 변경 사항에 대한 자세한 내용은 [세분화 서비스 섹션](#segmentation).

**릴리스 일자: 2023년 4월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 준비](#data-prep)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [실시간 고객 프로필](#profile)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 대시보드를 제공합니다.

**새 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 다음을 수행할 수 있습니다. **내역 데이터 필터링** 및 에서는 위젯 인사이트를 참조하고 최근 데이터 또는 사용자 지정 분석 기간을 사용합니다. 다음을 참조하십시오. [사용자 정의 대시보드 안내서](../../dashboards/user-defined-dashboards.md#filter-historical-data) 추가 정보.<br>이제 다음 작업을 수행할 수도 있습니다 **기존 위젯 복제**. 중복을 사용자 정의하고 속성을 편집하여 새로운 고유 위젯을 만들 때 처음부터 다시 시작하지 않도록 할 수 있습니다. 읽기 [위젯 복제 안내서](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) 자세히 알아보십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함하여 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md).

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어는 데이터를 XDM(Experience Data Model)에 매핑하고, 변환하고, 유효성을 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간에 대한 업데이트 | 비프로덕션 샌드박스에서 Adobe Analytics의 채우기 기간이 3개월로 단축되었습니다. 프로덕션 샌드박스의 채우기 기간은 13개월로 동일하게 유지됩니다. 이 변경 사항은 새 흐름에만 적용되며 기존 흐름에는 영향을 주지 않습니다. 자세한 내용은 [Adobe Analytics 개요](../../sources/connectors/adobe-applications/analytics.md). |
| FPID 문자열을 ECID로 변환하는 새로운 매퍼 함수 | 사용 `fpid_to_ecid` Experience Platform 및 Experience Cloud 애플리케이션에서 사용할 FPID 문자열을 ECID로 변환하는 함수입니다. 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터스트림에 대한 IP 주소 난독화 | 이제에서 부분 또는 전체 데이터스트림 수준 IP 난독화 옵션을 정의할 수 있습니다. [데이터 스트림 구성 UI](../../edge/datastreams/configure.md). <br><br>데이터스트림 수준의 IP 난독화 설정은 Adobe Target 및 Audience Manager에 구성된 모든 IP 난독화보다 우선합니다. <br><br>Adobe Analytics으로 전송된 데이터는 데이터 스트림 수준의 영향을 받지 않습니다 [!UICONTROL IP 난독화] 설정. Adobe Analytics은 현재 난독화되지 않은 IP 주소를 수신합니다. Analytics가 난독화된 IP 주소를 수신하려면 Adobe Analytics에서 별도로 IP 난독화를 구성해야 합니다. 이 동작은 향후 릴리스에서 업데이트됩니다.<br><br> IP 난독화에 대한 자세한 내용 및 구성 방법에 대한 지침은 다음을 참조하십시오. [데이터 스트림 구성 설명서](../../edge/datastreams/configure.md#advanced-options). |
| [데이터 스트림 구성 재정의](../../edge/datastreams/overrides.md) | 이제 데이터 스트림에 대한 추가 구성 옵션을 정의할 수 있습니다. 이 옵션을 사용하여 이벤트 데이터 세트, Target 속성 토큰, ID 동기화 컨테이너 및 Analytics 보고서 세트와 같은 특정 설정을 재정의할 수 있습니다. <br><br>데이터스트림 구성 재정의는 2단계 프로세스입니다. <ol><li>먼저, 에서 데이터 스트림 구성 재정의를 정의해야 합니다. [데이터스트림 구성 페이지](../../edge/datastreams/configure.md).</li><li>그런 다음 웹 SDK 명령을 사용하거나 웹 SDK를 사용하여 Edge Network에 재정의를 전송해야 합니다 [태그 확장](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT 암호 | 다음 [OAuth JWT 암호](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 는 고객이 Adobe 및 Google 서비스 토큰을 사용하여 이벤트 전달에서 서버 간 상호 작용을 지원할 수 있도록 합니다. |
| [!DNL Pinterest Conversions API] 확장 | 다음 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Pinterest] 를 사용하는 서버측 이벤트 형식으로 [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 연결](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Salesforce Marketing Cloud 계정 참여(이전의 Pardot) 대상을 사용하여 잠재 고객을 캡처, 추적, 점수 매기기 및 등급을 매깁니다. 판매 및 의사 결정 주기가 더 길어야 하는 여러 부서 및 의사 결정자와 관련된 B2B 사용 사례에 이 대상을 사용합니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 에 대한 데이터 흐름 모니터링 [!DNL Custom Personalization] 및 [!DNL Adobe Commerce] 대상 | <p> 이제 다음에 대한 활성화 지표를 볼 수 있습니다. [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [사용자 정의 개인화](../../destinations/catalog/personalization/custom-personalization.md) 및 [속성을 사용한 사용자 지정 개인화](../../destinations/catalog/personalization/custom-personalization.md) 연결. </p> <p>![Adobe Commerce 이미지](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce 지표"){width="100" zoomable="yes"}</p>  다음을 참조하십시오 [대상 작업 영역에서 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 을 참조하십시오. |
| 신규 **[!UICONTROL 세그먼트 이름에 세그먼트 ID 추가]** 필드 [!DNL Google Ad Manager] 및 [!DNL Google Ad Manager 360] 대상 | <p>이제 의 세그먼트 이름을 가질 수 있습니다. [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 및 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 다음과 같이 Experience Platform의 세그먼트 ID를 포함합니다. `Segment Name (Segment ID)`.</p><p>![세그먼트 ID 이미지 추가](/help/destinations/assets/common/append-segment-id-to-segment-name.png "새 세그먼트 이름 필드에 세그먼트 ID 추가 "){width="100" zoomable="yes"}</p> |
| 예약된 대상자 다시 채우기 | <p>의 경우 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 대상: 세그먼트가 대상 연결에 처음 매핑되고 24-48시간 후 대상에 대한 대상 다시 채우기 활성화가 예약됩니다. 이 업데이트는 데이터를 수집할 때까지 24시간 대기하는 Google의 정책에 따른 것으로, Real-Time CDP와 간의 일치율을 개선합니다 [!DNL Google Display & Video 360].</p> <p>이는 이 대상에만 적용할 수 있는 백엔드 구성이며 UI의 고객이 구성할 수 있는 예약 옵션과 관련이 없습니다.</p> |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- 의 문제를 수정했습니다. **ID 제외됨** 파일 기반 대상 내보내기에 대한 보고 지표. 고객은 예상대로 활성화된 내보내기에서 내보낸 모든 ID를 받고 있었습니다. 그러나 **ID 제외됨** 내보내기로 되어 있지 않은 id를 잘못 계산하여 UI의 보고 지표에 제외된 id가 잘못 표시되었습니다. (PLAT-149774)
- 의 문제를 수정했습니다. **예약** 활성화 워크플로의 단계입니다. 매핑 ID가 필요한 대상의 경우, 고객은 기존 대상 연결에 추가된 세그먼트에 대한 매핑 ID를 추가할 수 없었습니다. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 이름 표시 토글 | 이제 스키마 편집기에서는 원래 필드 이름과 사람이 읽을 수 있는 더 많은 표시 이름 사이를 변경하는 토글을 제공합니다.<br>![디스플레이 이름 토글이 강조 표시된 스키마 편집기.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "스키마 편집기 표시 이름 토글"){width="100" zoomable="yes"}<br>이러한 유연성을 통해 필드 검색 기능을 개선하고 스키마를 편집할 수 있습니다. 표준 필드 그룹의 표시 이름은 시스템에서 생성되지만 필요한 경우 UI를 통해 사용자 정의할 수도 있습니다. 다음을 읽으십시오. [표시 이름 전환 설명서](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) 자세히 알아보십시오. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 스키마 | [[!UICONTROL Adobe Target 분류 필드]](https://github.com/adobe/xdm/pull/1719/files) | Target 활동 및 경험을 분류하기 위한 메타 데이터 필드 세트가 포함된 Target 분류 데이터 세트에 대한 새 XDM 스키마. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL Adobe 통합 프로필 서비스 계정 공용 구조체 확장]](https://github.com/adobe/xdm/pull/1696/files) | 사용자가 계정 통합에 세그먼트 멤버십을 추가할 수 있도록 해주는 실시간 고객 프로필에 대한 계정 확장 필드 그룹을 추가했습니다. |
| 스키마 | [[!UICONTROL 계산된 속성 시스템 스키마]](https://github.com/adobe/xdm/pull/1696/files) | 실시간 고객 프로필에서 사용하는 계산된 속성 필드 그룹이 시스템 읽기 전용 글로벌 스키마로 업데이트되었습니다. |
| 필드 그룹 | 복수 | 의 필드로 여러 이벤트가 추가되었습니다. [[!UICONTROL 시계열 스키마]](https://github.com/adobe/xdm/pull/1718/files). |
| 필드 그룹 | 프로필 충성도 세부 정보 | [제목을 수정함](https://github.com/adobe/xdm/pull/1717/files) 대상 `xdm:upgradeDate` 을 &quot;프로그램 이름&quot;에서 &quot;업그레이드 날짜&quot;로 바꿉니다. |
| 필드 그룹 | 복수 | 의 여러 필드 [[!UICONTROL 결정 항목]](https://github.com/adobe/xdm/pull/1714/files) 이중 중첩 계층을 제거하도록 업데이트되었습니다. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## Real-Time Customer Data Platform

Experience Platform, Real-time Customer Data Platform([!DNL Real-Time CDP])는 기업이 알려진 데이터와 알 수 없는 데이터를 통합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정으로 고객 프로필을 활성화하는 데 도움이 됩니다. [!DNL Real-Time CDP] 여러 엔터프라이즈 데이터 소스를 결합하여 고객 프로필을 실시간으로 만듭니다. 그런 다음 모든 채널 및 디바이스에서 일대일 개인화된 고객 경험을 제공하기 위해 이러한 프로필에서 빌드된 세그먼트를 다운스트림 대상으로 전송할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 Real-Time CDP 홈 페이지 | 다음 [Real-Time CDP 홈 페이지](https://experience.adobe.com) 새로운 모양과 향상된 성능으로 향상되었습니다. 홈 페이지는 이제 권한을 인식하며 액세스 권한이 있는 기능과 관련된 위젯을 제공합니다. 자세한 내용은 [Real-Time CDP 홈페이지 대시보드 개요](../../rtcdp/home-page-dashboards.md). |
| 자기 식별 조사 | 자기인식조사는 Adobe Experience Platform UI 홈 페이지에 제시된 짧은 설문 문항이다. 자체 식별 설문 조사를 사용하여 Experience Platform 개인 프로필을 작성하고 선택한 항목에 따라 맞춤 지침을 받을 수 있습니다. 자세한 내용은 [자기 식별 설문 조사 개요](../../landing/self-identification.md). |

에 대한 자세한 내용 [!DNL Real-Time CDP], 다음을 참조하십시오. [[!DNL Real-Time CDP] 개요](../../rtcdp/overview.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 익명 프로필 데이터 만료 | 익명 프로필 데이터 만료는 이제 일반적으로 사용할 수 있습니다! 이 릴리스가 활성화되면 Experience Platform 인스턴스에서 오래된 익명 프로필이 계속 제거됩니다. 이 기능과 익명 프로필에 대해 자세히 알아보려면 [익명 프로필 데이터 만료 안내서](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 멤버십 맵 | 2023년 5월 15일 이전 발표에 대한 후속 조치입니다. `Existing` 상태는 세그먼트 멤버십 라이프사이클에서 중복을 제거하기 위해 세그먼트 멤버십 맵에서 더 이상 사용되지 않습니다. 이 변경 후에는 세그먼트에서 적격한 프로필이 다음과 같이 표시됩니다. `Realized` 및 부적격 프로필은 계속 다음과 같이 표시됩니다. `Exited`.<br/><br/> 이 변경 사항은 다음을 사용하는 경우에 영향을 줄 수 있습니다. [enterprise 대상](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) 및 를 기반으로 자동화된 다운스트림 프로세스가 제자리에 있을 수 있음 `Existing` 상태. 이러한 경우 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 자격을 얻은 프로필을 식별하는 데 관심이 있다면 다음을 조합하여 사용하는 것을 고려해 보십시오. `Realized` 상태 및 `lastQualificationTime` 세그먼트 멤버십 맵에서 을 참조하십시오. 자세한 내용은 Adobe 담당자에게 문의하십시오. |

{style="table-layout:auto"}

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud의 행 수준 데이터 필터링을 위한 API 지원 | 논리 및 비교 연산자를 사용하여 Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud 소스에 대한 행 수준 데이터를 필터링합니다. 의 안내서 읽기 [api를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md) 추가 정보. |
| Shopify 스트리밍의 Beta 가용성 | 다음 [Shopify 스트리밍 소스](../../sources/connectors/ecommerce/shopify-streaming.md) 는 현재 Beta에서 사용할 수 있습니다. Shopify 스트리밍 소스를 사용하여 Shopify 파트너 계정의 데이터를 Experience Platform으로 스트리밍합니다. |
| OneTrust 통합의 일반 가용성 | 다음 [OneTrust 통합 소스](../../sources/connectors/consent-and-preferences/onetrust.md) 은(는) 현재 GA입니다. OneTrust 통합 소스를 사용하여 OneTrust 통합 계정의 동의 및 환경 설정 데이터를 Experience Platform으로 가져옵니다. |
| oracle 서비스 클라우드의 일반 공급 | 다음 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md) 은(는) 현재 GA입니다. oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 데이터를 Experience Platform으로 가져옵니다. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).