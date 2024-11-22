---
title: 기능 엔지니어링 SQL 확장
description: 고급 통계 모델링을 위해 데이터를 사전 처리하는 데이터 Distiller 기능 엔지니어링 SQL 확장에 대해 알아봅니다. 사용 가능한 기능 추출, 변환 및 선택 기술에 대해 설명합니다.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# 기능 엔지니어링 SQL 확장

>[!AVAILABILITY]
>
>이 기능은 Data Distiller 추가 기능을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

SQL Transformer 확장을 사용하여 데이터 사전 처리를 단순화하고 자동화하여 엔지니어링 요구 사항을 충족합니다. 이 확장을 사용하여 피쳐를 구축하고 모델과 연관시키는 것을 포함하여 다양한 피쳐 엔지니어링 기술을 사용하여 원활한 실험을 수행할 수 있습니다. 분산 컴퓨팅을 위해 설계된 이 솔루션을 사용하면 대규모 데이터 세트에 대해 병렬 및 확장 가능한 방식으로 기능 엔지니어링을 수행할 수 있으므로 데이터 Distiller 기능 엔지니어링 SQL 확장을 사용하여 데이터 전처리에 필요한 시간을 크게 줄일 수 있습니다.

## 기술 개요 {#technique-overview}

이 기능 엔지니어링 기능은 기능 추출, 기능 변환 및 기능 선택의 세 가지 주요 영역을 다룹니다. 각 영역에는 데이터 사전 처리를 추출, 변환, 집중 및 개선하기 위해 설계된 특정 기능이 포함됩니다.

### 기능 추출 {#feature-extraction}

데이터, 특히 텍스트 데이터에서 관련 정보를 추출하고 지원되는 모델이 사용하거나 데이터 세트를 변환 및 파생할 수 있는 숫자 형식으로 변환합니다. 다음 기능을 사용하여 피쳐 추출을 수행합니다.

