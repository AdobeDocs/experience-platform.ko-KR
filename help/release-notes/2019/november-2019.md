---
title: Adobe Experience Platform 릴리스 노트 2019년 11월
description: Adobe Experience Platform에 대한 2019년 11월 릴리스 정보입니다.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 11월 18일**

Adobe Experience Platform의 새로운 기능:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

기존 기능에 대한 업데이트:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Adobe Experience Platform을 기반으로 구축된 Real-time Customer Data Platform(Real-Time CDP)은 기업이 알려진 데이터와 알 수 없는 데이터를 통합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정으로 고객 프로필을 활성화할 수 있도록 지원합니다. Real-Time CDP은 여러 엔터프라이즈 데이터 소스를 결합하여 실시간으로 통합 프로필을 만들어 모든 채널 및 장치에서 일대일 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.

[!DNL Real-Time Customer Data Platform] 에는 데이터 거버넌스, id 관리, 고급 세그먼테이션 및 데이터 과학을 위한 도구가 포함되어 있으므로 프로필을 빌드하고 대상을 정의할 수 있을 뿐만 아니라 엄격한 데이터 거버넌스 정책을 적용할 수 있는 동시에 풍부한 통찰력을 얻을 수 있습니다.

Adobe은 Adobe Experience Cloud과의 기본 통합은 물론 대규모 파트너 에코시스템에 연결되므로 온사이트 또는 인앱 개인화부터 이메일, 유료 미디어, 콜 센터, 연결된 장치 등에 이르기까지 모든 채널에 걸쳐 이러한 대상을 원활하게 활성화하고 우수한 고객 경험을 제공할 수 있습니다.

Real-Time CDP을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 기업 전체에서 고객 데이터의 스트리밍 수집으로 고객에 대한 단일 뷰를 얻을 수 있습니다.
* 신뢰할 수 있는 거버넌스 및 알 수 없는 식별자에 대한 개인 정보 컨트롤을 통해 프로필을 책임 있게 관리합니다.
* Adobe Sensei에서 지원하고 마케터를 위해 구축된 AI 및 머신 러닝을 사용하여 실행 가능한 통찰력을 생성하고 대상을 확장하십시오.
* 모든 채널 및 대상에 걸쳐 실시간으로 개인화된 경험을 제공합니다.

자세한 내용은 [Real-time Customer Data Platform 설명서](../../rtcdp/overview.md).

**주요 기능**

