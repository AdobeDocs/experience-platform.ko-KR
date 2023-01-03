---
title: Adobe Experience Platform 릴리스 노트 - 2021년 1월
description: Adobe Experience Platform에 대한 2021년 1월 릴리스 노트입니다.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 1월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 정규 표현식 함수 | [!DNL Data Prep] 이제 매퍼가 정규 표현식을 기반으로 입력 필드의 일부 일치 및 추출을 지원합니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 는 클라우드를 위한 Microsoft의 개체 저장 솔루션입니다. |

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 고급 ID 일치 | 의 대상 일치율 기능에 대한 개선 사항 [!DNL Facebook Custom Audiences] 및 [!DNL Google Customer Match]를 추가하여 외부 ID, 전화번호 및 모바일 장치 ID와 같은 추가적인 ID 일치에 대한 지원을 추가할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오. <ul><li>[Facebook 대상](../../destinations/catalog/social/facebook.md)</li><li>[Google 고객 일치 대상](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

자세한 내용은 [대상 개요](../../destinations/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. [!DNL Profile] 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 저장소에서 데이터 세트 삭제 | Experience Platform 데이터 레이크에서 데이터 세트를 삭제하면 프로필 스토어에서도 자동으로 삭제됩니다. 프로필 저장소에서 데이터 세트를 명시적으로 삭제하기 위해 더 이상 프로필 시스템 작업 API 엔드포인트를 사용할 필요가 없습니다. 자세한 내용은 [프로필 시스템 작업 API 끝점 안내서](../../profile/api/profile-system-jobs.md). |
| 지정된 세그먼트에 대한 예상 ID 네임스페이스 수입니다 | 예상 프로필 수의 경우 이제 미리 보기 API가 다음을 보고합니다.<ul><li>주어진 네임스페이스에 대한 세그먼트에서 예상되는 프로필의 총 수입니다.</li><li>지정된 네임스페이스에 대한 프로필 조합 스키마에서 예상되는 프로필의 총 수입니다.</li></ul>자세한 내용은 [프로필 미리 보기 API 엔드포인트 안내서](../../profile/api/preview-sample-status.md). |

작업 모범 사례 및 자습서를 비롯하여 실시간 고객 프로필에 대한 자세한 정보 [!DNL Profile] 데이터 읽기 [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Audience Manager 소스 커넥터 개선 사항 | 이제 Audience Manager에서 플랫폼으로 수집하기 위한 개별 자사 세그먼트를 필터링 및 선택하고 자사 트레이트를 필터링할 수 있습니다. 다음에서 자습서를 참조하십시오. [Audience Manager 소스 커넥터 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 추가 정보. |
| [!DNL Google BigQuery] 소스 커넥터 개선 사항 | 이제 를 사용하여 한 흐름 실행에서 10GB보다 큰 파일을 수집할 수 있습니다 [!DNL BigQuery] 소스 커넥터. 자세한 내용은 [[!DNL BigQuery] 소스 커넥터 개요](../../sources/connectors/databases/bigquery.md) 추가 정보. |
| 클라우드 스토리지를 위한 복잡한 데이터 유형 지원 | 이제 클라우드 스토리지 소스 커넥터를 사용할 때 JSON 파일의 배열과 같은 복잡한 데이터 유형을 수집할 수 있습니다. 클라우드 저장소 데이터 흐름 만들기에 대한 자습서를 참조하십시오 [UI에서](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 또는 [사용 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) 추가 정보. |
| 에 대한 서비스 주 키 기반 인증 지원 [!DNL Microsoft Dynamics] 소스 | 이제 [!DNL Dynamics] 암호 기반 인증의 대체 요소로 서비스 사용자 키를 사용하는 계정. 자세한 내용은 [[!DNL Dynamics] 소스 커넥터 개요](../../sources/connectors/crm/ms-dynamics.md) 추가 정보. |
| 클라우드 스토리지 소스의 사용자 지정 구분 기호를 위한 UI 지원 | 이제 쉼표( )와 같은 사용자 지정 열 구분 기호를 설정할 수 있습니다`,`), 탭 ( )`\t`) 또는 파이프(`|`), 로 구분된 파일을 UI에서 수집할 수 있습니다. 다음에서 자습서를 참조하십시오. [클라우드 저장소 소스 커넥터를 사용하여 데이터 흐름 만들기](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 자세한 정보 |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
