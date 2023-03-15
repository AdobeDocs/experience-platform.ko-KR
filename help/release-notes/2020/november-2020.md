---
title: Adobe Experience Platform 릴리스 노트 2020년 11월
description: Adobe Experience Platform에 대한 2020년 11월 릴리스 정보입니다.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 11월 11일**

Adobe Experience Platform의 새로운 기능:

- [Adobe Experience Platform 데이터 레이크 마이그레이션](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

기존 기능에 대한 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 서비스](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform 데이터 레이크 마이그레이션 {#migration}

Adobe이 Gen1에서 Gen2로 데이터 레이크를 마이그레이션하는 동안 사용자는 데이터 레이크에서 읽을 수 있지만 데이터 레이크에 쓰는 모든 기능이 영향을 받습니다. Adobe이 시스템 관리자에게 연락하여 마이그레이션의 영향을 자세히 논의하고 특정 IMS 조직의 마이그레이션 날짜 및 시간을 확인합니다.

자세한 내용은 다음을 참조하십시오. [Data Lake 마이그레이션 안내서](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 활용 [Adobe Admin Console](https://adminconsole.adobe.com) 제품 프로필 을 통해 사용자와 권한 및 샌드박스를 연결할 수 있습니다. 권한은 데이터 모델링, 프로필 관리 및 샌드박스 관리를 포함하여 다양한 플랫폼 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 권한 | 다음에서 [!DNL Admin Console], 내의 탭 [!DNL Platform] 제품 프로필을 통해 사용자 지정 [!DNL Platform] 해당 프로필에 첨부된 사용자가 기능을 사용할 수 있습니다. 사용 가능한 권한 범주는 다음과 같습니다. **[!UICONTROL 데이터 모델링]**, **[!UICONTROL 데이터 관리]**, **[!UICONTROL 프로필 관리]**, **[!UICONTROL Identity Management]**, **[!UICONTROL 데이터 모니터링]**, **[!UICONTROL 샌드박스 관리]**, **[!UICONTROL 대상]**, **[!UICONTROL 데이터 수집]**, **[!UICONTROL 데이터 과학 작업 영역]**, **[!UICONTROL 쿼리 서비스]**, 및 **[!UICONTROL 데이터 거버넌스]**. |
| 샌드박스에 대한 액세스 | 다음 **[!UICONTROL 권한]** 다음 내의 탭 [!DNL Platform] 제품 프로필은 사용자에게 특정 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 의 섹션을 참조하십시오. [샌드박스](#sandboxes) 자세한 내용은 아래를 참조하십시오. |

자세한 내용은 다음을 참조하십시오. [액세스 제어 개요](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 은(는) 애플리케이션 서비스와 [!DNL Experience Platform]. 다음을 활용할 수 있습니다. [!DNL Platform] 는 적절한 시기에 모든 접점에서 고객에게 최상의 오퍼와 경험을 제공합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 중앙 집중식 오퍼 라이브러리 | 오퍼를 구성하는 여러 요소를 만들고 관리하고, 규칙과 제약 조건을 정의하는 인터페이스입니다. |
| 오퍼 결정 엔진 | 오퍼 의사 결정 엔진에서 [!DNL Platform] 데이터 및 [!DNL Real-Time Customer Profiles]를 오퍼 라이브러리와 함께 사용하여 오퍼가 제공될 올바른 시간, 고객 및 채널을 선택합니다. |

자세한 내용은 다음을 참조하십시오. [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=ko-KR) 설명서를 참조하십시오.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 는 글로벌 규모로 디지털 경험 애플리케이션을 강화하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다. 이 필요를 해결하기 위해, [!DNL Experience Platform] 단일 파티션을 만드는 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로덕션 샌드박스 | [!DNL Experience Platform] 는 삭제하거나 재설정할 수 없는 단일 프로덕션 샌드박스를 제공합니다. 사용 가능한 총 샌드박스 수(프로덕션 및 비프로덕션)는 획득한 라이센스에 따라 결정됩니다. |
| 비프로덕션 샌드박스 | 하나에 대해 여러 비프로덕션 샌드박스를 생성할 수 있습니다 [!DNL Platform] 예를 들어 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고 실험을 실행하며 사용자 정의 구성을 만들 수 있습니다. |
| 샌드박스 전환기 | 다음에서 [!DNL Experience Platform] 사용자 인터페이스인 화면 왼쪽 상단 모서리에 있는 샌드박스 전환기를 사용하면 드롭다운 메뉴를 통해 사용 가능한 샌드박스 간을 전환할 수 있습니다. 샌드박스 전환기는 사용 가능한 샌드박스를 필터링할 수 있는 검색 기능도 제공합니다. |
| `x-sandbox-name` 머리글 | 모든 호출 [!DNL Experience Platform] 이제 API에 새 항목이 포함되어야 함 `x-sandbox-name` 값이 를 참조하는 헤더 `name` 작업이 수행될 샌드박스의 속성입니다. |

자세한 내용은 다음을 참조하십시오. [샌드박스 개요](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 반복 작업 | [!DNL Data Prep] Mapper는 이제 계층 구조에서 반복 작업을 수행할 수 있도록 지원합니다. |
| Mapper 함수 | [!DNL Data Prep] 이제 Mapper에서 **아님** 소스에서 타겟 XDM으로 속성을 복사합니다. |

자세한 내용은 다음을 참조하십시오. [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 데이터 과학 작업 영역 {#dsw}

Data Science Workspace 는 머신 러닝 및 인공 지능을 사용하여 데이터에서 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace는 Adobe 솔루션 전반에서 컨텐츠 및 데이터 에셋을 사용하여 예측을 수행하는 데 도움이 됩니다. Data Science Workspace에서 이를 수행하는 방법 중 하나는 을 사용하는 것입니다. [!DNL JupyterLab]. [!DNL JupyterLab] 은 의 웹 기반 사용자 인터페이스입니다. [[!DNL Project Jupyter]](https://jupyter.org/) 및 는 Adobe Experience Platform에 긴밀하게 통합되어 있습니다. 데이터 과학자가 작업할 수 있는 대화형 개발 환경을 제공합니다 [!DNL Jupyter] notebooks, code 및 data.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL JupyterLab] 레시피 빌더 템플릿 | 레시피 요구 사항 사용 및 버전을 보여주는 전자 필기장입니다. [!DNL Python] ML 런타임 기본 이미지가 을 사용하도록 업데이트되었습니다 [!DNL Python] 3.6.7 및 a [!DNL Conda] 환경 전용입니다. |

자세한 내용은 다음 문서를 참조하십시오. [Jupyter Notebooks를 사용하여 레시피 만들기](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] 서비스 {#destinations}

위치 [Real-time Customer Data Platform](../../rtcdp/overview.md), 대상은 이러한 파트너에게 데이터를 원활하게 활성화하는 대상 플랫폼과의 사전 구축된 통합입니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| 브레이즈 | Braze는 고객과 고객이 사랑하는 브랜드 간의 관련성 있고 기억에 남는 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다. |
| Microsoft Bing | Microsoft Bing 대상은 Microsoft 디스플레이 광고 전반에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행하는 데 도움이 됩니다. |
| 트레이드 데스크 | Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다. |

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상 세부 사항 UX 업데이트 | 이제 Real-Time CDP의 대상 워크플로우에 인라인 모니터링이 포함되므로 성공한 일괄 처리 활성화를 확인할 수 있습니다. 이 기능을 사용하면 경고 및 모니터링 대시보드를 통해 처리 파이프라인의 오류를 추적하여 배치 대상에 대한 워크플로우에서 직접 문제를 해결할 수 있습니다. |
| 파일 암호화 | 파일 기반 대상의 경우 이제 사용자는 내보낸 파일에 암호화를 추가할 수 있습니다. |
| 파일 예약 | 이메일 기반 및 클라우드 스토리지 대상 모두에 대해 사용자는 1회 내보내기를 생성하거나 일별 스냅샷을 생성할 수 있습니다. |
| 필수 필드 | 사용자는 필드를 필수 필드로 표시하여 필수 필드가 포함된 필드만 내보내도록 할 수 있습니다. |

자세한 내용은 다음을 참조하십시오. [대상 개요](../../destinations/home.md).

## 인텔리전트 서비스 {#intelligent-services}

인텔리전트 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있는 권한을 부여합니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준의 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 고객 경험 이벤트(CEE) 데이터 세트 | 이제 CEE 데이터 세트를 만들면 스키마 편집기를 사용하여 데이터 세트에 ID 필드를 추가할 수 있습니다. Attribution AI과 고객 AI는 이벤트를 결합하는 데 기본 ID를 사용합니다. |

자세한 내용은 의 섹션을 참조하십시오. [데이터 세트에 id 필드 추가](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) ( Intelligent Services 데이터 준비 안내서).

### 기여도 AI

인텔리전트 서비스의 일부인 Attribution AI은 지정된 결과에 대한 고객 상호 작용의 영향 및 점진적 영향을 계산하는 멀티채널 알고리즘 속성 서비스입니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 선택한 서비스 인스턴스의 오른쪽 레일에서 원래 데이터 세트 소스에 대한 링크를 보고 탐색할 수 있습니다. |
| 인스턴스 이름 편집 | 이제 기존 Attribution AI 인스턴스의 이름을 수정할 수 있습니다. |
| 인스턴스 복제 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 채점을 시작하지 않은 경우 기존 Attribution AI 인스턴스의 구성을 수정할 수 있습니다. |
| 1회 채점 | 이제 Attribution AI 인스턴스에서 임시 모델 점수를 트리거할 수 있습니다. |
| 열 통과 | 이제 원시 출력 점수 파일에 추가할 추가 열을 구성하여 BI 도구 보기에 차원을 추가할 수 있습니다. |
| 인스턴스 활성화 및 비활성화 | 이제 Attribution AI 인스턴스의 예약된 모델 교육 및 점수를 활성화하고 비활성화할 수 있습니다. |
| 권한 추적 | 인스턴스 만들기 컨테이너에서 귀하의 계정이 사용한 총 속성 인사이트 양을 찾을 수 있습니다. |
| 위치별 접점 분류 | 전환 경로 위치별 터치포인트 분석을 제공하는 새로운 인사이트 그래프. |
| 상위 전환 경로 | 경로 분석 탭에 있는 새로운 인사이트 그래프. 그래프에는 가장 많은 전환을 유도한 마케팅 채널 접점의 시퀀스를 보여 주는 상위 5개 전환 경로 목록이 포함되어 있습니다. |
| 접점 효율성 | 모델이 접점 효율성을 측정하는 가장 중요한 세 가지 변수에 대한 심층적인 통찰력을 제공합니다. 변수는 터치한 양수 및 음수 경로의 비율, 접점 효율성 및 접점 볼륨입니다. |

자세한 내용은 다음을 참조하십시오. [Attribution AI 개요](../../intelligent-services/attribution-ai/overview.md).

### 고객 AI

Intelligent Services의 일부인 고객 AI는 마케터에게 설명을 통해 개별 수준에서 고객 예측을 생성할 수 있는 권한을 제공합니다. 영향력 있는 요소를 통해 Customer AI는 고객이 무엇을 할 수 있고 왜 하는지 알려 줄 수 있습니다. 또한 마케터는 Customer AI 예측 및 통찰력을 활용하여 가장 적절한 오퍼와 메시지를 제공함으로써 고객 경험을 개인화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 선택한 서비스 인스턴스의 오른쪽 레일에서 원래 데이터 세트 소스에 대한 링크를 보고 탐색할 수 있습니다. |
| 인스턴스 이름 편집 | 기존 Customer AI 인스턴스의 이름을 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 아직 채점을 시작하지 않은 경우 기존 고객 AI 인스턴스의 구성을 수정할 수 있습니다. |
| 인스턴스 복제 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 권한 추적 | 인스턴스 만들기 컨테이너에서 계정에 대해 고객 AI가 점수화한 총 프로필 양을 찾을 수 있습니다. |
| 예측 목표 | &quot;발생할 것&quot; 또는 &quot;발생하지 않을 것&quot;인지 예측하는 새로운 옵션을 사용하여 예측 목표를 생성할 수 있는 유연성이 향상되었습니다. 또한 여러 이벤트가 사용될 때 &quot;모든&quot; 이벤트가 발생하는지 또는 &quot;임의의&quot; 이벤트가 발생하는지를 예측하는 옵션이 추가되었습니다. |
| 영향력 있는 요인 드릴다운 | 성향 상위 영향력 있는 요소 버킷에 이제 드릴다운이 포함됩니다. 드릴다운은 성향 버킷 내에서 가장 영향력 있는 각 요소에 대한 값을 더 심층적으로 요약한 것입니다. |

자세한 내용은 다음을 참조하십시오. [Customer AI 개요](../../intelligent-services/customer-ai/overview.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile] 에서는 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 다양한 고객 데이터를 통합할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 업데이트된 병합 정책 워크플로 | Platform이 병합 정책 구성을 새로운 단계별 워크플로우로 업그레이드했습니다. 이 워크플로를 통해 사용자는 여러 프로필 데이터 세트의 데이터 조각을 결합하고 이러한 데이터 세트에서 데이터가 병합되는 방식에 대한 우선 순위를 설정하여 각 개인에 대한 포괄적인 보기를 만들 수 있습니다. 사용자는 적절한 병합 방법(타임스탬프 정렬 또는 데이터 세트 우선 순위)을 선택하고 프로필 데이터 세트에 ExperienceEvent 데이터 세트를 추가하여 선택한 XDM 개별 프로필 데이터 세트를 병합할 수 있습니다. |
| 유니온 스키마 보기 | Experience Platform UI에서 사용자는 ID 및 관계 필드와 같은 표면 키 속성뿐만 아니라 유니온 스키마에 기여하는 모든 스키마 및 데이터 세트에 대한 정보를 더 쉽게 찾을 수 있습니다. 이러한 업데이트는 프로필이 올바르게 구성되었는지, ID가 올바르게 결합되었는지, 데이터가 성공적으로 수집되었는지 문제를 해결하고 확인하는 기능을 향상시킵니다. |

을 사용하여 작업하는 데 필요한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대한 자세한 내용 [!DNL Profile] 데이터, 다음을 읽으십시오. [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL Shopify] | 이제 연결할 수 있습니다 [!DNL Shopify] 끝 [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI. 다음을 참조하십시오. [Shopify 커넥터 개요](../../sources/connectors/ecommerce/shopify.md) 추가 정보. |

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 연결 정보 업데이트 | 이제 를 사용하여 기존 배치 연결의 이름, 설명 및 자격 증명을 업데이트할 수 있습니다. [!DNL Flow Service] API 및 UI. 자세한 내용은 다음 자습서를 참조하십시오. [흐름 서비스 API를 사용하여 연결 업데이트](../../sources/tutorials/api/update.md) 및 [ui를 사용하여 계정 세부 정보 편집](../../sources/tutorials/ui/monitor.md). |
| 연결 삭제 | 오류가 있거나 불필요하게 된 배치 연결은 이제 다음을 사용하여 삭제할 수 있습니다. [!DNL Flow Service] API 및 UI. 자세한 내용은 다음 자습서를 참조하십시오. [흐름 서비스 API를 사용하여 연결 삭제](../../sources/tutorials/api/delete.md) 및 [UI를 사용하여 계정 삭제](../../sources/tutorials/ui/delete-accounts.md). |
| 계층 구조 매핑 | 데이터 수집 프로세스 중에 JSON 또는 Parquet와 같은 계층적 소스 파일을 미리 볼 수 있습니다. 다음에서 자습서 보기: [ui에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 추가 정보. |
| 스트리밍 소스에서의 매핑을 위한 API 지원 | 이제 API를 사용하여 스트리밍 소스에서 매핑 기능을 수행할 수 있습니다. |
| 클라우드 스토리지 소스의 사용자 지정 구분 기호에 대한 API 지원 | 이제 클라우드 저장소 소스를 사용하여 CSV로 구분되지 않은 파일을 수집할 수 있습니다. 탭, 쉼표, 파이프, 세미콜론 또는 해시와 같은 단일 열 구분 기호를 사용하여 모든 형식의 플랫 파일을 수집할 수 있습니다. |
| Adobe Audience Manager 커넥터에 대한 샌드박스 지원 | 이제 Audience Manager 커넥터가 샌드박스를 인식합니다. 사용자는 커넥터가 Audience Manager 데이터 세트를 선택한 샌드박스(비프로덕션 샌드박스 포함)로 라우팅하도록 할 수 있습니다. 구성은 IMS 조직당 하나의 샌드박스로 제한됩니다. |
| UX 개선 사항 | 이제 소스 카탈로그를 통해 파일 기반 수집에 액세스할 수 있습니다. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
