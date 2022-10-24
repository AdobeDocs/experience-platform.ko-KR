---
title: Adobe Experience Platform 릴리스 노트 - 2020년 11월
description: Adobe Experience Platform에 대한 2020년 11월 릴리스 노트입니다.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 11월 11일**

Adobe Experience Platform의 새로운 기능:

- [Adobe Experience Platform Data Lake 마이그레이션](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 서비스](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake 마이그레이션 {#migration}

Adobe이 Gen1에서 Gen2로 Data Lake를 마이그레이션하는 동안 사용자는 Data Lake에서 읽을 수 있지만 Data Lake에 기록하는 모든 기능은 영향을 받게 됩니다. Adobe은 시스템 관리자에게 연락하여 마이그레이션의 영향을 자세히 설명하고 특정 IMS 조직의 마이그레이션 날짜 및 시간을 확인할 것입니다.

자세한 내용은 [Data Lake 마이그레이션 안내서](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 활용 [Adobe Admin Console](https://adminconsole.adobe.com) 사용 권한 및 샌드박스를 사용자와 연결하는 제품 프로필입니다. 권한은 데이터 모델링, 프로필 관리 및 샌드박스 관리를 포함하여 다양한 플랫폼 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 권한 | 에서 [!DNL Admin Console], 내의 탭 [!DNL Platform] 제품 프로필을 사용하면 사용자 정의할 수 있습니다 [!DNL Platform] 해당 프로필에 첨부된 사용자가 기능을 사용할 수 있습니다. 사용 가능한 권한 카테고리는 다음과 같습니다. **[!UICONTROL 데이터 모델링]**, **[!UICONTROL 데이터 관리]**, **[!UICONTROL 프로필 관리]**, **[!UICONTROL Identity Management]**, **[!UICONTROL 데이터 모니터링]**, **[!UICONTROL 샌드박스 관리]**, **[!UICONTROL 대상]**, **[!UICONTROL 데이터 수집]**, **[!UICONTROL 데이터 과학 작업 공간]**, **[!UICONTROL 쿼리 서비스]**, 및 **[!UICONTROL 데이터 거버넌스]**. |
| 샌드박스 액세스 | 다음 **[!UICONTROL 권한]** 탭 내 [!DNL Platform] 제품 프로필은 사용자에게 특정 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 의 섹션을 참조하십시오. [샌드박스](#sandboxes) 아래 정보를 참조하십시오. |

자세한 내용은 [액세스 제어 개요](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 는 [!DNL Experience Platform]. 활용할 수 있습니다 [!DNL Platform] 모든 터치 포인트에서 고객에게 최적의 오퍼 및 경험을 제공하기 위한 것입니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 중앙 집중식 오퍼 라이브러리 | 오퍼를 구성하는 여러 요소를 만들고 관리하고, 해당 규칙과 제한을 정의하는 인터페이스입니다. |
| 오퍼 결정 엔진 | 오퍼 결정 엔진이 활용하는 [!DNL Platform] 데이터 및 [!DNL Real-time Customer Profiles]를 오퍼 라이브러리와 함께 사용하여 적절한 시간을 선택하려면 오퍼가 배달될 고객 및 채널을 선택합니다. |

자세한 내용은 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=ko-KR) 설명서.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 는 글로벌 규모로 디지털 경험 애플리케이션을 보강하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 운영하고 있으며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 충족해야 합니다. 이런 요구를 해결하기 위해서 [!DNL Experience Platform] 단일 파티션을 구성하는 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로덕션 샌드박스 | [!DNL Experience Platform] 삭제하거나 재설정할 수 없는 단일 프로덕션 샌드박스를 제공합니다. 사용 가능한 샌드박스, 프로덕션 및 비프로덕션 총 수는 획득한 라이센스에 의해 결정됩니다. |
| 비프로덕션 샌드박스 | 한 번에 여러 비프로덕션 샌드박스를 만들 수 있습니다 [!DNL Platform] 예를 들어, 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있습니다. |
| 샌드박스 전환기 | 에서 [!DNL Experience Platform] 사용자 인터페이스와 화면 왼쪽 상단 모서리에 있는 샌드박스 전환기를 사용하면 드롭다운 메뉴를 통해 사용 가능한 샌드박스 간을 전환할 수 있습니다. 또한 샌드박스 전환기는 사용 가능한 샌드박스를 통해 필터링할 수 있는 검색 기능도 제공합니다. |
| `x-sandbox-name` 헤더 | 모든 호출 [!DNL Experience Platform] 이제 API에 새 `x-sandbox-name` 헤더. 값이 `name` 작업이 발생할 샌드박스의 속성입니다. |

자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 반복 작업 | [!DNL Data Prep] 이제 매퍼가 계층에서 반복 작업을 수행할 수 있습니다. |
| 매퍼 함수 | [!DNL Data Prep] 매퍼는 이제 **not** 소스에서 대상 XDM으로 속성을 복사합니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 데이터 과학 작업 영역 {#dsw}

Data Science Workspace는 기계 학습 및 인공 지능을 사용하여 데이터를 통해 통찰력을 생성합니다. Adobe Experience Platform에 통합된 Data Science Workspace을 사용하면 Adobe 솔루션에서 컨텐츠 및 데이터 자산을 사용하여 예측을 할 수 있습니다. Data Science Workspace가 수행하는 방법 중 하나는 [!DNL JupyterLab]. [!DNL JupyterLab] 는 용 웹 기반 사용자 인터페이스입니다 [[!DNL Project Jupyter]](https://jupyter.org/) 와 Adobe Experience Platform은 긴밀하게 통합되어 있습니다. 데이터 과학자들이 작업할 수 있도록 대화형 개발 환경을 제공합니다 [!DNL Jupyter] 노트북, 코드 및 데이터

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL JupyterLab] 레서피 빌더 템플릿 | 레서피 요구 사항 사용 및 버전에 대한 노트가 업데이트되었습니다. [!DNL Python] ML 런타임 기본 이미지가 사용하도록 업데이트되었습니다. [!DNL Python] 3.6.7 및 a [!DNL Conda] 환경 전용. |

자세한 내용은 다음 문서를 참조하십시오. [주피터 노트북을 사용하여 레서피 생성](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] 서비스 {#destinations}

in [Real-time Customer Data Platform](../../rtcdp/overview.md), 대상은 대상 플랫폼과의 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| 브레이즈 | Braze는 고객과 고객이 좋아하는 브랜드 간 연관성 있고 기억에 남을 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다. |
| Microsoft Bing | Microsoft Bing 대상은 Microsoft 디스플레이 광고에서 리타겟팅 및 대상 타깃팅된 디지털 캠페인을 실행하는 데 도움이 됩니다. |
| 무역센터 | Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 실행하고 재타겟팅할 수 있는 셀프서비스 플랫폼입니다. |

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대상 세부 사항 UX 업데이트 | 이제 Real-Time CDP의 대상 워크플로우에 인라인 모니터링이 포함되어 있어 성공적인 배치 활동을 확인할 수 있습니다. 이 기능을 사용하면 경고 및 모니터링 대시보드를 통해 배치 대상에 대한 워크플로우에서 직접 문제를 제거하여 처리 파이프라인의 오류를 추적할 수 있습니다. |
| 파일 암호화 | 파일 기반 대상의 경우 이제 사용자는 내보낸 파일에 암호화를 추가할 수 있습니다. |
| 파일 예약 | 전자 메일 기반 및 클라우드 스토리지 대상에 대해 일회성 내보내기를 생성하거나 일별 스냅샷을 생성할 수 있습니다. |
| 필수 필드 | 사용자는 필드를 필수로 표시할 수 있으므로 필수 필드가 포함된 필드만 내보낼 수 있습니다. |

자세한 내용은 [대상 개요](../../destinations/home.md).

## 인텔리전트 서비스 {#intelligent-services}

마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 인공 지능(AI) 및 머신 러닝을 활용할 수 있는 Intelligent Services를 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| CEE(소비자 경험 이벤트) 데이터 세트 | 이제 CEE 데이터 세트 만들기에서 스키마 편집기를 사용하여 데이터 세트에 ID 필드를 추가할 수 있습니다. Attribution AI 및 고객 AI는 이벤트를 결합하기 위해 기본 ID를 사용합니다. |

자세한 내용은 [데이터 집합에 ID 필드 추가](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) 을 참조하십시오.

### 기여도 AI

Attribution AI은 지능형 서비스의 일부로서 멀티 채널, 알고리즘 기반의 어트리뷰션 서비스로, 지정된 결과에 대한 고객 상호 작용의 영향과 점진적 효과를 계산합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 원래 데이터 세트 소스에 대한 링크를 보고 선택한 서비스 인스턴스의 오른쪽 레일에서 로 이동할 수 있습니다. |
| 인스턴스 이름 편집 | 이제 기존 Attribution AI 인스턴스의 이름을 수정할 수 있습니다. |
| 복제 인스턴스 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 기존 Attribution AI 인스턴스가 아직 점수 책정을 시작하지 않은 경우 구성을 수정할 수 있습니다. |
| 한 득점 | 이제 Attribution AI 인스턴스에서 임시 모델 점수를 트리거할 수 있습니다. |
| 열 전달 | 이제 원시 출력 점수 파일에 추가될 추가 열을 구성하여 BI 도구 보기에 추가 차원을 추가할 수 있습니다. |
| 인스턴스 활성화 및 비활성화 | 이제 Attribution AI 인스턴스의 예약된 모델 교육 및 점수 책정을 활성화하고 비활성화할 수 있습니다. |
| 자격 추적 | 인스턴스 만들기 컨테이너에서 계정이 사용한 총 속성 인사이트의 양을 찾을 수 있습니다. |
| 위치별 터치포인트 분류 | 전환 경로 위치별 터치포인트를 분석하는 새 인사이트 그래프 |
| 최고 전환 경로 | 경로 분석 탭에 있는 새 인사이트 그래프 그래프에는 가장 많은 전환을 유도한 마케팅 채널 터치포인트의 시퀀스를 보여주는 상위 5개의 전환 경로 목록이 포함되어 있습니다. |
| 터치포인트 효율성 | 모델이 터치 포인트 효과를 측정하는 세 가지 가장 중요한 변수에 대한 심도 있는 인사이트를 제공합니다. 변수는 터치된 양수 및 음수 경로, 터치 포인트 효율성 및 터치 포인트 볼륨의 비율입니다. |

자세한 내용은 [Attribution AI 개요](../../intelligent-services/attribution-ai/overview.md).

### 고객 AI

Customer AI는 Intelligent Services의 일부로 마케터에게 설명을 통해 개별 수준에서 고객 예측을 생성할 수 있는 기능을 제공합니다. 영향력 있는 요소를 통해 Customer AI는 고객이 무엇을 할 수 있고 왜 하는지 알려 줄 수 있습니다. 또한 마케터는 Customer AI 예측 및 통찰력을 활용하여 가장 적절한 오퍼와 메시지를 제공함으로써 고객 경험을 개인화할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 데이터 소스 링크 | 원래 데이터 세트 소스에 대한 링크를 보고 선택한 서비스 인스턴스의 오른쪽 레일에서 로 이동할 수 있습니다. |
| 인스턴스 이름 편집 | 기존 고객 AI 인스턴스의 이름을 수정할 수 있습니다. |
| 인스턴스 구성 매개 변수 수정 | 이제 기존 Customer AI 인스턴스가 아직 점수를 시작하지 않은 경우 구성을 수정할 수 있습니다. |
| 복제 인스턴스 | 현재 선택한 서비스 인스턴스 설정을 복사하고 수정할 수 있습니다. |
| 자격 추적 | 인스턴스 만들기 컨테이너에서 고객 AI가 계정에 대해 채점한 총 프로필 양을 찾을 수 있습니다. |
| 예측 목표 | &quot;발생할&quot; 또는 &quot;일어나지 않을&quot; 여부를 예측할 수 있는 새로운 옵션을 사용하여 예측 목표를 작성하는 유연성을 늘렸습니다. 또한 여러 이벤트를 사용할 때 이벤트가 발생하는지 또는 이벤트가 추가되었을 때 발생하는지 &quot;모두&quot; 여부를 예측하는 옵션입니다. |
| 영향력 있는 요소 드릴다운 | 이제 성향 상위 영향력 있는 요소 버킷에 드릴다운 이 포함됩니다. 드릴다운 은 성향 버킷 내에 있는 가장 영향력 있는 각 요소에 대한 보다 심층적인 값 요약입니다. |

자세한 내용은 [Customer AI 개요](../../intelligent-services/customer-ai/overview.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. [!DNL Profile] 서로 다른 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 병합 정책 워크플로우가 업데이트되었습니다. | 플랫폼이 병합 정책 구성을 새로운 단계별 워크플로우로 업그레이드했습니다. 이 워크플로우를 통해 사용자는 여러 프로필 데이터 세트의 데이터 조각을 가져와서 각 개인을 종합적으로 볼 수 있도록 데이터를 해당 데이터 세트에 병합하는 방법에 대한 우선 순위를 설정할 수 있습니다. 사용자는 적절한 병합 방법(타임스탬프 순서 또는 데이터 세트 우선 순위)을 선택하고 프로필 데이터 세트에 ExperienceEvent 데이터 세트를 추가하여 선택한 XDM 개별 프로필 데이터 세트를 병합할 수 있습니다. |
| 결합 스키마 보기 | Experience Platform UI에서 사용자는 ID 및 관계 필드와 같은 표면 키 속성은 물론 결합 스키마에 기여하는 모든 스키마 및 데이터 세트에 대한 정보를 보다 쉽게 찾을 수 있습니다. 이러한 업데이트를 통해 프로필이 올바르게 구성되었는지, ID가 올바르게 결합되고, 데이터가 성공적으로 수집되었는지 문제를 해결하고 확인할 수 있습니다. |

작업 시 유용한 자습서 및 우수 사례를 비롯하여 실시간 고객 프로필에 대한 자세한 정보 [!DNL Profile] 데이터, [실시간 고객 프로필 개요](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL Shopify] | 이제 연결할 수 있습니다 [!DNL Shopify] to [!DNL Experience Platform] 사용 [!DNL Flow Service] API 또는 UI입니다. 자세한 내용은 [Shopify 커넥터 개요](../../sources/connectors/ecommerce/shopify.md) 추가 정보. |

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 연결 정보 업데이트 | 이제 를 사용하여 기존 배치 연결의 이름, 설명 및 자격 증명을 업데이트할 수 있습니다 [!DNL Flow Service] API 및 UI. 자세한 내용은 [흐름 서비스 API를 사용하여 연결 업데이트](../../sources/tutorials/api/update.md) 및 [ui를 사용하여 계정 세부 사항 편집](../../sources/tutorials/ui/monitor.md). |
| 연결 삭제 | 이제 오류가 있거나 불필요하게 된 배치 연결을 [!DNL Flow Service] API 및 UI. 자세한 내용은 [흐름 서비스 API를 사용하여 연결 삭제](../../sources/tutorials/api/delete.md) 및 [UI를 사용하여 계정 삭제](../../sources/tutorials/ui/delete-accounts.md). |
| 계층 매핑 | 데이터 수집 프로세스 중에 JSON 또는 Parquet과 같은 계층적 소스 파일을 미리 볼 수 있습니다. 다음에서 자습서를 참조하십시오. [ui에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 추가 정보. |
| 스트리밍 소스에서의 매핑을 위한 API 지원 | 이제 API를 사용하여 스트리밍 소스를 사용하여 매핑 기능을 수행할 수 있습니다. |
| 클라우드 스토리지 소스에 대한 사용자 지정 구분 기호에 대한 API 지원 | 이제 클라우드 저장소 소스를 사용하여 CSV로 구분된 파일이 아닌 파일을 수집할 수 있습니다. 탭, 쉼표, 파이프, 세미콜론 또는 해시와 같은 단일 열 구분 기호를 사용하여 플랫 파일을 임의의 형식으로 수집할 수 있습니다. |
| Adobe Audience Manager 커넥터에 대한 샌드박스 지원 | 이제 Audience Manager 커넥터가 샌드박스를 인식합니다. 사용자는 커넥터가 Audience Manager 데이터 세트를 선택한 샌드박스(비프로덕션 샌드박스 포함)로 라우팅할 수 있습니다. 구성은 IMS 조직당 하나의 샌드박스로 제한됩니다. |
| UX 개선 사항 | 이제 소스 카탈로그를 통해 파일 기반 처리에 액세스할 수 있습니다. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
