---
keywords: Experience Platform;최적화;모델;데이터 과학 작업 공간;인기 항목;모델 통찰력
solution: Experience Platform
title: 모델 통찰력 프레임워크를 사용하여 모델 최적화
type: Tutorial
description: Model Insights Framework는 데이터 과학자에게 Data Science Workspace의 도구를 제공하여 실험을 기반으로 최적의 기계 학습 모델을 위한 빠르고 현명한 선택을 할 수 있도록 합니다.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 모델 통찰력 프레임워크를 사용하여 모델 최적화

모델 인사이트 프레임워크는 데이터 과학자에게 의 도구를 제공합니다 [!DNL Data Science Workspace] 실험을 기반으로 최적의 기계 학습 모델을 신속하고 정확하게 선택할 수 있습니다. 이 프레임워크는 기계 학습 워크플로우의 속도와 효과를 향상시키고 데이터 과학자의 사용 편의성을 향상시킬 것입니다. 이 작업은 모델 조정을 지원하기 위해 각 기계 학습 알고리즘 유형에 대한 기본 템플릿을 제공하여 수행됩니다. 최종 결과를 통해 데이터 과학자 및 시민 데이터 과학자들은 최종 고객을 위해 더 나은 모델 최적화 결정을 내릴 수 있습니다.

## 지표란?

모델을 구현하고 훈련한 후 데이터 과학자가 할 다음 단계는 모델이 얼마나 잘 수행될지 찾는 것입니다. 다양한 지표를 사용하여 모델이 다른 지표와 비교하여 얼마나 효과적인지를 찾습니다. 사용된 지표의 몇 가지 예는 다음과 같습니다.
- 분류 정확도
- 커브 아래의 영역
- 혼동 매트릭스
- 분류 보고서

## 레서피 코드 구성

