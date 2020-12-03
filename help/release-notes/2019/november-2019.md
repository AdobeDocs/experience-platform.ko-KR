---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 2%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 11월 18일**

Adobe Experience Platform의 새로운 기능:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

기존 기능 업데이트:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

실시간 CDP(Customer Data Platform)는 Adobe Experience Platform을 기반으로 구축된 실시간 고객 데이터 플랫폼(Real-time CDP)을 통해 알려져 있지 않은 데이터를 통합하여 고객 여정 전반에서 지능적인 의사 결정을 통해 고객 프로파일을 활성화할 수 있도록 지원합니다. 실시간 CDP는 여러 엔터프라이즈 데이터 소스를 통합하여 실시간으로 통합 프로파일을 생성하므로 모든 채널과 디바이스에서 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.

[!DNL Real-time Customer Data Platform] 엄격한 데이터 거버넌스 정책을 적용하면서 프로파일을 구축하고 고객을 정의할 수 있을 뿐만 아니라 풍부한 통찰력을 도출해낼 수 있도록 데이터 거버넌스, ID 관리, 고급 세분화 및 데이터 과학을 위한 툴이 포함되어 있습니다.

Adobe은 Adobe Experience Cloud와의 기본 통합은 물론 광범위한 파트너 에코시스템에 연결되므로 이러한 고객을 원활하게 활성화할 수 있고 온사이트 또는 인앱 개인화에서 이메일, 유료 미디어, 콜센터, 연결된 디바이스 등 모든 채널에서 탁월한 고객 경험을 전달할 수 있습니다.

실시간 CDP를 통해 가능한 작업

* 전사적으로 고객 데이터를 스트리밍하여 고객의 전체 상황을 파악할 수 있습니다.
* 알려진 식별자와 알 수 없는 식별자에 대한 신뢰할 수 있는 거버넌스 및 개인 정보 제어 기능을 사용하여 프로파일을 책임감 있게 관리할 수 있습니다.
* 마케터를 위해 마련된 Adobe Sensei 기반의 AI 및 머신 러닝을 통해 실행 가능한 인사이트를 생성하고 고객의 규모를 확장할 수 있습니다.
* 모든 채널과 대상을 통해 개인화된 경험을 실시간으로 제공할 수 있습니다.

자세한 내용은 [실시간 고객 데이터 플랫폼 설명서를 참조하십시오](../../rtcdp/overview.md).

**주요 기능**

