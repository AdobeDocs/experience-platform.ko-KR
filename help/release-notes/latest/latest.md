---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 93ac391370ddd1fe596b8515bd520fb870a10a3c
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 7월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [XDM(경험 데이터 모델)](#xdm)

<!-- - [Real-time Customer Data Platform B2B Edition](#b2b) -->
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 여러 기능을 제공합니다 [!DNL dashboards] 을 통해 일일 스냅샷 동안 캡처된 조직 데이터에 대한 중요한 정보를 볼 수 있습니다.

### 계정 프로필 대시보드

계정 프로필 대시보드는 마케팅 채널 전반에서 여러 소스의 통합 계정 정보와 조직에서 현재 고객 계정 정보를 저장하는 데 사용하는 다양한 시스템의 스냅숏을 표시합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 업계 위젯별 총 계정 | 이 위젯은 단일 지표에 있는 총 계정 수를 표시하며 도넛 차트를 사용하여 전체 개수를 구성하는 산업에 대한 비례 크기의 개수를 나타냅니다. |
| 계정 프로필이 추가된 위젯 | 이 위젯에서는 지정된 기간 동안 계정에 추가된 프로필의 수와 이러한 추가된 프로필을 구성하는 다양한 산업의 비율을 나타내는 색상 코딩된 막대 차트를 사용합니다. |

{style=&quot;table-layout:auto&quot;}

자세한 내용은 [실시간 CDP, B2B Edition 개요](../../rtcdp/b2b-overview.md) 사용 가능한 B2B 기능에 대해 자세히 알아보려면 [엔드 투 엔드 자습서](../../rtcdp/b2b-tutorial.md) B2B 워크플로우의 일부로 계정 프로필을 만드는 방법에 대해 자세히 알아보십시오.

계정 프로필 관련 지표를 시각화하는 데 사용할 수 있는 위젯에 대한 자세한 내용은 [계정 프로필 위젯 설명서](../../dashboards/guides/account-profiles.md#standard-widgets).

### 프로필 대시보드

프로필 대시보드는 Experience Platform의 프로필 저장소 내에 조직에 있는 속성(레코드) 데이터의 스냅숏을 표시합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 매핑된 대상 위젯 | 이 위젯은 프로필 대시보드 드롭다운에서 선택한 대상에 활성화할 수 있는 매핑된 대상의 총 수를 표시합니다. |

프로필 대시보드에 대한 자세한 내용은 [프로필 대시보드 개요](../../dashboards/guides/profiles.md).

### 대상 대시보드

대상 대시보드는 Experience Platform 내에서 조직에서 활성화한 대상의 스냅숏을 표시합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 위젯 | 이 위젯은 프로필 데이터에 적용된 선택한 병합 정책에 따라 활성화될 준비가 된 총 세그먼트 수를 제공합니다. |

{style=&quot;table-layout:auto&quot;}

대상 대시보드에 대한 자세한 내용은 [대상 대시보드 개요](../../dashboards/guides/destinations.md).

## 데이터 수집 {#collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Admin Console을 통한 권한 관리 | 데이터 수집 기능에 대한 액세스는 이제 Adobe Experience Platform 데이터 수집에 대한 카드에서 Adobe Admin Console을 통해 관리됩니다. 다음 안내서를 참조하십시오. [데이터 수집 권한](../../collection/permissions.md) 추가 정보.<br><br>이제 데이터 세트에 대한 권한도 Adobe Experience Platform용 카드의 Admin Console을 통해 관리되므로 각 사용자에 대해 이러한 권한을 수동으로 설정하는 이전 방법에 대한 보안을 강화할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 개선 사항 [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations은 이제 더 똑똑하고 더 빠릅니다. 새 유효성 검사 기능을 통해 가장 일반적인 매핑 오류가 크게 감소하여 시간-값 차이가 줄어듭니다. |
| 스트리밍 이변을 위한 계층적 지원 | 이제 함수를 사용할 수 있습니다 `upsert_array_append` 및 `upsert_array_replace` 를 업데이트하여 프로필에 스트리밍할 때 배열 및 개체를 업데이트합니다. 자세한 내용은 [[!DNL Data Prep] 매핑 함수 안내서](../../data-prep/functions.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

에 대해 자세히 알아보려면 [!DNL Data Prep]를 참조하고 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| [지금 파일 내보내기(베타)](../../destinations/ui/export-file-now.md) | 이전에 예약된 세그먼트의 현재 내보내기 일정을 중단하지 않고 전체 파일을 내보냅니다. 이 내보내기는 이전에 예약한 내보내기 외에 추가로 발생하며 세그먼트의 내보내기 빈도를 변경하지 않습니다. <br> 파일 내보내기는 즉시 트리거되며 Experience Platform 세그먼테이션 실행의 최신 결과를 선택합니다. <br> <br>이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오. |

{style=&quot;table-layout:auto&quot;}

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(베타) [!DNL Trade Desk] - CRM 연결](../../destinations/catalog/advertising/tradedesk-emails.md) | 사용 [!DNL The Trade Desk] 프로필을 활성화할 CRM 대상 [!DNL Trade Desk] crm 데이터를 기반으로 하여 대상 타깃팅 및 제외를 처리합니다. <br><br>이 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다. |
| [(베타) [!DNL Snap Inc.]](../../destinations/catalog/advertising/snap-inc.md) | 이 대상을 통해 마케터는 Experience Platform에서 만든 사용자 세그먼트를 Snapchat Ads로 가져와서 이를 사용하여 광고를 타깃팅할 수 있습니다. <br><br>이 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 의료 업계 데이터 모델 | 디지털 획득 증가, 프로그램 등록 개선 및 의약품 정보 홍보와 관련된 5가지 일반적인 업계 활용 사례를 지원하기 위해 표준 의료 데이터 모델이 도입되었습니다. 의 개요를 참조하십시오. [의료 데이터 모델](../../xdm/schema/industries/healthcare.md) 를 참조하십시오.<br><br>새 업계 필터가 [!UICONTROL 스키마] 사용자 지정 스키마를 구축할 때 보건의료와 관련된 구성 요소를 탐색하는 데 도움이 되는 UI입니다. |

{style=&quot;table-layout:auto&quot;}

**새로운 XDM 구성 요소**

>[!WARNING]
>
>아래 표에 나열된 새 XDM 구성 요소는 실험적이고 현재 테스트 중입니다. 이러한 구성 요소는 안정화되기 전에 변경 내용(필요한 경우)으로 업데이트해야 합니다. 그에 따라 개발 노력을 계획하십시오.

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 날씨]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | 날씨 데이터를 캡처하는 데 사용되는 레코드 기반 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 현재 날씨]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 우편 번호에 대한 현재 날씨 조건을 캡처하는 데 사용되는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 예측 날씨]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 우편 번호에 대한 예측 기상 상태를 캡처하는 데 사용되는 분류 |
| 필드 그룹 | [[!UICONTROL 제품 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 소비자 행동을 유도하는 알려진 날씨 조건을 활용하는 제품별 트리거를 캡처하는 데 사용되는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 상대 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 소비자 행동을 유도하는 알려진 날씨 조건을 활용하는 상대적 트리거를 캡처하는 데 사용되는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 심각한 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 소비자 행동을 유도하는 것으로 알려진 심각한 날씨 조건을 활용하는 트리거를 캡처하는 데 사용되는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 날씨 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/weather-triggers.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 및 [!UICONTROL 날씨] 소비자 행동을 유도하는 알려진 날씨 조건을 활용하는 일반적인 트리거를 캡처하는 데 사용되는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL MediaCollection 상호 작용 세부 사항]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-collection.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 미디어 상호 작용에 대한 세부 사항을 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL MediaReporting 상호 작용 세부 사항]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-reporting.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 미디어 보고와의 상호 작용에 대한 세부 사항을 캡처하는 클래스입니다. |
| 데이터 유형 | [[!UICONTROL 광고 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 광고 자산에 대한 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 광고 Pod 세부 정보 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json) | 단일 광고 브레이크 내에서 재생되는 여러 광고의 시퀀스인 광고 Pod에 대한 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 장 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) | 비디오 컨텐츠에서 장 또는 세그먼트에 대한 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 오류 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 비디오 재생 오류에 대한 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 플레이어 이벤트 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/playereventdetails.schema.json) | 플레이헤드 위치 및 세션 ID를 포함하여 비디오 플레이어에 대한 이벤트 관련 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 플레이어 상태 데이터 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) | 비디오 플레이어에 대한 상태 관련 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 비디오 재생 이벤트에 대한 QoE(체감 품질) 세부 사항을 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 비디오 재생 이벤트에 대한 세션 세부 사항을 캡처합니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

