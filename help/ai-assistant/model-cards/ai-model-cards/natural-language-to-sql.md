---
title: AI Assistant 자연어 - SQL 모델 카드
description: AI Assistant 자연어 - SQL AI 모델에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AI Assistant Operational Insights 자연어 - SQL 모델 카드

## 모델 개요 {#model-overview}

* 모델의 공식 이름은 AI Assistant Operational Insights Natural Language to SQL Model([!DNL NL2SQL])이며 2025년 2월 최신 GA 버전에서 출시되었습니다.
* 이 모델은 운영 통찰력에 대한 고객의 자연어 쿼리를 SQL 쿼리로 번역하도록 설계되었습니다. 이러한 SQL 쿼리는 스키마, 데이터 세트, 대상, 대상 및 여정 등 고객의 Experience Platform 엔티티에 대한 메타데이터가 포함된 Adobe Experience Platform 지식 그래프를 통해 실행됩니다. 그런 다음 SQL 쿼리 결과를 사용하여 고객의 원래 자연어 질문에 대한 응답을 생성합니다.
* 이 모델의 주요 사용자는 마케팅 전문가, 데이터 분석가 또는 고객 여정 관리자로서 자연어를 사용하여 Experience Platform 내에서 운영 통찰력을 이해하고 작용하려는 사람입니다. SQL 또는 데이터 엔지니어링의 전문가가 아닐 수 있지만 정보에 입각한 결정을 내리고 고객 경험을 최적화하기 위해 Experience Platform 엔티티에 대한 빠르고 정확한 답변이 필요합니다.
* 이 모델은 Operational Insights용 AI Assistant의 일부로, 사용자가 대상, 여정, 스키마, 특성, 데이터 세트 및 대상과 같은 Experience Platform 엔티티에 대한 메타데이터에 액세스할 수 있도록 지원합니다. 사용자는 어떤 대상이 활성화되었는지 또는 특정 스키마를 사용하고 있는지 등의 질문을 자연어로 던질 수 있으며 모델은 이를 Experience Platform 지식 그래프를 통해 SQL 쿼리로 변환합니다. 이를 통해 사용자는 시스템을 수동으로 탐색하거나 쿼리할 필요 없이 신속하게 운영 가시성을 확보하고 정보에 입각한 결정을 내릴 수 있습니다.
* 이 모델은 대규모 상호 연결된 메타데이터를 탐색하는 데 따르는 복잡성, 운영 통찰력을 검색하기 위해 SQL 쿼리를 수동으로 작성해야 하는 필요성, 대상, 데이터 세트 및 여정과 같은 Experience Platform 엔티티가 연결되거나 수행되는 방식에 대한 가시성 부족 등과 같이 Experience Platform을 사용하여 작업하는 비즈니스 사용자 및 분석가가 직면하는 주요 문제를 해결합니다. 이 모델은 메타데이터에 자연어 액세스를 가능하게 하고 SQL 생성을 자동화함으로써 기술 리소스에 대한 의존도를 줄이고, insight 검색 시간을 단축하며, 사용자가 데이터 중심의 더 빠른 의사 결정을 내릴 수 있도록 해 줍니다.
* 고객 이름, 이메일 주소 또는 전화 번호와 같은 개인 식별 정보(PII)가 플랫폼에 존재하는 경우에도 이 모델을 사용하여 액세스하거나 추론해서는 안 됩니다.
* 또한 데이터 보존 정책, 액세스 제어 규칙 또는 동의 상태 확인과 같은 규정 준수 또는 거버넌스 확인에 활용해서는 안 됩니다. 이러한 작업에는 전문적인 시스템과 전략이 필요하다.

## 모델 세부 정보 {#model-details}

* 모델 유형은 동적 컨텍스트 내 학습을 사용하는 LLM 프롬프트입니다.
* 모델 입력은 사용자 자연어 쿼리입니다.
* 이 모델은 Experience Platform Knowledge Graph를 통해 실행되는 [!DNL Snowflake] 구문으로 SQL 쿼리를 출력합니다.

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

## 모델 교육 {#model-training}

* [!DNL NL2SQL]이(가) 컨텍스트 내 학습에 [!DNL OpenAI]개의 GPT 기반 모델을 사용했습니다.
* [!DNL NL2SQL] 질문 뱅크에는 알파 사용 사례에 대한 [!DNL Operational Insights] 팀의 428개 쿼리와 외부 팀의 524개 쿼리가 포함되어 있습니다.

## 모델 평가 {#model-evaluation}

* 모델은 정확도를 사용하여 평가됩니다. 예를 들어 모든 [!DNL NL2SQL]개의 요청 중 올바른 SQL 결과를 생성하는 요청의 수는 몇 개입니까?
* 평가 프로세스는 규칙 기반 일치(SQL 표준화 후 직접 SQL 문자열 일치), LLM 기반 SQL 해 찾기 및 사람 평가의 조합입니다
* 오픈 세트는 회귀 테스트에 사용되며 주별 주석 프로젝트는 샘플링된 실제 고객 트래픽을 통해 모델의 성능을 모니터링합니다.
* 적대적 평가와 관련하여 [!DNL NL2SQL]에 대한 보호 기능 역할을 하는 별도의 범위 내 및 범위 외 모델이 있습니다.

## 모델 배포 {#model-deployment}

* LLM 모델은 [!DNL Azure OpenAI] API에서 호스팅하는 GPT 기반 모델입니다.
* 기본 모델은 [!DNL Azure]에 의해 호스팅됩니다.
* 모델은 문항 은행 확장을 통해 매주 정기적으로 업데이트됩니다. 필요한 경우 새로운 프롬프트 전략 및 지침을 통해 모드 목록도 업데이트됩니다.

## 설명성 {#explainability}

이 모델은 SQL에 대해 별도의 설명 모델을 사용합니다.

## 공정성과 편견 {#fairness-and-bias}

* 모델이 편향성을 도입하거나 스테레오타입을 강화하지 않고 다양한 사용자 의도와 언어적 변형에서 일관되게 쿼리를 해석하고 생성하도록 보장하기 위해 Adobe은 신속한 감사, 설명 가능성 및 편향되거나 비윤리적인 출력을 생성하지 않는 보호 장치를 사용합니다.
* 모델 출력은 컨텍스트 내 학습 예제와 검색자가 프롬프트에서 선택하는 내용에 의해 영향을 받습니다. 문항은행 사례는 PM의 입장에서 대표적으로 여겨지는 사례를 담고 있으며, 실제 고객 동선을 바탕으로 문항은행을 확대하고 있다.

## 견고성 {#robustness}

그것이 받는 대부분의 쿼리는 문제 은행에서 다루지 않기 때문에, 생산 트래픽 정확도는 모델의 견고성을 반영한다.

## 개인 정보 보호 및 보안 고려 사항 {#privacy-and-security-considerations}

모델은 PII(개인 식별 정보)를 처리하거나 유지하지 않으며, 이러한 정보는 SQL 생성을 위해 마스킹됩니다. 속성 기반 액세스 제어 권한 검사의 경우, 생성된 SQL은 거버넌스 품질을 보장하기 위해 Experience Platform Knowledge Graph 팀에서 추가로 처리됩니다.

## 윤리적 고려 사항 {#ethical-considerations}

PII 또는 민감한 특성이 노출되지 않도록 하기 위해 모델은 개인 정보를 지원하고, 기존 데이터 편향을 강화하지 않고, 액세스 제어 경계를 준수하도록 설계되었습니다. 여기에는 책임 있는 사용을 위한 필터링, 태깅 및 스키마 필드 감사가 포함됩니다.

