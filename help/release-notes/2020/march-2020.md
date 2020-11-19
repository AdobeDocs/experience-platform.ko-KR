---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 3월 11일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] 기업은 여러 엔터프라이즈 시스템의 데이터를 통합하여 마케터가 고객을 식별하고 이해하고 고객의 참여를 유도할 수 있습니다. [!DNL Experience Platform] 시스템 간에 데이터를 공유할 때 적절한 데이터 사용 [!DNL Platform] 을 보장하는 엔드 투 엔드 데이터 관리 인프라를 포함합니다.

Adobe Experience Platform [!DNL Data Governance] 는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다. 카탈로그 작성, 데이터 계보, 데이터 사용 표시, 데이터 액세스 정책, 마케팅 작업을 위한 데이터 액세스 제어 등 다양한 [!DNL Experience Platform] 수준에서 핵심적인 역할을 합니다.

**새로운 기능**

>[!NOTE]
>
>다음의 일부 새로운 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 베타 기능은 변경될 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 사용 정책 자동 적용 [!DNL Real-time Customer Data Platform] | 이제 데이터 사용 정책은 대상으로 데이터를 활성화하는 워크플로우에서 적용됩니다. [!DNL Data Governance] 데이터 세트 레이블 변경, 정책 병합, 세그먼트 정의 등 기존 활성화에 영향을 주는 변경 작업을 수행할 때도 이 옵션이 포함되고 적용됩니다. |
| 실행을 위한 데이터 계보 | 실시간 CDP에서 데이터 사용 정책을 위반하면 UI에 데이터 계보 정보가 포함된 알림이 표시되어 정책 위반 이유와 위반 해결을 위한 조치를 이해할 수 있습니다. |


**알려진 문제**

* None

자세한 내용 [!DNL Data Governance]은 [데이터 거버넌스 개요를 참조하십시오](../../data-governance/home.md).

## 데이터 수집 {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 인제스트하는 다양한 기능을 제공합니다. Adobe Experience Platform [!DNL Data Ingestion] 는 배치 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 비롯한 데이터 인제스트를 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 부분 일괄 처리 | 부분 일괄 처리란 오류가 포함된 데이터를 특정 임계값까지 인제스트하는 기능입니다. 이 기능을 사용하면 사용자가 모든 정확한 데이터를 Adobe Experience Platform으로 성공적으로 인제스트할 수 있으며 모든 잘못된 데이터는 별도로 일괄적으로 묶입니다. 실패한 배치에 유효성 검사에 합격하지 않은 이유를 설명하는 세부 사항이 추가됩니다. 부분 일괄 처리 통합에 대한 자세한 내용은 [부분 일괄 처리 통합 문서에서 확인할 수 있습니다](../../ingestion/batch-ingestion/partial.md). |

**알려진 문제**

* None

데이터를 플랫폼으로 인제스트하는 방법에 대한 자세한 내용은 [데이터 수집 설명서를 참조하십시오](../../ingestion/home.md).


## 대상 {#destinations}

실시간 [고객 데이터 플랫폼](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

Adobe Experience Platform 데이터를 활성화할 수 있는 새로운 대상을 사용할 수 있습니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| 클라우드 스토리지 대상 | Adobe 실시간 CDP를 사용하면 세그먼트를 데이터 파일로 사용자 [!DNL Amazon S3] 또는 SFTP 클라우드 스토리지 위치에 전달할 수 있습니다. 이렇게 하면 CSV 또는 탭으로 구분된 파일을 통해 대상과 프로필 속성을 내부 시스템으로 보낼 수 있습니다. |
| 광고 대상 | 이제 [!DNL Google] 대상 카드가 세 개의 대상 카드로 분할되어 현재 Adobe 실시간 CDP에서 지원되는 세 개의 다른 [!DNL Google] 플랫폼에 대해 제공됩니다. [!DNL Google Ads], [!DNL Google Ad Manager]Display &amp; [!DNL Google] Video 360. |

자세한 내용은 [대상 개요를 참조하십시오](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

고객의 기대에 부응하는 디지털 경험을 전달하려면 고객을 완벽하게 이해해야 합니다. 고객 데이터가 서로 다른 시스템에서 분열되어 각각의 개별 고객이 여러 개의 &quot;ID&quot;를 갖는 것처럼 보일 경우 이러한 문제는 더욱 복잡해집니다.

Adobe Experience Platform [!DNL Identity Service] 는 다양한 디바이스와 시스템에 ID를 연결함으로써 효과적이고 개인화된 디지털 경험을 실시간으로 전달할 수 있도록 함으로써 고객 및 고객의 행동을 보다 정확하게 파악할 수 있도록 지원합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 개인 그래프 | 비공개 그래프 기능은 주간 일괄 처리에서 매일 새로 고쳐진 그래프로 그래프 생성 지연을 줄이기 위해 향상되어 [!DNL Identity Service] 고객이 보다 최신 ID 그래프와 링크에 액세스할 수 있습니다. |

**알려진 문제**

* None

자세한 내용 [!DNL Identity Service]은 ID 서비스 [개요를 참조하십시오](../../identity-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Audience Manager 커넥터에 사용되지 않는 신호 | Audience Manager의 신호 수준 데이터는 더 이상 전송되지 않습니다. 트레이트 및 세그먼트에 대한 세그먼트 멤버십은 계속 포함됩니다. 이 변경 결과로 인바운드 데이터 집합이 더 이상 생성되지 않습니다. |
| 데이터 세트 이름 변경 | Audience Manger 커넥터로 생성된 데이터 세트에 업데이트된 이름과 설명이 있습니다. |
| Audience Manager [!DNL Profile] 에서 전환 활성화 | [!DNL Profile] 토글을 활성화하거나 비활성화하여 데이터 세트를 홍보할 수 있습니다 [!DNL Real-time Customer Profile]. 기본적으로 토글이 활성화됩니다. |
| 클라우드 스토리지 시스템에 대한 UI 지원 | UI에 대한 새 소스 커넥터 [!DNL Azure Data Lake Storage Gen2] 가 있습니다. |
| CRM 시스템에 대한 UI 지원 | UI [!DNL HubSpot], [!DNL Salesforce Service Cloud]및 [!DNL ServiceNow] 에 대한 새 소스 커넥터 |
| 데이터베이스 시스템에 대한 UI 지원 | UI [!DNL AWS Redshift], [!DNL Google BigQuery][!DNL MariaDB], [!DNL Microsoft SQL Server]및 [!DNL MySQL] 새 소스 커넥터 |

**알려진 문제**

* None

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).