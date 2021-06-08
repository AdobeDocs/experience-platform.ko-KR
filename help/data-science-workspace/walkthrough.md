---
keywords: Experience Platform;연습;데이터 과학 작업 공간;인기 있는 주제
solution: Experience Platform
title: 데이터 과학 작업 공간 연습
topic-legacy: Walkthrough
description: 이 문서에서는 Adobe Experience Platform 데이터 과학 작업 공간에 대한 연습을 제공합니다. 특히 데이터 과학자가 기계 학습을 사용하여 문제를 해결하기 위해 수행하는 일반적인 작업 과정입니다.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 연습

이 문서에서는 Adobe Experience Platform [!DNL Data Science Workspace]에 대한 연습을 제공합니다. 이 자습서에서는 일반 데이터 과학자 워크플로우와 기계 학습을 사용하여 문제를 어떻게 접근하고 해결할 수 있는지에 대해 설명합니다.

## 전제 조건

- 등록된 Adobe ID 계정
   - Adobe ID 계정이 Adobe Experience Platform 및 [!DNL Data Science Workspace]에 액세스할 수 있는 조직에 추가되어 있어야 합니다.

## 소매 사용 사례

소매업체는 현재 시장에서 경쟁력을 유지하기 위해 많은 도전에 직면해 있습니다. 소매점의 주요 관심사 중 하나는 제품의 최적 가격을 결정하고 판매 추세를 예측하는 것이다. 정확한 예측 모델을 통해 소매업체는 수요와 가격 정책 간의 관계를 파악하고 매출과 매출을 극대화하기 위해 최적화된 가격 결정을 내릴 수 있습니다.

## 데이터 과학자 솔루션

데이터 과학자 솔루션은 소매업체에서 제공하는 풍부한 과거 정보를 활용하여 향후 추세를 예측하고 가격 결정을 최적화하는 것입니다. 이 연습에서는 과거 판매 데이터를 사용하여 기계 학습 모델을 교육하고 모델을 사용하여 향후 판매 추세를 예측합니다. 이를 통해 인사이트를 생성하여 최적의 가격 변경을 수행할 수 있습니다.

이 개요는 데이터 과학자가 데이터 세트를 가져오고 매주 매출을 예측하는 모델을 만드는 단계를 설명합니다. 이 자습서에서는 Adobe Experience Platform [!DNL Data Science Workspace]의 Sample Retail Sales Notebook에서 다음 섹션을 다룹니다.

