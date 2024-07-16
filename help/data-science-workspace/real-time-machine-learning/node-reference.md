---
keywords: Experience Platform;개발자 안내서;Data Science Workspace;인기 주제;실시간 머신 러닝;노드 참조;
solution: Experience Platform
title: 실시간 머신 러닝 노드 참조
description: 노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 링크를 사용하여 서로 체인화되어 ML 파이프라인을 나타내는 그래프를 형성할 수 있습니다. 노드에 의해 수행되는 태스크는 데이터 또는 스키마의 변환, 또는 머신 러닝 추론과 같은 입력 데이터에 대한 동작을 나타낸다. 상기 노드는 상기 변환된 또는 추론된 값을 다음 노드(들)로 출력한다.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Real-time Machine Learning 노드 참조(Alpha)

>[!IMPORTANT]
>
>아직 모든 사용자가 실시간 머신 러닝을 사용할 수 있는 것은 아닙니다. 이 기능은 알파에 있으며 아직 테스트 중입니다. 이 문서는 변경될 수 있습니다.

노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 링크를 사용하여 서로 체인화되어 ML 파이프라인을 나타내는 그래프를 형성할 수 있습니다. 노드에 의해 수행되는 태스크는 데이터 또는 스키마의 변환, 또는 머신 러닝 추론과 같은 입력 데이터에 대한 동작을 나타낸다. 상기 노드는 상기 변환된 또는 추론된 값을 다음 노드(들)로 출력한다.

다음 안내서에서는 실시간 머신 러닝에 대해 지원되는 노드 라이브러리에 대해 간략히 설명합니다.

## ML 파이프라인에서 사용할 노드 검색

[!DNL Python] 전자 필기장에 다음 코드를 복사하여 사용할 수 있는 모든 노드를 봅니다.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**응답 예**

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

표준 노드는 Pandas 및 ScikitLearn과 같은 오픈 소스 데이터 과학 라이브러리를 기반으로 구축됩니다.

### 모델 업로드

ModelUpload 노드는 model_path를 사용하여 로컬 모델 경로에서 실시간 머신 러닝 blob 저장소로 모델을 업로드하는 내부 Adobe 노드입니다.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode는 모델 ID를 가져와서 사전 훈련된 ONNX 모델을 가져와서 이를 사용하여 들어오는 데이터에 대한 점수를 매기는 내부 Adobe 노드입니다.

>[!TIP]
>
>ONNX 모델에 데이터를 전송하여 점수를 매길 열을 동일한 순서로 지정합니다.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 판다스 {#pandas}

다음 Pandas 노드를 사용하면 `pd.DataFrame` 메서드 또는 일반 pandas 최상위 함수를 가져올 수 있습니다. Pandas 메서드에 대한 자세한 내용은 [Pandas 메서드 설명서](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)를 참조하세요. 최상위 함수에 대한 자세한 내용은 일반 함수에 대한 [Pandas API 참조 안내서](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)를 참조하십시오.

아래 노드는 `"import": "map"`을(를) 사용하여 메서드 이름을 매개 변수에서 문자열로 가져온 다음 매개 변수를 맵 함수로 입력합니다. 아래 예제에서는 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`을(를) 사용하여 이 작업을 수행합니다. 맵을 준비한 후에는 `inplace`을(를) `True` 또는 `False`(으)로 설정할 수 있습니다. 변환을 그대로 적용할지 여부를 기준으로 `inplace`을(를) `True` 또는 `False`(으)로 설정합니다. 기본적으로 `"inplace": False`은(는) 새 열을 만듭니다. 새 열 이름을 제공하기 위한 지원이 후속 릴리스에서 추가되도록 설정되었습니다. 마지막 줄 `cols`은(는) 단일 열 이름 또는 열 목록일 수 있습니다. 변형을 적용할 열을 지정합니다. 이 예제에서는 `device`을(를) 지정합니다.

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

ScikitLearn 노드를 사용하면 모든 ScikitLearn ML 모델이나 스케일러를 가져올 수 있습니다. 예제에 사용된 값에 대한 자세한 내용은 아래 표를 참조하십시오.

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
| 기능 | 모델에 대한 입력 기능(문자열 목록). <br> 예: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| 레이블 | 대상 열 이름(문자열)입니다. |
| 모드 | 교육/테스트(문자열). |
| model_path | onnx 형식으로 로컬에 저장된 모델의 경로. |
| params.model | 모델(문자열)에 대한 절대 가져오기 경로(예: `sklearn.linear_model.LogisticRegression`). |
| params.model_params | 모델 하이퍼매개 변수에 대한 자세한 내용은 [sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 설명서를 참조하십시오. |
| node_instance.process(data_message_from_previous_node) | `process()` 메서드는 이전 노드에서 DataMsg를 가져와서 변환을 적용합니다. 이는 사용 중인 현재 노드에 따라 다릅니다. |

### 분할

`train_size` 또는 `test_size`을(를) 전달하여 데이터 프레임을 트레인 및 테스트로 분할하려면 다음 노드를 사용하십시오. 다중 인덱스가 있는 데이터 프레임을 반환합니다. 다음 예제 `msg5.data.xs("train")`을(를) 사용하여 트레인 및 테스트 데이터 프레임에 액세스할 수 있습니다.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 다음 단계

다음 단계는 실시간 머신 러닝 모델을 점수화하는 데 사용할 노드를 만드는 것입니다. 자세한 내용은 [실시간 기계 학습 전자 필기장 사용 안내서](./rtml-authoring-notebook.md)를 참조하세요.
