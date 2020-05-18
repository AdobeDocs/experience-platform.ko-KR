---
title: Adobe Experience Platform 릴리스 정보
description: 2020년 5월 13일 경험 플랫폼 릴리스 노트
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: d41952e5905d4ebc579a29ad3282a8f732b7c331
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 5%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 5월 13일**

Adobe Experience Platform의 기존 기능 업데이트:

- [Adobe Experience Platform 릴리스 노트](#adobe-experience-platform-release-notes)
   - [사용자 인터페이스 업데이트 {#ux}](#user-interface-updates-ux)
   - [데이터 과학 작업 공간 {#dsw}](#data-science-workspace-dsw)
   - [대상 {#destinations}](#destinations-destinations)
   - [경험 플랫폼 웹 SDK 및 경험 플랫폼 에지 네트워크 {#edge}](#experience-platform-web-sdk-and-experience-platform-edge-network-edge)
   - [소스 {#sources}](#sources-sources)

## 사용자 인터페이스 업데이트 {#ux}

Adobe Experience Platform은 경험을 향상시키고 다른 Experience Cloud 애플리케이션과 통합할 수 있도록 도메인 및 헤더 막대에 대한 업데이트를 출시하고 있습니다.

- 조직 간 또는 다른 애플리케이션으로 쉽게 전환할 수 있습니다
- 도움말 메뉴의 주요 아티클 및 컨텍스트 관련 설명서를 비롯한 향상된 사용자 도움말
- 경험 플랫폼 및 파일 지원 티켓에 대한 피드백 제공

새로운 경험에서 점차 벗어나고 있다. https://experience.adobe.com/platform에서 경험을 볼 수 [있습니다](https://experience.adobe.com/platform).

## 데이터 과학 작업 공간 {#dsw}

Data Science Workspace는 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 도출합니다. Adobe Experience Platform에 통합된 데이터 과학 작업 공간을 사용하면 Adobe 솔루션 전체에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 있습니다. Data Science Workspace는 JupiterLab을 사용하여 이를 실현하고 있습니다. JupiterLab은 Project Jupiter를 위한 웹 기반 사용자 <a href="https://jupyter.org/" target="_blank">인터페이스로</a> Adobe Experience Platform과 긴밀하게 통합되어 있습니다. 데이터 과학자들이 Jupiter 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 인터랙티브한 개발 환경을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| JupiterLab Launcher | 이제 JupiterLab Launcher에는 Spark 2.4 노트북의 초보자 기능이 포함되어 있습니다. Spark 2.3 노트북 시작하기 사용자는 이제 더 이상 사용되지 않는 것으로 표시되며 이후 릴리스에서 제거되도록 설정됩니다. |
| Spark 2.4 | New Scala(Spark) 및 PySpark 레시피는 Spark 2.4를 사용합니다. |
| 커널 | Scala(Spark) 노트북은 이제 Scala 커널을 통해 제작됩니다. PySpark 노트북이 Python 커널을 통해 제작되었습니다. Spark 및 PySpark 커널은 더 이상 사용되지 않으며 이후 릴리스에서 제거되도록 설정됩니다. |
| 레서피 | 새로운 PySpark 및 Spark 레시피가 Python 및 R 레시피와 유사한 Docker 워크플로우를 따릅니다. |

Spark 2.4 사용을 위한 노트북 및 레시피 마이그레이션에 대한 자세한 내용은 [노트북 마이그레이션 가이드를 참조하십시오](../../data-science-workspace/recipe-notebook-migration.md). 데이터 과학 작업 공간에 대한 자세한 내용은 [개요 설명서를 참조하십시오](../../data-science-workspace/home.md).

## 대상 {#destinations}

실시간 고객 데이터 플랫폼 [](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로, 해당 파트너에게 데이터를 원활하게 활성화할 수 있습니다.

**Facebook**

Adobe 실시간 CDP는 이제 Facebook에 대한 데이터 활성화를 지원하므로 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로파일을 활성화할 수 있습니다.

새 기능에 대한 자세한 내용은 [Facebook 대상](/help/rtcdp/destinations/facebook-destination.md) 페이지를 참조하십시오.

<br> 

**Amazon Kinesis 및 Azure 이벤트 허브 스트리밍 클라우드 스토리지 대상**

이제 Adobe 실시간 CDP는 스트리밍 클라우드 스토리지 대상에 대한 데이터 활성화를 지원하므로 JSON 포맷으로 대상 데이터와 이벤트를 이러한 대상으로 내보낼 수 있습니다. 그런 다음 대상에 있는 이러한 이벤트 위에 비즈니스 논리를 설명할 수 있습니다. 자세한 내용은 아래를 참조하십시오.

>[!NOTE]
>
>Adobe Real-time CDP의 [!DNL Amazon Kinesis] 대상 및 [!DNL Azure Event Hubs] 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

| 설명서 | 설명 |
|--- | ---|
| [(베타) Amazon Kinesis 대상](/help/rtcdp/destinations/amazon-kinesis-destination.md) | 이 문서에서는 Adobe Experience Platform에서 데이터를 스트리밍하기 위해 스토리지에 대한 실시간 아웃바운드 연결을 만드는 방법에 대해 설명합니다. [!DNL Amazon Kinesis] |
| [(베타) Azure 이벤트 허브 대상](/help/rtcdp/destinations/azure-event-hubs-destination.md) | 이 문서에서는 Adobe Experience Platform에서 데이터를 스트리밍하기 위해 스토리지에 대한 실시간 아웃바운드 연결을 만드는 방법에 대해 설명합니다. [!DNL Azure Event Hubs] |
| [API 자습서 - 스트리밍 대상에 연결 및 데이터 활성화](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md) | 이 자습서에서는 API 호출을 사용하여 Adobe Experience Platform 데이터에 연결하고, 스트리밍 클라우드 스토리지 대상(Amazon Kinesis 또는 Azure 이벤트 허브)에 연결을 만들고, 데이터 흐름을 새로 만든 대상에 만들고, 데이터를 새로 만든 대상에 활성화하는 방법을 설명합니다. |

자세한 내용은 대상 [개요를 참조하십시오](/help/rtcdp/destinations/destinations-overview.md).

## 경험 플랫폼 웹 SDK 및 경험 플랫폼 에지 네트워크 {#edge}

Experience Platform 웹 SDK 및 Experience Platform Edge Network를 사용하면 최종 사용자 디바이스 및 브라우저를 위해 Adobe Experience Platform과 기타 Adobe 솔루션으로 데이터를 실시간으로 전송할 수 있습니다. 최신 활용 사례 목록은 자주 업데이트되는 [공개 로드맵에](https://github.com/adobe/alloy/projects/5) 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| ECID 지원 | SDK는 설치할 추가 라이브러리 또는 정보 없이 즉시 사용 가능한 ECID를 지원합니다 |
| 구성 UI | Launch의 새로운 Edge 구성 UI를 사용하여 구성 ID 설정을 관리합니다. 액세스하려면 허용 목록에 포함되어야 합니다. |
| Adobe Experience Platform 웹 SDK Mixin | 지원되는 모든 필드를 포함하는 Experience Platform 웹 SDK와 함께 사용할 수 있는 믹스인입니다. |
| 강좌 동의 제어 | Experience Platform 웹 SDK의 옵트인 및 옵트아웃을 제어하는 회사 |
| 새로운 Experience Cloud Debugger 확장의 클라이언트측 디버깅 지원 | Experience Platform 웹 SDK의 요청과 Edge Traces를 참조하여 데이터를 통해 시스템을 어떻게 전달하는지 확인하십시오. |
| Adobe Analytics | 에지 구성을 통해 데이터를 Analytics 보고서 세트로 보냅니다. XDM은 컨텍스트 데이터로 분리되며 다중 세트 태그 지정 지원 |
| Adobe Target | Adobe Target 지원. VEC, 양식 기반 컴포저, A/B, XT, 자동화된 개인화, MVT 포함 |
| Adobe Audience Manager 지원 | Audience Manager ID 동기화, URL 대상 및 쿠키 대상 지원 |
| ID 동기화 | 더 명확하게 하기 `setCustomersIds` 로 `syncIdentity` 이름 변경 |
| XDM 개체 빌더 | 론치 익스텐션에서 이제 XDM 개체를 데이터 요소로 만들 수 있습니다 |

플랫폼 웹 SDK 및 에지 네트워크에 대한 자세한 내용은 [설명서를 참조하십시오](../../edge/home.md).

## 소스 {#sources}

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 인제스트할 수 있으며, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

경험 플랫폼은 다양한 데이터 제공업체의 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 클라우드 스토리지 시스템에 대한 추가 API 및 UI 지원 | Azure 파일 저장소의 새 소스 커넥터를 사용합니다. |
| 데이터베이스에 대한 추가 API 및 UI 지원 | Azure 데이터 탐색기, IBM DB2 및 Oracle DB에 대한 새 소스 커넥터입니다. |
| Adobe Audience Manager에서 경험 플랫폼 데이터 공유 | Audience Manager 커넥터에 대한 프로비저닝 프로세스가 업데이트되었습니다. 이제 실시간 고객 프로필에 대한 Audience Manager 데이터 세트를 기본적으로 사용할 수 없습니다. 프로필로 승격할 데이터 세트를 수동으로 선택할 수 있습니다. 새 기본 설정은 소급 적용되지 않으며 새 Audience Manager 커넥터에 대한 프로비저닝에만 영향을 줍니다. 데이터 집합 사용자 안내서에서 자세한 [내용을 참조하십시오](../../catalog/datasets/user-guide.md). |

**알려진 문제**

- 없음

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).