| 기능 | 설명 |
|---|---|
| 대상 | Adobe이 지원하는 대상 플랫폼과의 사전 구축된 통합 기능을 통해 해당 파트너 [!DNL Real-time Customer Data Platform] 에게 데이터를 원활하게 제공할 수 있습니다. See [Destinations](#destinations) below for more information. |
| 홈 페이지 지표 대시보드 | 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지에는 프로필 및 세그먼트에 대한 정보를 보여주는 지표 대시보드가 포함되어 있습니다. 홈 페이지에는 학습 자료에 대한 링크도 포함되어 있습니다. 아래의 [실시간 고객 데이터 플랫폼 지표에](#real-time-customer-data-platform-metrics) 대한 섹션을 참조하십시오. |
| 소스 | Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다. 자세한 내용은 아래 [소스](#sources) 섹션을 참조하십시오. |

**[!DNL Real-time Customer Data Platform]지표**

측정 지표 대시보드가 포함된 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지는 실시간 CDP에 로그인할 때 나타납니다.

홈 페이지는 지표 카드가 표시되는 곳 중 하나입니다. 실시간 CDP는 고객 경험 전반에서 측정 카드를 제공합니다. 이러한 지표는 시스템의 데이터, 프로필 및 세그먼트 대상에 대해 알려줍니다.

실시간 CDP에 로그인할 때 시스템에 데이터가 없으면 홈 페이지의 대시보드가 나타나지 않습니다. 이 경우 홈 페이지에서 처음 사용자 경험을 위한 학습 자료를 제공합니다. 데이터가 수집되면 대시보드는 자동으로 업데이트되어 해당 데이터에 대한 정보를 표시합니다.

자세한 내용은 [실시간 고객 데이터 플랫폼 지표 개요를 참조하십시오](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] adobe의 실시간 고객 데이터 플랫폼에서 지원하는 대상 플랫폼과의 사전 구축된 통합으로, 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다. 자세한 내용은 [대상 개요](../../destinations/home.md) 문서를 참조하십시오.

**사용 가능한 대상**

11월 릴리스에서는 Adobe의 실시간 고객 데이터 플랫폼이 다음과 같은 대상을 지원합니다.

* 광고: [!DNL Google]
* 이메일 마케팅:Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys][!DNL Oracle Eloqua]

각 대상에 대한 자세한 내용은 [대상 카탈로그를](../../destinations/catalog/overview.md) 참조하십시오.

**알려진 제한 사항**

* 초기 릴리스에서는 [활성화 과정](../../destinations/ui/activate-destinations.md#activate-data) (예약 단계)에서 사용자 정의 활성화 일정을 허용하는 컨트롤을 사용할 수 없습니다.
* 현재 대상 구성을 편집하거나 삭제할 수 있는 방법이 없습니다. 이 제한 사항을 해결하려면 [대상 세부 정보 페이지의 오른쪽 위 모서리에 있는 대상을 활성화하거나 비활성화할 수 있습니다](../../destinations/ui/destination-details-page.md).
* 대상 또는 저장소 계정에 연결할 때 현재 계정 세부 사항, 경로 또는 자격 증명을 위한 유효성 검사가 수행되지 않습니다. 올바른 자격 증명을 입력하고 맞춤법 오류나 오타를 다시 확인하십시오.
* 초기 릴리스와 함께 자격 증명 갱신이 이루어지지 않습니다. 계정이 만료되거나 새로 고침이 필요한 경우 새 대상 연결을 만들고 이전에 매핑된 세그먼트를 다시 매핑해야 합니다.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 접속을 통해 스토리지 시스템 및 CRM 서비스에 대한 인증, 통합 실행 시간 설정, 데이터 통합 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 소스 UI | 소스 연결을 만들고, 보고, 관리하기 위한 새로운 사용자 인터페이스입니다. |
| CRM 커넥터를 위한 개선된 워크플로우 | 연결 및 커넥터를 만들고 관리하기 위한 새로운 직관적인 UI 워크플로우 [!DNL Microsoft Dynamics] 를 [!DNL Salesforce] 제공합니다. |
| 클라우드 기반의 스토리지 커넥터 지원 | 이제 커넥터는 클라우드 기반 스토리지에 액세스할 수 있습니다. 새로운 소스에는 FTP/SFTP 서버 [!DNL Amazon S3], [!DNL Azure Blob]및 FTP 서버가 포함됩니다. |

**알려진 문제**

* 클라우드 기반 스토리용 소스 커넥터는 압축된 파일 전송을 지원하지 않습니다.

소스에 대한 자세한 내용은 소스 [개요를 참조하십시오](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 를 사용하면 머신 러닝 모델을 구축 및 운영하여 Adobe 애플리케이션과 타사 시스템에서 데이터 및 컨텐츠에 대한 인사이트를 원활하게 생성할 수 있습니다. [!DNL Data Science Workspace] XDM 데이터 [!DNL Platform] 의 탐색 및 준비 등 종합적인 데이터 과학 라이프사이클과 긴밀하게 통합되어 있으며, CDM 데이터 개발 및 운영 체제에 따라 CMS(Machine Learning Insights)를 통해 자동으로 풍부한 기능을 제공합니다 [!DNL Real-time Customer Profile] .

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| SDK를 사용한 데이터 [!DNL Platform] 액세스 | 사전 빌드된 레서피 및 런처 노트북은 [!DNL Python] 이제 데이터에 액세스하기 위해 [!DNL Platform] SDK를 사용합니다. |
| 샌드박스 지원 | 노트북과 레서피를 개발 또는 프로덕션 샌드박스로 격리하는 기능을 비롯하여 앞으로 출시되는 샌드박스 기능(현재 베타 버전)을 지원합니다. See the [sandboxes overview](../../sandboxes/home.md) for more information. |

자세한 내용은 [데이터 과학 작업 공간 개요를 참조하십시오](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화와 상호 운용성은 그 이면의 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 공개적으로 문서화된 사양입니다. 이 소프트웨어는 Adobe Experience Platform의 서비스와 통신하기 위해 모든 애플리케이션에 대한 공통 구조와 정의를 제공합니다. 모든 고객 경험 데이터는 XDM 표준을 준수하여 보다 빠르고 통합된 방식으로 인사이트를 제공하는 공통 표현에 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고 세그먼트를 통해 고객 고객을 정의하며 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 알림 스키마 | 데이터 수집 프로세스 중에 전송된 알림 데이터를 나타내는 새 스키마입니다. |
| Adobe AdCloud DSP 스키마 | 5개의 새 스키마가 Adobe Advertising Cloud 광고 구매 플랫폼(DSP) 메타데이터를 나타내는 데 추가되었습니다.배치, 캠페인, 패키지, 광고주, 계정. |
| ExperienceEvent 구현 세부 정보 혼합 | 이벤트를 수집하는 데 사용되는 소프트웨어에 대한 정보를 저장할 표준 필드를 추가하는 새로운 ExperienceEvent 믹스입니다. |
| [!DNL Profile Privacy] 믹싱 | 일반적인 아웃아웃 및 영업/공유 옵트아웃 신호를 수락하는 필드를 추가하는 새로운 프로필 믹스입니다 [!DNL Real-time Customer Profile]. |
| 형식 제한 `xdm:alternateDisplayInfo` | 유효성 검사를 통과하려면 &quot;제목&quot; 및 &quot;설명&quot; 필드가 모두 문자열이어야 `xdm:alternateDisplayInfo` 합니다. |
| 이름 변경:XDM [!DNL Individual Profile] | &quot;XDM&quot; [!DNL Profile]클래스의 &quot;title&quot;이 &quot;XDM&quot;으로 [!DNL Individual Profile]업데이트되었습니다. 그 반 `$id` 의 문체는 변하지 않았다. |

**알려진 문제**

* None.

API 및 사용자 인터페이스를 사용하여 XDM을 사용하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] XDM 시스템 설명서를 참조하십시오 [!DNL Schema Editor] [](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 언제 어디에서나 고객의 기대에 부응하는 일관된 경험을 제공할 수 있습니다. 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널의 데이터를 결합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Real-time Customer Profile] [!DNL Profile] 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| 조회 개선 [!DNL Profile] 사항 | 이제 사용자는 참조 설명자 및 관련 엔티티를 사용하여 프로파일을 조회할 수 있습니다. |
| 지정된 데이터 세트에 대한 데이터 정리 | 이제 사용자는 시스템 작업 API를 사용하여 지정된 데이터 세트 또는 일괄 처리에 대한 데이터를 삭제할 수 [!DNL Profile] 있습니다. |
| 향상된 Edge [!DNL Profile] 쿼리 | 이제 응용 프로그램에서 지정된 프로필의 ID [!DNL Profile] 로 Edge를 쿼리할 수 있습니다. |
| 프로젝션별 병합 정책 구성 | 이제 응용 프로그램에서 특정 병합 정책의 적용을 받는 데이터 뷰를 생성하기 위해 프로젝션별 병합 정책을 구성할 수 있습니다. |
| 계산된 속성 | 계산된 속성은 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산합니다. 계산된 속성은 들어오는 이벤트, 들어오는 이벤트 및 프로필 데이터 또는 들어오는 이벤트, 프로필 데이터 및 내역 이벤트를 기반으로 &quot;총 구매&quot;, &quot;라이프타임 값&quot; 또는 &quot;단계 상태&quot;와 같은 값을 집계하기 위해 프로필 수준에서 작동합니다. |

**버그 수정**

* 병합 정책 작성 워크플로우에서 사용 가능한 ID 연결 전략의 간소화된 목록입니다.

**알려진 문제**

* None.

데이터 작업을 위한 자습서 및 모범 사례 [!DNL Real-time Customer Profile]를 비롯한 자세한 내용은 [!DNL Profile] 실시간 고객 프로필 개요를 참조하십시오 [](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 는 세그먼트를 작성하고 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 [!DNL Real-time Customer Profile] 제공합니다. 이러한 세그먼트는 중앙에서 구성 및 관리되므로 모든 Adobe 애플리케이션에서 쉽게 액세스할 수 [!DNL Platform]있습니다.

[!DNL Segmentation Service] 고객 기반 내에서 마케팅 가능한 사람들을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(인구 통계 정보 등) 또는 시간 시리즈 이벤트를 기반으로 할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| 예약된 세그먼테이션 | 이제 사용자는 UI 및 API를 통해 모든 세그먼트에 대해 예약된 세그먼트 평가를 활성화할 수 있습니다. 활성화되면 모든 세그먼트가 하루에 한 번 평가됩니다. 이는 이전에 수행한 대로 계속 작동하는 on-demand 세그멘테이션 기능에는 영향을 주지 않습니다.<br/><br/>참고:5개 이상의 병합 정책이 있는 샌드박스에서 예약된 세그멘테이션 기능을 사용할 수 없습니다 [!DNL XDM Individual Profile]. |
| 스트리밍 세분화 | 세그먼트(스트리밍 세그멘테이션)의 지속적인 평가에 대한 지원을 통해 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 [!DNL Platform]있습니다. 이 기능은 예약된 세그멘테이션 작업을 실행하지 않아도 세그먼트 멤버십이 최신 상태로 유지됨을 의미합니다. 다중 엔티티 관계를 사용하는 세그먼트 또는 강화된 페이로드 포함 등 일부 예외가 적용됩니다. |
| 블록 작성 시 세그먼트 | 세그먼트 빌더 UI를 사용하여 세그먼트를 만들 때 이제 사용자는 추가 세그먼트를 위한 기본 요소로 이전에 정의한 세그먼트를 사용할 수 있습니다. <ul><li>현재 대상 멤버십 참조:사용자가 대상을 드나들 때 업데이트됨</li><li>논리 복사:선택한 세그먼트 정의를 새 세그먼트에서 복제합니다.</li></ul> |
| ID 네임스페이스별 세그먼트 구성원 보기 | 이제 세그먼트 멤버십을 ID 네임스페이스(이메일, ECID 및 총 수)로 볼 수 있습니다. |
| RBAC 지원 | 이제 세그먼트 빌더가 기본 역할 기반 액세스 제어 및 권한을 지원합니다. |
| Adobe 솔루션 간 외부 고객 공유 [!DNL Platform] 지원 강화 | 이제 사용자는 대상자 수가 크거나[!DNL Experience Platform]미알려진 시나리오에서 외부(비-대상) 대상 메타데이터를 가져올 수 있습니다. 이 릴리스에는 솔루션 커넥터를 프로비저닝한 고객의 메타데이터에 대한 액세스 권한이 포함됩니다. [!DNL Audience Manager] 세그먼트 빌더 내에서 이 대상 메타데이터를 사용하여 새 세그먼트를 만들 수 [!DNL Experience Platform] 있습니다. <br/><br/> 또한 에서 생성된 세그먼트 [!DNL Experience Platform] 는 이제 통합 Adobe 솔루션 [!DNL Audience Manager], [!DNL Target]및 [!DNL Ad Cloud]에서 사용할 수 있습니다. |

**버그 수정**

* 중첩된 관계의 경우 다중 엔티티 세그먼테이션이 0개의 프로필을 반환하는 문제를 해결했습니다.
* 제외 로직이 잘못된 결과를 반환하는 문제를 수정했습니다.
* 다중 엔티티 폴더에 대한 가독성 개선 이제 XDM 클래스의 친숙한 이름이 표시됩니다.
* 동일한 XDM 폴더의 여러 복사본이 가끔씩 표시되는 간헐적인 문제가 해결되었습니다.
* 이제 선택한 병합 정책에 대해 세그먼트 추정을 사용할 수 없는 경우 사용자에게 알리기 위해 메시지가 생성됩니다.

**알려진 문제**

* None.

자세한 내용 [!DNL Segmentation Service]은 세그멘테이션 [서비스 개요를 참조하십시오](../../segmentation/home.md).