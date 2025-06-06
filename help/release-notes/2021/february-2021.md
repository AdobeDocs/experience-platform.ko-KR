---
title: Adobe Experience Platform 릴리스 노트 2021년 2월
description: Adobe Experience Platform의 2021년 2월 릴리스 정보.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 21%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2021년 2월 24일 목요일**

Adobe Experience Platform의 새로운 기능:

- [(Beta) 대시보드](#dashboards)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 정보를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필, 세그먼트, 대상 및 라이선스 사용 대시보드(Beta) | **참고: 대시보드 기능은 현재 Beta 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.**<br/><br/>&#x200B;대시보드는 조직의 데이터에 대한 기본 보고를 제공하며 Experience Platform 내의 마케터 워크플로우에 직접 빌드됩니다. 이러한 대시보드는 추가적인 IT 지원이나 추가적인 데이터 웨어하우징 설계 및 구현으로 데이터를 내보내고 처리하는 데 소요되는 시간과 노력 없이 사용할 수 있습니다. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace은 머신 러닝 및 인공 지능을 사용하여 데이터에서 통찰력을 만듭니다. Adobe Experience Platform에 통합된 Data Science Workspace은 Adobe 솔루션 전반에서 컨텐츠 및 데이터 에셋을 사용하여 예측을 수행하는 데 도움이 됩니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| JupyterLab EDA 노트북 | EDA(Exploratory Data Analysis) Python 노트북은 이제 Jupyterlab에서 사용할 수 있습니다. 이 노트북은 데이터의 패턴을 찾고, 데이터의 온전성을 확인하고, 예측 모델에 대한 관련 데이터를 요약하는 데 도움이 되도록 설계되었습니다. 자세한 내용은 [예측 모델에 대한 웹 기반 데이터 탐색](../../data-science-workspace/jupyterlab/eda-notebook.md)에 대한 자습서를 참조하십시오. |

Data Science Workspace에 대한 일반적인 정보는 [Data Science Workspace 개요](../../data-science-workspace/home.md)를 참조하십시오.

## [!DNL Dataflows] {#dataflows}

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되고, Experience Platform 내에서 분석되며, 다양한 대상으로 활성화됩니다. Experience Platform은 데이터 흐름을 투명하게 제공하여 이 잠재적으로 비선형적인 데이터 흐름을 추적하는 프로세스를 보다 쉽게 만듭니다.

데이터 흐름은 Experience Platform 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 있으므로 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하는 데 도움이 됩니다. [!DNL Identity Service] 및 [!DNL Real-Time Customer Profile]에서 사용한 후 최종적으로 [!DNL Destinations]에 활성화됩니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 새 모니터링 대시보드 | 이제 모니터링 대시보드를 사용하여 소스 데이터 수집에 대한 교차 서비스 투명도와 실행 가능한 인사이트를 얻을 수 있습니다. 새 모니터링 대시보드에서는 [!DNL Data Lake]에서 [!DNL Identity Service] 및 [!DNL Profile]까지 처리된 데이터를 종합적으로 볼 수 있으며 수집 비율, 성공 및 실패를 모니터링할 수 있습니다. 자세한 내용은 [UI에서 원본 데이터 흐름 모니터링](../../dataflows/ui/monitor-sources.md)에 대한 자습서를 참조하십시오. |

데이터 흐름에 대한 일반적인 정보는 [데이터 흐름 개요](../../dataflows/home.md)를 참조하세요.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | [!DNL LinkedIn Matched Audiences] 연결을 사용하면 [!DNL LinkedIn] 소셜 플랫폼에서 대상을 활성화할 수 있습니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## [!DNL Experience Data Model (XDM) System] {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 핵심 개념입니다. Adobe을 기반으로 하는 [!DNL Experience Data Model]&#x200B;(XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 업그레이드된 검색 UI | 이제 [!UICONTROL 스키마] 작업 영역의 [!UICONTROL 찾아보기] 탭과 [!DNL Schema Editor]의 스키마 필드 그룹 선택 대화 상자에서 향상된 검색 기능을 사용할 수 있습니다.<br><br>이전에 검색했을 때 검색 쿼리와 이름이 일치하는 XDM 리소스만 결과에 포함됩니다. 이제 이름과 쿼리가 일치하는 리소스 외에도 용어와 일치하는 개별 속성이 포함된 리소스도 포함됩니다. 이를 통해 리소스 이름이 아닌 포함된 속성을 기준으로 XDM 리소스를 검색할 수 있습니다.<br><br>자세한 내용은 UI에서 [XDM 리소스 탐색](../../xdm/ui/explore.md) 및 [스키마 관리](../../xdm/ui/resources/schemas.md)의 문서를 참조하십시오. |

XDM에 대한 일반적인 정보는 [XDM 시스템 개요](../../xdm/home.md)를 참조하세요.

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 이러한 문제는 고객 데이터가 서로 다른 시스템 간에 분산되어 각 개별 고객이 여러 개의 &quot;ID&quot;를 가지는 것처럼 보이는 경우 더욱 어려워집니다.

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스와 시스템 간에 id를 연결하여 고객 및 고객 행동에 대한 더 나은 보기를 얻을 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 뷰어 | ID 그래프 뷰어를 사용하면 UI에서 함께 결합된 ID를 확인하고 시각화할 수 있으므로 디버깅 및 투명도를 향상시킬 수 있습니다. 자세한 내용은 [ID 그래프 뷰어 문서](../../identity-service/features/identity-graph-viewer.md)를 참조하십시오. |

[!DNL Identity Service]에 대한 일반적인 정보는 [ID 서비스 개요](../../identity-service/home.md)를 참조하세요.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile]을(를) 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계산된 속성(Alpha) | ***참고: 이 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.*** <br/><br/>계산된 특성은 이벤트 수준 데이터를 프로필 수준 특성으로 집계하는 데 사용되는 함수입니다. 그런 다음 세분화, 활성화 및 개인화에서 합계를 사용할 수 있습니다. 이들 함수의 일부 예는 count, sum, average, min, max, true/false를 포함한다. 계산된 속성은 현재 API를 통해서만 사용할 수 있습니다. |

[!DNL Profile] 데이터 작업에 대한 자습서 및 모범 사례를 포함하여 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 읽는 것부터 시작하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Google PubSub]을(를) [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Google PubSub] 커넥터 개요](../../sources/connectors/cloud-storage/google-pubsub.md)를 참조하십시오. |
| [!DNL Oracle Object Storage] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Oracle Object Storage]을(를) [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Oracle Object Storage] 커넥터 개요](../../sources/connectors/cloud-storage/oracle-object-storage.md)를 참조하십시오. |

소스에 대한 일반적인 정보는 [소스 개요](../../sources/home.md)를 참조하세요.
