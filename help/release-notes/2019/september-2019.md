---
title: Adobe Experience Platform 릴리스 노트 2019년 9월
description: Adobe Experience Platform의 2019년 9월 릴리스 정보.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 9월 10일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 수집할 수 있는 다양한 기능 세트를 제공합니다. Adobe Experience Platform [!DNL Data Ingestion] 일괄 처리 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 포함하여 데이터 수집을 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ----------- | ---------- |
| 신규 스트리밍 수집을 위한 도메인 | 다음 `dcs.data.adobe.net` 도메인이 새 공통 데이터 수집 도메인으로 이동되었습니다. `dcs.adobedc.net`. 사용자는 수정된 Adobe Experience Platform 스트리밍 수집 설명서에 따라 구현을 업데이트해야 합니다. Adobe Experience Platform 스트리밍 수집과 관련된 모든 설명서가 새 도메인을 사용하도록 업데이트되었습니다. |

자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 은(는) 내의 전체 관리 서비스입니다. [!DNL Experience Platform] 이를 통해 데이터 과학자는 머신 러닝 모델을 구축하고 운영하여 Adobe 솔루션 및 서드파티 시스템 전반의 데이터와 콘텐츠에서 통찰력을 원활하게 생성할 수 있습니다. [!DNL Data Science Workspace] 와 밀접하게 통합되어 있습니다. [!DNL Platform] 및 는 XDM 데이터 탐색 및 준비, 자동 강화 모델 개발 및 운영을 포함하여 종단간 데이터 과학 라이프사이클을 강화합니다 [!DNL Real-Time Customer Profile] (기계 학습 통찰력 포함)

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI를 통한 서비스 예약 | 통합 [!DNL Platform] Orchestration Service를 통해 UI를 사용하여 사용자 정의 일정으로 모델 교육 및 채점을 자동화할 수 있습니다. |
| [!DNL Service Gallery] | 재설계된 모든 내에서 자동화된 교육 및 채점 작업을 예약할 수 있는 기능을 통해 머신 러닝 서비스를 탐색, 모니터링 및 액세스합니다 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI 개선 사항. |

**알려진 문제**

* 현재에 액세스할 수 있는 방법이 없습니다. [!DNL Service Gallery] 기존 서비스를 삭제합니다. 그 동안 다음을 참조하십시오. [Sensei 머신 러닝 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) API 호출을 통해 기존 서비스를 삭제합니다.
* 다음 [!DNL Service Gallery] 은(는) 서비스의 교육 및 채점 실행을 필터링할 수 있는 페이지 매김을 지원하지 않습니다.
* 다음을 통해 예약된 교육 또는 채점 실행을 구성할 때: [!DNL Service Gallery]에서 빈도를 시간별로 설정하면 일정이 적용되지 않습니다.

자세한 내용은 [데이터 과학 작업 영역 개요](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 는 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리하여 다양한 분석 및 데이터 관리 사용 사례를 지원하는 기능을 제공합니다. 에서 데이터 세트를 결합할 수 있는 서버를 사용하지 않는 도구입니다 [!DNL Data Lake] 보고에 사용할 새 데이터 세트로 쿼리 결과를 캡처합니다. [!DNL Data Science Workspace]또는 를 통해 수집할 수 있습니다 [!DNL Real-Time Customer Profile].

다음을 사용할 수 있습니다. [!DNL Query Service] 데이터 분석 에코시스템을 구축하기 위해 다양한 상호 작용 채널에서 고객의 그림을 만듭니다. 이러한 채널에는 판매 지점 시스템, 웹, 모바일 또는 CRM 시스템이 포함될 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 개선 사항 [!DNL Query Editor] | 쿼리를 저장하고 나중에 작업할 수 있는 저장 기능이 추가되었습니다. 에 &quot;찾아보기&quot; 탭이 추가되었습니다. [!DNL Query Service] 조직의 사용자가 저장한 쿼리를 보여 주는 Adobe Experience Platform의 사용자 인터페이스입니다. 조회 중인 쿼리에 대한 유용한 메타데이터를 표시하는 &quot;쿼리 세부 정보&quot; 패널을 구현했습니다. |
| 새로운 속성 함수 | 에서 Adobe 정의 함수 [!DNL Query Service] 만료 매개 변수를 사용하여 채널 속성을 쿼리합니다. |
| SQL 구문 개선 사항 | iLike 구문 지원 |
| 정의된 XDM 스키마로 데이터 세트 생성 | 대상 스키마를 지정할 수 있는 CTAS(Create Table as Select) 쿼리에 새 절을 추가했습니다. |

자세한 내용은 [쿼리 서비스 설명서](../../query-service/home.md).
