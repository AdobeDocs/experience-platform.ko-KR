---
title: Adobe Experience Platform 릴리스 정보 2023년 4월
description: Adobe Experience Platform의 2023년 4월 릴리스 정보입니다.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 98%

---

# Adobe Experience Platform 릴리스 정보

>[!IMPORTANT]
>
>2023년 5월 15일부터 `Existing` 상태는 세그먼트 멤버십 수명 주기에서 중복을 없애기 위해 세그먼트 멤버십 맵에서 더 이상 사용되지 않습니다. 이러한 변경 후에 세그먼트에 적격한 프로필은 `Realized`로 표시되고 부적격 프로필은 계속 `Exited`로 표시됩니다. 이 변경 사항에 대한 자세한 내용은 [Segmentation Service 섹션](#segmentation)을 참조하십시오.

**릴리스 일자: 2023년 4월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 준비](#data-prep)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [실시간 고객 프로필](#profile)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 위젯 인사이트에서 **내역 데이터를 필터링**&#x200B;하고 최근 데이터 또는 사용자 정의 분석 기간을 사용할 수 있습니다. 자세한 내용은 [사용자 정의 대시보드 안내서](../../dashboards/user-defined-dashboards.md#filter-historical-data)를 참조하십시오.<br>이제 **기존 위젯을 복제**&#x200B;할 수도 있습니다. 복제본을 사용자 정의하고 해당 속성을 편집하면 고유한 새 위젯을 만들 때 처음부터 다시 시작하지 않아도 됩니다. 자세한 내용은 [위젯 복제 안내서](../../dashboards/user-defined-dashboards.md#duplicate-a-widget)를 참조하십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 비프로덕션 샌드박스에서 Adobe Analytics의 채우기 기간 업데이트 | 비프로덕션 샌드박스에서 Adobe Analytics의 채우기 기간이 3개월로 단축되었습니다. 프로덕션 샌드박스의 채우기는 13개월로 동일하게 유지됩니다. 이 변경 사항은 새 흐름에만 적용되며 기존 흐름에는 영향을 미치지 않습니다. 자세한 내용은 [Adobe Analytics 개요](../../sources/connectors/adobe-applications/analytics.md)를 참조하십시오. |
| FPID 문자열을 ECID로 전환하는 새로운 매퍼 함수 | FPID 문자열을 ECID로 전환하여 Experience Platform 및 Experience Cloud 애플리케이션에서 `fpid_to_ecid` 함수를 사용할 수 있습니다. 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md)를 참조하십시오. |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터스트림에 대한 IP 주소 난독화 | 이제 [데이터스트림 구성 UI](../../datastreams/configure.md)에서 부분 또는 전체의 데이터스트림 수준 IP 난독화 옵션을 정의할 수 있습니다. <br><br>데이터스트림 수준의 IP 난독화 설정은 Adobe Target 및 Audience Manager에서 구성된 모든 IP 난독화보다 우선합니다. <br><br>Adobe Analytics로 전송된 데이터는 데이터스트림 수준의 [!UICONTROL IP 난독화] 설정의 영향을 받지 않습니다. Adobe Analytics는 현재 난독화되지 않은 IP 주소를 수신합니다. Analytics가 난독화된 IP 주소를 수신하려면 Adobe Analytics에서 별도로 IP 난독화를 구성해야 합니다. 이 동작은 향후 릴리스에서 업데이트될 예정입니다.<br><br> IP 난독화 및 구성 방법에 대한 자세한 내용은 [데이터스트림 구성 설명서](../../datastreams/configure.md#advanced-options)를 참조하십시오. |
| [데이터스트림 구성 재정의](../../datastreams/overrides.md) | 이제 이벤트 데이터 세트, Target 속성 토큰, ID 동기화 컨테이너 및 Analytics 보고서 세트와 같은 특정 설정을 재정의하는 데 사용할 수 있는 데이터스트림에 대한 추가 구성 옵션을 정의할 수 있습니다. <br><br>데이터스트림 구성 재정의는 2단계 프로세스입니다. <ol><li>먼저 [데이터스트림 구성 페이지](../../datastreams/configure.md)에서 데이터스트림 구성 재정의를 정의해야 합니다.</li><li>그런 다음 Web SDK 명령 또는 Web SDK [태그 확장 기능](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)을 사용하여 Edge Network에 해당 재정의를 보내야 합니다.</li></ol> |
| OAuth JWT Secret | 고객은 [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)을 사용하여 Adobe 및 Google Service 토큰으로 이벤트 전달에서 서버 간 상호 작용을 지원할 수 있습니다. |
| [!DNL Pinterest Conversions API] 확장 기능 | [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 이벤트 전달 확장 기능을 사용하면 Adobe Experience Platform Edge Network에서 캡처된 데이터를 활용하여 [!DNL Pinterest Conversions API]을 통해 서버측 이벤트의 형태로 [!DNL Pinterest]로 전송할 수 있습니다 |

{style="table-layout:auto"}

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 연결](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Salesforce Marketing Cloud Account Engagement(이전의 Pardot) 대상을 사용하여 잠재 고객을 캡처 및 추적하고 점수 및 등급을 매깁니다. 더 긴 판매 및 의사 결정 주기가 필요한 여러 부서 및 의사 결정권자와 관련된 B2B 사용 사례에 이 대상을 사용합니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| [!DNL Custom Personalization] 및 [!DNL Adobe Commerce]대상에 대한 데이터 흐름 모니터링 | <p> 이제 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [사용자 정의 개인 설정](../../destinations/catalog/personalization/custom-personalization.md) 및 [속성을 사용한 사용자 정의 개인 설정](../../destinations/catalog/personalization/custom-personalization.md) 연결에 대한 활성화 지표를 확인할 수 있습니다. </p> <p>![Adobe Commerce 이미지](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce 지표"){width="100" zoomable="yes"}</p>  자세한 내용은 [대상 작업 영역의 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace)을 참조하십시오. |
| [!DNL Google Ad Manager] 및 [!DNL Google Ad Manager 360] 대상에 대한 새로운 **[!UICONTROL 세그먼트 이름에 세그먼트 ID 추가]** 필드 | <p>이제 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 및 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details)의 세그먼트 이름에 Experience Platform의 세그먼트 ID가 포함되도록 할 수 있습니다(`Segment Name (Segment ID)`).</p><p>![세그먼트 ID 이미지 추가](/help/destinations/assets/common/append-segment-id-to-segment-name.png "세그먼트 이름 필드에 세그먼트 ID 새로 추가 "){width="100" zoomable="yes"}</p> |
| 예약된 대상자 채우기 | <p>[[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 대상의 경우 대상에 대한 대상자 채우기 활성화는 세그먼트가 대상 연결에 처음 매핑된 후 24 ~ 48시간 후에 진행되도록 예약됩니다. 이 업데이트는 데이터를 수집할 때까지 24시간 대기하는 Google의 정책에 따른 것으로, Real-Time CDP과 간의 일치율을 개선합니다 [!DNL Google Display & Video 360].</p> <p>이는 이 대상에만 적용할 수 있는 백엔드 구성이며, UI에서 고객이 구성할 수 있는 일정 옵션과는 관련이 없습니다.</p> |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- 파일 기반의 대상 내보내기에 대한 **제외된 ID** 보고 지표의 문제를 해결했습니다. 고객은 예상대로 활성화된 내보내기에서 내보낸 모든 ID를 수신했습니다. 단, UI의 **제외된 ID** 보고 지표는 내보내지 않아야 할 ID 수를 잘못 계산하여 제외된 ID 수를 높게 표시했습니다. (PLAT-149774)
- 활성화 워크플로에서 **예약** 단계의 문제를 해결했습니다. 매핑 ID가 필요한 대상의 경우 고객은 기존 대상 연결에 추가된 세그먼트에 대한 매핑 ID를 추가할 수 없었습니다. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 표시 이름 전환 | 이제 스키마 편집기는 원래 필드 이름과 사람이 읽을 수 있는 표시 이름 간에 변경할 수 있는 전환 기능을 제공합니다.<br>![표시 이름 전환 기능이 강조 표시된 스키마 편집기.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "스키마 편집기 표시 이름 전환"){width="100" zoomable="yes"}<br>이러한 유연성을 통해 필드 검색 및 스키마 편집 기능이 향상됩니다. 표준 필드 그룹의 표시 이름은 시스템에서 생성되지만, 필요한 경우 UI를 통해 사용자 정의할 수도 있습니다. 자세한 내용은 [표시 이름 전환 설명서](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle)를 참조하십시오. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 스키마 | [[!UICONTROL Adobe Target 분류 필드]](https://github.com/adobe/xdm/pull/1719/files) | Target 활동 및 경험을 분류하기 위한 메타 데이터 필드 세트를 포함하는 Target 분류 데이터 세트에 대한 새로운 XDM 스키마. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL Adobe 통합 프로필 서비스 계정 합집합 확장 기능]](https://github.com/adobe/xdm/pull/1696/files) | 사용자가 계정 합집합에 세그먼트 멤버십을 추가할 수 있는 실시간 고객 프로필용 계정 확장 필드 그룹을 추가했습니다. |
| 스키마 | [[!UICONTROL 계산된 속성 시스템 스키마]](https://github.com/adobe/xdm/pull/1696/files) | 실시간 고객 프로필에서 사용하는 계산된 속성 필드 그룹이 시스템 읽기 전용 전역 스키마로 업데이트되었습니다. |
| 필드 그룹 | 다수 | 여러 이벤트를 [[!UICONTROL 시계열 스키마]](https://github.com/adobe/xdm/pull/1718/files) 필드로 추가했습니다. |
| 필드 그룹 | 프로필 충성도 세부 사항 | [`xdm:upgradeDate`의 제목](https://github.com/adobe/xdm/pull/1717/files)을 “프로그램 이름”에서 “업그레이드 날짜”로 수정했습니다. |
| 필드 그룹 | 다수 | 중첩된 이중 계층 구조를 제거하기 위해 [[!UICONTROL 의사 결정 항목]](https://github.com/adobe/xdm/pull/1714/files)의 여러 필드가 업데이트되었습니다. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 살펴보십시오.

## Real-Time Customer Data Platform

Experience Platform을 기반으로 구축된 Real-Time Customer Data Platform([!DNL Real-Time CDP])으로 기업은 알려진 데이터와 알 수 없는 데이터를 수집하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로필을 활성화할 수 있습니다. [!DNL Real-Time CDP]는 여러 기업의 데이터 소스를 결합하여 실시간으로 고객 프로필을 생성합니다. 이러한 프로필에서 구축된 세그먼트는 다운스트림 대상으로 전송되어 모든 채널과 디바이스에서 일대일로 개인 설정된 고객 경험을 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 Real-Time CDP 홈 페이지 | [Real-Time CDP 홈 페이지는](https://experience.adobe.com)의 외관이 새로워지고 성능이 향상되었습니다. 이제 홈 페이지는 권한을 인식하고 액세스 권한이 있는 기능과 관련된 위젯을 표시합니다. 자세한 내용은 [Real-Time CDP 홈 페이지 대시보드 개요](../../rtcdp/home-page-dashboards.md)를 참조하십시오. |
| 자가 식별 설문 조사 | 자가 식별 설문 조사는 Adobe Experience Platform UI 홈 페이지에 표시되는 짧은 설문지입니다. 자가 식별 설문 조사를 사용하여 Experience Platform 개인 프로필을 작성하고 선택 사항에 따라 맞춤형 지침을 받으십시오. 자세한 내용은 [자가 식별 설문 조사 개요](../../landing/self-identification.md)를 참조하십시오. |

[!DNL Real-Time CDP]에 대한 자세한 내용은 [[!DNL Real-Time CDP] 개요](../../rtcdp/overview.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 익명 프로필 데이터 만료 | 이제 익명 프로필 데이터 만료는 일반적으로 사용할 수 있습니다! 일단 활성화되면 이 릴리스는 Experience Platform 인스턴스에서 오래된 익명 프로필을 지속적으로 제거합니다. 이 기능과 익명 프로필에 대한 자세한 내용은 [익명 프로필 데이터 만료 안내서](../../profile/pseudonymous-profiles.md)를 참조하십시오. |

{style="table-layout:auto"}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 멤버십 맵 | 이전 발표(2월)에 대한 후속 조치로 2023년 5월 15일에 세그먼트 멤버십 수명 주기의 중복을 없애기 위해 `Existing` 상태는 세그먼트 구성원 맵에서 더 이상 사용되지 않습니다. 이러한 변경 후에 세그먼트에 적격한 프로필은 `Realized`로 표시되고 부적격 프로필은 계속 `Exited`로 표시됩니다.<br/><br/> [기업 대상](../../destinations/destination-types.md#streaming-profile-export)(Amazon Kinesis, Azure Event Hubs, HTTP API)을 사용하고 있으며 `Existing` 상태에 따라 자동화된 다운스트림 프로세스가 있을 경우 이러한 변경 사항은 영향을 미칠 수 있습니다. 이 경우에 해당하면 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 인증된 프로필을 확인하려는 경우 세그먼트 멤버십 맵에서 `Realized` 상태 및 `lastQualificationTime`을 조합하여 사용하도록 하십시오. 자세한 내용은 Adobe 담당자에게 문의하십시오. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 라벨링하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Salesforce CRM 소스에 대한 행 수준의 데이터 필터링을 위한 API 지원. | 논리 및 비교 연산자를 사용하여 Salesforce CRM 소스의 행 수준 데이터를 필터링합니다. 자세한 내용은 [API를 사용하여 소스의 데이터를 필터링](../../sources/tutorials/api/filter.md)하는 방법에 관한 안내서를 참조하십시오. |
| Shopify Streaming의 Beta 가용성 | 현재 [Shopify Streaming 소스](../../sources/connectors/ecommerce/shopify-streaming.md)는 베타 버전으로 제공됩니다. Shopify Streaming 소스를 사용하여 Shopify 파트너 계정에서 Experience Platform으로 데이터를 스트리밍합니다. |
| OneTrust 통합의 일반 가용성 | 현재 [OneTrust 통합 소스](../../sources/connectors/consent-and-preferences/onetrust.md)는 GA 버전입니다. OneTrust 통합 소스를 사용하여 OneTrust 통합 계정에서 Experience Platform으로 동의 및 환경 설정 데이터를 가져옵니다. |
| Oracle 서비스 클라우드의 일반 가용성 | 현재 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md)는 GA 버전입니다. Oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 데이터를 Experience Platform으로 가져옵니다. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.
