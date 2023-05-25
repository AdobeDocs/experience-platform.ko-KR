---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform의 2023년 5월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fea5fdf4b4982b59fb1c4954b8f81e131af9955b
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

>[!IMPORTANT]
>
>Audience Portal 기능이 일반적으로 사용할 수 있게 될 것을 대비하여 Adobe Experience Platform은 시스템 및 설명서 내에서 &quot;대상&quot; 및 &quot;세그먼트&quot;의 사용을 업데이트하고 있습니다.
>
>- **대상자**: 사람, 계정, 가계 또는 일반적인 특성과 행동을 공유하는 기타 엔티티의 집합입니다.
>
>- **세그먼트 정의**: Adobe Experience Platform에서 타겟 대상의 주요 특성 또는 동작을 설명하는 데 사용되는 규칙입니다. 이 용어는 이전에 &quot;세그먼트&quot;라고도 했습니다.
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

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| **[[!UICONTROL Mailchimp 관심 범주]](../../destinations/catalog/email-marketing/mailchimp-interest-categories.md)** | **[!UICONTROL Mailchimp]** 는 메일링 목록 및 이메일 마케팅 캠페인을 사용하여 연락처(클라이언트, 고객 또는 기타 이해 당사자)를 관리하고 연락하는 데 기업에서 사용하는 인기 있는 마케팅 자동화 플랫폼 및 이메일 마케팅 서비스입니다. 이 커넥터를 사용하여 관심 분야 및 환경 설정에 따라 연락처를 정렬할 수 있습니다. |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

| Functionality | Description |
| ----------- | ----------- |
| General availability of attribute-based personalization through the [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) and [Custom personalization](../../destinations/catalog/personalization/custom-personalization.md) destinations. | Leverage profile attributes in real-time to deliver one-to-one web and mobile personalization, via Adobe Target or other custom personalization destinations in Experience Platform. See the [dedicated documentation](../../destinations/ui/activate-edge-personalization-destinations.md) for more details. |
| Destination SDK support for grouping exported audiences based on merge policy. | When building a file-based destination with Destination SDK, you can now configure the grouping of exported audiences into one or multiple files, based on merge policy. <br><br> Additionally, you can now include the merge policy ID and merge policy name in the exported file names, by using the dedicated template macros. <br><br>See the [batch configuration documentation](../../destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md) for more details on how to use the `segmentGroupingEnabled` parameter and the new file name template macros.|

{style="table-layout:auto"}

-->

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- 사용자가 포트 매개 변수의 값을 사용자 지정할 수 없었던 (베타) SFTP 클라우드 스토리지 대상의 제한을 수정했습니다. 이제 값을 를 통해 (베타) SFTP 대상 연결을 설정할 때 편집할 수 있습니다. [API](/help/destinations/api/activate-segments-file-based-destinations.md) 또는 [UI](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information).

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

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
| 초안 모드에 대한 확장된 API 지원 | 이제 를 사용할 때 소스 워크플로우 중에 진행 상황을 일시 중지하고 저장할 수 있습니다. [!DNL Flow Service] 언제든지 API를 사용할 수 있습니다. 사용 `mode=draft` 기본, 소스 및 타겟 연결을 초안으로 저장하는 상태입니다. 모든 도면 요소는 나중에 완료를 위해 다시 방문할 수 있습니다. 의 안내서 읽기 [설정 [!DNL Flow Service] 도면 상태에 엔티티](../../sources/tutorials/api/draft.md) 추가 정보. |
| 의 일반 가용성 [!DNL Salesforce Marketing Cloud] 소스 | 다음 [[!DNL Salesforce Marketing Cloud source] 은(는) 현재 GA 상태입니다](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). 이 소스를 사용하여 [!DNL Salesforce Marketing Cloud] Experience Platform 대상 데이터. |
| [!DNL Google Ads] 인증 업데이트 | 이제 인증 시 로그인 고객 ID를 제공할 수 있습니다. [!DNL Google Ads] 소스 계정을 사용하여 특정 운영 고객으로부터 보고서 데이터를 가져올 수 있습니다. 읽기 [[!DNL Google Ads] 소스 설명서](../../sources/connectors/advertising/ads.md) 추가 정보. |
| [!DNL Google PubSub] 인증 업데이트 | 이제 다음에 대한 액세스 권한을 정의할 수 있습니다. [!DNL Google PubSub] 소스(새 계정을 만들 때). 프로젝트 기반 인증을 사용하여 루트 수준 액세스를 허용하거나 주제 및 구독 기반 인증을 사용하여 특정 주제 및 구독 스트림에 대한 액세스를 제한합니다. 읽기 [[!DNL Google PubSub] 소스 설명서](../../sources/connectors/cloud-storage/google-pubsub.md) 추가 정보. |
| 에 대한 새 페이지 매김 필드 매개 변수 `type=PAGE` 셀프서비스 소스(일괄 SDK)에서 | 이제 다음을 사용할 수 있습니다. `initialPageIndex` 및 `endPageIndex` 소스를 와 통합할 때 `type=PAGE` 배치 SDK를 통해 다음을 수행합니다. <ul><li>`initialPageIndex`: 이 매개 변수를 사용하면 페이지 매김이 시작되는 페이지 번호를 정의할 수 있습니다. </li><li>`endPageIndex`: 이 매개 변수를 사용하면 종료 조건을 설정하고 페이지 매김을 중지할 수 있습니다.</li></ul> 이러한 새 매개 변수에 대한 자세한 내용은 [셀프서비스 소스 일괄 처리 SDK 설명서](../../sources/sources-sdk/config/sourcespec.md#page). |
| 초안 모드에 대한 UI 지원 | 이제 사용자 인터페이스를 통해 소스 워크플로우 중에 진행 상황을 일시 중지하고 저장할 수 있습니다. 다음을 선택할 수 있습니다. **[!UICONTROL 초안으로 저장]** 워크플로우의 데이터 흐름 세부 사항, 매핑 및 예약 단계 중에 데이터 흐름을 나중에 완료할 수 있도록 초안으로 저장합니다. 의 안내서 읽기 [UI에서 데이터 흐름을 초안으로 저장](../../sources/tutorials/ui/draft.md) 추가 정보. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).

<!-- | API support for streaming data from a [!DNL Snowflake] database | You can now stream data from a [[!DNL Snowflake] source](../../sources/connectors/databases/snowflake.md) using the [!DNL Flow Service] API. | -->