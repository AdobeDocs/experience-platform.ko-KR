---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: 데이터 과학 작업 공간 연습
topic: Walkthrough
description: 이 문서에서는 Adobe Experience Platform 데이터 과학 작업 공간에 대한 연습을 제공합니다. 특히 데이터 전문가가 머신 러닝을 통해 문제를 해결하기 위해 진행하는 일반적인 워크플로우입니다.
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 연습

이 문서에서는 Adobe Experience Platform에 대한 연습을 제공합니다 [!DNL Data Science Workspace]. 특히, 우리는 데이터 과학자가 기계 학습을 통해 문제를 해결하기 위해 진행하는 일반적인 워크플로우를 살펴봅니다.

## 전제 조건

- 등록된 Adobe ID 계정
   - Adobe Experience Platform 및 [!DNL Data Science Workspace]

## 데이터 과학자의 동기

한 소매업체는 현재 시장에서 경쟁력을 유지하기 위해 많은 과제에 직면해 있습니다. 소매업체의 주요 관심 중 하나는 제품의 최적의 가격을 결정하고 판매 동향을 예측하는 것이다. 정확한 예측 모델을 통해 소매업체는 수요와 가격 정책 간의 관계를 파악할 수 있을 뿐만 아니라 최적화된 가격 결정을 내림으로써 매출과 매출을 극대화할 수 있습니다.

## 데이터 과학자의 솔루션

데이터 과학자는 소매업체가 액세스할 수 있는 방대한 데이터를 활용하여 향후 동향을 예측하고 가격 결정을 최적화하는 것이 그 해답입니다. 과거 판매 데이터를 사용하여 머신 러닝 모델을 교육하고 이 모델을 사용하여 향후 판매 동향을 예측할 수 있습니다. 이를 통해 소매업체는 가격을 변경할 때 유용한 인사이트를 얻을 수 있습니다.

이 개요에서는 데이터 과학자가 데이터 세트를 선택하고 주간 판매를 예측할 수 있는 모델을 만드는 단계를 살펴봅니다. Adobe Experience Platform의 샘플 소매 판매 노트에 있는 다음 섹션을 살펴봅니다 [!DNL Data Science Workspace].

