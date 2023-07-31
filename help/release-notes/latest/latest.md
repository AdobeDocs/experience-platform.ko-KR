---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform의 2023년 7월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3090b8a8eade564190dc32142c3fc71701007337
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 26%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2023년 7월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [카탈로그 서비스](#catalog-service)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [쿼리 서비스](#query-service)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치와 계보를 위한 기록 시스템입니다. Experience Platform에 수집되는 모든 데이터는 파일 및 디렉터리로 데이터 레이크에 저장되지만, 카탈로그는 조회 및 모니터링을 위해 이러한 파일 및 디렉터리에 대한 메타데이터 및 설명을 포함합니다.

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 인벤토리 관리 | 이제 데이터 세트 UI는 데이터 세트를 더 잘 관리하기 위해 인라인 작업 컬렉션을 제공합니다. 고급 데이터 세트 관리를 사용하면 필터링 및 검색 기능을 향상시킬 수 있는 데이터 세트에 폴더 및 태그를 만들고 할당하여 작업 효율성을 높일 수 있습니다. 에 대한 자세한 내용은 설명서 를 참조하십시오 [인라인 작업](../../catalog/datasets/user-guide.md#inline-actions), 방법 [데이터 세트 검색 및 필터링](../../catalog/datasets/user-guide.md#search-and-filter), 및 [데이터 세트를 폴더로 이동](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 태그 및 이벤트 전달 | 데이터 수집 감사 로그 | 이제 태그 및 이벤트 전달에서 작업이 수행된 시기와 이 작업을 수행한 사용자를 볼 수 있습니다. 이를 통해 제품 문제 해결, 적절한 거버넌스 및 내부 감사 활동이 용이해집니다. 이 감사 데이터는 빠른 작업 및 리소스 상태 업데이트도 포함된 상황에 맞는 슬라이드 아웃 메뉴를 통해 표시됩니다. 이 데이터는 다음 화면의 태그 및 이벤트 전달 UI에서 볼 수 있습니다.<br><ul><li>[속성 개요](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[규칙](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[데이터 요소](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[확장](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[라이브러리 검토](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[라이브러리 마지막 빌드 및 게시](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| 데이터스트림 | [지역 조회](../../datastreams/configure.md#advanced-options) | 이제 다음과 같은 정보를 포함하도록 데이터스트림에 대한 지리적 위치 및 네트워크 조회를 구성할 수 있습니다. <ul><li>국가</li><li>우편 번호</li><li>시/도</li><li>DMA</li><li>구/군/시</li><li>위도 </li><li>경도</li><li>통신사</li><li>도메인</li><li>ISP</li></ul> 정확한 지리적 위치 정보를 포함한 개인 데이터를 수집, 처리 및 전송하기 위해 해당 법률 및 규정에 따라 필요한 모든 권한, 동의, 승인 및 인증을 획득했는지 확인할 책임이 있습니다. <br> IP 주소 난독화 선택은 IP 주소에서 파생되어 구성된 Adobe 솔루션으로 전송되는 지리적 위치 정보 수준에 영향을 주지 않습니다. 지리적 위치 조회는 별도로 제한하거나 비활성화해야 합니다. <br> 다음을 참조하십시오. [데이터스트림 설명서](../../datastreams/configure.md#advanced-options) 을 참조하십시오. |

{style="table-layout:auto"}

데이터 수집에 대한 자세한 내용은 [데이터 컬렉션 개요](../../tags/home.md).
<!-- 
## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions | You can now use the following functions when mapping objects in Data Prep: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

For more information on Data Prep, please read the [Data Prep overview](../../data-prep/home.md). -->

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 신규 또는 업데이트됨 | 설명 |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | 신규 | Adobe Experience Platform에서 로 ID 온보드 [!DNL LiveRamp Connect] 를 사용하면 모바일, 오픈 웹, 소셜 및 [!DNL CTV] 플랫폼, 사용 [!DNL Ramp ID] 식별자. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 신규 | 에 대한 실시간 아웃바운드 연결 만들기 [!DNL Azure Data Lake Storage Gen2] Adobe Experience Platform의 데이터 파일을 정기적으로 고유한 저장소 위치로 내보냅니다. 이 새 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다 [!BADGE 베타]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | 신규 | [!DNL Data Landing Zone] 은(는) [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, 안전한 클라우드 기반 파일 스토리지 시설에 대한 액세스 권한을 부여하여 플랫폼 외부로 파일을 내보낼 수 있습니다. 이 새 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다 [!BADGE 베타]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 신규 | 에 대한 실시간 아웃바운드 연결 만들기 [!DNL Google Cloud Storage] Adobe Experience Platform의 데이터 파일을 정기적으로 고유한 버킷으로 내보냅니다. 이 새 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다 [!BADGE 베타]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 업데이트됨 | 이 업데이트를 통해 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다. [!BADGE 베타]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 업데이트됨 | 이 업데이트를 통해 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다. [!BADGE 베타]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 업데이트됨 | 이 업데이트를 통해 대상은 향상된 파일 내보내기 기능을 제공하며 을 지원합니다. [!BADGE 베타]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] 연결](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | 업데이트됨 | 다음 [!DNL Adobe Campaign Managed Services] 이제 Adobe Experience Platform과의 통합은 다양한 대상 동기화 유형을 지원합니다. 동기화 유형 선택 컨트롤을 사용하여 대상을 Adobe Campaign으로 내보내야 하는지 아니면 대상 및 해당 프로필 속성으로 내보내야 하는지 결정합니다. <br> ![새 동기화 유형 선택 선택기가 강조 표시되어 있습니다.](/help/release-notes/2023/assets/acms-destination-export-type.png "새 동기화 유형 선택 선택기가 강조 표시되어 있습니다."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

위의 6개 클라우드 스토리지 대상의 업데이트 및 일반 가용성 릴리스는 다음 기능을 제공합니다.

- 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- 를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능 [매핑 단계 개선](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- 사용자 정의 기능 [내보낸 CSV 데이터 파일의 형식 지정](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[데이터 세트 내보내기 지원](/help/destinations/ui/export-datasets.md).


**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

- 매핑 단계에서 사용 가능한 모든 대상 속성이 Salesforce에서 반환되지 않은 (API) Salesforce Marketing Cloud 대상 문제를 해결했습니다. 이제 다음 항목이 있습니다. [대상 속성의 상한 2000](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) Salesforce에서 가져왔습니다.
- Microsoft Dynamics 365 대상 문제를 해결했습니다. 이제 대상은 를 통해 데이터의 지역 라우팅을 지원합니다. [영역 선택기](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate)를 사용하면 Microsoft 생태계 내에서 회사가 프로비저닝되는 지역에 따라 데이터 내보내기를 라우팅할 수 있습니다. <br> ![강조 표시된 새 영역 선택기입니다.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "강조 표시된 새 영역 선택기입니다."){width="100" zoomable="yes"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크에서 데이터를 쿼리할 수 있습니다. 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 향상된 쿼리 편집기 토글 | 향상된 쿼리 편집기 토글은 향상된 액세스 가능성 및 다중 테마 지원을 제공합니다. 향상된 편집기 설정을 통해 어두운 테마 또는 밝은 테마를 활성화할 수 있습니다. 자세한 내용은 [설명서](../../query-service/ui/user-guide.md#enhanced-editor-toggle)를 참조하십시오. |
| 계산된 통계의 별칭 이름 | 이제 별칭 이름을 제공하여 SQL 쿼리의 계산된 통계에서 의 결과를 기술적으로 참조할 수 있습니다. 이 업데이트 및 COMPUTE STATISTICS 명령의 기타 업데이트에 대한 자세한 내용은 설명서를 참조하십시오. 자세한 내용은 [설명서](../../query-service/essential-concepts/dataset-statistics.md#alias-name)를 참조하십시오. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 에 저장된 데이터를 세그먼트화할 수 있습니다. [!DNL Experience Platform] 고객, 잠재 고객, 사용자 또는 조직과 같은 개인 사용자를 대상으로 합니다. 에서 세그먼트 정의 또는 기타 소스를 통해 대상자를 만들 수 있습니다. [!DNL Real-Time Customer Profile] 데이터. 이러한 대상은에서 중앙 집중식으로 구성 및 유지 관리됩니다. [!DNL Platform]및 는 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Audience 포털 | Audience Portal에서는 Adobe Experience Platform 내의 대상에 액세스, 생성 및 관리할 수 있는 새로운 탐색 환경을 제공합니다. Audience Portal에서는 플랫폼에서 생성한 및 외부에서 생성된 대상을 보고, 필터링, 폴더 및 태그를 통해 작업 효율성을 개선하고, 플랫폼에서 생성한 대상을 만들고, CSV 파일을 통해 외부에서 생성된 대상을 가져올 수 있습니다. 대상 포털에 대한 자세한 내용은 다음을 참조하십시오. [세그먼테이션 서비스 UI 안내서](../../segmentation/ui/overview.md). |
| 대상자 구성 | 대상 컴포지션은 다양한 작업을 나타내는 데 사용되는 블록을 사용하여 대상을 작성하고 편집하는 사용하기 쉬운 작업 영역을 제공합니다. 대상자 구성에 대한 자세한 내용은 [대상 구성 UI 안내서](../../segmentation/ui/audience-composition.md). |

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 읽으십시오. [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | 이제 다음을 사용할 수 있습니다. [[!DNL SAP Commerce] 소스](../../sources/connectors/ecommerce/sap-commerce.md) 에서 구독 청구 데이터를 가져오려면 [!DNL SAP Commerce] Experience Platform 계정. |
| [!DNL Phoenix] 지원 | 이제 다음을 사용할 수 있습니다. [[!DNL Phoenix] 소스](../../sources/connectors/databases/phoenix.md) 에서 데이터를 가져오려면 [!DNL Phoenix] Experience Platform 대상 데이터베이스. |
| 에 대한 인증 업데이트 [!DNL Salesforce] 및 [!DNL Salesforce Service Cloud] | 이제 의 API 버전을 지정할 수 있습니다. [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 및 [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) 소스: Experience Platform UI 또는 [!DNL Flow Service] API. |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).
