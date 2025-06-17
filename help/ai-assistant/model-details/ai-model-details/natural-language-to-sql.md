---
title: AI Assistant 자연어 - SQL 모델 세부 정보
description: AI Assistant 자연어 - SQL AI 모델에 대해 알아봅니다.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 3d870c367317d73bba8b75b38f7b2a93ab6b5bbd
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# AI Assistant Operational Insights 자연어 - SQL 모델 세부 정보

>[!IMPORTANT]
>
>Adobe은 더 많은 모델 세부 정보를 게시하고 있습니다. 사용 가능한 추가 설명서가 Experience League에 추가됩니다.

## 모델 개요 {#model-overview}

* **모델 이름 및 버전**: Adobe Experience Platform AI Assistant Operational Insights 자연어 - SQL 모델([!DNL NL2SQL])
* **모델 릴리스 날짜**: 2025년 2월
* **모델 목적**: 이 모델은 운영 통찰력에 대한 고객의 자연어 쿼리를 SQL 쿼리로 번역하도록 설계되었습니다. 이러한 SQL 쿼리는 스키마, 데이터 세트, 대상, 대상 및 여정 등 고객의 Experience Platform 엔티티에 대한 메타데이터가 포함된 Adobe Experience Platform 지식 그래프를 통해 실행됩니다. 그런 다음 SQL 쿼리 결과를 사용하여 고객의 원래 자연어 질문에 대한 응답을 생성합니다.
* **의도한 사용자**: 이 모델의 주 사용자는 마케팅 전문가, 데이터 분석가 또는 고객 여정 관리자입니다. 이들은 자연어를 사용하여 Experience Platform 내에서 운영 통찰력을 이해하고 작용하려고 합니다. SQL 또는 데이터 엔지니어링의 전문가가 아닐 수 있지만 정보에 입각한 결정을 내리고 고객 경험을 최적화하기 위해 Experience Platform 엔티티에 대한 빠르고 정확한 답변이 필요합니다.
* **사용 사례**: 이 모델은 사용자가 대상, 여정, 스키마, 특성, 데이터 세트 및 대상과 같은 Experience Platform 엔터티에 대한 메타데이터에 액세스할 수 있도록 지원합니다. 사용자는 어떤 대상이 활성화되었는지 또는 특정 스키마를 사용하고 있는지 등의 질문을 자연어로 던질 수 있으며 모델은 이를 Experience Platform 지식 그래프를 통해 SQL 쿼리로 변환합니다. 이를 통해 사용자는 시스템을 수동으로 탐색하거나 쿼리할 필요 없이 신속하게 운영 가시성을 확보하고 정보에 입각한 결정을 내릴 수 있습니다.
* **문제점**: 이 모델은 대규모 상호 연결된 메타데이터를 탐색하는 데 따르는 복잡성, 운영 통찰력을 검색하기 위해 SQL 쿼리를 수동으로 작성해야 하는 필요성, 대상, 데이터 세트, 여정과 같은 Experience Platform 엔터티가 연결되거나 수행되는 방식에 대한 가시성 부족 등 Experience Platform과 함께 작업하는 비즈니스 사용자 및 분석가가 직면하는 주요 문제점을 해결합니다. 이 모델은 메타데이터에 자연어 액세스를 가능하게 하고 SQL 생성을 자동화함으로써 기술 리소스에 대한 의존도를 줄이고, insight 검색 시간을 단축하며, 사용자가 데이터 중심의 더 빠른 의사 결정을 내릴 수 있도록 해 줍니다.

## 모델 세부 정보 {#model-details}

* **모델 유형**: 동적 컨텍스트 내 학습이 포함된 LLM 프롬프트
* **입력**: 사용자 자연어 쿼리입니다.
* **출력**: 이 모델은 Experience Platform 지식 그래프를 통해 실행되는 [!DNL Snowflake] 구문으로 SQL 쿼리를 출력합니다.

**입력 예**

```console
How many datasets were created within the last 10 days?
```

**출력 예**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## 모델 평가 {#model-evaluation}

* **평가 지표 및 프로시저**: [!DNL NL2SQL] 요청을 보고 올바른 SQL 결과를 생성하는 요청 수를 평가하여 모델을 평가합니다. 평가 프로세스는 규칙 기반 일치(SQL 표준화 후 직접 SQL 문자열 일치), LLM 기반 SQL 해 찾기 및 사람 평가의 조합입니다.
* **평가 데이터 및 사전 처리**: 회귀 테스트를 위해 오픈 세트를 사용하며, 샘플링된 실제 고객 트래픽을 통해 모델의 성능을 모니터링하는 주별 주석 프로젝트도 있습니다.

## 모델 배포 {#model-deployment}

* **모델 모니터링**: 기본 모델은 [!DNL Azure]에 의해 호스팅됩니다.
* **모델 업데이트**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model은 물음표 확장을 통해 정기적으로(매주) 업데이트됩니다. 필요할 때 새로운 프롬프트 전략 및 지침을 통해 모델을 업데이트하기도 합니다.

## 공정성과 편견 {#fairness-and-bias}

* Adobe **모델 공정성**: 모델이 다양한 사용자 의도와 언어적 변형에 걸쳐 일관되게 쿼리를 해석하고 생성하도록 하려면 편견 또는 비윤리적인 출력을 생성하지 않도록 신속한 감사, 설명, 보호 조치를 사용합니다.
* **데이터 편향**: 모델 출력은 컨텍스트 내 학습 예제와 검색기가 프롬프트에서 선택하는 내용에 의해 영향을 받습니다. 질문 은행 사례에는 상품 관리의 관점에서 대표적이라고 생각되는 예들이 포함되어 있다. 사용 사례에 따라 고객은 모델 출력의 잠재적 편향이 의도한 애플리케이션과 어떻게 일치하거나 영향을 미칠 수 있는지 고려해야 합니다.

## 윤리적 고려 사항 {#ethical-considerations}

**모델과 관련된 윤리적 고려 사항**: PII 또는 민감한 특성이 노출되지 않도록 기존 데이터 편향을 강화하고 액세스 제어 경계를 준수하도록 모델을 설계했습니다. 여기에는 책임 있는 사용을 위한 필터링, 태깅 및 스키마 필드 감사가 포함됩니다.
