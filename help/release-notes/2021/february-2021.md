---
title: Adobe Experience Platform 릴리스 노트 2021년 2월
description: Adobe Experience Platform의 2021년 2월 릴리스 정보.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2021년 2월 24일**

Adobe Experience Platform의 새로운 기능:

- [(베타) 대시보드](#dashboards)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (베타) 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 조직 데이터에 관한 중요한 정보를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필, 세그먼트, 대상 및 라이선스 사용 대시보드(베타) | **참고: 대시보드 기능은 현재 베타 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.**<br/><br/>&#x200B;대시보드는 조직의 데이터에 대한 기본 보고를 제공하며 Platform 내의 마케터 워크플로우에 직접 빌드됩니다. 이러한 대시보드는 추가적인 IT 지원이나 추가적인 데이터 웨어하우징 설계 및 구현으로 데이터를 내보내고 처리하는 데 소요되는 시간과 노력 없이 사용할 수 있습니다. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace 는 머신 러닝 및 인공 지능을 사용하여 데이터에서 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace는 Adobe 솔루션 전반에서 컨텐츠 및 데이터 에셋을 사용하여 예측을 수행하는 데 도움이 됩니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| JupyterLab EDA 노트북 | EDA(Exploratory Data Analysis) Python 노트북은 이제 Jupyterlab에서 사용할 수 있습니다. 이 노트북은 데이터의 패턴을 찾고, 데이터의 온전성을 확인하고, 예측 모델에 대한 관련 데이터를 요약하는 데 도움이 되도록 설계되었습니다. 다음 튜토리얼 참조: [예측 모델을 위한 웹 기반 데이터 탐색](../../data-science-workspace/jupyterlab/eda-notebook.md) 추가 정보. |

데이터 과학 작업 영역에 대한 자세한 내용은 [데이터 과학 작업 영역 개요](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되고, Experience Platform 내에서 분석되며, 다양한 대상으로 활성화됩니다. Platform은 데이터 흐름과 함께 투명성을 제공하여 이 잠재적으로 비선형적인 데이터 흐름을 추적하는 프로세스를 보다 쉽게 만듭니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하여 다음에서 활용할 수 있습니다. [!DNL Identity Service] 및 [!DNL Real-Time Customer Profile] 에 최종적으로 활성화되기 전에 [!DNL Destinations].

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 모니터링 대시보드 | 이제 모니터링 대시보드를 사용하여 소스 데이터 수집에 대한 교차 서비스 투명도와 실행 가능한 인사이트를 얻을 수 있습니다. 새로운 모니터링 대시보드는에서 처리된 데이터에 대한 포괄적인 보기를 제공합니다. [!DNL Data Lake] 끝 [!DNL Identity Service] 및 종료 [!DNL Profile], 수집 비율, 성공 및 실패를 모니터링할 수 있습니다. 다음 튜토리얼 참조: [ui에서 소스 데이터 흐름 모니터링](../../dataflows/ui/monitor-sources.md) 추가 정보. |

데이터 흐름에 대한 일반적인 정보는 [데이터 흐름 개요](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 다음 [!DNL LinkedIn Matched Audiences] 연결을 통해 의 대상을 활성화할 수 있습니다. [!DNL LinkedIn] 소셜 플랫폼입니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

표준화 및 상호 운용성은 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe을 기반으로 하는 (XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 업그레이드된 검색 UI | 향상된 검색 기능을 이제 [!UICONTROL 찾아보기] 의 탭 [!UICONTROL 스키마] 작업 공간 및 의 스키마 필드 그룹 선택 대화 상자 [!DNL Schema Editor].<br><br>이전에 검색했던 용어만 검색 결과에 포함되고, 검색 쿼리와 이름이 일치하는 XDM 리소스입니다. 이제 이름과 쿼리가 일치하는 리소스 외에도 용어와 일치하는 개별 속성이 포함된 리소스도 포함됩니다. 이를 통해 리소스 이름이 아닌 포함된 속성을 기준으로 XDM 리소스를 검색할 수 있습니다.<br><br>의 문서 보기 [xdm 리소스 살펴보기](../../xdm/ui/explore.md) 및 [스키마 관리](../../xdm/ui/resources/schemas.md) 을 참조하십시오. |

XDM에 대한 일반적인 정보는 [XDM 시스템 개요](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 이러한 문제는 고객 데이터가 서로 다른 시스템 간에 분산되어 각 개별 고객이 여러 개의 &quot;ID&quot;를 가지는 것처럼 보이는 경우 더욱 어려워집니다.

Adobe Experience Platform [!DNL Identity Service] 은 디바이스와 시스템 간에 id를 연결하여 고객 및 고객 행동을 더 잘 파악할 수 있도록 하여 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 뷰어 | ID 그래프 뷰어를 사용하면 UI에서 함께 결합된 ID를 확인하고 시각화할 수 있으므로 디버깅 및 투명도를 향상시킬 수 있습니다. 다음을 참조하십시오. [id 그래프 뷰어 문서](../../identity-service/ui/identity-graph-viewer.md) 추가 정보. |

에 대한 일반적인 추가 정보 [!DNL Identity Service]을(를) 참조하십시오. [ID 서비스 개요](../../identity-service/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile] 에서는 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계산된 속성(알파) | ***참고: 이 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.*** <br/><br/>계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 그런 다음 세분화, 활성화 및 개인화에서 합계를 사용할 수 있습니다. 이들 함수의 일부 예는 count, sum, average, min, max, true/false를 포함한다. 계산된 속성은 현재 API를 통해서만 사용할 수 있습니다. |

을 사용하여 작업하는 데 필요한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대한 자세한 내용 [!DNL Profile] 데이터, 다음을 읽는 것부터 시작하십시오. [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub] | 이제 연결할 수 있습니다 [!DNL Google PubSub] 끝 [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI. 다음을 참조하십시오. [[!DNL Google PubSub] 커넥터 개요](../../sources/connectors/cloud-storage/google-pubsub.md) 추가 정보. |
| [!DNL Oracle Object Storage] | 이제 연결할 수 있습니다 [!DNL Oracle Object Storage] 끝 [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI. 다음을 참조하십시오. [[!DNL Oracle Object Storage] 커넥터 개요](../../sources/connectors/cloud-storage/oracle-object-storage.md) 추가 정보. |

소스에 대한 일반적인 정보는 [소스 개요](../../sources/home.md).
