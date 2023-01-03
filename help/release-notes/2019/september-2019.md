---
title: Adobe Experience Platform 릴리스 노트 - 2019년 9월
description: Adobe Experience Platform에 대한 2019년 9월 릴리스 노트입니다.
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

Adobe Experience Platform은 모든 유형의 데이터와 지연을 수집하는 풍부한 기능을 제공합니다. Adobe Experience Platform [!DNL Data Ingestion] 에서는 일괄 처리 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 포함한 데이터를 수집하기 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ----------- | ---------- |
| 신규 스트리밍 수집의 도메인 | 다음 `dcs.data.adobe.net` 도메인이 새 일반 데이터 수집 도메인으로 이동되었습니다 `dcs.adobedc.net`. 수정된 Adobe Experience Platform 스트리밍 수집 설명서에 따라 구현을 업데이트해야 합니다. 새 도메인을 사용하도록 Adobe Experience Platform 스트리밍 수집과 관련된 모든 설명서를 업데이트했습니다. |

자세한 내용은 [데이터 수집 설명서](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 는 내에서 완전히 관리되는 서비스입니다 [!DNL Experience Platform] 이를 통해 데이터 과학자가 시스템 학습 모델을 구축 및 운영하여 Adobe 솔루션 및 타사 시스템 전반에서 데이터와 컨텐츠를 통해 통찰력을 원활하게 생성할 수 있습니다. [!DNL Data Science Workspace] 는 [!DNL Platform] 및 는 XDM 데이터 탐색 및 준비 등 종단 간 데이터 과학 라이프사이클을 지원하고 모델 개발 및 운영 과정을 통해 자동으로 보강합니다 [!DNL Real-Time Customer Profile] ( 머신 러닝 인사이트 사용)

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI를 통한 서비스 예약 | 통합 [!DNL Platform] Orchestration Service를 통해 UI를 사용하여 사용자 정의 스케줄로 모델 교육 및 점수 책정 자동화 |
| [!DNL Service Gallery] | 재설계에서 자동 교육 및 점수 책정 작업을 예약할 수 있는 기능을 통해 기계 학습 서비스를 탐색, 모니터링 및 액세스할 수 있습니다 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI 개선 사항. |

**알려진 문제**

* 현재 에는 액세스할 수 있는 방법이 없습니다 [!DNL Service Gallery] 기존 서비스를 삭제하려면 다음을 수행하십시오. 그 동안에는 [Sensei 기계 학습 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) api 호출을 통해 기존 서비스를 삭제하려면 다음을 수행하십시오.
* 다음 [!DNL Service Gallery] 서비스의 교육 및 점수 실행을 필터링하기 위한 페이지 매김 지원이 없습니다.
* 예약된 교육 또는 점수를 구성할 때 다음을 통해 실행됩니다 [!DNL Service Gallery]를 시간별로 설정하면 예약이 적용되지 않습니다.

자세한 내용은 [데이터 과학 작업 공간 개요](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 에서는 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리하여 다양한 분석 및 데이터 관리 사용 사례를 지원합니다. 에서 데이터 세트에 가입할 수 있는 서버를 사용하지 않는 도구입니다 [!DNL Data Lake] 쿼리 결과를 보고에 사용할 새 데이터 세트로 캡처하고 [!DNL Data Science Workspace], 또는 를 수집하여 [!DNL Real-Time Customer Profile].

다음을 사용할 수 있습니다 [!DNL Query Service] 데이터 분석 에코시스템을 구축하려면 다양한 상호 작용 채널에서 고객의 사진을 만들어야 합니다. 이러한 채널에는 판매 지점 시스템, 웹, 모바일 또는 CRM 시스템이 포함될 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 개선 사항 [!DNL Query Editor] | 쿼리를 저장하고 나중에 작업할 수 있는 저장 함수가 추가되었습니다. 에 &quot;찾아보기&quot; 탭을 추가했습니다. [!DNL Query Service] 조직의 사용자가 저장한 쿼리를 보여주는 Adobe Experience Platform의 사용자 인터페이스. 보고 있는 쿼리에 대한 유용한 메타데이터를 표시하는 &quot;쿼리 세부 사항&quot; 패널을 구현했습니다. |
| 새로운 속성 함수 | 의 Adobe 정의 함수 [!DNL Query Service] 만료 매개 변수가 있는 채널 속성을 쿼리하려면 |
| SQL 구문 개선 사항 | iLike 구문 지원. |
| 정의된 XDM 스키마를 사용하여 데이터 세트 생성 | 대상 스키마를 지정할 수 있는 CTAS(Create Table as Select) 쿼리에 새 절을 추가했습니다. |

자세한 내용은 [Query Service 설명서](../../query-service/home.md).
