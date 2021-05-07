---
title: Adobe Experience Platform 릴리스 정보
description: 2021년 2월 24일자 Experience Platform 릴리스 노트
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 7%

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

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 조직의 데이터에 대한 중요한 정보를 볼 수 있는 여러 개의 대시보드를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필, 세그먼트, 대상 및 라이센스 사용 대시보드(베타) | **참고:대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.**<br/><br/>&#x200B;대시보드는 조직의 데이터에 대한 즉시 보고를 제공하며 Platform의 마케터 워크플로우에 직접 구축됩니다. 이러한 대시보드는 추가 IT 지원이 필요하거나 추가 데이터 웨어하우징 설계 및 구현을 통해 데이터를 내보내고 처리하는 데 소요되는 시간 및 노력 없이도 사용할 수 있습니다. |

## [!DNL Data Science Workspace] {#dsw}

데이터 과학 작업 공간은 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace를 사용하면 Adobe 솔루션에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| JupiterLab EDA 노트북 | Jupiterlab에서는 EDA(Survey Data Analysis) Python 노트북을 사용할 수 있습니다. 이 노트북은 데이터에서 패턴을 찾고, 데이터 안정성을 확인하고, 예측 모델에 대한 관련 데이터를 요약하는 데 도움이 되도록 설계되었습니다. 자세한 내용은 [예측 모델에 대한 웹 기반 데이터 탐색](../../data-science-workspace/jupyterlab/eda-notebook.md)의 자습서를 참조하십시오. |

데이터 과학 작업 공간에 대한 자세한 내용은 [데이터 과학 작업 공간 개요](../../data-science-workspace/home.md)를 참조하십시오.

## [!DNL Dataflows] {#dataflows}

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. Platform(플래시 플랫폼)을 사용하면 데이터 흐름 투명도를 활용하여 잠재적으로 선형 방식으로 데이터 흐름을 보다 손쉽게 추적할 수 있습니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 이동시키고, 이 데이터 흐름은 [!DNL Identity Service] 및 [!DNL Real-time Customer Profile]에서 활용하여 궁극적으로 [!DNL Destinations]로 활성화됩니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 모니터링 대시보드 | 이제 모니터링 대시보드를 사용하여 소스 데이터 가져오기 작업을 위한 크로스 서비스 투명도와 실행 가능한 통찰력을 얻을 수 있습니다. 새로운 모니터링 대시보드에서는 처리 속도, 성공 및 실패를 모니터링할 수 있는 동시에 [!DNL Data Lake]에서 [!DNL Identity Service] 및 [!DNL Profile]로 처리된 데이터를 포괄적으로 볼 수 있습니다. 자세한 내용은 UI](../../dataflows/ui/monitor-sources.md)에서 소스 데이터 흐름 모니터링에 대한 자습서를 참조하십시오.[ |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md)를 참조하십시오.

## [!DNL Destinations] {#destinations}

[!DNL Destinations] Adobe Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 여러 가지 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | [!DNL LinkedIn Matched Audiences] 연결을 사용하면 [!DNL LinkedIn] 소셜 플랫폼에서 대상을 활성화할 수 있습니다. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## [!DNL Experience Data Model (XDM) System] {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 주요 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 일반적인 표현 방식으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 고객 속성을 개인화를 위해 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 검색 UI 업그레이드 | 이제 [!UICONTROL Schemas] 작업 영역의 [!UICONTROL Browse] 탭과 [!DNL Schema Editor]의 스키마 필드 그룹 선택 대화 상자에서 향상된 검색 기능을 사용할 수 있습니다.<br><br>이전에 검색어를 검색할 때 검색 쿼리와 이름이 일치하는 XDM 리소스만 결과에 포함됩니다. 이제 쿼리와 이름이 일치하는 리소스 외에도 용어와 일치하는 개별 속성이 포함된 리소스도 포함됩니다. 따라서 리소스 이름이 아닌 XDM 리소스를 포함하는 특성을 기준으로 검색할 수 있습니다.<br><br>자세한 내용은 XDM 리소스  [탐색 ](../../xdm/ui/explore.md) 및 UI [의 구성 ](../../xdm/ui/resources/schemas.md) 관리에 대한 문서를 참조하십시오. |

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## [!DNL Identity Service] {#identity}

고객의 기대에 부응하는 디지털 경험을 제공하려면 고객을 완벽하게 이해해야 합니다. 고객 데이터가 서로 다른 시스템에서 단편화되어 있는 경우 이를 더욱 어렵게 만들 수 있으므로, 개별 고객은 여러 개의 &quot;ID&quot;를 갖고 있는 것처럼 보입니다.

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스 및 시스템 전반에 걸쳐 ID를 연결함으로써 효과적이고 개인화된 디지털 경험을 실시간으로 전달할 수 있으므로 고객의 행동과 행동을 보다 정확하게 파악할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 뷰어 | ID 그래프 뷰어를 사용하면 UI에서 서로 연결된 ID의 유효성을 확인하고 시각화하여 디버깅과 투명도를 개선할 수 있습니다. 자세한 내용은 [ID 그래프 뷰어 문서](../../identity-service/ui/identity-graph-viewer.md)를 참조하십시오. |

[!DNL Identity Service]에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소 또는 시기와 상관없이 고객의 관심사와 연관성 있는 경험을 일관되게 전달할 수 있습니다. 실시간 고객 프로파일을 사용하면 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 다양한 채널의 데이터를 취합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Profile] 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계산된 속성(알파) | ***참고:이 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.*** <br/><br/>계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 그런 다음 세그먼트를 세분화, 활성화 및 개인화에서 집계물을 사용할 수 있습니다. 이러한 함수의 일부 예에는 count, sum, average, min, max, true/false가 있습니다. 계산된 속성은 현재 API를 통해서만 사용할 수 있습니다. 자세한 내용은 [계산된 특성 개요](../../profile/computed-attributes/overview.md)를 참조하십시오. |

[!DNL Profile] 데이터 작업에 대한 자습서 및 모범 사례를 포함하여 실시간 고객 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 읽으십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 한편, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Google PubSub]을 [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Google PubSub] 커넥터 개요](../../sources/connectors/cloud-storage/google-pubsub.md)를 참조하십시오. |
| [!DNL Oracle Object Storage] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Oracle Object Storage]을 [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Oracle Object Storage] 커넥터 개요](../../sources/connectors/cloud-storage/oracle-object-storage.md)를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
