---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트(2021년 1월 27일)
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 1월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변형 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 정규 표현식 함수 | [!DNL Data Prep] 이제 매퍼가 일반 표현식을 기반으로 입력 필드의 일부를 일치 및 추출할 수 있습니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations] Adobe Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 여러 가지 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 는 클라우드를 위한 Microsoft의 객체 스토리지 솔루션입니다. |

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 고급 ID 일치 | 외부 ID, 전화 번호 및 모바일 장치 ID와 같은 추가 ID 일치에 대한 지원을 추가하여 [!DNL Facebook Custom Audiences] 및 [!DNL Google Customer Match]의 대상 일치 비율 기능이 향상되었습니다. 자세한 내용은 다음 설명서를 참조하십시오. <ul><li>[Facebook 대상](../../destinations/catalog/social/facebook.md)</li><li>[Google 고객 일치 대상](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[대상에 프로필 및 세그먼트 활성화](../../destinations/ui/activate-destinations.md)</li></ul> |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소 또는 시기와 상관없이 고객의 관심사와 연관성 있는 경험을 일관되게 전달할 수 있습니다. 실시간 고객 프로파일을 사용하면 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 다양한 채널의 데이터를 취합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Profile] 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 저장소에서 데이터 집합 삭제 | Experience Platform Data Lake에서 데이터 세트를 삭제하면 이 데이터 세트는 프로필 저장소에서도 자동으로 삭제됩니다. 프로필 저장소에서 데이터 집합을 명시적으로 삭제하기 위해 프로필 시스템 작업 API 끝점을 사용하여 삭제 요청을 할 필요가 없습니다. 자세한 내용은 [프로필 시스템 작업 API 끝점 안내서](../../profile/api/profile-system-jobs.md)를 참조하십시오. |
| 지정된 세그먼트에 대한 예상 ID 네임스페이스 수 | 예상 프로필 수에 대해 미리 보기 API가 이제 다음과 같이 보고합니다.<ul><li>지정된 네임스페이스에 대한 세그먼트에서 예상 프로필의 총 수입니다.</li><li>지정된 네임스페이스에 대한 프로필 조합 스키마의 예상 프로필의 총 수입니다.</li></ul>자세한 내용은 [프로필 미리 보기 API 끝점 안내서](../../profile/api/preview-sample-status.md)를 참조하십시오. |

[!DNL Profile] 데이터 작업에 대한 자습서 및 모범 사례를 포함하여 실시간 고객 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 읽으십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 한편, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Audience Manager 소스 커넥터 개선 사항 | 이제 Audience Manager에서 인제스트까지 개별 자사 세그먼트를 필터링하고 선택할 수 있을 뿐만 아니라 자사 트레이트를 필터링할 수 있습니다. 자세한 내용은 [Audience Manager 소스 커넥터 만들기](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)의 자습서를 참조하십시오. |
| [!DNL Google BigQuery] 소스 커넥터 개선 사항 | 이제 [!DNL BigQuery] 소스 커넥터를 사용하여 하나의 흐름 실행에서 10GB 이상의 파일을 인제스트할 수 있습니다. 자세한 내용은 [[!DNL BigQuery] 소스 커넥터 개요](../../sources/connectors/databases/bigquery.md)를 참조하십시오. |
| 클라우드 스토리지를 위한 복잡한 데이터 유형 지원 | 이제 클라우드 스토리지 소스 커넥터를 사용할 때 JSON 파일의 배열과 같은 복잡한 데이터 유형을 인제스트할 수 있습니다. 자세한 내용은 UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 또는 [API](../../sources/tutorials/api/collect/cloud-storage.md)를 사용하여 클라우드 저장소 데이터 흐름 [을 만드는 방법에 대한 자습서를 참조하십시오. [!DNL Flow Service]  |
| [!DNL Microsoft Dynamics] 소스에 대한 서비스 주 키 기반 인증 지원 | 이제 서비스 인증 키를 사용하여 암호 기반 인증에 대한 대안으로 [!DNL Dynamics] 계정에 인증할 수 있습니다. 자세한 내용은 [[!DNL Dynamics] 소스 커넥터 개요](../../sources/connectors/crm/ms-dynamics.md)를 참조하십시오. |
| 클라우드 스토리지 소스의 사용자 정의 구분 기호를 위한 UI 지원 | 이제 쉼표(`,`), 탭(`\t`) 또는 파이프(`|`)와 같은 사용자 지정 열 구분 기호를 설정하여 UI에서 구분된 파일을 수집할 수 있습니다. 자세한 내용은 [클라우드 저장소 소스 커넥터를 사용하여 데이터 흐름 만들기](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)에서 자습서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