- [설정](#setup)
- [데이터 탐색](#exploring-data)
- [기능 엔지니어링](#feature-engineering)
- [교육 및 검증](#training-and-verification)

### [!DNL Data Science Workspace]의 전자 필기장

Adobe Experience Platform UI의 **[!UICONTROL 데이터 과학]** 탭 내에서 **[!UICONTROL 노트북]**&#x200B;을 선택하여 [!UICONTROL 노트북] 개요 페이지로 이동합니다. 이 페이지에서 [!DNL JupyterLab] 탭을 선택하여 [!DNL JupyterLab] 환경을 시작합니다. [!DNL JupyterLab]에 대한 기본 랜딩 페이지는 **[!UICONTROL 시작 관리자]**&#x200B;입니다.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

이 자습서에서는 [!DNL JupyterLab Notebooks]에서 [!DNL Python] 3을 사용하여 데이터에 액세스하고 데이터를 탐색하는 방법을 보여 줍니다. 시작 관리자 페이지에는 샘플 전자 필기장이 제공됩니다. **[!UICONTROL Retail Sales]** 샘플 노트북은 아래 제공된 예에서 사용됩니다.

### 설정 {#setup}

소매 판매 전자 필기장이 열려 있을 때 가장 먼저 워크플로우에 필요한 라이브러리를 로드해야 합니다. 다음 목록에서는 이후 단계의 예제에 사용된 각 라이브러리에 대한 간단한 설명을 제공합니다.

- **숫자**:대형 다차원 배열 및 행렬에 대한 지원을 추가하는 과학 컴퓨팅 라이브러리
- **판다**:데이터 조작 및 분석에 사용되는 데이터 구조 및 작업을 제공하는 라이브러리입니다
- **matplotlib.pyplot**:플로팅할 때 MATLAB 유사 경험을 제공하는 플로팅 라이브러리
- **검색** :Matplolib을 기반으로 하는 높은 수준의 인터페이스 데이터 시각화 라이브러리
- **sklearn**:분류, 회귀, 지원 벡터 및 클러스터 알고리즘을 제공하는 기계 학습 라이브러리
- **경고**:경고 메시지를 제어하는 라이브러리

### 데이터 탐색 {#exploring-data}

#### 데이터 로드

라이브러리가 로드되면 데이터 보기를 시작할 수 있습니다. 다음 [!DNL Python] 코드는 팬더의 `DataFrame` 데이터 구조 및 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 함수를 사용하여 [!DNL Github]에 호스팅된 CSV를 팬더 DataFrame으로 읽습니다.

![](./images/walkthrough/read_csv.png)

판다의 DataFrame 데이터 구조는 2차원적 데이터 구조입니다. 데이터의 차원을 빠르게 보려면 `df.shape`을 사용하십시오. DataFrame의 차원을 나타내는 튜플을 반환합니다.

![](./images/walkthrough/df_shape.png)

마지막으로 데이터의 모습을 미리 볼 수 있습니다. `df.head(n)` 을 사용하여 DataFrame의 첫 번째 `n` 행을 볼 수 있습니다.

![](./images/walkthrough/df_head.png)

#### 통계 요약

[!DNL Python's] 팬더 라이브러리를 활용하여 각 특성의 데이터 유형을 가져올 수 있습니다. 다음 호출의 결과에서는 각 열의 항목 수 및 데이터 유형에 대한 정보를 제공합니다.

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

이 정보는 각 열의 데이터 유형을 알면 데이터를 처리하는 방법을 알 수 있으므로 유용합니다.

이제 통계 요약을 살펴보겠습니다. 숫자 데이터 유형만 표시되므로 `date`, `storeType` 및 `isHoliday`가 출력되지 않습니다.

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

이를 통해 각 특성에 대해 6435개의 인스턴스가 있음을 알 수 있습니다. 또한 평균, 표준 편차(표준 편차), 최소, 최대 및 사분위수 등의 통계적 정보가 제공됩니다. 이는 데이터의 편차에 대한 정보를 제공합니다. 다음 섹션에서는 데이터에 대한 완전한 이해를 제공하기 위해 이 정보와 함께 작동하는 시각화를 살펴봅니다.

`store`에 대한 최소값과 최대값을 보면 데이터가 나타내는 45개의 고유한 저장소가 있음을 알 수 있습니다. 또한 스토어를 구별하는 `storeTypes` 도 있습니다. 다음을 수행하면 `storeTypes` 분포를 볼 수 있습니다.

![](./images/walkthrough/df_groupby.png)

즉, 22개의 스토어가 `storeType A` 이고, 17은 `storeType B` 이고, 6은 `storeType C`입니다.

#### 데이터 시각화

이제 데이터 프레임 값을 알고 있으므로 패턴을 보다 명확하고 쉽게 식별할 수 있도록 시각화를 사용하여 이를 보완하려고 합니다. 이러한 그래프는 결과를 대상으로 전송할 때도 유용합니다.

#### 다변량 그래프

다변량 그래프는 개별 변수의 그래프입니다. 데이터를 시각화하는 데 사용되는 일반적인 다변량 그래프는 박스 및 거품기 그래프입니다.

이전부터 소매 데이터 세트를 사용하면 45개의 각 스토어와 해당 주별 매출에 대한 상자 및 거품형 플롯을 생성할 수 있습니다. 플롯은 `seaborn.boxplot` 함수를 사용하여 생성됩니다.

![](./images/walkthrough/box_whisker.png)

상자나 휘스커 플롯은 데이터의 분포를 보여주는 데 사용됩니다. 플롯의 외부 선은 상부 및 하부 사분위를 보여주며 상자는 사분위수 범위에 걸쳐 있습니다. 상자의 선은 중간값을 표시합니다. 상위 또는 하위 사분위의 1.5배 이상의 데이터 포인트는 원으로 표시됩니다. 이 요점들은 이상치로 간주된다.

그 다음, 시간에 따라 주간 판매를 계획할 수 있습니다. 첫 번째 저장소의 출력만 표시됩니다. 노트북의 코드는 데이터 세트에 있는 45개 저장소 중 6개에 해당하는 6개의 플롯을 생성합니다.

![](./images/walkthrough/weekly_sales.png)

이 다이어그램을 사용하여 2년의 기간 동안 주별 매출을 비교할 수 있습니다. 시간이 지남에 따라 판매 최고점과 골격을 쉽게 볼 수 있다.

#### 다변량 그래프

변수 간의 상호 작용을 보는 데 다변량 플롯이 사용됩니다. 데이터 과학자들은 시각화를 통해 변수 간에 상관 관계 또는 패턴이 있는지 확인할 수 있습니다. 사용되는 일반적인 다변량 그래프는 상관 관계 매트릭스입니다. 상관 관계 매트릭스를 사용하면 여러 변수 간의 종속성이 상관 계수로 수량화됩니다.

동일한 소매 데이터 세트를 사용하여 상관 관계 매트릭스를 생성할 수 있습니다.

![](./images/walkthrough/correlation_1.png)

가운데 아래에 있는 대각선을 보세요. 이는 변수를 자신과 비교할 때 완전한 긍정적인 상관관계가 있음을 보여줍니다. 긍정적인 상관관계가 1에 가깝고 상관관계가 약하면 0에 가깝다는 것이다. 역 트렌드를 나타내는 음수 계수와 함께 음수 상관 관계가 표시됩니다.

### 기능 엔지니어링 {#feature-engineering}

이 섹션에서는 다음 작업을 수행하여 소매 데이터 세트를 수정하는 데 기능 엔지니어링 을 사용합니다.

- 주 및 연도 열 추가
- storeType을 표시기 변수로 변환
- isHoliday를 숫자 변수로 변환
- 다음 주의 주별 판매 예측

#### 주 및 연도 열 추가

날짜의 현재 형식(`2010-02-05`)을 사용하면 데이터를 매주 구분하기 어려울 수 있습니다. 따라서 날짜를 주 및 연도를 포함하는 날짜로 변환해야 합니다.

![](./images/walkthrough/date_to_week_year.png)

이제 주 및 날짜는 다음과 같습니다.

![](./images/walkthrough/date_week_year.png)

#### storeType을 표시기 변수로 변환

그런 다음 storeType 열을 각 `storeType`을 나타내는 열로 변환하려고 합니다. 3개의 새 열을 만드는 3개의 저장소 유형(`A`, `B`, `C`)이 있습니다. 각 열에 설정된 값은 `storeType` 의 값에 따라 &#39;1&#39;이 설정되고 다른 2개의 열에 대해 `0` 이 설정되는 부울 값입니다.

![](./images/walkthrough/storeType.png)

현재 `storeType` 열이 삭제되었습니다.

#### isHoliday를 숫자 유형으로 변환

다음 수정 사항은 `isHoliday` 부울을 숫자 표현으로 변경하는 것입니다.

![](./images/walkthrough/isHoliday.png)

#### 다음 주의 주별 판매 예측

이제 각 데이터 세트에 이전 및 이후의 주별 매출을 추가하려고 합니다. 이 작업은 `weeklySales`을(를) 오프셋하여 수행할 수 있습니다. 또한 `weeklySales` 차이가 계산됩니다. 이 작업은 이전 주의 `weeklySales`에서 `weeklySales`을 뺀 것입니다.

![](./images/walkthrough/weekly_past_future.png)

`weeklySales` 데이터 세트 45를 전달과 45개의 데이터 세트를 뒤로 오프셋하여 새 열을 만들려면 첫 번째 데이터 포인트와 마지막 45개의 데이터 포인트에 NaN 값이 있습니다. NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

![](./images/walkthrough/dropna.png)

수정 사항 후의 데이터 세트에 대한 요약이 아래에 표시되어 있습니다.

![](./images/walkthrough/df_info_new.png)

### 교육 및 확인 {#training-and-verification}

이제 데이터의 일부 모델을 만들어 향후 매출을 예측할 수 있는 가장 적합한 모델을 선택해야 합니다. 다음 5가지 알고리즘을 평가합니다.

- 선형 회귀
- 의사 결정 트리
- Random Forest
- 그라데이션 증폭
- K 이웃

#### 데이터 세트를 교육 및 테스트 하위 집합으로 분할

모델이 값을 예측할 수 있는 정확성을 파악하는 방법이 필요합니다. 이 평가는 데이터 집합 일부를 유효성 확인으로 사용하고 나머지는 교육 데이터로 할당하여 수행할 수 있습니다. `weeklySalesAhead`은 `weeklySales`의 실제 미래 값이므로 이 값을 사용하여 모델이 값을 예측하는 정확도를 평가할 수 있습니다. 분할은 다음과 같이 수행됩니다.

![](./images/walkthrough/split_data.png)

이제 모델을 준비하려면 `X_train` 및 `y_train`, 나중에 평가하려면 `X_test` 및 `y_test`이 있어야 합니다.

#### 스팟 확인 알고리즘

이 섹션에서는 모든 알고리즘을 `model` 이라는 배열로 선언합니다. 그런 다음 이 배열을 반복하고 각 알고리즘에 대해 `model.fit()` 모델을 만드는 교육 데이터를 입력합니다(`mdl`). 이 모델을 사용하여 `X_test` 데이터로 `weeklySalesAhead`을 예측할 수 있습니다.

![](./images/walkthrough/training_scoring.png)

점수의 경우 예측된 `weeklySalesAhead` 간의 평균 퍼센트 차이를 `y_test` 데이터의 실제 값과 함께 구합니다. 예측과 실제 결과 간의 차이를 최소화하려는 경우 그래디언트 증폭 회수는 가장 성과가 좋은 모델입니다.

#### 예측 시각화

마지막으로, 실제 주별 판매 값으로 예측 모델을 시각화합니다. 파란색 선은 실제 숫자를 나타내고 녹색 은 그라디언트 증폭을 사용하여 예측을 나타냅니다. 다음 코드는 데이터 세트에 있는 45개 저장소 중 6개를 나타내는 6개의 플롯을 생성합니다. 여기에 `Store 1`만 표시됩니다.

![](./images/walkthrough/visualize_prediction.png)

## 다음 단계

이 문서에서는 소매 영업 문제를 해결하기 위한 일반적인 데이터 과학자 워크플로우에 대해 다룹니다. 요약하려면:

- 워크플로우에 필요한 라이브러리를 로드합니다.
- 라이브러리가 로드되면 통계 요약, 시각화 및 그래프를 사용하여 데이터를 볼 수 있습니다.
- 다음으로, 기능 엔지니어링은 소매 데이터 세트를 수정하는 데 사용됩니다.
- 마지막으로, 데이터 모델을 만들고 향후 매출을 예측할 수 있는 가장 적합한 모델을 선택합니다.

준비가 되면 [JupiterLab 사용 안내서](./jupyterlab/overview.md)를 참조하여 Adobe Experience Platform Data Science Workspace에서 전자 필기장에 대한 빠른 개요를 살펴보십시오. 또한 모델 및 레서피 학습에 관심이 있는 경우 [소매 판매 스키마 및 데이터 세트](./models-recipes/create-retails-sales-dataset.md) 자습서를 읽으십시오.
