---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: 데이터 과학 작업 공간 연습
topic: Walkthrough
description: 이 문서에서는 Adobe Experience Platform 데이터 과학 작업 공간에 대한 연습을 제공합니다. 특히 데이터 전문가가 머신 러닝을 통해 문제를 해결하기 위해 진행하는 일반적인 워크플로우입니다.
translation-type: tm+mt
source-git-commit: 0d76b14599bc6b6089f9c760ef6a6be3a19243d4
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 연습

이 문서에서는 Adobe Experience Platform에 대한 연습을 제공합니다 [!DNL Data Science Workspace]. 이 자습서에서는 일반적인 데이터 과학자 워크플로우와 머신 러닝을 사용하여 이러한 워크플로우가 어떻게 접근하고 문제를 해결할 수 있는지 설명합니다.

## 전제 조건

- 등록된 Adobe ID 계정
   - Adobe ID 계정은 Adobe Experience Platform 및 에 액세스할 수 있는 조직에 추가해야 합니다 [!DNL Data Science Workspace].

## 소매 사용 사례

한 소매업체는 현재 시장에서 경쟁력을 유지하기 위해 많은 과제에 직면해 있습니다. 소매업체의 주요 관심 중 하나는 제품의 최적의 가격을 결정하고 판매 동향을 예측하는 것이다. 정확한 예측 모델을 사용하면 소매업체는 수요와 가격 정책 간의 관계를 파악할 수 있을 뿐만 아니라 최적화된 가격 결정을 내림으로써 매출과 매출을 극대화할 수 있습니다.

## 데이터 과학자의 솔루션

데이터 과학자는 소매업체에서 제공하는 풍부한 내역 정보를 활용하여 향후 동향을 예측하고 가격 결정을 최적화하는 것이 그 해답입니다. 이 연습에서는 이전 판매 데이터를 사용하여 기계 학습 모델을 교육하고 모델을 사용하여 향후 판매 동향을 예측합니다. 이를 통해 인사이트를 생성하여 최적의 가격 변경을 수행할 수 있습니다.

이 개요는 데이터 과학자가 데이터 세트를 선택하고 주간 판매를 예측할 수 있는 모델을 만들기 위해 수행하는 단계를 반영합니다. 이 자습서에서는 Adobe Experience Platform의 샘플 소매 판매 전자 필기장에 있는 다음 섹션에 대해 설명합니다 [!DNL Data Science Workspace].

