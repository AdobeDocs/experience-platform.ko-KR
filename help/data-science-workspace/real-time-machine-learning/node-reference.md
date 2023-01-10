---
keywords: Experience Platform;개발자 안내서;데이터 과학 작업 공간;인기 항목;실시간 머신 러닝;노드 참조;
solution: Experience Platform
title: 실시간 기계 학습 노드 참조
description: 노드는 그래프가 형성된 기본 단위입니다. 각 노드는 특정 작업을 수행하며 링크를 사용하여 함께 체인으로 연결하여 ML 파이프라인을 나타내는 그래프를 구성할 수 있습니다. 노드에 의해 수행되는 작업은 데이터나 스키마의 변형 또는 학습유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변환 또는 유추된 값을 다음 노드에 출력합니다.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 실시간 기계 학습 노드 참조(알파)

>[!IMPORTANT]
>
>아직 모든 사용자가 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 상태이며 아직 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

노드는 그래프가 형성된 기본 단위입니다. 각 노드는 특정 작업을 수행하며 링크를 사용하여 함께 체인으로 연결하여 ML 파이프라인을 나타내는 그래프를 구성할 수 있습니다. 노드에 의해 수행되는 작업은 데이터나 스키마의 변형 또는 학습유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변환 또는 유추된 값을 다음 노드에 출력합니다.

다음 안내서에서는 실시간 머신 러닝을 위해 지원되는 노드 라이브러리에 대해 설명합니다.

## ML 파이프라인에서 사용할 노드 살펴보기

다음 코드를 [!DNL Python] 사용 가능한 모든 노드를 볼 수 있는 노트북

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**예제 응답**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## 표준 노드

표준 노드는 Pendanda 및 ScikitLearn과 같은 오픈 소스 데이터 과학 라이브러리에 구축됩니다.

### ModelUpload

ModelUpload 노드는 model_path를 사용하여 로컬 모델 경로에서 실시간 기계 학습 blob 저장소로 모델을 업로드하는 내부 Adobe 노드입니다.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode는 사전 교육된 ONNX 모델을 가져오기 위해 모델 ID를 가져와 수신 데이터에 대해 점수를 매기는 내부 Adobe 노드입니다.

>[!TIP]
>
>데이터를 ONNX 모델로 전송하여 점수를 매길 것과 동일한 순서로 열을 지정합니다.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 판다 {#pandas}

다음 Penders 노드를 사용하여 원하는 항목을 가져올 수 있습니다 `pd.DataFrame` 일반적인 판다들의 최상위 수준 기능을 제공하는 방법 팬더 방법에 대해 더 배우기 위해, [판다형 방법 설명서](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 최상위 함수에 대한 자세한 내용은 [일반 기능에 대한 Penders API 참조 안내서](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

아래 노드는 `"import": "map"` 메서드 이름을 매개 변수에 문자열로 가져온 다음 매개 변수를 맵 함수로 입력합니다. 아래 예제는 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 지도가 제위치에 배치되면 설정할 수 있는 선택 사항이 있습니다 `inplace` 로서의 `True` 또는 `False`. 설정 `inplace` 로서의 `True` 또는 `False` 변환 대신 적용할지 여부를 기준으로 합니다. 기본적으로 `"inplace": False` 새 열을 만듭니다. 새 열 이름을 제공하기 위한 지원이 후속 릴리스에서 추가되도록 설정되어 있습니다. 마지막 줄 `cols` 단일 열 이름 또는 열 목록일 수 있습니다. 변형을 적용할 열을 지정합니다. 이 예에서 `device` 이 지정됩니다.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

ScikitLearn 노드를 사용하면 ScrikitLearn ML 모델 또는 스케일러를 가져올 수 있습니다. 이 예에서 사용된 값에 대한 자세한 내용은 아래 표를 사용하십시오.

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 값 | 설명 |
| --- | --- |
| 기능 | 모델에 피쳐를 입력합니다(문자열 목록). <br> 예: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Target 열 이름(문자열). |
| 모드 | 교육/테스트(문자열). |
| model_path | onnx 형식으로 로컬에서 저장 모델의 경로입니다. |
| params.model | 모델(문자열)의 절대 가져오기 경로: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 모델 하이퍼매개 변수에 대해서는 [sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 설명서 를 참조하십시오. |
| node_instance.process(data_message_from_previous_node) | 메서드 `process()` 이전 노드에서 DataMsg를 가져와 변형을 적용합니다. 사용 중인 현재 노드에 따라 다릅니다. |

### 분할

다음 노드를 사용하여 데이터 프레임을 교육 및 테스트로 분할합니다. `train_size` 또는 `test_size`. 이렇게 하면 다중 인덱스가 있는 데이터 프레임이 반환됩니다. 다음 예를 사용하여 데이터 프레임을 교육 및 테스트할 수 있습니다. `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 다음 단계

다음 단계는 실시간 기계 학습 모델 점수를 매기는 데 사용할 노드를 만드는 것입니다. 자세한 내용은 [실시간 기계 학습 노트북 사용 안내서](./rtml-authoring-notebook.md).
