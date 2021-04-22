---
keywords: Experience Platform;최적화;모델;데이터 과학 작업 공간;인기 있는 주제;모델 통찰력
solution: Experience Platform
title: 모델 인사이트 프레임워크를 사용하여 모델 최적화
topic-legacy: tutorial
type: Tutorial
description: Model Insights Framework는 데이터 과학자에게 실험을 기반으로 최적의 기계 학습 모델을 위한 신속하고 정확한 선택을 할 수 있는 데이터 과학 작업 공간의 툴을 제공합니다.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Model Insights 프레임워크를 사용하여 모델 최적화

Model Insights Framework는 실험을 기반으로 최적의 기계 학습 모델을 위한 신속하고 정확한 선택을 할 수 있도록 데이터 과학자에게 [!DNL Data Science Workspace]의 도구를 제공합니다. 이 프레임워크는 시스템 학습 워크플로우의 속도와 효율성을 향상시키고 데이터 과학자의 사용 용이성을 향상시킵니다. 이 작업은 모델 조정을 지원하기 위해 각 기계 학습 알고리즘 유형에 대한 기본 템플릿을 제공하여 수행됩니다. 최종 결과를 통해 데이터 과학자와 시민 데이터 과학자는 최종 고객을 위해 보다 효과적인 모델 최적화 결정을 내릴 수 있습니다.

## 지표란?

모델을 구현하고 교육한 후, 데이터 과학자는 모델이 얼마나 잘 수행되는지 찾는 것입니다. 다양한 지표는 모델이 다른 지표와 비교하여 얼마나 효과적인지 찾는 데 사용됩니다. 사용되는 지표의 일부 예는 다음과 같습니다.
- 분류 정확도
- 곡선 아래의 영역
- 혼동 행렬
- 분류 보고서

## 레서피 코드 구성