- [설정](#setup)
- [데이터 탐색](#exploring-data)
- [기능 엔지니어링](#feature-engineering)
- [교육 및 확인](#training-and-verification)

### 전자 필기장 [!DNL Data Science Workspace]

Adobe Experience Platform UI의 [ **[!UICONTROL 데이터 과학]** ] 탭 내에서 **[!UICONTROL 전자 필기장]** 을 선택하여 [!UICONTROL 노트북] 개요 페이지로이동합니다. 이 페이지에서 [!DNL JupyterLab] 탭을 선택하여 환경을 [!DNL JupyterLab] 실행합니다. 의 기본 랜딩 페이지는 론처 [!DNL JupyterLab] 입니다 ****.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

이 자습서에서는 [!DNL Python] 3을 사용하여 데이터 [!DNL JupyterLab Notebooks] 에 액세스하고 탐색하는 방법을 보여 줍니다. 실행 시작 페이지에는 제공된 샘플 전자 필기장이 있습니다. 소매 **[!UICONTROL 판매]** 샘플 노트북은 아래 예에서 사용됩니다.

### 설정 {#setup}

소매 판매 전자 필기장이 열리면 먼저 워크플로우에 필요한 라이브러리를 로드해야 합니다. 다음 목록은 이후 단계의 예에서 사용되는 각 라이브러리에 대한 간략한 설명을 제공합니다.

- **숫자**:대형 다차원 배열 및 행렬에 대한 지원이 추가된 과학 컴퓨팅 라이브러리
- **판다**:데이터 조작 및 분석에 사용되는 데이터 구조 및 작업을 제공하는 라이브러리
- **matplotlib.pyplot**:플로팅 시 MATLAB과 유사한 경험을 제공하는 라이브러리
- **seabn** :Matplotlib을 기반으로 하는 고급 인터페이스 데이터 시각화 라이브러리
- **sklearn**:분류, 회귀, 지원 벡터 및 클러스터 알고리즘을 제공하는 기계 학습 라이브러리
- **경고**:경고 메시지를 제어하는 라이브러리

### 데이터 살펴보기 {#exploring-data}

#### 데이터 로드

라이브러리가 로드되면 데이터를 볼 수 있습니다. 다음 [!DNL Python] 코드는 판다의 `DataFrame` 데이터 구조와 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 함수를 사용하여 판다 DataFrame에 호스팅된 CSV를 [!DNL Github] 읽습니다.

![](./images/walkthrough/read_csv.png)

팬더의 데이터프레임 데이터 구조는 2차원 라벨의 데이터 구조입니다. 데이터 차원을 빠르게 보려면 `df.shape` DataFrame의 크기를 나타내는 튜플을 반환합니다.

![](./images/walkthrough/df_shape.png)

마지막으로 데이터의 모양을 미리 볼 수 있습니다. DataFrame `df.head(n)` 의 첫 번째 `n` 행을 보는 데 사용할 수 있습니다.

![](./images/walkthrough/df_head.png)

#### 통계 요약

팬더 라이브러리를 활용하여 각 속성의 데이터 유형을 가져올 수 있습니다. [!DNL Python's] 다음 호출의 결과에는 각 열에 대한 항목 수 및 데이터 유형에 대한 정보가 제공됩니다.

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

이 정보는 각 열에 대한 데이터 유형을 알면 데이터를 처리하는 방법을 알 수 있기 때문에 유용합니다.

이제 통계 요약을 살펴봅시다. 숫자 데이터 유형만 `date`표시되고, 이렇게 출력되지 `storeType``isHoliday` 않습니다.

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

이를 통해 각 특성에 대해 6435개의 인스턴스가 있음을 확인할 수 있습니다. 또한 평균, 표준 편차(표준), 최소, 최대 및 사분위수와 같은 통계 정보가 제공됩니다. 이는 데이터의 편차에 대한 정보를 제공합니다. 다음 섹션에서는 데이터에 대한 완벽한 이해를 제공하기 위해 이 정보와 함께 작동하는 시각화를 살펴봅니다.

의 최소 및 최대 값을 보면 데이터가 나타내는 45개의 고유 스토어 `store`가 있음을 확인할 수 있습니다. 가게 `storeTypes` 를 구별하는 것도 있다. 다음을 수행하여 분포를 볼 수 `storeTypes` 있습니다.

![](./images/walkthrough/df_groupby.png)

이것은 22개 매장 `storeType A` , 17개 매장, 6 `storeType B`개 매장을 의미합니다 `storeType C`.

#### 데이터 시각화

데이터 프레임 값을 알고 있으므로 시각화를 통해 보다 명확하고 손쉽게 패턴을 식별할 수 있습니다. 이러한 그래프는 결과를 대상자에게 전달하는 데에도 유용합니다.

#### 다변량 그래프

다변수 그래프는 개별 변수의 그래프입니다. 데이터를 시각화하는 데 사용되는 일반적인 다변량 그래프는 박스 모양과 휘젓는 그래프입니다.

이전에 출시된 소매 데이터 세트를 사용하여 45개 매장과 매주 영업을 위한 상자를 생성하고 신속하게 사진을 관리할 수 있습니다. 플롯은 함수를 사용하여 `seaborn.boxplot` 생성됩니다.

![](./images/walkthrough/box_whisker.png)

상자나 휘저는 줄거리는 데이터의 분포를 보여주는 데 사용된다. 플롯의 외부 선은 상단 및 하단 사분위수를 보여주며 상자는 사분위수 범위를 나타냅니다. 상자 안의 선은 중간선을 표시합니다. 1.5배 이상의 데이터 포인트가 상위 사분위나 하위 사분위보다 큰 것으로 표시됩니다. 이 점들은 이상치라고 간주된다.

그 다음, 시간과 함께 주간 판매를 계획할 수 있습니다. 첫 번째 점포의 결과만 표시됩니다. 노트북의 코드는 데이터세트에 있는 45개 스토어 중 6개에 해당하는 6개의 플롯을 생성합니다.

![](./images/walkthrough/weekly_sales.png)

이 다이어그램에서는 2년의 기간 동안 주간 매출을 비교할 수 있습니다. 시간이 지남에 따라 세일이 가장 잘 되고 종이가 잘 된다.

#### 다변량 그래프

변수 간의 상호 작용을 보는 데 다변량 플롯이 사용됩니다. 시각화를 사용하여 데이터 과학자들은 변수 사이에 상관 관계나 패턴이 있는지 확인할 수 있습니다. 일반적인 다변량 그래프는 상관 관계 행렬입니다. 상관 관계 매트릭스를 사용하면 여러 변수 간의 종속성을 상관 계수로 수량화합니다.

동일한 소매 데이터 세트를 사용하여 상관 관계 지표를 생성할 수 있습니다.

![](./images/walkthrough/correlation_1.png)

가운데 아래에 있는 대각선을 보세요. 이것은 변수를 자신과 비교할 때 완전한 긍정적인 상관관계가 있음을 보여줍니다. 긍정적 상관관계는 1에 가까울수록 약하지만 상관관계는 0에 가깝다. 부정적인 상관관계는 역트렌드를 나타내는 부정 계수로 표시됩니다.

### 기능 엔지니어링 {#feature-engineering}

이 섹션에서는 다음 작업을 수행하여 소매 데이터 세트를 수정하는 데 기능 엔지니어링이 사용됩니다.

- 주 및 연도 열 추가
- storeType을 표시기 변수로 변환
- 휴일을 숫자 변수로 변환
- 다음 주의 주별 판매 예측

#### 주 및 연도 열 추가

현재 날짜 형식(`2010-02-05`)으로 인해 데이터가 매주 사용되도록 구별하기가 어려울 수 있습니다. 따라서 날짜를 주 및 연도를 포함하는 날짜로 변환해야 합니다.

![](./images/walkthrough/date_to_week_year.png)

이제 주와 날짜는 다음과 같습니다.

![](./images/walkthrough/date_week_year.png)

#### storeType을 표시기 변수로 변환

그런 다음 storeType 열을 각 열을 나타내는 열로 변환할 수 `storeType`있습니다. 3개의 새 열을 만드는 스토어 유형(`A`, `B`, `C`)이 있습니다. 각 열에 설정된 값은 부울 값으로서, 값 `storeType` 이 무엇이고 다른 2개 열에 대해 &#39;1&#39;이 설정되는 `0` 경우

![](./images/walkthrough/storeType.png)

현재 `storeType` 열이 삭제됩니다.

#### 휴일을 숫자 유형으로 변환

다음 수정 사항은 부울을 숫자 표현으로 변경하는 `isHoliday` 것입니다.

![](./images/walkthrough/isHoliday.png)

#### 다음 주의 주별 판매 예측

이제 데이터 세트 각각에 이전 및 향후 주별 매출을 추가할 수 있습니다. 이를 상쇄하면 됩니다 `weeklySales`. 또한, `weeklySales` 차이가 계산됩니다. 이것은 지난 주 `weeklySales` 와 함께 빼서 행해진다 `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

45개의 데이터 데이터 세트를 앞으로 및 45개의 데이터 세트를 뒤로 대체하여 새 열을 만들기 때문에 첫 번째 및 마지막 45개의 데이터 포인트는 NaN 값을 가집니다. `weeklySales` NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

![](./images/walkthrough/dropna.png)

수정 후 데이터 세트에 대한 요약이 아래에 나와 있습니다.

![](./images/walkthrough/df_info_new.png)

### 교육 및 확인 {#training-and-verification}

이제 데이터의 일부 모델을 만들어 향후 매출을 예측할 수 있는 가장 효과적인 모델을 선택해야 합니다. 다음 5가지 알고리즘을 평가하게 됩니다.

- 선형 회귀
- 의사 결정 트리
- Random Forest
- 그라디언트 향상
- K Sibers

#### 데이터 세트를 트레이닝 및 테스트 하위 세트로 분할

모델이 얼마나 정확한지 알 수 있는 방법이 필요합니다. 이 평가에서는 데이터 집합의 일부를 인증으로 사용하고 나머지는 교육 데이터로 할당하여 수행할 수 있습니다. 이 값 `weeklySalesAhead` 은 실제 미래 값이므로 이 값을 사용하여 모델이 값을 예측할 때 얼마나 정확한지 평가할 수 있습니다 `weeklySales`. 분할은 다음과 같습니다.

![](./images/walkthrough/split_data.png)

이제 모델 `X_train` 과 `y_train` 를 준비하고 나중에 `X_test` 평가를 `y_test` 위해 준비할 수 있습니다.

#### 스팟 확인 알고리즘

이 섹션에서 모든 알고리즘을 `model` 그런 다음 이 배열과 각 알고리즘에 대해 모델을 만드는 교육 데이터 `model.fit()` 를 입력합니다 `mdl`. 이 모델을 사용하면 데이터 `weeklySalesAhead` 로 예측할 수 `X_test` 있습니다.

![](./images/walkthrough/training_scoring.png)

점수 지정 시 예측된 값과 데이터의 실제 값 간 평균 백분율 차이 `weeklySalesAhead` 를 `y_test` 갖습니다. 예측과 실제 결과 간의 차이를 최소화하려는 경우 그래디언트 증폭 회귀 모델이 가장 효과적인 모델입니다.

#### 예측 시각화

마지막으로 예측 모델을 실제 주간 판매 값으로 시각화합니다. 파란색 선은 실제 숫자를, 녹색 선은 그라디언트 향상을 사용하여 예측을 나타냅니다. 다음 코드는 데이터 세트에 있는 45개 스토어 중 6개를 나타내는 6개의 플롯을 생성합니다. 여기에만 `Store 1` 표시됩니다.

![](./images/walkthrough/visualize_prediction.png)

## 다음 단계

이 문서에서는 소매 영업 문제를 해결하는 일반적인 데이터 과학자 워크플로우에 대해 설명합니다. 요약하려면

- 워크플로우에 필요한 라이브러리를 로드합니다.
- 라이브러리가 로드되면 통계 요약, 시각화 및 그래프를 사용하여 데이터를 볼 수 있습니다.
- 다음으로 리테일 데이터 세트를 수정하는 데 기능 엔지니어링이 사용됩니다.
- 마지막으로 데이터의 모델을 생성하고 향후 매출을 예측할 수 있는 가장 효과적인 모델을 선택합니다.

준비가 되면 JupiterLab 사용자 가이드 [](./jupyterlab/overview.md) 를 참조하여 Adobe Experience Platform 데이터 과학 작업 공간에서 전자 필기장에 대한 빠른 개요를 살펴보십시오. 또한 모델 및 레서피에 대해 학습하려는 경우 [소매 판매 스키마 및 데이터 세트](./models-recipes/create-retails-sales-dataset.md) 자습서를 읽으십시오. 이 자습서는 데이터 과학 작업 공간 자습서 페이지에서 볼 수 있는 후속 데이터 과학 작업 공간 자습서 [를 준비합니다](../tutorials/data-science-workspace.md).