---
title: Adobe Experience Platform 릴리스 노트 - 2021년 2월
description: Adobe Experience Platform에 대한 2021년 2월 릴리스 노트입니다.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 2월 24일**

Adobe Experience Platform의 새로운 기능:

- [(베타) 대시보드](#dashboards)

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (베타) 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 정보를 볼 수 있는 여러 개의 대시보드를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필, 세그먼트, 대상 및 라이선스 사용 대시보드(베타) | **참고: 대시보드 기능은 현재 베타에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.**<br/><br/>&#x200B;대시보드는 조직의 데이터에 대한 기본 보고를 제공하며 Platform 내의 마케터 워크플로우에 직접 빌드됩니다. 이러한 대시보드는 추가 IT 지원이 필요하거나 추가적인 데이터 웨어하우징 설계 및 구현을 통해 데이터를 내보내고 처리하는 데 소요되는 시간과 노력 없이 사용할 수 있습니다. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace는 기계 학습 및 인공 지능을 사용하여 데이터를 통해 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace을 사용하면 Adobe 솔루션에서 컨텐츠 및 데이터 자산을 사용하여 예측을 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| JupiterLab EDA 노트북 | 이제 Jupiterlab에서 EDA(예비 데이터 분석) Python 노트북을 사용할 수 있습니다. 이 노트북은 데이터의 패턴을 발견하고, 데이터 안정성을 확인하고, 예측 모델에 대한 관련 데이터를 요약하는 데 도움을 주기 위해 설계되었습니다. 다음에서 자습서를 참조하십시오. [예측 모델을 위한 웹 기반 데이터 탐색](../../data-science-workspace/jupyterlab/eda-notebook.md) 추가 정보. |

Data Science Workspace에 대한 일반적인 정보는 [Data Science Workspace 개요](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. 플랫폼 을 사용하면 데이터 흐름에 투명성을 제공하여 비선형 이외의 데이터 흐름을 쉽게 추적할 수 있습니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 다양한 서비스에 걸쳐 구성되어 있으므로, 소스 커넥터에서 대상 데이터 세트로 데이터를 이동한 다음 이 데이터 흐름을 사용 [!DNL Identity Service] 및 [!DNL Real-time Customer Profile] 궁극적으로 [!DNL Destinations].

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 대시보드 모니터링 | 이제 소스 데이터 수집을 위해 모니터링 대시보드를 사용하여 서비스 간 투명성 및 실행 가능한 통찰력을 사용할 수 있습니다. 새로운 모니터링 대시보드는 에서 처리된 데이터에 대한 포괄적인 보기를 제공합니다 [!DNL Data Lake] to [!DNL Identity Service] 및 [!DNL Profile]를 사용하여 수집 비율, 성공 및 실패를 모니터링할 수도 있습니다. 다음에서 자습서를 참조하십시오. [UI에서 소스 데이터 흐름 모니터링](../../dataflows/ui/monitor-sources.md) 추가 정보. |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 다음 [!DNL LinkedIn Matched Audiences] 연결을 통해 에서 대상을 활성화할 수 있습니다. [!DNL LinkedIn] 소셜 플랫폼. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

표준화와 상호 운용성은 이면의 주요 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe 기반의 XDM(Customer Experience Management)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력입니다.

XDM은 디지털 경험의 힘을 향상시키기 위해 설계된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 애플리케이션에 대한 공통 구조 및 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 공통 표현에 통합할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 업그레이드된 검색 UI | 이제 향상된 검색 기능을 [!UICONTROL 찾아보기] 탭에서 다음을 수행합니다. [!UICONTROL 스키마] 작업 공간 및 스키마 필드 그룹 선택 대화 상자의 [!DNL Schema Editor].<br><br>이전에 검색어를 검색할 때 검색 쿼리와 이름이 일치하는 XDM 리소스만 포함됩니다. 이제 이름이 쿼리와 일치하는 리소스 외에 해당 용어와 일치하는 개별 속성이 포함된 리소스도 포함됩니다. 이렇게 하면 리소스 이름이 아닌 해당 속성이 포함된 XDM 리소스를 검색할 수 있습니다.<br><br>다음 문서를 참조하십시오. [xdm 리소스 탐색](../../xdm/ui/explore.md) 및 [스키마 관리](../../xdm/ui/resources/schemas.md) ( UI에서)를 참조하십시오. |

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 개별 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform [!DNL Identity Service] 은 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 고객의 행동을 더 잘 파악할 수 있도록 지원하고 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있도록 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 뷰어 | ID 그래프 뷰어를 사용하면 UI에서 함께 결합되는 ID의 유효성을 확인하고 시각화할 수 있으므로 디버깅과 투명성을 향상시킬 수 있습니다. 자세한 내용은 [id 그래프 뷰어 문서](../../identity-service/ui/identity-graph-viewer.md) 추가 정보. |

자세한 내용은 [!DNL Identity Service]를 참조하려면 [ID 서비스 개요](../../identity-service/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. [!DNL Profile] 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계산된 속성(알파) | ***참고: 이 기능은 현재 알파 상태이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.*** <br/><br/>계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 그런 다음 세그먼테이션, 활성화 및 개인화에서 합계를 사용할 수 있습니다. 이러한 함수의 일부 예에는 count, sum, average, min, max, true/false가 있습니다. 현재 계산된 속성은 API를 통해서만 사용할 수 있습니다. 자세한 내용은 [계산된 속성 개요](../../profile/computed-attributes/overview.md). |

작업 시 유용한 자습서 및 우수 사례를 비롯하여 실시간 고객 프로필에 대한 자세한 정보 [!DNL Profile] 데이터 읽기 [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub] | 이제 연결할 수 있습니다 [!DNL Google PubSub] to [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI입니다. 자세한 내용은 [[!DNL Google PubSub] 커넥터 개요](../../sources/connectors/cloud-storage/google-pubsub.md) 추가 정보. |
| [!DNL Oracle Object Storage] | 이제 연결할 수 있습니다 [!DNL Oracle Object Storage] to [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI입니다. 자세한 내용은 [[!DNL Oracle Object Storage] 커넥터 개요](../../sources/connectors/cloud-storage/oracle-object-storage.md) 추가 정보. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).