현재 Model Insights Framework는 다음 런타임을 지원합니다.
- [스칼라](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

레서피에 대한 샘플 코드는 `recipes` 아래의 [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 저장소에서 찾을 수 있습니다. 이 보관소의 특정 파일은 이 자습서 전체에서 참조됩니다.

### Scala {#scala}

레서피에 지표를 가져오는 두 가지 방법이 있습니다. 하나는 SDK에서 제공하는 기본 평가 지표를 사용하는 것이고 다른 하나는 사용자 지정 평가 지표를 작성하는 것입니다.

#### Scala에 대한 기본 평가 지표

기본 평가는 분류 알고리즘의 일부로 계산됩니다. 다음은 현재 구현된 평가자의 몇 가지 기본값입니다.

| 평가기 클래스 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEcoder | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEcoder | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEager | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

평가기는 `recipe` 폴더의 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 파일의 레서피에서 정의할 수 있습니다. `DefaultBinaryClassificationEvaluator`을(를) 활성화하는 샘플 코드가 아래에 표시됩니다.

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

평가기 클래스가 활성화되면 기본적으로 교육 도중 여러 지표가 계산됩니다. 기본 지표는 `application.properties`에 다음 행을 추가하여 명시적으로 선언할 수 있습니다.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>지표가 정의되지 않은 경우 기본 지표가 활성화됩니다.

`evaluation.metrics.com`에 대한 값을 변경하여 특정 지표를 활성화할 수 있습니다. 다음 예에서 F-점수 지표가 활성화됩니다.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

다음 표에는 각 클래스에 대한 기본 지표가 나와 있습니다. 사용자는 `evaluation.metric` 열의 값을 사용하여 특정 지표를 활성화할 수도 있습니다.

| `evaluator.class` | 기본 지표 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Incomputed Matrix <br>-F-Score <br>-정확도 <br>-수신기 운영 특성 <br> - 받는 사람 운영 특성 | -`PRECISION` <br>`RECALL`-<br>-`CONFUSION_MATRIX`<br>-`FSCORE`<br>-`ACCURACY`<br>`ROC`<br>-`AUROC`> |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Incomputed Matrix <br>-F-Score <br>-정확도 <br>-수신기 운영 특성 <br> - 받는 사람 운영 특성 | -`PRECISION` <br>`RECALL`-<br>-`CONFUSION_MATRIX`<br>-`FSCORE`<br>-`ACCURACY`<br>`ROC`<br>-`AUROC`> |
| `RecommendationsEvaluator` | -평균 평균 정밀도(MAP) <br>-표준화된 할인된 누적 게인 <br>-평균 상호 등급 <br>-지표 K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala에 대한 사용자 정의 평가 지표

`Evaluator.scala` 파일에서 `MLEvaluator.scala` 인터페이스를 확장하여 사용자 지정 평가기를 제공할 수 있습니다. 예제 [Eager.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 파일에서 사용자 정의 `split()` 및 `evaluate()` 함수를 정의합니다. `split()` 함수는 8:2 비율로 데이터를 임의로 분할하고 `evaluate()` 함수는 3개의 지표를 정의하고 반환합니다.MAPE, MAE 및 RMSE.

>[!IMPORTANT]
>
>`MLMetric` 클래스의 경우 새 `MLMetric`을 만들 때 `valueType`에 `"measures"`을 사용하지 마십시오. 그렇지 않으면 지표가 사용자 지정 평가 지표 테이블에 채워지지 않습니다.
>  
> 방법: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 그렇지 않음:`metrics.add(new MLMetric("MAPE", mape, "measures"))`


레서피에 정의되면 다음 단계는 레서피에서 이를 활성화하는 것입니다. 이 작업은 프로젝트의 `resources` 폴더에 있는 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 파일에서 수행됩니다. 여기서 `evaluation.class`은 `Evaluator.scala`에 정의된 `Evaluator` 클래스로 설정됩니다.

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

[!DNL Data Science Workspace]에서 사용자는 실험 페이지의 &quot;평가 지표&quot; 탭에서 통찰력을 볼 수 있습니다.

### [!DNL Python/Tensorflow] {#pythontensorflow}

현재 [!DNL Python] 또는 [!DNL Tensorflow]에 대한 기본 평가 지표가 없습니다. 따라서 [!DNL Python] 또는 [!DNL Tensorflow]에 대한 평가 지표를 가져오려면 사용자 지정 평가 지표를 만들어야 합니다. 이 작업은 `Evaluator` 클래스를 구현하여 수행할 수 있습니다.

#### [!DNL Python]에 대한 사용자 지정 평가 지표

사용자 지정 평가 지표의 경우 평가기에 대해 구현해야 하는 두 가지 주요 방법이 있습니다.`split()` 및 `evaluate()`.

[!DNL Python]의 경우 이러한 메서드는 `Evaluator` 클래스의 [evaluer.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)에 정의됩니다. `Evaluator`의 예를 보려면 [eager.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 링크를 클릭하십시오.

[!DNL Python]에서 평가 지표를 만들려면 사용자가 `evaluate()` 및 `split()` 메서드를 구현해야 합니다.

`evaluate()` 메서드는 `name`, `value` 및 `valueType`의 속성이 있는 지표 객체의 배열을 포함하는 지표 객체를 반환합니다.

`split()` 메서드의 목적은 데이터를 입력하고 교육 및 테스트 데이터 세트를 출력하는 것입니다. 이 예제에서 `split()` 메서드는 `DataSetReader` SDK를 사용하여 데이터를 입력한 다음 관련 없는 열을 제거하여 데이터를 정리합니다. 여기에서 데이터의 기존 원시 기능에서 추가 기능이 만들어집니다.

`split()` 메서드는 교육 및 테스트 데이터 프레임을 반환하고, 이 데이터 프레임을 `pipeline()` 메서드에서 사용하여 ML 모델을 트레이닝하고 테스트해야 합니다.

#### Tensorflow에 대한 사용자 정의 평가 지표

[!DNL Python]과 유사한 [!DNL Tensorflow]의 경우 `Evaluator` 클래스의 `evaluate()` 및 `split()` 메서드를 구현해야 합니다. `evaluate()`의 경우 `split()`이 열차 및 테스트 데이터 세트를 반환하는 동안 지표가 반환되어야 합니다.

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

현재 R에 대한 기본 평가 지표가 없습니다. 따라서 R에 대한 평가 지표를 가져오려면 레서피의 일부로 `applicationEvaluator` 클래스를 정의해야 합니다.

#### R에 대한 사용자 정의 평가 지표

`applicationEvaluator`의 주된 목적은 지표의 키-값 쌍을 포함하는 JSON 개체를 반환하는 것입니다.

이 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R)을 예로 사용할 수 있습니다. 이 예에서 `applicationEvaluator`은(는) 다음과 같은 세 개의 친숙한 섹션으로 분할됩니다.
- 데이터 로드
- 데이터 준비/기능 엔지니어링
- 저장된 모델 검색 및 평가

데이터는 먼저 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)에 정의된 대로 소스의 데이터 세트에 로드됩니다. 여기서, 데이터는 기계 학습 모델에 맞게 정리되고 엔지니어링됩니다. 마지막으로, 모델은 데이터세트를 사용하여 예측을 하는 데 사용되며 예측된 값과 실제 값으로부터 지표가 계산됩니다. 이 경우 MAPE, MAE 및 RMSE가 정의되고 `metrics` 개체에서 반환됩니다.

## 미리 작성된 지표 및 시각화 차트 사용

[!DNL Sensei Model Insights Framework]은 각 유형의 기계 학습 알고리즘에 대해 하나의 기본 템플릿을 지원합니다. 아래 표는 일반적인 고급 기계 학습 알고리즘 클래스와 해당 평가 지표 및 시각화를 보여줍니다.

| ML 알고리즘 유형 | 평가 지표 | 시각화 |
| --- | --- | --- |
| 회귀 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 예측된 값과 실제 값 오버레이 곡선 비교 |
| 이진 분류 | - 혼동 매트릭스<br>- Precision-recover<br>- Accuracy<br>- F-점수(특히 F1,F2)<br>- AUC<br>- ROC | ROC 곡선 및 혼동 매트릭스 |
| 다중 클래스 분류 | -혼동 행렬 <br>- 각 클래스에 대해:<br>- precision-recover 정확도 <br>- F-점수(특히 F1, F2) | ROC 곡선 및 혼동 매트릭스 |
| 클러스터링(기본 진실 포함) | - NMI(정규화된 상호 정보 점수), AMI(조정된 상호 정보 점수)<br>- RI(랜드 인덱스)<br>- 동질점수, 완전점 및 V-measurement<br>- FMI(파울러-멜로우 인덱스)<br>- 순도<br>- Jacard index | 클러스터 플롯 - 클러스터 내에 있는 데이터 포인트의 반사성을 나타내는 상대적인 클러스터 크기의 클러스터 및 중앙 ID 표시 |
| 클러스터링(기본 진실 포함) | - 관성<br>- 실루엣 계수<br>- CHI(Calinski-Harabaz index)<br>- DBI(Davis-Bouldin 인덱스)<br>- Dunn 인덱스 | 클러스터 플롯 - 클러스터 내에 있는 데이터 포인트의 반사성을 나타내는 상대적인 클러스터 크기의 클러스터 및 중앙 ID 표시 |
| 권장 사항 | -평균 평균 정밀도(MAP) <br>-표준화된 할인된 누적 게인 <br>-평균 상호 등급 <br>-지표 K | TBD |
| 텐서흐름 사용 사례 | 텐소르 흐름 모델 분석(TFMA) | 신경망 모델 비교/시각화 심층 비교 |
| 기타/오류 캡처 메커니즘 | 모델 작성자가 정의한 사용자 지정 지표 논리(및 해당 평가 차트). 템플릿이 일치하지 않는 경우 적절한 오류 처리 | 평가 지표에 대한 키-값 쌍이 있는 표 |
