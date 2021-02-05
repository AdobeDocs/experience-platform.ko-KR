---
title: Adobe Experience Platform 릴리스 노트
description: 2020년 11월 11일 Experience Platform 릴리스 노트
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 3%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 11월 11일**

Adobe Experience Platform의 새로운 기능:

- [Adobe Experience Platform Data Lake 마이그레이션](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

기존 기능에 대한 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 서비스](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake 마이그레이션 {#migration}

Adobe이 Data Lake를 Gen1에서 Gen2로 마이그레이션하는 동안 사용자는 Data Lake에서 읽을 수 있지만 Data Lake에 쓰는 모든 기능은 영향을 받게 됩니다. Adobe은 마이그레이션의 영향을 자세히 설명하고 특정 IMS 조직에 대한 마이그레이션 날짜와 시간을 확인하기 위해 시스템 관리자에게 문의할 것입니다.

자세한 내용은 [데이터 레이크 마이그레이션 안내서](../../landing/adls2-gen2-migration.md)를 참조하십시오.

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 는  [Adobe Admin ](https://adminconsole.adobe.com) Console 제품 프로필을 활용하여 사용자에게 사용 권한 및 샌드박스를 연결합니다. 권한은 데이터 모델링, 프로필 관리, 샌드박스 관리 등 다양한 플랫폼 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 권한 | [!DNL Admin Console]에서 [!DNL Platform] 제품 프로필 내의 탭을 사용하여 해당 프로필에 연결된 사용자가 사용할 수 있는 [!DNL Platform] 기능을 사용자 정의할 수 있습니다. 사용 가능한 권한 카테고리에는 다음이 포함됩니다.**[!UICONTROL 데이터 모델링]**, **[!UICONTROL 데이터 관리]**, **[!UICONTROL 프로필 관리]**, **[!UICONTROL Identity Management]**, **[!UICONTROL 데이터 모니터링]**, **[!UICONTROL 샌드박스 관리]**, ****, **[!UICONTROL 데이터 통합]**, **[!UICONTROL 데이터 과학 작업 공간]**, **[!UICONTROL 쿼리 서비스]** 및 **[!UICONTROL 데이터 거버넌스]**. |
| 샌드박스 액세스 | [!DNL Platform] 제품 프로필 내의 **[!UICONTROL 권한]** 탭에서 사용자에게 특정 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 자세한 내용은 아래 [샌드박스](#sandboxes)의 섹션을 참조하십시오. |

자세한 내용은 [액세스 제어 개요](../../access-control/home.md)를 참조하십시오.

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 는 응용 프로그램 서비스와 통합되어 있습니다 [!DNL Experience Platform]. 이를 통해 [!DNL Platform]을(를) 활용하여 모든 접점에서 정확한 타이밍에 고객에게 최상의 제안과 경험을 제공할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 중앙 집중식 제공 라이브러리 | 오퍼를 구성하는 여러 요소를 만들고 관리하고, 규칙과 제한을 정의하는 인터페이스입니다. |
| 오퍼 결정 엔진 | 오퍼 결정 엔진은 오퍼 라이브러리와 함께 [!DNL Platform] 데이터 및 [!DNL Real-time Customer Profiles]을 활용하여 오퍼가 제공될 올바른 시간, 고객 및 채널을 선택합니다. |

자세한 내용은 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) 설명서를 참조하십시오.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 디지털 경험 애플리케이션을 글로벌 규모로 보완하도록 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 고려해야 합니다. 이러한 요구 사항을 해결하기 위해 [!DNL Experience Platform]은 디지털 경험 애플리케이션을 개발하고 진화하는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로덕션 샌드박스 | [!DNL Experience Platform] 는 삭제 또는 재설정할 수 없는 단일 프로덕션 샌드박스를 제공합니다. 사용 가능한 샌드박스, 프로덕션 및 비프로덕션 총 수는 취득한 라이선스에 의해 결정됩니다. |
| 비프로덕션 샌드박스 | 하나의 [!DNL Platform] 인스턴스에 대해 여러 개의 비프로덕션 샌드박스를 만들 수 있으므로 프로덕션 샌드박스에 영향을 미치지 않고 기능을 테스트하고 실험을 실행하고 사용자 정의 구성을 만들 수 있습니다. |
| 샌드박스 전환기 | [!DNL Experience Platform] 사용자 인터페이스에서 화면의 왼쪽 위 모서리에 있는 샌드박스 전환기를 사용하면 드롭다운 메뉴를 통해 사용 가능한 샌드박스 간을 전환할 수 있습니다. 샌드박스 전환기는 사용 가능한 샌드박스를 통해 필터링할 수 있도록 해주는 검색 기능도 제공합니다. |
| `x-sandbox-name` header | [!DNL Experience Platform] API에 대한 모든 호출에는 이제 작업이 발생할 샌드박스의 `name` 특성을 참조하는 값이 새 `x-sandbox-name` 헤더가 포함되어야 합니다. |

자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변형 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 반복적인 작업 | [!DNL Data Prep] 이제 매퍼가 계층에서 반복적인 작업을 수행할 수 있습니다. |
| 매퍼 함수 | [!DNL Data Prep] 이제 매퍼에는 소스에서 대상 XDM **** 으로 속성을 복사할 수 없습니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하십시오.

## 데이터 과학 작업 공간 {#dsw}

데이터 과학 작업 공간은 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace를 사용하면 Adobe 솔루션에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 있습니다. 데이터 과학 작업 공간이 이것을 수행하는 방법 중 하나는 [!DNL JupyterLab]을 사용하는 것입니다. [!DNL JupyterLab] 는 Adobe Experience Platform에 긴밀하게 통합되어  [[!DNL Project Jupyter]](https://jupyter.org/) 있고 웹 기반의 유저 인터페이스입니다. 데이터 과학자들이 [!DNL Jupyter] 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 대화형 개발 환경을 제공합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL JupyterLab] Recipe Builder 템플릿 | 레서피 요구 사항 사용 및 버전이 업데이트되었습니다. [!DNL Python] ML 런타임 기본 이미지가  [!DNL Python] 3.6.7 및 환경만 사용하도록  [!DNL Conda] 업데이트되었습니다. |

자세한 내용은 [Jupiter Notebooks](../../data-science-workspace/jupyterlab/create-a-recipe.md)를 사용하여 레서피 만들기 문서를 참조하십시오.

## [!DNL Destinations] 서비스 {#destinations}

[실시간 고객 데이터 플랫폼](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로, 데이터를 해당 파트너에게 원활하게 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| 브라즈 | Braze는 고객과 브랜드 간의 연관성 있고 기억에 오래 남는 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다. |
| Microsoft Bing | Microsoft Bing 대상은 Microsoft 디스플레이 광고에서 리타깃팅 및 대상 타깃팅된 디지털 캠페인을 실행하는 데 도움이 됩니다. |
| 더 트레이드데스크 | Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 리타겟팅하고 실행할 수 있는 셀프 서비스 플랫폼입니다. |

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상 세부 정보 UX 업데이트 | 실시간 CDP의 대상 워크플로우에는 인라인 모니터링이 포함되어 있으므로 성공적인 일괄 작업을 확인할 수 있습니다. 이 기능을 사용하면 경고 및 모니터링 대시보드를 통해 배치 대상에 대한 워크플로우에서 직접 문제를 해결하고 처리 과정에서 발생하는 오류를 추적할 수 있습니다. |
| 파일 암호화 | 이제 파일 기반 대상의 경우 내보낸 파일에 암호화를 추가할 수 있습니다. |
| 파일 예약 | 이메일 기반 및 클라우드 스토리지 대상에 대해 사용자는 일회성 내보내기를 만들거나 일별 스냅샷을 만들 수 있습니다. |
| 필수 필드 | 필수 필드를 포함하는 필드만 내보내도록 필드를 필수로 표시할 수 있습니다. |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## Intelligent Services {#intelligent-services}

Intelligent Services를 통해 마케팅 분석가와 전문가는 인공 지능과 머신 러닝을 활용하여 고객 경험 사례를 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| CEE(Consumer Experience Events) 데이터 세트 | 이제 CEE 데이터 세트를 만들면 스키마 편집기를 사용하여 데이터 세트에 ID 필드를 추가할 수 있습니다. Attribution AI 및 고객 AI는 이벤트를 결합하는 데 기본 ID를 사용합니다. |

자세한 내용은 Intelligent Services 데이터 준비 안내서의 데이터 세트](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset)에 ID 필드 추가 섹션을 참조하십시오.[

### Attribution AI

Attribution AI은 지능형 서비스의 일부로 고객 상호 작용에 대한 영향과 증분 영향을 지정된 결과에 따라 계산하는 다중 채널 알고리즘 속성 서비스입니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 원본 데이터 세트 소스에 대한 링크를 보고 선택한 서비스 인스턴스의 오른쪽 레일에서 탐색할 수 있습니다. |
| 인스턴스 이름 편집 | 이제 기존 Attribution AI 인스턴스의 이름을 수정할 수 있습니다. |
| 복제 인스턴스 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 채점을 시작하지 않은 기존 Attribution AI 인스턴스의 구성을 수정할 수 있습니다. |
| 한 번의 득점 | 이제 Attribution AI 인스턴스에서 애드혹 모델 점수를 트리거할 수 있습니다. |
| 통과 열 | 이제 BI 도구 보기에 추가 차원을 추가하기 위해 원시 출력 점수 파일에 추가할 추가 열을 구성할 수 있습니다. |
| 인스턴스 활성화 및 비활성화 | 이제 Attribution AI 인스턴스의 예약된 모델 트레이닝과 점수 지정을 활성화하고 비활성화할 수 있습니다. |
| 권한 추적 | 인스턴스 만들기 컨테이너에서 계정에 의해 사용된 총 속성 인사이트의 양을 찾을 수 있습니다. |
| 위치별 터치포인트 분류 | 전환 경로 위치별 접점 분석을 제공하는 새로운 인사이트 그래프. |
| 주요 전환 경로 | 경로 분석 탭에 있는 새로운 인사이트 그래프. 그래프에는 가장 많은 전환을 유도한 마케팅 채널 접점의 시퀀스를 보여주는 상위 5개의 전환 경로 목록이 포함되어 있습니다. |
| 터치포인트 효과 | 모델이 터치포인트 효과를 측정하는 가장 중요한 3가지 변수에 대한 심도 있는 통찰력을 제공합니다. 변수는 터치되는 긍정 및 부정 경로, 터치포인트 효율성 및 터치포인트 볼륨의 비율입니다. |

자세한 내용은 [Attribution AI 개요](../../intelligent-services/attribution-ai/overview.md)를 참조하십시오.

### 고객 AI

고객 AI는 지능형 서비스의 일환으로 마케터에게 설명 자료를 통해 개별 수준에서 고객 예측을 생성할 수 있는 기능을 제공합니다. 고객 AI는 영향력 있는 요소를 활용하여 고객의 관심사와 이유를 파악할 수 있습니다. 또한 마케터는 고객 AI의 예측과 인사이트를 활용하여 가장 적절한 제안과 메시지를 제공함으로써 고객 경험을 개인화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 원본 데이터 세트 소스에 대한 링크를 보고 선택한 서비스 인스턴스의 오른쪽 레일에서 탐색할 수 있습니다. |
| 인스턴스 이름 편집 | 기존 고객 AI 인스턴스의 이름을 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 기존 고객 AI 인스턴스가 점수를 아직 시작하지 않은 경우 구성을 수정할 수 있습니다. |
| 복제 인스턴스 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 권한 추적 | 인스턴스 만들기 컨테이너에서 고객 AI가 고객 계정에 대해 획득한 총 프로필 수를 찾을 수 있습니다. |
| 예측 목표 | &quot;발생할&quot; 또는 &quot;발생하지 않을&quot; 여부를 예측할 수 있는 새로운 옵션을 사용하여 예측 목표를 만드는 데 있어 유연성이 높아졌습니다. 또한 여러 이벤트를 사용할 때 이벤트가 발생하는지 또는 &quot;이벤트 중 하나&quot;가 발생하는지를 예측하는 옵션이 추가되었습니다. |
| 영향력 있는 요소 드릴다운 | 영향력이 높은 상위 요인 버킷에는 이제 드릴다운이 포함됩니다. 드릴다운은 성향 버킷 내에서 가장 영향력 있는 요인 각각에 대한 값의 보다 심도 있는 요약입니다. |

자세한 내용은 [고객 AI 개요](../../intelligent-services/customer-ai/overview.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소 또는 시기와 상관없이 고객의 관심사와 연관성 있는 경험을 일관되게 전달할 수 있습니다. 실시간 고객 프로파일을 사용하면 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 다양한 채널의 데이터를 취합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Profile] 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 정책 병합 작업 과정 업데이트 | 플랫폼이 병합 정책 구성을 새 단계 작업 과정으로 업그레이드했습니다. 이 워크플로우에서는 여러 프로필 데이터 세트에서 데이터 조각을 취합하고 데이터를 이러한 데이터 세트에 병합하는 방식에 대한 우선 순위를 설정하여 각 개인에 대한 포괄적인 보기를 만들 수 있습니다. 적절한 병합 방법(타임스탬프가 순서가 지정되거나 데이터 세트 우선 순위)을 선택하고 프로필 데이터 집합에 ExperienceEvent 데이터 세트를 추가하여 선택한 XDM 개별 프로필 데이터 집합을 병합할 수 있습니다. |
| 결합 스키마 보기 | Experience Platform UI에서 사용자는 ID 및 관계 필드와 같은 표면 키 속성뿐만 아니라 조합 스키마에 기여하는 모든 스키마 및 데이터 세트에 대한 정보를 보다 쉽게 찾을 수 있습니다. 이 업데이트는 프로필이 올바르게 구성되고, ID가 올바르게 연결되고, 데이터가 성공적으로 수집되었는지 문제를 해결하고 확인하는 기능을 개선합니다. |

[!DNL Profile] 데이터 작업에 대한 자습서 및 모범 사례를 비롯하여 실시간 고객 프로파일에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 동시에 [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 소스**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL Shopify] | 이제 [!DNL Flow Service] API 또는 UI를 사용하여 [!DNL Shopify]을 [!DNL Experience Platform]에 연결할 수 있습니다. 자세한 내용은 [Shopify 커넥터 개요](../../sources/connectors/ecommerce/shopify.md)를 참조하십시오. |

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 연결 정보 업데이트 | 이제 [!DNL Flow Service] API 및 UI를 사용하여 기존 일괄 연결의 이름, 설명 및 자격 증명을 업데이트할 수 있습니다. 자세한 내용은 Flow Service API](../../sources/tutorials/api/update.md)을 사용하여 연결 업데이트 및 UI](../../sources/tutorials/ui/monitor.md)를 사용하여 계정 세부 사항 편집에 대한 자습서를 참조하십시오.[[ |
| 연결 삭제 | 이제 [!DNL Flow Service] API 및 UI를 사용하여 오류가 있거나 불필요한 일괄 연결을 삭제할 수 있습니다. 자세한 내용은 Flow Service API](../../sources/tutorials/api/delete.md) 및 [UI](../../sources/tutorials/ui/delete-accounts.md)를 사용하여 계정 삭제에 대한 자습서를 참조하십시오.[ |
| 계층적 매핑 | 데이터 수집 프로세스 중에 JSON 또는 Paretailored와 같은 계층적 소스 파일을 미리 볼 수 있습니다. 자세한 내용은 UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성의 자습서를 참조하십시오.[ |
| 스트리밍 소스의 매핑을 위한 API 지원 | 이제 API를 사용하여 스트리밍 소스에서 매핑 기능을 수행할 수 있습니다. |
| 클라우드 스토리지 소스에 대한 사용자 정의 구분 기호에 대한 API 지원 | 이제 클라우드 스토리지 소스를 사용하여 CSV로 구분된 파일 이외의 파일을 수집할 수 있습니다. 탭, 쉼표, 파이프, 세미콜론 또는 해시와 같은 단일 열 구분 기호를 사용하여 모든 형식의 플랫 파일을 수집할 수 있습니다. |
| Adobe Audience Manager 커넥터에 대한 샌드박스 지원 | Audience Manager 커넥터는 이제 샌드박스를 인식합니다. 사용자는 Audience Manager 데이터 세트를 선택한 샌드박스(비프로덕션 샌드박스 포함)로 라우팅하도록 커넥터를 활성화할 수 있습니다. 구성은 IMS 조직당 하나의 샌드박스로 제한됩니다. |
| 향상된 UX | 이제 소스 카탈로그를 통해 파일 기반 수집에 액세스할 수 있습니다. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.