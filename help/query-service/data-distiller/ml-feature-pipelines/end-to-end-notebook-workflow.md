---
title: AI/ML 데이터 파이프라인 강화 통합 워크플로
description: 클라우드 기반 머신 러닝 환경 notebooks를 사용하여 Adobe Experience Platform 데이터에서 구독 전환을 예측하는 교육 및 점수 책정 모델을 만듭니다.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# AI/ML 데이터 파이프라인 강화 통합 워크플로

Data Distiller을 사용하여 Adobe Experience Platform에서 수집 및 선별된 고가치 고객 경험 데이터로 머신 러닝 파이프라인을 보강합니다.

이 문서에서는 전체적인 워크플로를 보여 주는 일련의 클라우드 기반 머신 러닝 환경 전자 필기장을 제공합니다. 워크플로는 기본 머신 러닝 도구를 사용하여 Experience Platform 데이터와 함께 마케팅 사용 사례를 지원하는 사용자 정의 데이터 모델을 구축합니다.

이 워크플로를 사용하려면 [!DNL Python] 기계 학습 환경의 전자 필기장입니다. 시작하기 위한 지침 [!DNL Python] 노트북은 해당 readme 파일에 포함되어 있습니다.

이 안내서를 계속 진행하기 전에 [AI/ML 기능 파이프라인 개요](./overview.md) 이 AI/ML 기능 파이프라인 사용 사례에서 사용되는 샘플 Python 노트북의 사용을 활성화하려면 다음을 수행하십시오.

## 클라우드 머신 러닝 환경 노트북 {#cmle-notebooks}

엔드 투 엔드 워크플로우는 워크플로를 구현하는 데 사용되는 서비스에 따라 세 가지 광범위한 단계로 나눌 수 있습니다.

- 플랫폼 데이터의 초기 탐색 및 준비는 플랫폼 서비스에 의존합니다.
- 모델 교육 및 점수는 클라우드 기반 ML 환경의 도구 기능을 활용합니다. ML 플랫폼에 대한 일반적인 선택으로는 Databricks ML, AWS Sagemaker, DataRobot 등이 있습니다.
- 점수를 플랫폼으로 다시 수집하고 이를 기반으로 한 코드 기반 대상 생성 및 활성화는 다시 플랫폼 서비스를 사용합니다.

그러나 이러한 모든 단계는 사용자가 플랫폼과 클라우드 기반 ML 도구 간에 컨텍스트를 전환할 필요 없이 ML 환경에서 하나 이상의 노트북에서 실행할 수 있습니다.

이러한 전체적인 흐름의 일반적인 단계는 모듈식 노트북으로 나뉘어 있으며, 모듈식 노트북에서는 플랫폼 데이터와 관련된 일반적인 머신 러닝 프로젝트의 단계를 보여줍니다. 이렇게 하면 특정 활동을 구현하기 위한 참조로 노트북을 더 쉽게 사용할 수 있으며, 관련 노트북에서 코드를 선택하고 조정하여 실제 사용 사례를 구현할 수 있습니다. 실제로 데이터 과학자는 ML 프로젝트에 대한 엔드 투 엔드 파이프라인을 구현하는 단일 노트북을 준비할 수 있습니다. 또는 데이터 과학자는 ML 플랫폼에서 UI 기반 기능을 사용하여 프로젝트를 계속하기 전에 플랫폼 데이터를 쿼리하고 ML 환경에서 사용할 수 있도록 샘플 코드를 간단하게 조정할 수 있습니다.

연결된 저장소에 포함된 샘플 전자 필기장이 아래에 간략하게 설명되어 있습니다. 각 전자 필기장에 대한 자세한 설명서는 전자 필기장 자체의 코드와 함께 제공됩니다.

<!-- Below is the meat - the how to (but without links or details) -->

### 합성 데이터 생성 {#generate-synthetic-data}

이 전자 필기장은 CMLE 워크플로를 설명하는 데 사용할 합성 프로필 및 플랫폼에서 경험 이벤트의 데이터 세트를 생성하는 코드를 제공합니다.

### 쿼리 서비스로 EDA 및 피쳐 생성 {#eda-and-featurization-with-query-service}

이 전자 필기장에는 Platform Query Service를 통한 대화형 쿼리를 사용하는 Platform 데이터 세트에 대한 탐색적 분석의 예가 포함되어 있습니다. 이러한 항목 뒤에 예제 성향 모델에 대한 교육 데이터 세트를 만들기 위한 기능 쿼리 예제가 나옵니다.

### 교육 데이터 내보내기 {#export-training-data}

이 노트북에서는 ML 도구에서 읽을 수 있는 클라우드 스토리지로 교육 데이터 세트를 내보내는 방법을 보여 줍니다.

### 성향 모델 교육 {#train-a-propensity-model}

이 전자 필기장은 성향 모델 교육을 보여 줍니다. Databricks ML을 ML 환경으로 간주하지만 다른 플랫폼에 맞게 조정할 수 있도록 일반적으로(즉, Databricks 관련 기능/API를 많이 사용하지 않고) 작성됩니다.

### 성향 모델에 점수 매기기

이 노트북에서는 각 플랫폼 고객 프로필에 대한 성향 점수 데이터 세트를 생성할 수 있도록 훈련된 성향 모델에 대한 점수를 매기는 방법을 설명합니다.

### AEP로 점수 수집

이 간략한 전자 필기장은 AEP에서 고객 프로필을 보강하기 위해 성향 점수 데이터 세트를 수집하는 방법을 보여줍니다.

### 코드에서 대상자 만들기 및 활성화

이 전자 필기장은 사용자가 전자 필기장 코드에서 Platform 앱을 통해 점수에서 대상을 만들고 이러한 대상을 활성화하는 방법을 보여 줍니다.
