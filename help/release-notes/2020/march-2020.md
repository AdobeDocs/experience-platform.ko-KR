---
title: Adobe Experience Platform 릴리스 노트 - 2020년 3월
description: Adobe Experience Platform에 대한 2020년 3월 릴리스 노트입니다.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 릴리스 노트;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2020년 3월 11일**

Adobe Experience Platform의 기존 기능 업데이트:

* [데이터 거버넌스](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 데이터 거버넌스 {#governance}

[!DNL Experience Platform] 에서는 여러 엔터프라이즈 시스템의 데이터를 함께 가져와서 마케터가 고객을 식별, 이해 및 참여시킬 수 있도록 합니다. [!DNL Experience Platform] 에는 내에서 데이터를 적절하게 사용할 수 있도록 하는 완벽한 데이터 거버넌스 인프라가 포함되어 있습니다 [!DNL Platform] 시스템 간에 공유할 때 사용할 수 있습니다.

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용량에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 이 구성 요소는 [!DNL Experience Platform] 카탈로그 작성, 데이터 계보, 데이터 사용 레이블 지정, 데이터 액세스 정책, 마케팅 작업을 위한 데이터 액세스 제어 등 다양한 수준에서 사용할 수 있습니다.

**새로운 기능**

>[!NOTE]
>
>다음 새 기능 중 일부는 현재 베타 버전이며 모든 사용자가 사용할 수 없습니다. 베타 기능은 변경될 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 에 대한 데이터 사용 정책 자동 적용 [!DNL Real-Time Customer Data Platform] | 이제 대상에 데이터를 활성화하는 워크플로우에서 데이터 사용 정책이 적용됩니다. 데이터 거버넌스는 기존 활성화(예: 데이터 세트 레이블, 병합 정책, 세그먼트 정의 등)에 영향을 주는 변경 사항을 적용할 때 포함 및 적용됩니다. |
| 실행을 위한 데이터 계보 | Real-Time CDP에서 데이터 사용 정책을 위반하면 UI에 데이터 계보 정보가 포함된 알림이 표시되므로 사용자가 정책이 위반되는 이유와 위반을 해결하기 위해 수행할 수 있는 작업을 이해할 수 있습니다. |


**알려진 문제**

* None

데이터 거버넌스에 대한 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md).

## 데이터 수집 {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연을 수집하는 풍부한 기능을 제공합니다. Adobe Experience Platform [!DNL Data Ingestion] 에서는 일괄 처리 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 포함한 데이터를 수집하기 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 부분 배치 수집 | 부분 배치 섭취는 특정 임계값까지 오류가 포함된 데이터를 수집하는 기능입니다. 이 기능을 사용하면 사용자가 모든 잘못된 데이터를 Adobe Experience Platform에 성공적으로 수집하면서 모든 잘못된 데이터를 개별적으로 일괄 처리할 수 있습니다. 유효성 검사를 통과하지 못한 이유를 설명하는 세부 사항이 실패한 배치에 추가됩니다. 부분 배치 처리에 대한 자세한 내용은 [부분 배치 수집 설명서](../../ingestion/batch-ingestion/partial.md). |

**알려진 문제**

* None

Platform으로 데이터를 수집하는 방법에 대한 자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md).


## 대상 {#destinations}

in [Real-time Customer Data Platform](../../rtcdp/overview.md), 대상은 대상 플랫폼과의 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

새 대상은 Adobe Experience Platform 데이터를 활성화할 수 있는 곳입니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| 클라우드 스토리지 대상 | 이제 Real-Time CDP에서 세그먼트를 데이터 파일로 [!DNL Amazon S3] 또는 SFTP 클라우드 저장소 위치. 이렇게 하면 CSV 또는 탭으로 구분된 파일을 통해 대상자 및 해당 프로필 속성을 내부 시스템으로 보낼 수 있습니다. |
| 광고 대상 | 다음 [!DNL Google] 대상 카드는 이제 세 개의 대상 카드로 분할됩니다. [!DNL Google] Real-Time CDP에서 현재 지원되는 플랫폼 [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] 디스플레이 및 비디오 360. |

자세한 내용은 [대상 개요](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 개별 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform [!DNL Identity Service] 은 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 고객의 행동을 더 잘 파악할 수 있도록 지원하고 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있도록 합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 개인 그래프 | 개인 그래프 기능이 향상되어 주별 일괄 처리 프로세스에서 매일 새로 고쳐진 그래프로 그래프 생성 지연을 줄여 줍니다. [!DNL Identity Service] 최신 ID 그래프 및 링크에 액세스할 수 있는 고객 |

**알려진 문제**

* None

에 대한 자세한 정보 [!DNL Identity Service]를 참조하고 [ID 서비스 개요](../../identity-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Audience Manager 커넥터에 사용되지 않는 신호 | Audience Manager의 신호 수준 데이터는 더 이상 전송되지 않습니다. 트레이트 및 세그먼트에 대한 세그먼트 멤버십은 계속 포함됩니다. 이 변경의 결과로 인바운드 데이터 세트는 더 이상 생성되지 않습니다. |
| 이름이 변경된 데이터 세트 | Audience Manager 커넥터에서 생성한 데이터 세트에는 업데이트된 이름과 설명이 있습니다. |
| 활성화 [!DNL Profile] Audience Manager에서 전환 | [!DNL Profile] 토글 기능을 활성화하거나 비활성화하여 데이터 세트를 [!DNL Real-Time Customer Profile]. 토글은 기본적으로 활성화되어 있습니다. |
| 클라우드 스토리지 시스템에 대한 UI 지원 | 에 대한 새 소스 커넥터 [!DNL Azure Data Lake Storage Gen2] ( UI) 아래에 그룹화됩니다. |
| CRM 시스템에 대한 UI 지원 | 에 대한 새 소스 커넥터 [!DNL HubSpot], [!DNL Salesforce Service Cloud], 및 [!DNL ServiceNow] ( UI) 아래에 그룹화됩니다. |
| 데이터베이스 시스템에 대한 UI 지원 | 에 대한 새 소스 커넥터 [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], 및 [!DNL MySQL] ( UI) 아래에 그룹화됩니다. |

**알려진 문제**

* None

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
