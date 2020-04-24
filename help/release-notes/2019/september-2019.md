---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트(2019년 9월 10일)
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 9월 10일**

Adobe Experience Platform의 기존 기능 업데이트:

* [데이터 통합](#ingestion)
* [데이터 과학 작업 영역](#dsw)
* [쿼리 서비스](#query)

## 데이터 통합 {#ingestion}

Adobe Experience Platform은 모든 유형의 데이터와 지연 시간을 인제스트할 수 있는 다양한 기능을 제공합니다. Adobe Experience Platform 데이터 인제스트는 배치 API, 스트리밍 API, 기본 Adobe 커넥터, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 비롯한 데이터 인제스트를 위한 다양한 대체 요소를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ----------- | ---------- |
| 스트리밍 처리를 위한 새로운 도메인 | 도메인이 `dcs.data.adobe.net` 새 일반 데이터 수집 도메인으로 이동되었습니다 `dcs.adobedc.net`. 사용자는 개정된 Adobe Experience Platform 스트리밍 통합 문서에 따라 구현을 업데이트해야 합니다. Adobe Experience Platform 스트리밍 통합 관련 모든 문서가 새 도메인을 사용하도록 업데이트되었습니다. |

자세한 내용은 데이터 통합 [설명서를](../../ingestion/home.md)참조하십시오.

## 데이터 과학 작업 영역 {#dsw}

Adobe Experience Platform Data Science Workspace는 경험 플랫폼 내에서 완벽하게 관리되는 서비스로, 데이터 과학자는 기계 학습 모델을 구축 및 운영하여 Adobe 솔루션 및 타사 시스템 전반에서 데이터와 컨텐츠로 얻은 인사이트를 원활하게 생성할 수 있습니다. 데이터 과학 작업 공간은 플랫폼과 긴밀하게 통합되어 있어 XDM 데이터 탐색 및 준비 등 전반적인 데이터 과학 라이프사이클과 시스템 학습 인사이트를 통해 실시간 고객 프로파일을 자동으로 강화할 수 있는 모델 개발 및 운영 등의 기능을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| UI를 통한 서비스 예약 | UI를 사용하여 사용자 정의 일정을 통해 모델 트레이닝 및 점수 지정을 자동화할 수 있는 플랫폼 오케스트레이션 서비스와 통합되었습니다. |
| 서비스 갤러리 | 재설계된 서비스 갤러리에서 자동화된 트레이닝 및 점수 지정 작업을 예약할 수 있는 기능을 통해 머신 러닝 서비스를 검색하고 모니터링 및 이용할 수 있습니다. |
| JupiterLab 5.0.0 | JupiterLab UI 개선 사항. |

**알려진 문제**

* 현재 서비스 갤러리에서는 기존 서비스를 삭제할 수 있는 액세스 가능한 방법이 없습니다. API 호출을 통해 기존 [서비스를 삭제하려면 Sensei Machine Learning API 참조를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 참조하십시오.
* 서비스 갤러리에 서비스의 교육 및 점수 실행을 필터링하기 위한 페이지 지정 지원이 없습니다.
* 서비스 갤러리를 통해 예약된 교육 또는 점수 지정을 구성할 때 빈도를 시간별로 설정하면 일정이 적용되지 않습니다.

자세한 내용은 데이터 과학 작업 [공간 개요를 참조하십시오](../../data-science-workspace/home.md).

## 쿼리 서비스 {#query}

쿼리 서비스는 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리하여 다양한 분석 및 데이터 관리 사용 사례를 지원하는 기능을 제공합니다. Data Lake의 데이터 집합에 참여하고 쿼리 결과를 보고, 데이터 과학 작업 공간 또는 실시간 고객 프로파일에 수집하기 위한 새로운 데이터 세트로 캡처할 수 있는 서버를 사용하지 않는 도구입니다.

Query Service를 사용하여 데이터 분석 환경을 구축하고 다양한 상호 작용 채널에서 고객의 그림을 만들 수 있습니다. 이러한 채널에는 판매 시점(POS) 시스템, 웹, 모바일 또는 CRM 시스템이 포함될 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 쿼리 편집기 개선 사항 | 쿼리를 저장하고 나중에 작업할 수 있도록 해주는 저장 기능을 추가했습니다. 조직의 사용자가 저장한 쿼리를 보여주는 &quot;검색&quot; 탭을 Adobe Experience Platform의 쿼리 서비스 사용자 인터페이스에 추가했습니다. 보고 있는 쿼리에 대한 유용한 메타데이터를 표시하는 &quot;쿼리 세부 사항&quot; 패널을 구현했습니다. |
| 새로운 속성 기능 | 만료 매개 변수를 사용하여 채널 속성을 쿼리하는 쿼리 서비스에 Adobe가 정의한 함수입니다. |
| 향상된 SQL 구문 | iLike 구문 지원. |
| 정의된 XDM 스키마를 사용하여 데이터 집합 생성 | 대상 스키마를 지정할 수 있는 CTAS(Create Table as Select) 쿼리에 새 절을 추가했습니다. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).