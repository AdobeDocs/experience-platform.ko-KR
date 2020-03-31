---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: 모델 최적화
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 모델 최적화


이 자습서는 다음과 같이 진행됩니다.

- 레서피 코드 구성
- 사용자 지정 지표 정의
- 미리 작성된 평가 지표 및 시각화 차트 사용

이 튜토리얼을 종료하려면 레서피 코드를 구성하고, 사용자 지정 지표를 정의하며, 사전 작성된 평가 지표 및 기본 시각화 차트를 사용할 수 있어야 합니다.

## 지표란?

모델을 구현하고 교육한 후 데이터 과학자가 할 다음 단계는 모델이 얼마나 잘 작동하는지 찾는 것입니다. 다양한 지표는 모델이 다른 모델과 얼마나 효과적인지를 찾는 데 사용됩니다. 사용된 지표의 일부 예는 다음과 같습니다.
- 분류 정확도
- 곡선 아래 영역
- 혼동 매트릭스
- 분류 보고서

## Model Insights Framework 소개

Model Insights Framework는 데이터 과학자에게 실험을 기반으로 최적의 기계 학습 모델을 위한 신속하고 정확한 선택을 할 수 있는 데이터 과학 작업 영역의 도구를 제공합니다. 이 프레임워크는 기계 학습 워크플로우의 속도와 효율성을 향상시키고 데이터 과학자의 사용 편의성을 향상시킵니다. 이 작업은 모델 조정을 지원하기 위해 각 기계 학습 알고리즘 유형에 대한 기본 템플릿을 제공하여 수행됩니다. 최종 결과를 통해 데이터 과학자와 시민 데이터 과학자는 최종 고객을 위한 모델 최적화 결정을 내릴 수 있습니다.

## 레서피 코드 구성

현재 Model Insights Framework는 다음 런타임을 지원합니다.
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

레서피에 대한 샘플 코드는 [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 저장소에서 `recipes`찾을 수 있습니다. 이 저장소의 특정 파일은 이 자습서 전체에서 참조됩니다.

### Scala {#scala}

레서피에 지표를 가져오는 방법에는 두 가지가 있습니다. 하나는 SDK에서 제공하는 기본 평가 지표를 사용하는 것이고 다른 하나는 사용자 지정 평가 지표를 작성하는 것입니다.

#### Scala에 대한 기본 평가 지표

기본 평가는 분류 알고리즘의 일부로 계산됩니다. 다음은 현재 구현된 평가기의 몇 가지 기본값입니다.

| 평가기 클래스 | `evaluation.class` |
--- | ---
| Default이진 분류 평가기 | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| 기본 다중 분류 평가기 | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| 권장 사항 평가기 | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

평가기는 [폴더에 있는 application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) `recipe` 파일의 레서피에서 정의할 수 있습니다. Sample code enabling the `DefaultBinaryClassificationEvaluator` is shown below:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

평가기 클래스가 활성화되면 기본적으로 교육 중에 여러 지표가 계산됩니다. 기본 지표는 다음 줄을 사용자 `application.properties`계정에 추가하여 명시적으로 선언할 수 있습니다.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE] 지표가 정의되지 않은 경우 기본 지표가 활성화됩니다.

에 대한 값을 변경하여 특정 지표를 활성화할 수 `evaluation.metrics.com`있습니다. 다음 예에서는 F-점수 지표가 활성화됩니다.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

다음 표에는 각 클래스에 대한 기본 지표가 나와 있습니다. 사용자는 열의 값을 사용하여 특정 지표를 활성화할 수도 있습니다. `evaluation.metric`

| `evaluator.class` | 기본 지표 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | 정밀한 <br>리콜 <br>혼동 매트릭스 <br>-F-스코어 <br>정확도-리시버 작동특성-리시버 작동특성-리시버 <br><br>운전특성 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | 정밀한 <br>리콜 <br>혼동 매트릭스 <br>-F-스코어 <br>정확도-리시버 작동특성-리시버 작동특성-리시버 <br><br>운전특성 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -평균 평균 정밀도(MAP) <br>- 표준화된 할인된 누적 게인 <br>평균 상호 <br>순위 지표 K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala에 대한 사용자 정의 평가 지표