| 기능 | 설명 |
|---|---|
| 대상 | Adobe에서 지원하는 대상 플랫폼과의 사전 구축 통합 [!DNL Real-Time Customer Data Platform] 이를 통해 파트너에게 데이터를 원활하게 제공할 수 있습니다. 다음을 참조하십시오 [대상](#destinations) 자세한 내용은 아래를 참조하십시오. |
| 홈 페이지 지표 대시보드 | Real-time Customer Data Platform(Real-Time CDP) 홈 페이지에는 프로필 및 세그먼트에 대한 정보를 보여주는 지표 대시보드가 있습니다. 홈 페이지에는 학습 자료에 대한 링크도 포함되어 있습니다. 의 섹션을 참조하십시오. [Real-time Customer Data Platform 지표](#real-time-customer-data-platform-metrics) 아래요. |
| 소스 | Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM과 같은 다양한 소스에서 데이터를 수집할 수 있습니다. 다음을 참조하십시오. [소스](#sources) 자세한 내용은 아래 섹션을 참조하십시오. |

**[!DNL Real-Time Customer Data Platform]지표**

Real-Time CDP에 로그인하면 지표 대시보드가 포함된 Real-time Customer Data Platform(Real-Time CDP) 홈 페이지가 표시됩니다.

홈 페이지는 지표 카드가 나타나는 위치 중 하나일 뿐입니다. Real-Time CDP은 환경 전반에 걸쳐 지표 카드를 제공합니다. 이러한 지표는 시스템의 데이터, 프로필 및 세그먼트 대상자에 대해 알려 줍니다.

Real-Time CDP에 로그인할 때 시스템에 데이터가 없는 경우 홈 페이지의 대시보드가 표시되지 않습니다. 이 경우, 홈페이지는 처음 사용자 경험을 위한 학습 자료를 제공한다. 데이터가 수집되면 대시보드가 자동으로 업데이트되어 해당 데이터에 대한 정보를 표시합니다.

자세한 내용은 [Real-time Customer Data Platform 지표 개요](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe의 Real-time Customer Data Platform에서 지원하는 대상 플랫폼과의 사전 구축된 통합으로 이들 파트너에게 데이터를 원활하게 제공할 수 있습니다. 자세한 내용은 [대상 개요](../../destinations/home.md) 기사.

**사용 가능한 대상**

11월 릴리스를 통해 Adobe의 Real-time Customer Data Platform은 다음 대상을 지원합니다.

* Advertising: [!DNL Google]
* 이메일 마케팅: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

다음을 참조하십시오. [대상 카탈로그](../../destinations/catalog/overview.md) 각 대상에 대한 자세한 내용.

**알려진 제한 사항**

* 활성화 플로우(일정 단계)에서 사용자 지정 활성화 일정을 허용하는 컨트롤은 초기 릴리스에서 사용할 수 없습니다.
* 현재 대상 구성을 편집하거나 삭제할 수 있는 방법이 없습니다. 이 제한을 해결하려면 의 오른쪽 상단 모서리에서 대상을 활성화하거나 비활성화합니다. [대상 세부 정보 페이지](../../destinations/ui/destination-details-page.md).
* 대상 또는 저장소 계정에 연결할 때 계정 세부 정보, 경로 또는 자격 증명에 대한 유효성 검사가 현재 적용되지 않습니다. 올바른 자격 증명을 입력하고 맞춤법 오류 또는 오타가 있는지 다시 확인하십시오.
* 초기 릴리스와 함께 자격 증명 갱신이 수행되지 않습니다. 계정이 만료되거나 새로 고침이 필요한 경우 새 대상 연결을 만들고 이전에 매핑된 세그먼트를 다시 매핑해야 합니다.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Platform] 서비스. Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 스토리지 시스템 및 CRM 서비스를 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 소스 UI | 소스 연결 생성, 보기 및 관리를 위한 새로운 사용자 인터페이스입니다. |
| CRM 커넥터용 워크플로우 개선 | 생성 및 관리를 위한 직관적인 새 UI 워크플로 [!DNL Microsoft Dynamics] 및 [!DNL Salesforce] 커넥터. |
| 클라우드 기반 스토리지에 대한 커넥터 지원 | 이제 커넥터가 클라우드 기반 저장소에 액세스할 수 있습니다. 새 소스는 다음과 같습니다. [!DNL Amazon S3], [!DNL Azure Blob]및 FTP/SFTP 서버. |

**알려진 문제**

* 클라우드 기반 스토리지용 소스 커넥터는 압축된 파일의 수집을 지원하지 않습니다.

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 는 머신 러닝 모델을 구축하고 운영하여 데이터 과학자가 Adobe 애플리케이션 및 서드파티 시스템 전반의 데이터와 콘텐츠에서 통찰력을 원활하게 생성할 수 있도록 합니다. [!DNL Data Science Workspace] 와 밀접하게 통합되어 있습니다. [!DNL Platform] 및 는 XDM 데이터 탐색 및 준비, 자동 강화 모델 개발 및 운영을 포함하여 종단간 데이터 과학 라이프사이클을 강화합니다 [!DNL Real-Time Customer Profile] (기계 학습 통찰력 포함)

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 데이터 액세스 [!DNL Platform] SDK | 의 미리 빌드된 레서피 및 런처 노트북 [!DNL Python] 지금 사용 [!DNL Platform] 데이터에 액세스하기 위한 SDK입니다. |
| 샌드박스 지원 | 노트북 및 레서피를 개발 또는 프로덕션 샌드박스로 분리하는 기능을 포함하여 예정된 샌드박스 기능(현재 베타 버전)을 지원합니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오. |

자세한 내용은 [데이터 과학 작업 영역 개요](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화 및 상호 운용성은 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe을 기반으로 하는 (XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 알림 스키마 | 데이터 수집 프로세스 중에 전송된 알림 데이터를 나타내는 새 스키마. |
| AdCloud DSP 스키마 Adobe | Adobe Advertising Cloud 수요 측 플랫폼(DSP) 메타데이터를 나타내는 5개의 새 스키마(배치, 캠페인, 패키지, 광고주, 계정)가 추가되었습니다. |
| ExperienceEvent 구현 세부 사항 스키마 필드 그룹 | 새 ExperienceEvent 필드 그룹은 이벤트를 수집하는 데 사용되는 소프트웨어에 대한 정보를 저장하는 표준 필드를 추가합니다. |
| [!DNL Profile Privacy] 필드 그룹 | 일반 옵트아웃 및 판매/공유 옵트아웃 신호를 수락하기 위한 필드를 추가하는 새 프로필 필드 그룹 [!DNL Real-Time Customer Profile]. |
| 다음에 대한 형식 제한 `xdm:alternateDisplayInfo` | 의 &quot;제목&quot; 및 &quot;설명&quot; 필드 `xdm:alternateDisplayInfo` 유효성 검사를 통과하려면 둘 다 문자열이어야 합니다. |
| 이름 변경: XDM [!DNL Individual Profile] | &quot;XDM&quot;의 &quot;title&quot; [!DNL Profile]&quot; 클래스가 &quot;XDM&quot;으로 업데이트되었습니다. [!DNL Individual Profile]&quot;. 형식 `$id` 의 클래스는 변경되지 않았습니다. |

**알려진 문제**

* None.

를 사용하여 XDM 작업에 대해 자세히 알아보려면 [!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스입니다. [XDM 시스템 설명서](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 포함 [!DNL Real-Time Customer Profile]에서는 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile] 에서는 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 다양한 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| 개선 사항 [!DNL Profile] 조회 | 이제 사용자는 참조 설명자 및 관련 엔티티를 사용하여 프로필을 조회할 수 있습니다. |
| 주어진 데이터 세트에 대한 데이터 정리 | 이제 사용자는 다음을 사용하여 주어진 데이터 세트 또는 배치에 대한 데이터를 삭제할 수 있습니다. [!DNL Profile] 시스템 작업 API. |
| Edge [!DNL Profile] 쿼리 개선 사항 | 이제 애플리케이션에서 Edge를 쿼리할 수 있습니다. [!DNL Profile] (특정 프로필의 id에 해당) |
| 프로젝트별 병합 정책 구성 | 이제 애플리케이션은 특정 병합 정책이 제어하는 데이터 보기를 생성하기 위해 프로젝트별로 병합 정책을 구성할 수 있습니다. |
| 계산된 속성 | 계산된 속성은 다른 값, 계산 및 표현식을 기반으로 필드 값을 자동으로 계산합니다. 계산된 속성은 프로필 수준에서 작동하여 수신 이벤트, 수신 이벤트 및 프로필 데이터 또는 수신 이벤트, 프로필 데이터 및 이전 이벤트를 기반으로 &quot;총 구매&quot;, &quot;라이프타임 값&quot; 또는 &quot;단계 상태&quot;와 같은 값을 집계합니다. |

**버그 수정**

* 병합 정책 생성 워크플로우에서 사용할 수 있는 ID 결합 전략의 간소화된 목록입니다.

**알려진 문제**

* None.

에 대한 자세한 내용 [!DNL Real-Time Customer Profile]를 사용하여 작업하기 위한 자습서 및 모범 사례를 포함 [!DNL Profile] 데이터, 다음을 읽으십시오. [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 는 세그먼트를 작성하고 에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. [!DNL Real-Time Customer Profile] 데이터. 이러한 세그먼트는에서 중앙 집중식으로 구성 및 유지 관리됩니다. [!DNL Platform]를 사용하여 모든 Adobe 애플리케이션에서 간편하게 액세스할 수 있습니다.

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

| 기능 | 설명 |
| -----------| ---------- |
| 예약된 세분화 | 이제 사용자는 UI 및 API를 통해 모든 세그먼트에 대해 예약된 세그먼트 평가를 활성화할 수 있습니다. 활성화되면 모든 세그먼트가 하루에 한 번 평가됩니다. 이는 이전처럼 계속 작동하는 온디맨드 세그먼테이션 기능에는 영향을 주지 않습니다.<br/><br/>참고: 예약된 세분화 기능은 5개 이상의 병합 정책이 있는 샌드박스에서 사용할 수 없습니다. [!DNL XDM Individual Profile]. |
| 스트리밍 세분화 | 세그먼트의 지속적인 평가(스트리밍 세분화)를 지원하므로 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 있습니다 [!DNL Platform]. 이 기능은 예약된 세분화 작업을 실행하지 않고도 세그먼트 멤버십이 최신 상태가 됨을 의미합니다. 다중 엔티티 관계를 사용하거나 보강된 페이로드가 있는 세그먼트와 같은 일부 예외가 적용됩니다. |
| 세그먼트를 빌딩 블록으로 | 이제 세그먼트 빌더 UI를 사용하여 세그먼트를 만들 때 사용자는 이전에 정의한 세그먼트를 추가 세그먼트를 위한 빌딩 블록으로 사용할 수 있습니다. <ul><li>현재 대상 멤버십 참조: 사람들이 대상으로 들어오고 나갈 때 업데이트됩니다.</li><li>복사 논리: 선택한 세그먼트 정의를 가져와 새 세그먼트에 복제합니다.</li></ul> |
| ID 네임스페이스별 세그먼트 멤버십 보기 | 이제 ID 네임스페이스(이메일, ECID 및 총 개수)별로 세그먼트 멤버십을 볼 수 있습니다. |
| RBAC 지원 | 이제 세그먼트 빌더에서 기본 역할 기반 액세스 제어 및 권한을 지원합니다. |
| 간 외부 대상 공유에 대한 지원 개선 [!DNL Platform] 및 Adobe 솔루션 | 사용자는 이제 외부 (비-[!DNL Experience Platform]) 대상자 수가 많거나 선험적으로 알려지지 않은 시나리오의 대상자 메타데이터. 이 릴리스에는 다음에 대한 액세스 권한이 포함됩니다. [!DNL Audience Manager] 솔루션 커넥터를 프로비저닝한 고객을 위한 메타데이터. 이 대상 메타데이터는 세그먼트 빌더 내에서 사용하여 새로 만들 수 있습니다. [!DNL Experience Platform] 세그먼트. <br/><br/> 또한 세그먼트는에서 생성됩니다. [!DNL Experience Platform] 이제 다음을 포함한 통합 Adobe 솔루션에서 사용할 수 있습니다. [!DNL Audience Manager], [!DNL Target], 및 [!DNL Ad Cloud]. |

**버그 수정**

* 중첩된 관계의 경우 다중 엔티티 세그먼테이션이 0의 프로필을 반환하던 문제를 수정했습니다.
* 제외 로직이 잘못된 결과를 반환하는 문제를 해결했습니다.
* 다중 엔티티 폴더에 대한 가독성이 개선되었습니다. 이제 XDM 클래스의 친숙한 이름이 표시됩니다.
* 동일한 XDM 폴더의 사본이 여러 개 표시되는 간헐적인 문제가 해결되었습니다.
* 이제 선택한 병합 정책에 대해 세그먼트 예상치를 사용할 수 없는 경우 사용자에게 알리기 위해 메시지가 생성됩니다.

**알려진 문제**

* None.

에 대해 자세히 알아보기 [!DNL Segmentation Service], 다음을 읽으십시오. [세그먼테이션 서비스 개요](../../segmentation/home.md).
