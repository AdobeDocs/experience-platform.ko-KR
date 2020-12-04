---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 10월 9일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 인제스트하는 다양한 기능을 제공합니다. Adobe Experience Platform [!DNL Data Ingestion] 는 배치 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 비롯한 데이터 인제스트를 위한 여러 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ----------- | ---------- |
| 스트리밍 처리를 위한 새로운 도메인 | 도메인이 새 일반 데이터 수집 도메인으로 이동되었습니다 `dcs.data.adobe.net` `dcs.adobedc.net`. 사용자는 개정된 Adobe Experience Platform 스트리밍 통합 설명서에 따라 구현을 업데이트해야 합니다. Adobe Experience Platform 스트리밍 섭취 관련 모든 설명서가 새 도메인을 사용하도록 업데이트되었습니다. |

자세한 내용은 [데이터 수집 설명서를 참조하십시오](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 는 완전 관리되는 서비스로서, 머신 러닝 모델을 구축 및 운영하여 데이터 과학자가 Adobe 솔루션 및 타사 시스템에서 데이터 및 컨텐츠에 대한 인사이트를 원활하게 생성할 수 [!DNL Experience Platform] 있습니다. [!DNL Data Science Workspace] XDM 데이터 [!DNL Platform] 의 탐색 및 준비 등 종합적인 데이터 과학 라이프사이클과 긴밀하게 통합되어 있으며, CDM 데이터 개발 및 운영 체제에 따라 CMS(Machine Learning Insights)를 통해 자동으로 풍부한 기능을 제공합니다 [!DNL Real-time Customer Profile] .

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI를 통한 서비스 예약 | UI를 사용하여 사용자 정의 일정에 따라 모델 트레이닝 및 점수를 자동화할 수 있는 통합 운영 서비스 [!DNL Platform] |
| [!DNL Service Gallery] | 새로워진 기능 내에서 자동화된 트레이닝 및 점수 지정 작업을 예약할 수 있는 기능을 통해 머신 러닝 서비스를 검색하고 모니터링 및 이용할 수 있습니다 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI 개선 사항. |

**알려진 문제**

* 현재 서비스 삭제 방법은 [!DNL Service Gallery] 없습니다. API 호출을 통해 기존 서비스를 삭제하려면 [Sensei 기계 학습 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 자료를 참조하십시오.
* 서비스 트레이닝 및 점수 실행을 필터링하기 위한 페이지 매김 지원이 [!DNL Service Gallery] 없습니다.
* 예약된 교육 또는 점수 지정이 을 통해 실행될 때 빈도를 시간별로 설정하면 예약 [!DNL Service Gallery]이 적용되지 않습니다.

자세한 내용은 [데이터 과학 작업 공간 개요를 참조하십시오](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 는 다양한 분석 및 데이터 관리 사용 사례를 지원하기 위해 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리하는 기능을 제공합니다. It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. 이러한 채널에는 판매 시점(POS) 시스템, 웹, 모바일 또는 CRM 시스템이 포함될 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 향상된 기능 [!DNL Query Editor] | 쿼리를 저장하고 나중에 작업할 수 있도록 해주는 저장 기능을 추가했습니다. 조직의 사용자가 저장한 쿼리를 보여주는 &quot;검색&quot; 탭을 Adobe Experience Platform의 [!DNL Query Service] 사용자 인터페이스에 추가했습니다. 보고 있는 쿼리에 대한 유용한 메타데이터를 표시하는 &quot;쿼리 세부 사항&quot; 패널을 구현했습니다. |
| 새로운 속성 기능 | 만료 매개 변수를 사용하여 채널 속성에 대한 쿼리 [!DNL Query Service] 에 Adobe이 정의된 함수입니다. |
| SQL 구문 개선 사항 | iLike 구문을 지원합니다. |
| 정의된 XDM 스키마를 사용하여 데이터 집합 생성 | 대상 스키마를 지정할 수 있는 CTAS(Create Table as Select) 쿼리에 새 절을 추가했습니다. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).