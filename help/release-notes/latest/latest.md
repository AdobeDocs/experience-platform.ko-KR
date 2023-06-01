---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform의 2023년 5월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 09d8014eea2d31649eed3814ad07172027b2c435
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

>[!IMPORTANT]
>
>대상자 포털 기능의 정식 출시를 대비하여 Adobe Experience Platform 시스템과 설명서에서 “대상자”와 “세그먼트”라는 단어의 사용 방식을 업데이트합니다.
>
>- **대상자**: 사람, 계정, 가계 또는 일반적인 특성과 행동을 공유하는 기타 엔티티의 집합입니다.
>
>- **세그먼트 정의**: Adobe Experience Platform에서 타겟 대상의 주요 특성 또는 동작을 설명하는 데 사용되는 규칙입니다. 전에는 이 용어를 그냥 “세그먼트”라고만 지칭했습니다.
>
>- **세그먼트**: 프로필을 대상자로 분리하는 작업입니다. &quot;세그먼트&quot;라는 용어는 이제 동사로만 사용됩니다.
>
>- **세분화**: 대상과 같은 결과 세트를 생성하기 위해 함께 그룹화할 프로필의 특성을 식별하고 아티큘레이션하는 작업입니다.
>
>그 결과, Adobe Experience Platform UI 내에는 이러한 새로운 대상 생성 및 관리 경로를 반영하기 위해 &quot;세그먼트&quot;가 &quot;대상&quot;으로 대체되는 것이 표시됩니다.