- **[텍스트 변환기](./feature-transformation.md#textual-transformations)**: 텍스트 데이터를 숫자 기능으로 변환합니다.
- **[Count Vectorizer](./feature-transformation.md#countvectorizer)**: 텍스트 문서 컬렉션을 토큰 카운트의 벡터로 변환합니다.
- **[N-그램](./feature-transformation.md#ngram)**: 텍스트 데이터에서 n-그램 시퀀스를 생성합니다.
- **[정지어 제거기](./feature-transformation.md#stopwordsremover)**: 의미가 크지 않은 일반적인 단어를 필터링합니다.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: 말뭉치와 관련하여 문서에 있는 단어의 중요도를 측정합니다.
- **[토큰화 도구](./feature-transformation.md#tokenizer)**: 텍스트를 개별 용어(단어)로 분류합니다.
- **[Word2Vec](./feature-transformation.md#word2vec)**: 단어를 고정 크기 벡터에 매핑하고 단어 임베딩을 만듭니다.

### 기능 변환 {#feature-transformation}

피쳐를 추출할 뿐만 아니라 다음의 일반 변환기를 사용하여 고급 통계 모델 및 파생된 데이터 세트에 대한 피쳐를 준비합니다. 배율 조정, 표준화 또는 인코딩을 적용하여 피쳐가 동일한 배율에 있고 비슷한 분포를 갖도록 합니다.

#### 일반적인 변압기

다음은 데이터 사전 처리 워크플로를 개선하기 위해 다양한 데이터 유형을 처리하는 도구 목록입니다.

- **[숫자 컴퓨터](./feature-transformation.md#numeric-imputer)**: 숫자 열의 누락된 값을 평균이나 중위수와 같은 지정된 값으로 채웁니다.
- **[문자열 Imputer](./feature-transformation.md#string-imputer)**: 누락된 문자열 값을 열에서 가장 빈번한 문자열과 같이 지정된 값으로 바꿉니다.
- **[벡터 어셈블러](./feature-transformation.md#vector-assembler)**: 여러 열을 단일 벡터 열로 결합하여 머신 러닝 모델에 사용할 데이터를 준비합니다.
- **[부울 컴퓨터](./feature-transformation.md#boolean-imputer)**: 누락된 부울 값을 `true` 또는 `false`과(와) 같이 지정된 값으로 채웁니다.

#### 숫자 변환기

이러한 기술을 적용하여 수치 데이터를 효과적으로 처리하고 확장하여 모델 성능을 향상시킵니다.

- **[이진수](./feature-transformation.md#binarizer)**: 연속 기능을 임계값에 따라 이진 값으로 변환합니다.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: 연속 기능을 개별 버킷에 매핑합니다.
- **[최소-최대 스케일러](./feature-transformation.md#minmaxscaler)**: 기능을 지정된 범위(일반적으로 [0, 1])로 다시 스케일합니다.
- **[최대 Abs 스케일러](./feature-transformation.md#maxabsscaler)**: 희소성을 변경하지 않고 기능을 [-1, 1] 범위로 다시 스케일합니다.
- **[정규화기](./feature-transformation.md#normalizer)**: 단위 정규성을 갖도록 벡터를 정규화합니다.
- **[분위수 분할기](./feature-transformation.md#quantilediscretizer)**: 연속적인 기능을 분위수로 바인딩하여 범주별 기능으로 변환합니다.
- **[표준 스케일러](./feature-transformation.md#standardscaler)**: 단위 표준 편차 및/또는 평균이 0이 되도록 기능을 정규화합니다.

#### 범주형 변압기

이러한 변환기를 사용하여 범주형 데이터를 기계 학습 모델에 적합한 형식으로 변환 및 인코딩합니다.

- **[문자열 인덱서](./feature-transformation.md#stringindexer)**: 범주 문자열 데이터를 숫자 인덱스로 변환합니다.
- **[One Hot Encoder](./feature-transformation.md#onehotencoder)**: 범주형 데이터를 이진 벡터로 매핑합니다.

### 기능 선택 {#feature-selection}

다음으로, 원래 세트에서 가장 중요한 피쳐의 서브셋을 선택하는 것에 초점을 맞춥니다. 이 프로세스를 통해 데이터의 차원을 줄여 모델을 보다 쉽게 처리하고 전체 모델 성능을 향상시킬 수 있습니다.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## OPTIONS 절 구현 {#options-clause}

모델을 정의할 때 `OPTIONS` 절을 사용하여 알고리즘과 해당 매개 변수를 지정합니다. `K-Means`과(와) 같이 사용 중인 알고리즘을 나타내는 `type` 매개 변수를 설정하는 것부터 시작합니다. 그런 다음 `OPTIONS` 절의 관련 매개 변수를 키-값 쌍으로 정의하여 모델을 미세 조정합니다. 특정 매개변수를 사용자 정의하지 않도록 선택하면 기본 설정이 적용됩니다. 각 매개 변수의 함수 및 기본값을 이해하려면 관련 설명서를 참조하십시오.

### 다음 단계

이 문서에 설명된 기능 엔지니어링 기법을 학습한 후 [모델](./models.md) 문서로 진행하십시오. 엔지니어링한 기능을 사용하여 신뢰할 수 있는 모델을 만들고, 교육하고, 관리하는 과정을 안내합니다. 모델이 만들어지면 [고급 통계 모델 구현 문서를 계속 진행하십시오.](./implement-models/implement-models.md) 질문에 답합니다. 이 문서는 클러스터링, 분류 및 회귀 분석을 포함한 다양한 모델링 기법을 위한 심층 안내서에 연결하는 개요 역할을 합니다. 이러한 문서를 따라 SQL 워크플로 내에서 신뢰할 수 있는 다양한 모델을 구성 및 구현하고 고급 데이터 분석을 위해 모델을 최적화하는 방법에 대해 알아봅니다.
