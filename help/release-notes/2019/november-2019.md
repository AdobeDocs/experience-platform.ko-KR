---
title: Adobe Experience Platform 릴리스 정보
description: 'Experience Platform 릴리스 노트: 2019년 11월 18일'
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 2%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 11월 18일**

Adobe Experience Platform의 새로운 기능:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

기존 기능에 대한 업데이트:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Adobe Experience Platform 기반의 실시간 고객 데이터 플랫폼(실시간 CDP)을 사용하면 알려진 데이터와 알려지지 않은 데이터를 결합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로파일을 활성화할 수 있습니다. 실시간 CDP는 여러 엔터프라이즈 데이터 소스를 통합하여 실시간으로 통합 프로파일을 생성하여 모든 채널과 디바이스에서 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.

[!DNL Real-time Customer Data Platform] 엄격한 데이터 거버넌스 정책을 적용하면서 프로파일을 구축하고 고객을 정의할 수 있을 뿐만 아니라 풍부한 통찰력을 도출해낼 수 있도록 데이터 거버넌스, ID 관리, 고급 세분화 및 데이터 과학을 위한 툴이 포함되어 있습니다.

Adobe은 Adobe Experience Cloud와의 기본 통합은 물론 광범위한 파트너 에코시스템에 연결되므로 이러한 고객을 원활하게 활성화할 수 있고 온사이트 또는 인앱 개인화부터 이메일, 유료 미디어, 콜센터, 연결된 디바이스 등 모든 채널에 탁월한 고객 경험을 전달할 수 있습니다.

실시간 CDP를 통해 가능한 작업

* 전사적으로 고객 데이터를 스트리밍하여 하나의 관점에서 고객을 파악할 수 있습니다.
* 알려진 식별자와 알 수 없는 식별자에 대한 신뢰할 수 있는 거버넌스 및 개인 정보 제어를 사용하여 프로파일을 책임감 있게 관리할 수 있습니다.
* 마케터를 위해 마련된 Adobe Sensei 기반의 AI 및 머신 러닝을 통해 실행 가능한 인사이트를 생성하고 고객의 규모를 확장할 수 있습니다.
* 모든 채널과 대상을 통해 개인화된 경험을 실시간으로 제공

자세한 내용은 [실시간 고객 데이터 플랫폼 설명서](../../rtcdp/overview.md)를 참조하십시오.

**주요 기능**

