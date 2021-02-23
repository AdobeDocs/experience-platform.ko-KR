---
title: Adobe Experience Platform 릴리스 노트
description: 2021년 2월 24일자 Experience Platform 릴리스 노트
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 9f7d7ae9c721d1ce7abf0dc7d3eaff18eed09d6f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 8%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 2월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 흐름](#dataflows)
- [경험 데이터 모델(XDM) 시스템](#xdm)
- [ID 서비스](#identity)
- [소스](#sources)

## 데이터 흐름 {#dataflows}

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. Platform(플래시 플랫폼)을 사용하면 데이터 흐름 투명도를 활용하여 잠재적으로 선형 방식으로 데이터 흐름을 보다 손쉽게 추적할 수 있습니다.

데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 이동시키고, 이 데이터 흐름은 [!DNL Identity Service] 및 [!DNL Real-time Customer Profile]에서 활용하여 궁극적으로 [!DNL Destinations]로 활성화됩니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 모니터링 대시보드 | 이제 모니터링 대시보드를 사용하여 소스 데이터 가져오기 작업을 위한 크로스 서비스 투명도와 실행 가능한 통찰력을 얻을 수 있습니다. 새로운 모니터링 대시보드에서는 처리 속도, 성공 및 실패를 모니터링할 수 있는 동시에 [!DNL Data Lake]에서 [!DNL Identity Service] 및 [!DNL Profile]로 처리된 데이터를 포괄적으로 볼 수 있습니다. 자세한 내용은 UI](../../dataflows/ui/monitor-sources.md)에서 소스 데이터 흐름 모니터링에 대한 자습서를 참조하십시오.[ |

데이터 흐름에 대한 자세한 내용은 [데이터 흐름 개요](../../dataflows/home.md)를 참조하십시오.

## 경험 데이터 모델(XDM) 시스템 {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 주요 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 일반적인 표현 방식으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 고객 속성을 개인화를 위해 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 검색 UI 업그레이드 | 이제 [!UICONTROL 스키마] 작업 영역의 [!UICONTROL 찾아보기] 탭과 [!DNL Schema Editor]의 혼합 선택 대화 상자에서 향상된 검색 기능을 사용할 수 있습니다.<br><br>이전에 검색어를 검색할 때 검색 쿼리와 이름이 일치하는 XDM 리소스만 결과에 포함됩니다. 이제 쿼리와 이름이 일치하는 리소스 외에도 용어와 일치하는 개별 속성이 포함된 리소스도 포함됩니다. 따라서 리소스 이름이 아닌 XDM 리소스를 포함하는 특성을 기준으로 검색할 수 있습니다.<br><br>자세한 내용은 XDM 리소스  [탐색 ](../../xdm/ui/explore.md) 및 UI [의 구성 ](../../xdm/ui/resources/schemas.md) 관리에 대한 문서를 참조하십시오. |

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## ID 서비스 {#identity}

고객의 기대에 부응하는 디지털 경험을 제공하려면 고객을 완벽하게 이해해야 합니다. 고객 데이터가 서로 다른 시스템에서 단편화되어 있는 경우 이를 더욱 어렵게 만들 수 있으므로, 개별 고객은 여러 개의 &quot;ID&quot;를 갖고 있는 것처럼 보입니다.

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스 및 시스템 전반에 걸쳐 ID를 연결함으로써 효과적이고 개인화된 디지털 경험을 실시간으로 전달할 수 있으므로 고객의 행동과 행동을 보다 정확하게 파악할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 뷰어 | ID 그래프 뷰어를 사용하면 UI에서 서로 연결된 ID의 유효성을 확인하고 시각화하여 디버깅과 투명도를 개선할 수 있습니다. 자세한 내용은 [ID 그래프 뷰어 문서](../../identity-service/ui/identity-graph-viewer.md)를 참조하십시오. |

[!DNL Identity Service]에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 한편, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Google PubSub]을 [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Google PubSub] 커넥터 개요](../../sources/connectors/cloud-storage/google-pubsub.md)를 참조하십시오. |
| [!DNL Oracle Object Storage] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Oracle Object Storage]을 [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [[!DNL Oracle Object Storage] 커넥터 개요](../../sources/connectors/cloud-storage/oracle-object-storage.md)를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
