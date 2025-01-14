---
title: Adobe Experience Platform 릴리스 노트 2019년 9월
description: Adobe Experience Platform의 2019년 9월 릴리스 정보.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2019년 9월 10일 수요일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 수집할 수 있는 다양한 기능 세트를 제공합니다. Adobe Experience Platform [!DNL Data Ingestion]은(는) 일괄 처리 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 포함하여 데이터 수집을 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ----------- | ---------- |
| 스트리밍 수집을 위한 새 도메인 | `dcs.data.adobe.net` 도메인이 새 공통 데이터 수집 도메인 `dcs.adobedc.net`(으)로 이동되었습니다. 사용자는 수정된 Adobe Experience Platform 스트리밍 수집 설명서에 따라 구현을 업데이트해야 합니다. Adobe Experience Platform 스트리밍 수집과 관련된 모든 설명서가 새 도메인을 사용하도록 업데이트되었습니다. |

자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md)를 참조하세요.

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]은(는) [!DNL Experience Platform] 내의 완전히 관리되는 서비스로, 데이터 과학자가 머신 러닝 모델을 구축하고 운영하여 Adobe 솔루션 및 서드파티 시스템의 데이터와 콘텐츠에서 통찰력을 원활하게 생성할 수 있습니다. [!DNL Data Science Workspace]은(는) [!DNL Platform]과(와) 긴밀하게 통합되어 있으며 XDM 데이터 탐색 및 준비, 머신 러닝 인사이트로 [!DNL Real-Time Customer Profile]을(를) 자동으로 보강하는 모델 개발 및 운영 등 엔드투엔드 데이터 과학 라이프사이클을 지원합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI를 통한 서비스 예약 | [!DNL Platform] 오케스트레이션 서비스와 통합하여 UI를 사용하여 사용자 정의 일정으로 모델 교육 및 채점을 자동화합니다. |
| [!DNL Service Gallery] | 다시 설계된 [!DNL Service Gallery] 내에서 자동화된 교육 및 채점 작업을 예약하는 기능을 사용하여 머신 러닝 서비스를 탐색, 모니터링 및 액세스합니다. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI 개선 사항. |

**알려진 문제**

* 현재 [!DNL Service Gallery]에서 기존 서비스를 삭제할 수 있는 방법이 없습니다. 그동안 API 호출을 통해 기존 서비스를 삭제하려면 [Sensei 기계 학습 API 참조](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)를 참조하십시오.
* [!DNL Service Gallery]에는 서비스의 교육 및 채점 실행을 필터링하기 위한 페이지 매김이 지원되지 않습니다.
* [!DNL Service Gallery]을(를) 통해 예약된 교육 또는 채점 실행을 구성할 때 빈도를 시간별로 설정하면 일정이 적용되지 않습니다.

자세한 내용은 [데이터 과학 Workspace 개요](../../data-science-workspace/home.md)를 참조하세요.

## [!DNL Query Service] {#query}

[!DNL Query Service]은(는) 표준 SQL을 사용하여 Adobe Experience Platform의 데이터를 쿼리하여 다양한 분석 및 데이터 관리 사용 사례를 지원하는 기능을 제공합니다. [!DNL Data Lake]에서 데이터 세트에 참여하고 쿼리 결과를 보고 또는 [!DNL Data Science Workspace]에 수집하기 위한 새 데이터 세트로 캡처할 수 있는 서버를 사용하지 않는 도구입니다.[!DNL Real-Time Customer Profile]

[!DNL Query Service]을(를) 사용하여 데이터 분석 에코시스템을 구축하고 다양한 상호 작용 채널에서 고객의 그림을 그릴 수 있습니다. 이러한 채널에는 판매 지점 시스템, 웹, 모바일 또는 CRM 시스템이 포함될 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| [!DNL Query Editor] 개선 사항 | 쿼리를 저장하고 나중에 작업할 수 있는 저장 기능이 추가되었습니다. 조직의 사용자가 저장한 쿼리를 표시하는 Adobe Experience Platform의 [!DNL Query Service] 사용자 인터페이스에 &quot;찾아보기&quot; 탭을 추가했습니다. 조회 중인 쿼리에 대한 유용한 메타데이터를 표시하는 &quot;쿼리 세부 정보&quot; 패널을 구현했습니다. |
| 새로운 속성 함수 | 만료 매개 변수를 사용하여 채널 특성을 쿼리하기 위해 [!DNL Query Service]의 Adobe 정의 함수입니다. |
| SQL 구문 개선 사항 | iLike 구문 지원 |
| 정의된 XDM 스키마로 데이터 세트 생성 | 대상 스키마를 지정할 수 있는 CTAS(Create Table as Select) 쿼리에 새 절을 추가했습니다. |

자세한 내용은 [쿼리 서비스 설명서](../../query-service/home.md)를 참조하세요.