| 기능 | 설명 |
|---|---|
| 대상 | Adobe의 [!DNL Real-time Customer Data Platform]에서 지원하는 대상 플랫폼과의 사전 구축된 통합으로, 해당 파트너에게 데이터를 원활하게 활성화할 수 있습니다. 자세한 내용은 아래 [대상](#destinations)을 참조하십시오. |
| 홈 페이지 지표 대시보드 | 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지에는 프로필 및 세그먼트에 대한 정보를 보여주는 지표 대시보드가 포함되어 있습니다. 홈 페이지에는 학습 자료에 대한 링크도 포함되어 있습니다. 아래의 [실시간 고객 데이터 플랫폼 지표](#real-time-customer-data-platform-metrics)에 대한 섹션을 참조하십시오. |
| 소스 | Adobe 솔루션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다. 자세한 내용은 아래의 [소스](#sources) 섹션을 참조하십시오. |

**[!DNL Real-time Customer Data Platform]메트릭**

측정 지표 대시보드가 포함된 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지는 실시간 CDP에 로그인할 때 나타납니다.

홈 페이지는 지표 카드가 표시되는 위치 중 하나입니다. 실시간 CDP는 경험 전반에 측정 카드를 제공합니다. 이러한 지표는 시스템의 데이터, 프로필 및 세그먼트 대상에 대해 알려줍니다.

실시간 CDP에 로그인할 때 시스템에 데이터가 없으면 홈 페이지의 대시보드가 나타나지 않습니다. 이 경우 홈 페이지에서 처음 사용자 경험을 위한 학습 자료를 제공합니다. 데이터가 수집되면 대시보드는 자동으로 업데이트되어 해당 데이터에 대한 정보를 표시합니다.

자세한 내용은 [실시간 고객 데이터 플랫폼 지표 개요](../../rtcdp/home-page-dashboards.md)를 참조하십시오.

## [!DNL Destinations] {#destinations}

[!DNL Destinations] Adobe의 실시간 고객 데이터 플랫폼에서 지원되는 대상 플랫폼과의 사전 구축된 통합으로, 해당 파트너에게 데이터를 원활하게 활성화할 수 있습니다. 자세한 내용은 [대상 개요](../../destinations/home.md) 문서를 참조하십시오.

**사용 가능한 대상**

11월 릴리스부터 Adobe의 실시간 고객 데이터 플랫폼은 다음 대상을 지원합니다.

* 광고: [!DNL Google]
* 이메일 마케팅:Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

각 대상에 대한 자세한 내용은 [대상 카탈로그](../../destinations/catalog/overview.md)를 참조하십시오.

**알려진 제한 사항**

* [활성화 흐름](../../destinations/ui/activate-destinations.md#activate-data)(예약 단계)의 사용자 정의 활성화 일정을 허용하는 컨트롤은 초기 릴리스에서 사용할 수 없습니다.
* 현재 대상 구성을 편집하거나 삭제할 방법이 없습니다. 이 제한 사항을 해결하려면 [대상 세부 정보 페이지](../../destinations/ui/destination-details-page.md)의 오른쪽 위 모서리에서 대상을 활성화하거나 비활성화할 수 있습니다.
* 대상 또는 저장소 계정에 연결할 때 현재 계정 세부 사항, 경로 또는 자격 증명을 위한 유효성 검사가 없습니다. 올바른 자격 증명을 입력하고 맞춤법 오류 또는 오타를 다시 확인하십시오.
* 초기 릴리스를 통해 자격 증명을 갱신하지 않습니다. 계정이 만료되거나 새로 고침이 필요한 경우 새 대상 연결을 만들고 이전에 매핑한 세그먼트를 다시 매핑해야 합니다.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 동시에 [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 솔루션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 스토리지 시스템 및 CRM 서비스에 대한 인증, 통합 실행 시간 설정, 데이터 통합 처리량 관리를 수행할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 소스 UI | 소스 연결을 만들고, 보고, 관리하기 위한 새로운 사용자 인터페이스입니다. |
| CRM 커넥터에 대한 개선된 워크플로우 | [!DNL Microsoft Dynamics] 및 [!DNL Salesforce] 커넥터를 만들고 관리하기 위한 새로운 직관적인 UI 작업 과정입니다. |
| 클라우드 기반의 스토리지에 대한 커넥터 지원 | 이제 커넥터는 클라우드 기반 스토리지에 액세스할 수 있습니다. 새 소스에는 [!DNL Amazon S3], [!DNL Azure Blob] 및 FTP/SFTP 서버가 포함됩니다. |

**알려진 문제**

* 클라우드 기반 스토리용 소스 커넥터는 압축된 파일 전송을 지원하지 않습니다.

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]을(를) 사용하면 머신 러닝 모델을 구축 및 운영하여 데이터 과학자는 Adobe 애플리케이션과 제3자 시스템 전반에서 데이터와 컨텐츠의 통찰력을 원활하게 생성할 수 있습니다. [!DNL Data Science Workspace] XDM 데이터 [!DNL Platform] 의 탐색 및 준비 등 종합적인 데이터 과학 라이프사이클과 긴밀하게 통합되어 있으며, XDM 데이터 개발 및 운영 체제를 통해 기계 학습 인사이트를 자동으로  [!DNL Real-time Customer Profile] 강화합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| [!DNL Platform] SDK를 사용한 데이터 액세스 | 이제 [!DNL Python]의 사전 빌드된 레서피 및 런처 노트북에서 데이터를 액세스하기 위해 [!DNL Platform] SDK를 사용합니다. |
| 샌드박스 지원 | 노트북과 레서피를 개발 또는 프로덕션 샌드박스로 분리하는 기능을 포함하여 예정된 샌드박스 기능(현재 베타 버전)을 지원합니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오. |

자세한 내용은 [데이터 과학 작업 공간 개요](../../data-science-workspace/home.md)를 참조하십시오.

## [!DNL Experience Data Model] (XDM) 시스템  {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 주요 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 일반적인 표현 방식으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 고객 속성을 개인화를 위해 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 알림 스키마 | 데이터 수집 프로세스 중에 전송된 알림 데이터를 나타내는 새 스키마입니다. |
| Adobe AdCloud DSP 스키마 | DSP(Adobe Advertising Cloud Demand-Side Platform) 메타데이터를 나타내기 위해 5개의 새 스키마가 추가되었습니다.배치, 캠페인, 패키지, 광고주, 계정. |
| ExperienceEvent 구현 세부 정보 스키마 필드 그룹 | 이벤트를 수집하는 데 사용되는 소프트웨어에 대한 정보를 저장할 표준 필드를 추가하는 새 ExperienceEvent 필드 그룹입니다. |
| [!DNL Profile Privacy] 필드 그룹 | [!DNL Real-time Customer Profile]에 대한 일반적인 옵트아웃 및 영업/공유 옵트아웃 신호를 수락하는 필드를 추가하는 새 프로필 필드 그룹입니다. |
| `xdm:alternateDisplayInfo`에 대한 형식 제약 조건 | 유효성 검사를 전달하려면 `xdm:alternateDisplayInfo`에 대한 &quot;제목&quot; 및 &quot;설명&quot; 필드가 모두 문자열이어야 합니다. |
| 이름 변경:XDM [!DNL Individual Profile] | &quot;XDM [!DNL Profile]&quot; 클래스의 &quot;title&quot;이 &quot;XDM [!DNL Individual Profile]&quot;으로 업데이트되었습니다. 클래스의 형식 `$id`이(가) 변경되지 않았습니다. |

**알려진 문제**

* None.

[!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스를 사용하여 XDM을 사용하는 방법에 대한 자세한 내용은 [XDM 시스템 설명서](../../xdm/home.md)를 참조하십시오.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소 또는 시기와 상관없이 고객의 관심사와 연관성 있는 경험을 일관되게 전달할 수 있습니다. [!DNL Real-time Customer Profile]을 사용하면 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 여러 채널의 데이터를 결합하는 각 개별 고객의 전체 보기를 확인할 수 있습니다. [!DNL Profile] 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| [!DNL Profile] 조회 개선 사항 | 이제 사용자는 참조 설명자 및 관련 엔티티를 사용하여 프로파일을 조회할 수 있습니다. |
| 지정된 데이터 세트에 대한 데이터 정리 | 이제 사용자는 [!DNL Profile] 시스템 작업 API를 사용하여 지정된 데이터 세트 또는 일괄 처리에 대한 데이터를 삭제할 수 있습니다. |
| 가장자리 [!DNL Profile] 쿼리 개선 사항 | 이제 응용 프로그램에서 지정된 프로필의 ID 중 하나에서 가장자리 [!DNL Profile]를 쿼리할 수 있습니다. |
| 프로젝션별 병합 정책 구성 | 이제 애플리케이션은 특정 병합 정책을 통해 제어되는 데이터 뷰를 생성하기 위해 프로젝션별 병합 정책을 구성할 수 있습니다. |
| 계산된 속성 | 계산된 속성은 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산합니다. 계산된 속성은 들어오는 이벤트, 들어오는 이벤트 및 프로필 데이터 또는 들어오는 이벤트, 프로필 데이터 및 내역 이벤트를 기반으로 &quot;총 구매&quot;, &quot;라이프타임 값&quot; 또는 &quot;단계 상태&quot;와 같은 값을 집계하기 위해 프로필 수준에서 작동합니다. |

**버그 수정**

* 병합 정책 만들기 워크플로우에서 사용 가능한 ID 연결 전략의 간소화된 목록입니다.

**알려진 문제**

* 없음.

[!DNL Profile] 데이터 작업에 대한 자습서 및 모범 사례를 포함하여 [!DNL Real-time Customer Profile]에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service]은 세그먼트를 작성하고 [!DNL Real-time Customer Profile] 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 Adobe 응용 프로그램에서 쉽게 액세스할 수 있도록 [!DNL Platform]에 중앙에서 구성 및 유지 관리됩니다.

[!DNL Segmentation Service] 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드 고객과의 상호 작용을 나타내는 레코드 데이터(인구 통계 정보 등) 또는 시간 시리즈 이벤트를 기반으로 할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| 예약된 세그먼테이션 | 이제 사용자는 UI 및 API를 통해 모든 세그먼트에 대해 예약된 세그먼트 평가를 활성화할 수 있습니다. 활성화되면 모든 세그먼트가 하루에 한 번 평가됩니다. 이는 이전에 수행한 대로 계속 작동하는 주문형 세그먼테이션 기능에는 영향을 주지 않습니다.<br/><br/>참고:예약된 세그멘테이션 기능은 5개 이상의 병합 정책이 있는 샌드박스에서 사용할 수 없습니다 [!DNL XDM Individual Profile]. |
| 스트리밍 세분화 | 세그먼트(스트리밍 세그멘테이션)의 지속적인 평가가 지원되므로 데이터가 [!DNL Platform]에 전달될 때 대부분의 세그먼트 규칙을 평가할 수 있습니다. 이 기능은 예약된 세그멘테이션 작업을 실행하지 않고 세그먼트 멤버십이 최신 상태로 유지됨을 의미합니다. 다중 엔티티 관계를 사용하는 세그먼트 또는 강화된 페이로드가 있는 세그먼트와 같은 일부 예외가 적용됩니다. |
| 구성 블록으로 세그먼트 | 세그먼트 빌더 UI를 사용하여 세그먼트를 만들 때 이제 사용자는 추가 세그먼트를 위한 빌드 블록으로 이전에 정의한 세그먼트를 사용할 수 있습니다. <ul><li>현재 대상 멤버십 참조:사용자가 대상 안팎으로 이동할 때 업데이트됨</li><li>논리 복사:선택한 세그먼트 정의를 새 세그먼트에서 복제합니다.</li></ul> |
| ID 네임스페이스별 세그먼트 구성원 자격 보기 | 이제 세그먼트 멤버십을 ID 네임스페이스(이메일, ECID 및 총 개수)로 볼 수 있습니다. |
| RBAC 지원 | 이제 세그먼트 빌더에서 기본 역할 기반 액세스 제어 및 권한을 지원합니다. |
| [!DNL Platform] 및 Adobe 솔루션 간 외부 대상 공유에 대한 지원 향상 | 이제 사용자 개수가 크거나 미알려진 시나리오에서 사용자가 외부(비[!DNL Experience Platform]) 대상 메타데이터를 가져올 수 있습니다. 이 릴리스에는 솔루션 커넥터를 프로비저닝한 고객의 [!DNL Audience Manager] 메타데이터에 대한 액세스가 포함됩니다. 세그먼트 빌더 내에서 이 대상 메타데이터를 사용하여 새 [!DNL Experience Platform] 세그먼트를 만들 수 있습니다. <br/><br/> 또한 에서 만든 세그먼트 [!DNL Experience Platform] 는 이제 통합 Adobe 솔루션에서 사용할 수 있습니다(예:  [!DNL Audience Manager] [!DNL Target],  [!DNL Ad Cloud]포함). |

**버그 수정**

* 중첩된 관계의 경우 다중 엔티티 세그먼테이션이 0개의 프로필을 반환하는 문제를 해결했습니다.
* 제외 로직이 잘못된 결과를 반환하던 문제를 수정했습니다.
* 다중 엔티티 폴더에 대한 가독성 개선. 이제 XDM 클래스의 친숙한 이름이 표시됩니다.
* 동일한 XDM 폴더의 여러 복사본이 간헐적으로 표시되는 문제가 해결되었습니다.
* 이제 선택한 병합 정책에 대해 세그먼트 추정을 사용할 수 없는 경우 사용자에게 알리기 위해 메시징이 생성됩니다.

**알려진 문제**

* 없음.

[!DNL Segmentation Service]에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../../segmentation/home.md)를 참조하십시오.