**릴리스 날짜: 2023년 5월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [데이터 거버넌스](#data-governance)
- [데이터 수집](#data-ingestion)
- [대상](#destinations)
- [경험 데이터 모델(XDM)](#xdm)
- [ID 서비스](#identity-service)
- [쿼리 서비스](#query-service)
- [소스](#sources)


## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Twitter] 전환 API 확장 | 다음 [[!DNL Twitter] 전환 API](../../tags/extensions/server/twitter/overview.md) 이벤트 전달 확장을 사용하면 를 사용하여 이벤트 변환을 위해 이벤트 데이터를 서버측에 실시간으로 전달할 수 있습니다. [!DNL Twitter] 전환 API입니다. |
| 데이터 요소 경로 지원 | 내에서 데이터 요소의 경로 확인 [코어 확장](../../tags/extensions/client/core/overview.md) 이전보다 훨씬 쉬워졌습니다. 이 개선 사항은 올바른 데이터 요소 경로를 선택하고 서식을 지정하는 데 도움이 되는 안내식 양식을 제공합니다. |

{style="table-layout:auto"}

데이터 수집에 대해 자세히 알아보려면 [데이터 컬렉션 개요](../../tags/home.md).

## 데이터 거버넌스 {#data-governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 카탈로그 작성, 데이터 계보, 데이터 사용 레이블 지정, 데이터 액세스 정책, 마케팅 작업을 위한 데이터에 대한 액세스 제어 등 다양한 수준에서 Experience Platform 내에서 중요한 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 필드 수준 레이블 지정 중단 | 개별 필드에 레이블을 적용하는 기능이 데이터 세트에서 스키마로 이동되었습니다. 이를 통해 데이터 거버넌스, 동의 및 액세스 제어를 위해 필드 레이블을 업스트림 관리할 수 있습니다. 이전에 적용된 데이터 세트 필드 레이블은 Experience Platform UI를 통해 일시적으로 지원됩니다. 2024년 5월 31일까지 기존 데이터 세트 필드 레이블을 스키마 필드 레이블로 수동으로 마이그레이션해야 합니다. 다음을 읽으십시오. [데이터 거버넌스 전체 안내서](../../data-governance/e2e.md) 레이블 마이그레이션에 대한 자세한 내용을 보려면 여기를 클릭하십시오. |

{style="table-layout:auto"}

데이터 거버넌스에 대해 자세히 알아보려면 [데이터 거버넌스 개요](../../data-governance/home.md).

## 데이터 수집 {#data-ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 수집할 수 있는 다양한 기능 세트를 제공합니다. Adobe이 빌드한 소스, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 사용하여 일괄 처리 또는 스트리밍 API를 사용하여 수집할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 수집 템플릿의 Beta 가용성 | 데이터 수집 템플릿은 데이터 설계자 및 엔지니어에게 스키마 및 데이터 세트 생성 및 매핑 규칙 구성을 비롯한 데이터 수집 프로세스를 가속화하는 표준 템플릿 및 자동화 도구를 제공합니다. 데이터 수집 템플릿은 현재 [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md), [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 및 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 소스. 자세한 내용은 의 안내서를 참조하십시오. [UI에서 템플릿 사용](../../sources/tutorials/ui/templates.md). |

데이터 수집에 대해 자세히 알아보려면 [데이터 수집 개요](../../ingestion/home.md).

## 대상(5월 31일에 업데이트됨) {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| **[[!UICONTROL Mailchimp 관심 범주]](../../destinations/catalog/email-marketing/mailchimp-interest-categories.md)** | **[!UICONTROL Mailchimp]** 는 메일링 목록 및 이메일 마케팅 캠페인을 사용하여 연락처(클라이언트, 고객 또는 기타 이해 당사자)를 관리하고 연락하는 데 기업에서 사용하는 인기 있는 마케팅 자동화 플랫폼 및 이메일 마케팅 서비스입니다. 이 커넥터를 사용하여 관심 분야 및 환경 설정에 따라 연락처를 정렬할 수 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 다음을 통한 속성 기반 개인화의 일반 가용성 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 정의 개인화](../../destinations/catalog/personalization/custom-personalization.md) 대상. | 프로필 속성을 실시간으로 활용하여 Adobe Target 또는 Experience Platform의 다른 사용자 지정 개인화 대상을 통해 일대일 웹 및 모바일 개인화를 제공할 수 있습니다. 읽기 [전용 설명서](../../destinations/ui/activate-edge-personalization-destinations.md) 및 [FAQ](/help/destinations/destinations-faq.md#same-next-page-personalization) 을 참조하십시오. |
| 병합 정책을 기반으로 내보낸 대상을 그룹화하기 위한 Destination SDK 지원. | 이제 Destination SDK을 사용하여 파일 기반 대상을 작성할 때 병합 정책에 따라 내보낸 대상을 하나 이상의 파일로 그룹화하여 구성할 수 있습니다. <br><br> 또한 이제 전용 템플릿 매크로를 사용하여 내보낸 파일 이름에 병합 정책 ID 및 병합 정책 이름을 포함할 수 있습니다. <br><br>다음을 참조하십시오. [일괄 처리 구성 설명서](../../destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md) 을(를) 사용하는 방법에 대한 자세한 내용은 `segmentGroupingEnabled` 매개 변수와 새 파일 이름 템플릿 매크로를 사용하여 새 파일 이름을 만듭니다. |
| Beta 클라우드 스토리지 대상으로 내보내기에 매니페스트 파일 포함 | 이제 6개의 클라우드 스토리지 베타 대상으로 데이터를 내보낼 때 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 포함할 수 있습니다. [(베타) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(베타) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(베타) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(베타) 데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(베타) Google 클라우드 스토리지](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(베타) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br><br> 에서 추가 정보 가져오기 **[!UICONTROL 대상 세부 사항]** 위에 링크된 페이지 섹션. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- 사용자가 포트 매개 변수의 값을 사용자 지정할 수 없었던 (베타) SFTP 클라우드 스토리지 대상의 제한을 수정했습니다. 이제 값을 를 통해 (베타) SFTP 대상 연결을 설정할 때 편집할 수 있습니다. [API](/help/destinations/api/activate-segments-file-based-destinations.md) 또는 [UI](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information).

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | (여러 개) | 에 대한 여러 필드 [오퍼 항목](https://github.com/adobe/xdm/pull/1720/files) 스키마에서 이중 계층 구조를 제거하도록 업데이트되었습니다. |
| 필드 그룹 | [[!UICONTROL XDM 개별 잠재 고객 프로필]](https://github.com/adobe/xdm/pull/1721/files) | 다음 `partnerProspect` 메타데이터 태그 옵션이 [!UICONTROL XDM 개별 잠재 고객 프로필] 클래스. |
| 데이터 형식 | (여러 개) | 에 대한 여러 필드가 추가되었습니다. [[!UICONTROL 미디어 세부 정보]](https://github.com/adobe/xdm/pull/1716/files) 데이터 유형. |
| 데이터 형식 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/pull/1716/files) | 리디렉션이 발생했는지 여부를 나타내는 새 필드가 추가되었습니다. |
| 필드 그룹 | [[!UICONTROL MediaAnalytics 인터랙션 세부 정보]](https://github.com/adobe/xdm/pull/1716/files) | 미디어 보고와 관련된 새 필드가 추가되었습니다. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## ID 서비스 {#identity-service}

Adobe Experience Platform Identity Service는 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 제공하여 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**기능 업데이트**

| 기능 | 설명 |
| --- | --- |
| Adobe Experience Cloud 애플리케이션 내에서 파트너 ID 지원 [!BADGE 베타]{type=Informative} | 이제 Identity Service에서 파트너 ID를 사용할 수 있습니다. 파트너 ID는 데이터 파트너가 사람을 나타내는 데 사용하는 식별자입니다. Real-time Customer Data Platform에서 파트너 ID는 주로 확장된 대상 활성화 및 데이터 보강에 사용됩니다. 파트너 ID는 ID 그래프에 저장되지 않습니다. 자세한 내용은 [id 유형](../../identity-service/namespaces.md#identity-types). |

ID 서비스에 대해 자세히 알아보려면 [ID 서비스 개요](../../identity-service/home.md)

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL data lake]. 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| ADLS 데이터 세트에 대한 열 수준 통계 계산 | 다음 `ANALYZE TABLE` 명령을 확장했습니다. `COMPUTE STATISTICS` 및 `SHOW STATISTICS` 명령. 이제 ADLS 데이터 세트의 하위 집합 또는 해당 데이터 세트 내의 특정 열에 대한 통계를 계산할 수 있습니다. 자세한 내용은 [데이터 세트 통계 계산 안내서](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 에서 데이터 스트리밍을 위한 API 지원 [!DNL Snowflake] 데이터베이스 | 이제 다음에서 데이터를 스트리밍할 수 있습니다. [[!DNL Snowflake] 소스](../../sources/connectors/databases/snowflake-streaming.md) 사용 [!DNL Flow Service] API. |
| 초안 모드에 대한 확장된 API 지원 | 이제 를 사용할 때 소스 워크플로우 중에 진행 상황을 일시 중지하고 저장할 수 있습니다. [!DNL Flow Service] 언제든지 API를 사용할 수 있습니다. 사용 `mode=draft` 기본, 소스 및 타겟 연결을 초안으로 저장하는 상태입니다. 모든 도면 요소는 나중에 완료를 위해 다시 방문할 수 있습니다. 의 안내서 읽기 [설정 [!DNL Flow Service] 도면 상태에 엔티티](../../sources/tutorials/api/draft.md) 추가 정보. |
| 의 일반 가용성 [!DNL Salesforce Marketing Cloud] 소스 | 다음 [[!DNL Salesforce Marketing Cloud source] 은(는) 현재 GA 상태입니다](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). 이 소스를 사용하여 [!DNL Salesforce Marketing Cloud] Experience Platform 대상 데이터. |
| [!DNL Google Ads] 인증 업데이트 | 이제 인증 시 로그인 고객 ID를 제공할 수 있습니다. [!DNL Google Ads] 소스 계정을 사용하여 특정 운영 고객으로부터 보고서 데이터를 가져올 수 있습니다. 읽기 [[!DNL Google Ads] 소스 설명서](../../sources/connectors/advertising/ads.md) 추가 정보. |
| [!DNL Google PubSub] 인증 업데이트 | 이제 다음에 대한 액세스 권한을 정의할 수 있습니다. [!DNL Google PubSub] 소스(새 계정을 만들 때). 프로젝트 기반 인증을 사용하여 루트 수준 액세스를 허용하거나 주제 및 구독 기반 인증을 사용하여 특정 주제 및 구독 스트림에 대한 액세스를 제한합니다. 읽기 [[!DNL Google PubSub] 소스 설명서](../../sources/connectors/cloud-storage/google-pubsub.md) 추가 정보. |
| 에 대한 새 페이지 매김 필드 매개 변수 `type=PAGE` 셀프서비스 소스(일괄 SDK)에서 | 이제 다음을 사용할 수 있습니다. `initialPageIndex` 및 `endPageIndex` 소스를 와 통합할 때 `type=PAGE` 배치 SDK를 통해 다음을 수행합니다. <ul><li>`initialPageIndex`: 이 매개 변수를 사용하면 페이지 매김이 시작되는 페이지 번호를 정의할 수 있습니다. </li><li>`endPageIndex`: 이 매개 변수를 사용하면 종료 조건을 설정하고 페이지 매김을 중지할 수 있습니다.</li></ul> 이러한 새 매개 변수에 대한 자세한 내용은 [셀프서비스 소스 일괄 처리 SDK 설명서](../../sources/sources-sdk/config/sourcespec.md#page). |
| 초안 모드에 대한 UI 지원 | 이제 사용자 인터페이스를 통해 소스 워크플로우 중에 진행 상황을 일시 중지하고 저장할 수 있습니다. 다음을 선택할 수 있습니다. **[!UICONTROL 초안으로 저장]** 워크플로우의 데이터 흐름 세부 사항, 매핑 및 예약 단계 중에 데이터 흐름을 나중에 완료할 수 있도록 초안으로 저장합니다. 의 안내서 읽기 [UI에서 데이터 흐름을 초안으로 저장](../../sources/tutorials/ui/draft.md) 추가 정보. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