사용자 지정 평가기는 `MLEvaluator.scala` `Evaluator.scala` 파일에서 의 인터페이스를 확장하여 제공할 수 있습니다. 예제 [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 파일에서 사용자 지정 `split()` 및 `evaluate()` 함수를 정의합니다. Adobe의 `split()` 기능은 8:2의 비율로 데이터를 무작위로 분할하며, Adobe의 `evaluate()` 기능은 3개의 지표를 정의하고 반환합니다.MAPE, AME 및 RMSE.

>[!IMPORTANT] 이 `MLMetric` 클래스의 경우, 새 `"measures"` 항목을 만들 `valueType` `MLMetric` 때 이 지표가 사용자 지정 평가 지표 테이블에 채워지지 않게 됩니다.
>  
> 다음을 수행합니다. `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 그렇지 않음: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


레서피에 정의되면 다음 단계는 레서피에서 이를 활성화하는 것입니다. 이 작업은 프로젝트의 [폴더에 있는 application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 파일에서 수행됩니다 `resources` . 여기에서 `evaluation.class` `Evaluator` 는 `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

데이터 과학 작업 공간에서 사용자는 실험 페이지의 &quot;평가 지표&quot; 탭에서 통찰력을 볼 수 있습니다.

### Python/Tensorflow {#pythontensorflow}

현재 Python 또는 Tensorflow에 대한 기본 평가 지표가 없습니다. 따라서 Python 또는 Tensorflow의 평가 지표를 얻으려면 사용자 지정 평가 지표를 만들어야 합니다. 이 작업은 `Evaluator` 클래스를 구현하여 수행할 수 있습니다.

#### Python에 대한 사용자 정의 평가 지표

사용자 지정 평가 지표의 경우 평가기에 대해 구현해야 하는 두 가지 기본 방법이 있습니다. `split()` 및 `evaluate()`Adobe

Python의 경우 이러한 메서드는 [클래스의 eager.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 에 정의됩니다 `Evaluator` . 의 예를 보려면 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 링크를 `Evaluator`따르십시오.

Python에서 평가 지표를 만들려면 사용자가 `evaluate()` 및 `split()` 메서드를 구현해야 합니다.

이 `evaluate()` 메서드는 속성이 `name`, `value`및 `valueType`있는 지표 객체의 배열을 포함하는 지표 객체를 반환합니다.

이 `split()` 방법은 데이터를 입력하고 교육 및 테스트 데이터 세트를 출력하는 것입니다. 이 예제에서는 `split()` SDK를 사용하여 데이터를 입력한 `DataSetReader` 다음 관련 없는 열을 제거하여 데이터를 정리합니다. 여기에서 데이터의 기존 원시 기능에서 추가 기능이 만들어집니다.

이 `split()` 메서드는 교육 및 테스트 데이터 프레임을 반환하고 이 데이터 프레임을 `pipeline()` 메서드에서 사용하여 ML 모델을 트레이닝하고 테스트해야 합니다.

#### Tensorflow에 대한 사용자 정의 평가 지표

텐소플로우의 경우, 파이톤과 유사한 방법과 `evaluate()``split()` `Evaluator` 수업 방법을 시행해야 한다. 예를 `evaluate()`들어, 기차 및 테스트 데이터 세트를 반환하면서 지표를 반환해야 `split()` 합니다.

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

현재 R에 대한 기본 평가 지표가 없습니다.따라서 R에 대한 평가 지표를 얻으려면 `applicationEvaluator` 클래스를 레서피의 일부로 정의해야 합니다.

#### R에 대한 사용자 정의 평가 지표

기본 목적은 `applicationEvaluator` 지표의 키-값 쌍을 포함하는 JSON 개체를 반환하는 것입니다.

이 [applicationEvaluator.](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) R을 예로 사용할 수 있습니다. 이 예에서는 `applicationEvaluator` 다음 세 개의 친숙한 섹션으로 분할됩니다.
- 데이터 로드
- 데이터 준비/기능 엔지니어링
- 저장된 모델 검색 및 평가

데이터는 먼저 [retail.config.json에 정의된 것처럼 소스에서 데이터 세트에](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)로드됩니다. 이 데이터를 정리하여 머신 러닝 모델에 맞게 제작할 수 있습니다. 마지막으로, 모델은 데이터세트를 사용하여 예측을 하는 데 사용되며 예측된 값과 실제 값에서 지표가 계산됩니다. 이 경우 MAPE, AME 및 RMSE가 정의되고 `metrics` 개체에서 반환됩니다.

## 미리 작성된 지표 및 시각화 차트 사용

Sensei Model Insights Framework는 각 유형의 기계 학습 알고리즘에 대해 하나의 기본 템플릿을 지원합니다. 아래 표는 일반적인 고급 기계 학습 알고리즘 클래스와 해당 평가 지표 및 시각화를 보여줍니다.

| ML 알고리즘 유형 | 평가 지표 | 시각화 |
--- | --- | ---
| 회귀 | - RMSE<br>- MAPE<br>- MASE<br>- 마에 | 예측된 값과 실제 값 오버레이 곡선 |
| 이진 분류 | - 혼동 매트릭스<br>- Precision-requake<br>- Accuracy<br>- F-score (구체적으로 F1,F2)<br>- AUC<br>- ROC | ROC 곡선 및 혼동 매트릭스 |
| 다중 클래스 분류 | -혼동 매트릭스 <br>- 각 클래스에 대해: <br>- 정밀도 회수 정확도 <br>- F 스코어(구체적으로 F1, F2) | ROC 곡선 및 혼동 매트릭스 |
| 클러스터링(근거 없는 정보 포함) | - NMI(정규화된 상호 정보 점수), AMI(조정된 상호 정보 점수)<br>- RI(랜드 인덱스), ARI(조정된 랜드 인덱스)<br>- 동질점, 완전점 및 V-measure<br>- FMI(파울크스-멜로우 인덱스)<br>- 순도<br>- Jacard 인덱스 | 클러스터 플롯 - 클러스터 내에 있는 데이터 포인트를 반영하는 상대적인 클러스터 크기의 클러스터 및 중심 ID를 표시합니다. |
| 클러스터링(근거 없음) | - 관성<br>- 실루엣 계수<br>- CHI (Calinski-Harabaz index)<br>- DBI (Davis-Bouldin index)<br>- Dunn index | 클러스터 플롯 - 클러스터 내에 있는 데이터 포인트를 반영하는 상대적인 클러스터 크기의 클러스터 및 중심 ID를 표시합니다. |
| 권장 사항 | -평균 평균 정밀도(MAP) <br>- 표준화된 할인된 누적 게인 <br>평균 상호 <br>순위 지표 K | TBD |
| 텐서흐름 사용 사례 | 텐소르 흐름 모델 분석(TFMA) | 신경망 모델 비교/시각화 심층 비교 |
| 기타/오류 캡처 메커니즘 | 모델 작성자가 정의한 사용자 지정 지표 로직(및 해당 평가 차트) 템플릿 불일치의 경우 정상적인 오류 처리 | 평가 지표에 대한 키-값 쌍이 있는 표 |