- [설정](#setup)
- [데이터 탐색](#exploring-data)
- [기능 엔지니어링](#feature-engineering)
- [교육 및 확인](#training-and-verification)

### 전자 필기장 [!DNL Data Science Workspace]

먼저, &quot;소매 판매&quot; 샘플 노트북을 열기 위한 [!DNL JupyterLab] 노트북을 만들고 싶습니다. 노트북에서 데이터 과학자가 수행한 단계를 따라 일반적인 워크플로우를 이해할 수 있습니다.

Adobe Experience Platform UI의 상단 메뉴에서 데이터 과학 탭을 클릭하여 페이지로 이동합니다 [!DNL Data Science Workspace]. 이 페이지에서 실행 관리자를 열 [!DNL JupyterLab] 탭을 [!DNL JupyterLab] 클릭합니다. 이와 유사한 페이지가 표시됩니다.

![](./images/walkthrough/jupyterlab_launcher.png)

튜토리얼에서는 데이터 액세스 및 탐색 방법을 보여주는 데 [!DNL Python] 3 [!DNL Jupyter Notebook] 을 사용합니다. 실행 시작 페이지에는 제공된 샘플 전자 필기장이 있습니다. Adobe는 &quot;소매 판매&quot; 샘플을 [!DNL Python] 3에 사용할 예정입니다.

![](./images/walkthrough/retail_sales.png)

### 설정 {#setup}

소매 판매 전자 필기장이 열리면 먼저 워크플로우에 필요한 라이브러리를 로드하는 것입니다. 다음 목록은 각 용도에 대한 간략한 설명을 제공합니다.
- **숫자** - 다차원 배열 및 행렬에 대한 지원을 추가하는 과학 컴퓨팅 라이브러리
- **판다** - 데이터 조작 및 분석에 사용되는 데이터 구조와 작업을 제공하는 라이브러리
- **matplotlib.pyplot** - 플로팅 시 MATLAB과 유사한 경험을 제공하는 플로팅 라이브러리
- **seabn** - matplotlib을 기반으로 하는 고급 인터페이스 데이터 시각화 라이브러리
- **sklearn** - 분류, 회귀, 지원 벡터 및 클러스터 알고리즘을 제공하는 기계 학습 라이브러리
- **경고** - 경고 메시지를 제어하는 라이브러리

### 데이터 살펴보기 {#exploring-data}

#### 데이터 로드

라이브러리가 로드되면 데이터를 볼 수 있습니다. 다음 [!DNL Python] 코드는 판다의 `DataFrame` 데이터 구조와 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 함수를 사용하여 판다 DataFrame에 호스팅된 CSV를 [!DNL Github] 읽습니다.

![](./images/walkthrough/read_csv.png)

팬더의 데이터프레임 데이터 구조는 2차원 라벨의 데이터 구조입니다. 데이터의 크기를 빠르게 보기 위해 사용할 수 있습니다 `df.shape`. DataFrame의 크기를 나타내는 튜플을 반환합니다.

![](./images/walkthrough/df_shape.png)

마지막으로 데이터가 어떻게 표시되는지 살펴볼 수 있습니다. DataFrame의 첫 번째 `df.head(n)` `n` 행을 보는 데 사용할 수 있습니다.

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

의 최소 및 최대 값을 보면 데이터가 나타내는 45개의 고유 스토어 `store`가 있음을 알 수 있습니다. 가게 `storeTypes` 를 구별하는 것도 있다. 다음을 수행하여 분포를 볼 수 `storeTypes` 있습니다.

![](./images/walkthrough/df_groupby.png)

이것은 22개 매장 `storeType A` , 17개 매장, 6 `storeType B`개 매장을 의미합니다 `storeType C`.

#### 데이터 시각화

데이터 프레임 값을 알고 있으므로 시각화를 통해 보다 명확하고 손쉽게 패턴을 식별할 수 있습니다. 이러한 그래프는 결과를 대상자에게 전달하는 데에도 유용합니다.

#### 다변량 그래프

다변수 그래프는 개별 변수의 그래프입니다. 데이터를 시각화하는 데 사용되는 일반적인 다변량 그래프는 박스 모양과 휘젓는 그래프입니다.

이전에 출시된 소매 데이터 세트를 사용하여 45개 매장과 매주 영업을 위한 상자를 만들어 낼 수 있습니다. 플롯은 함수를 사용하여 `seaborn.boxplot` 생성됩니다.

![](./images/walkthrough/box_whisker.png)

상자나 휘저는 줄거리는 데이터의 분포를 보여주는 데 사용된다. 플롯의 외부 선은 상단 및 하단 사분위수를 보여주며 상자는 사분위수 범위를 나타냅니다. 상자 안의 선은 중간선을 표시합니다. 1.5배 이상의 데이터 포인트가 상위 사분위나 하위 사분위보다 큰 것으로 표시됩니다. 이 점들은 이상치라고 간주된다.

다음으로, 우리는 시간을 두고 주간 판매를 계획할 수 있다. 첫 가게의 결과물만 보여드리겠습니다 노트북의 코드는 데이터세트에 있는 45개 스토어 중 6개에 해당하는 6개의 플롯을 생성합니다.

![](./images/walkthrough/weekly_sales.png)

이 도표로 2년 동안 주간 판매를 비교할 수 있습니다. 시간이 지남에 따라 세일이 가장 잘 되고 종이가 잘 된다.

#### 다변량 그래프

변수 간의 상호 작용을 보는 데 다변량 플롯이 사용됩니다. 시각화를 사용하여 데이터 과학자들은 변수 사이에 상관 관계나 패턴이 있는지 확인할 수 있습니다. 일반적인 다변량 그래프는 상관 관계 행렬입니다. 상관 관계 매트릭스를 사용하면 여러 변수 간의 종속성을 상관 계수로 수량화합니다.

동일한 소매 데이터 세트를 사용하여 상관 관계 지표를 생성할 수 있습니다.

![](./images/walkthrough/correlation_1.png)

가운데 아래에 있는 대각선을 보세요. 이것은 변수를 자신과 비교할 때 완전한 긍정적인 상관관계가 있음을 보여줍니다. 긍정적 상관관계는 1에 가까울수록 약하지만 상관관계는 0에 가깝다. 부정적인 상관관계는 역트렌드를 나타내는 부정 계수로 표시됩니다.

### 기능 엔지니어링 {#feature-engineering}

이 섹션에서는 소매 데이터 세트를 수정할 것입니다. 다음 작업을 수행합니다.

- 주 및 연도 열 추가
- storeType을 표시기 변수로 변환
- isHoliday를 숫자 변수로 변환
- 주별 판매 예측

#### 주 및 연도 열 추가

현재 날짜 형식(`2010-02-05`)은 데이터가 매주 사용되는지 구분하기가 어렵습니다. 이 때문에 날짜를 주 및 년으로 변환할 것입니다.

![](./images/walkthrough/date_to_week_year.png)

이제 주와 날짜는 다음과 같습니다.

![](./images/walkthrough/date_week_year.png)

#### storeType을 표시기 변수로 변환

그런 다음 storeType 열을 각 열을 나타내는 열로 변환하려고 `storeType`합니다. 3개의 새 열을 만드는 스토어 유형(`A`, `B`, `C`)이 있습니다. 각 열에 설정된 값은 부울 값으로서, 값 `storeType` 이 무엇이었는지에 따라 설정되고 다른 2개 열에 대해 &#39;1&#39; `0` 이 설정됩니다.

![](./images/walkthrough/storeType.png)

현재 `storeType` 열이 삭제됩니다.

#### 휴일을 숫자 유형으로 변환

다음 수정 사항은 부울을 숫자 표현으로 변경하는 `isHoliday` 것입니다.

![](./images/walkthrough/isHoliday.png)


#### 다음 주의 주별 판매 예측

이제 데이터 세트 각각에 이전 및 향후 주간 매출을 추가하고 싶습니다. 우리는 이 일을 상쇄함으로써 하고 있다 `weeklySales`. 게다가, 우리는 그 `weeklySales` 차액을 계산하고 있다. 이것은 지난 주 `weeklySales` 와 함께 빼서 행해진다 `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

새 열을 만들기 위해 `weeklySales` 데이터 45개의 데이터 세트와 45개의 데이터 세트를 뒤로 대체하므로 첫 번째 및 마지막 45개의 데이터 포인트에는 NaN 값이 있습니다. NaN 값이 있는 모든 행을 제거하는 `df.dropna()` 함수를 사용하여 데이터 세트에서 이러한 점을 제거할 수 있습니다.

![](./images/walkthrough/dropna.png)

수정 후 데이터 세트에 대한 요약이 아래에 나와 있습니다.

![](./images/walkthrough/df_info_new.png)

### 교육 및 확인 {#training-and-verification}

이제 데이터의 일부 모델을 만들어 향후 매출을 예측할 수 있는 가장 효과적인 모델을 선택해야 합니다. 다음 5가지 알고리즘을 평가합니다.

- 선형 회귀
- 의사 결정 트리
- Random Forest
- 그라디언트 향상
- K Sibers

#### 데이터 세트를 트레이닝 및 테스트 하위 세트로 분할

우리의 모델이 얼마나 정확한지 알 수 있는 방법이 필요합니다. 이 평가에서는 데이터 집합의 일부를 인증으로 사용하고 나머지는 교육 데이터로 할당하여 수행할 수 있습니다. 이 `weeklySalesAhead` 는 실제 미래 값이므로, 이 값을 사용하여 모델이 얼마나 정확한지 평가할 수 `weeklySales`있습니다. 분할은 다음과 같습니다.

![](./images/walkthrough/split_data.png)

우리는 이제 모델 `X_train` 과 `y_train` 를 준비하고, 나중에 `X_test` 에 평가를 `y_test` 위해 준비한다.

#### 스팟 확인 알고리즘

이 섹션에서는 모든 알고리즘을 `model` 다음으로 이 배열과 각 알고리즘에 대해 모델을 만드는 교육 데이터 `model.fit()` 를 입력합니다 `mdl`. 이 모델을 사용하면 우리 데이터 `weeklySalesAhead` 로 예측할 수 `X_test` 있습니다.

![](./images/walkthrough/training_scoring.png)

점수의 경우 예측된 값과 실제 데이터 값 간의 평균 백분율 차이 `weeklySalesAhead` 를 `y_test` 갖습니다. 예측과 실제 데이터의 차이를 최소화하려고 하므로 그래디언트 증폭 회귀 모델이 가장 효과적인 모델입니다.

#### 예측 시각화

마지막으로, 실제 주간 판매 가격으로 예측 모델을 시각화할 것입니다. 파란색 선은 실제 숫자를, 녹색 선은 그라디언트 향상을 사용하여 예측을 나타냅니다. 다음 코드는 데이터 세트에 있는 45개 스토어 중 6개를 나타내는 6개의 플롯을 생성합니다. 여기에만 `Store 1` 표시됩니다.

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## 결론

이 개요를 통해 데이터 과학자는 소매 판매 문제를 해결하기 위해 진행했던 워크플로우를 살펴보았습니다. 특히 다음 단계를 통해 향후 주간 매출을 예측하는 솔루션을 선택했습니다.

- [설정](#setup)
- [데이터 탐색](#exploring-data)
- [기능 엔지니어링](#feature-engineering)
- [교육 및 확인](#training-and-verification)