<!-- ## Real-time Customer Data Platform B2B Edition {#b2b}

Built on Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition is purpose-built for marketers operating in a business-to-business service model. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

| Feature | Description |
| Lead to account matching | Lead to account matching allows you to use Real-time CDP B2B edition to match known person profiles to account profiles so that these profiles can be segmented and targeted with B2B context data like account, opportunity (and add something else like don't use etc. to the description). For more information, see the document on [lead to account matching](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md). For a guide on how to monitor profile enrichment, see the document on [monitoring profile enrichment in the UI](../../dataflows/ui/b2b/monitor-profile-enrichment.md). For instructions on how to use related accounts in segment definitions, see the guide on [Segmentation use cases for Real-time Customer Data Platform B2B Edition](../../rtcdp/segmentation/b2b.md#related-accounts)."|

{style="table-layout:auto"}

To learn more about Real-time CDP B2B Edition, see the [Real-time CDP B2B overview](../../rtcdp/overview.md). -->

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 분리된 프로필 에지 특성 정리(제한된 릴리스) | 조직에서 이 기능에 액세스할 수 있는 경우 프로필 서비스는 이제 남은 사용자 활동 영역의 에지 속성을 매일 제거하여 시스템에서 프로필을 보다 정확하게 표현합니다. 이 정리는 주어진 프로필에 대한 모든 프로필 조각이 삭제된 후 발생하며 이 프로필은 `com_adobe_aep_profile_region_dataset` 이 true로 표시됩니다. 이 지표들은 이번 릴리스 전에 남은 에지 특성 조각을 포함했으므로 라이선스 사용 대시보드의 &quot;주소 지정 가능 대상&quot; 지표에 감소가 표시될 수 있으며, 프로필 대시보드의 &quot;프로필 수&quot; 지표에 이 릴리스 전의 남은 에지 특성 조각이 포함되어 있을 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

프로필 데이터 작업에 대한 자습서 및 모범 사례 등 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 의 일반 공급 [!DNL Azure Data Explorer] 소스 | Azure Data Explorer 소스를 사용하여 [!DNL Azure] 인스턴스를 Experience Platform에 추가합니다. 자세한 내용은 [[!DNL Azure Data Explorer] 소스 개요](../../sources/connectors/databases/data-explorer.md) 추가 정보. |
| 의 일반 공급 [!DNL Generic OData] 소스 | 를 사용하십시오 [!DNL Generic OData] 오픈 데이터 프로토콜을 지원하는 시스템에서 Experience Platform으로 리소스를 가져오는 소스. 자세한 내용은 [[!DNL Generic OData] 소스 개요](../../sources/connectors/protocols/odata.md) 추가 정보. |
| 에 대한 소스 파일 속성의 자동 검색 지원 [!DNL Data Landing Zone] Experience Platform UI | 다음 [!DNL Data Landing Zone] 이제 소스가 Experience Platform UI를 사용할 때 파일 속성 자동 검색을 지원합니다. 다음 문서를 참조하십시오. [만들기 [!DNL Data Landing Zone] 소스 연결](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