현재 모델 인사이트 프레임워크는 다음 런타임을 지원합니다.
- [스칼라](#scala)
- [파이톤/텐소플로우](#pythontensorflow)
- [R](#r)

레서피에 대한 샘플 코드는 [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 저장소 아래의 `recipes`. 이 자습서 전체에서 이 저장소의 특정 파일을 참조합니다.

### 스칼라 {#scala}

레서피에 지표를 가져오는 방법에는 두 가지가 있습니다. 하나는 SDK에서 제공하는 기본 평가 지표를 사용하는 것이고 다른 하나는 사용자 지정 평가 지표를 작성하는 것입니다.

#### Scala에 대한 기본 평가 지표

기본 평가는 분류 알고리즘의 일부로 계산됩니다. 다음은 현재 구현된 평가자의 몇 가지 기본값입니다.

| 평가기 클래스 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

평가기는 의 레서피에서 정의할 수 있습니다 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 파일의 `recipe` 폴더를 입력합니다. 를 활성화하는 샘플 코드 `DefaultBinaryClassificationEvaluator` 아래와 같이 표시됩니다.

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

평가기 클래스를 활성화하면 기본적으로 교육 중에 많은 지표가 계산됩니다. 기본 지표는 다음 줄을 `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>지표가 정의되지 않으면 기본 지표가 활성화됩니다.

특정 지표는 `evaluation.metrics.com`. 다음 예에서는 F-점수 지표가 활성화됩니다.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

다음 표에는 각 클래스에 대한 기본 지표가 나와 있습니다. 사용자는 또한 `evaluation.metric` 열 을 클릭하여 특정 지표를 활성화합니다.

| `evaluator.class` | 기본 지표 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -정밀도 <br>-리콜 <br>-혼동 매트릭스 <br>-F 스코어 <br>-정확도 <br>-수신기 동작 특성 <br>- 리시버 동작 특성 하의 영역 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -정밀도 <br>-리콜 <br>-혼동 매트릭스 <br>-F 스코어 <br>-정확도 <br>-수신기 동작 특성 <br>- 리시버 동작 특성 하의 영역 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -평균 평균 정밀도(MAP) <br>-정규화된 할인된 누적 이득 <br>-평균 상호 등급 <br>-지표 K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala에 대한 사용자 지정 평가 지표

사용자 지정 평가기는 `MLEvaluator.scala` 다음 위치에서 `Evaluator.scala` 파일. 예제에서는 [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 파일, 사용자 정의 `split()` 및 `evaluate()` 함수 위에 있어야 합니다. Adobe `split()` 함수는 8:2의 비율로 데이터를 임의로 분할하고 `evaluate()` 함수는 3개의 지표를 정의하고 반환합니다. MAPE, MAE, RMSE.

>[!IMPORTANT]
>
>대상 `MLMetric` 클래스, 사용하지 않음 `"measures"` 대상 `valueType` 새 `MLMetric` 그렇지 않으면 지표가 사용자 지정 평가 지표 표에 채워지지 않습니다.
>  
> 방법: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 이 아님: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


레서피에서 정의되면 다음 단계는 레서피에서 이를 활성화하는 것입니다. 이 작업은 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 프로젝트의 `resources` 폴더를 입력합니다. 여기에서 `evaluation.class` 이(가) `Evaluator` 정의된 클래스 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

에서 [!DNL Data Science Workspace]를 입력하면 실험 페이지의 &quot;평가 지표&quot; 탭에서 통찰력을 볼 수 있습니다.

### [!DNL Python/Tensorflow] {#pythontensorflow}

현재, [!DNL Python] 또는 [!DNL Tensorflow]. 따라서, [!DNL Python] 또는 [!DNL Tensorflow]를 채울 때는 사용자 지정 평가 지표를 만들어야 합니다. 이 작업은 를 구현하여 수행할 수 있습니다. `Evaluator` 클래스 이름을 지정합니다.

#### 에 대한 사용자 지정 평가 지표 [!DNL Python]

사용자 지정 평가 지표의 경우, 평가자를 위해 구현해야 하는 두 가지 기본 방법이 있습니다. `split()` 및 `evaluate()`.

대상 [!DNL Python]로 설정되면 이러한 메서드는 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 대상 `Evaluator` 클래스 이름을 지정합니다. 다음을 수행합니다 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 링크의 예 `Evaluator`.

에서 평가 지표 만들기 [!DNL Python] 를 구현하려면 사용자가 `evaluate()` 및 `split()` 메서드를 사용합니다.

다음 `evaluate()` 메서드는 속성이 있는 지표 개체 배열을 포함하는 지표 개체를 반환합니다 `name`, `value`, 및 `valueType`.

의 목적 `split()` 방법은 데이터를 입력하고 교육 및 테스트 데이터 세트를 출력하는 것입니다. 이 예제에서는 `split()` 메서드는 `DataSetReader` SDK와 관련이 없는 열을 제거하여 데이터를 정리합니다. 여기에서 데이터의 기존 원시 피쳐에서 추가 기능이 생성됩니다.

다음 `split()` 메서드는 교육 및 테스트 데이터 프레임을 반환해야 하며 이 데이터 프레임은 `pipeline()` ML 모델을 교육하고 테스트하는 방법입니다.

#### Tensorflow에 대한 사용자 지정 평가 지표

대상 [!DNL Tensorflow]: [!DNL Python], 메서드 `evaluate()` 및 `split()` 에서 `Evaluator` 클래스를 구현해야 합니다. 대상 `evaluate()`, 다음 기간 동안 지표가 반환되어야 함 `split()` 열차 및 테스트 데이터 세트를 반환합니다.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

현재 R에 대한 기본 평가 지표가 없습니다. 따라서 R에 대한 평가 지표를 얻으려면 를 정의해야 합니다 `applicationEvaluator` 배합식의 일부로서 클래스

#### R에 대한 사용자 지정 평가 지표

의 주요 목적 `applicationEvaluator` 는 지표 키-값 쌍이 포함된 JSON 개체를 반환하는 것입니다.

이 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 예로 사용할 수 있습니다. 이 예에서 `applicationEvaluator` 는 세 개의 친숙한 섹션으로 분할됩니다.
- 데이터 로드
- 데이터 준비/기능 엔지니어링
- 저장된 모델 검색 및 평가

데이터는 먼저 다음에 정의된 대로 소스에서 데이터 집합에 로드됩니다 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). 여기서, 데이터는 청소되고 기계 학습 모델에 맞게 제작됩니다. 마지막으로, 모델은 데이터 세트를 사용하여 예측을 수행하는 데 사용되며 예측된 값과 실제 값에서 지표를 계산합니다. 이 경우 MAPE, MAE 및 RMSE가 정의되고 `metrics` 개체.

## 사전 빌드된 지표 및 시각화 차트 사용

다음 [!DNL Sensei Model Insights Framework] 에서는 각 기계 학습 알고리즘 유형에 대해 하나의 기본 템플릿을 지원합니다. 아래 표는 일반적인 높은 수준의 기계 학습 알고리즘 클래스와 해당 평가 지표 및 시각화를 보여줍니다.

| ML 알고리즘 유형 | 평가 지표 | 시각화 |
| --- | --- | --- |
| 회귀 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 예측된 값과 실제 값 오버레이 곡선 |
| 이진 분류 | - 혼동 매트릭스<br>정밀 회수<br>- 정확도<br>- F 스코어(특히 F1,F2)<br>- AUC<br>- ROC | ROC 곡선 및 혼동 매트릭스 |
| 다중 클래스 분류 | -혼동 매트릭스 <br>- 각 클래스에 대해: <br>- 정밀회수 정확도 <br>- F 스코어(구체적으로 F1, F2) | ROC 곡선 및 혼동 매트릭스 |
| 클러스터링(기본 진리를 포함) | - NMI(정규화된 상호 정보 점수), AMI(조정된 상호 정보 점수)<br>- RI(랜드 인덱스), ARI(랜드 인덱스 조정)<br>- 동질성 점수, 완결성 점수 및 V 측정<br>- FMI(파울크-멜로우 인덱스)<br>순도<br>- Jaccard 인덱스 | 클러스터 플롯은 클러스터 내에 속하는 데이터 포인트를 반영하도록 상대 클러스터 크기를 갖는 클러스터 및 centroid를 보여 줍니다 |
| 클러스터링(기본 정보 포함) | 관성<br>- 실루엣 계수<br>- CHI(칼린스키-하라바즈 색인)<br>- DBI(데이비스-불딘 인덱스)<br>던인덱스 | 클러스터 플롯은 클러스터 내에 속하는 데이터 포인트를 반영하도록 상대 클러스터 크기를 갖는 클러스터 및 centroid를 보여 줍니다 |
| 권장 사항 | -평균 평균 정밀도(MAP) <br>-정규화된 할인된 누적 이득 <br>-평균 상호 등급 <br>-지표 K | TBD |
| 텐서흐름 사용 사례 | 텐서흐름 모델 분석(TFMA) | 신경망 모델 비교/시각화 깊이 비교 |
| 기타/오류 캡처 메커니즘 | 모델 작성자가 정의한 사용자 정의 지표 논리(및 해당 평가 차트) 템플릿이 일치하지 않는 경우 정상 오류 처리 | 평가 지표에 대한 키-값 쌍이 있는 테이블 |
