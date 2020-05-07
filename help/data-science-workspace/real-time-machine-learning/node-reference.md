---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: 실시간 기계 학습 노드 참조 안내서
topic: Nodes reference
translation-type: tm+mt
source-git-commit: a37a3dd0c8f784d69da25ac503ad388b57b05ed9
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 실시간 기계 학습 노드 참조 안내서

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

다음 가이드는 실시간 기계 학습을 위해 지원되는 노드 라이브러리에 대해 간략하게 설명합니다.

## ML 파이프라인에서 사용할 노드 검색

다음 코드를 Python 전자 필기장에 복사하여 사용할 수 있는 모든 노드를 확인합니다.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**예제 응답**

```python
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

표준 노드는 Pendanda 및 ScikitLearn과 같은 오픈 소스 데이터 과학 라이브러리를 기반으로 구축됩니다.

### ModelUpload

ModelUpload 노드는 model_path를 가져와 로컬 모델 경로에서 실시간 기계 학습 Blob 저장소에 모델을 업로드하는 내부 Adobe 노드입니다.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode는 모델 ID를 가져와 사전 교육된 ONNX 모델을 가져와서 들어오는 데이터에 대해 점수를 매기는 내부 Adobe 노드입니다.

>[!TIP]
>데이터를 ONNX 모델로 전송하여 점수를 매길 것과 동일한 순서로 열을 지정합니다.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 팬더 {#pandas}

다음 팬더 노드를 사용하면 모든 `pd.DataFrame` 방식이나 일반적인 팬더 최상위 기능을 가져올 수 있습니다. 팬더 기술에 대한 자세한 내용은 [팬더 방법 설명서를 참조하십시오](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 최상위 기능에 대한 자세한 내용은 일반 기능에 대한 [Fanda API 참조 안내서를 참조하십시오](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

아래 노드는 매개 변수 `"import": "map"` 에서 메서드 이름을 문자열로 가져온 다음 매개 변수를 지도 함수로 입력하는 데 사용합니다. 아래 예제는 다음을 사용하여 수행합니다 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 맵을 제자리에 두고 나면 true 또는 false `inplace` 로 설정할 수 있습니다. 변형 `inplace` 을 즉석 `True` 으로 적용할지 여부 `False` 를 기준으로 설정할 수 있습니다. 기본적으로 새 열 `"inplace": False` 이 만들어집니다. 새 열 이름을 제공하기 위한 지원이 이후 릴리스에서 추가되도록 설정되어 있습니다. 마지막 줄은 단일 열 이름 또는 열 목록일 `cols` 수 있습니다. 변형을 적용할 열을 지정합니다. 이 예에서 `device` 는 지정됩니다.

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

### Scikit학습

ScrikitLearn 노드를 사용하면 ScrikitLearn ML 모델 또는 스케일러를 가져올 수 있습니다. 아래 표를 사용하여 예제에서 사용되는 값에 대한 자세한 내용을 살펴보십시오.

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 값 | 설명 |
| --- | --- |
| features | 모델에 기능 입력(문자열 목록). <br> 예: &#39;browser&#39;, &#39;device&#39;, &#39;login_page&#39;, &#39;product_page&#39;, &#39;search_page&#39; |
| label | 대상 열 이름(문자열). |
| mode | 기차/테스트(문자열). |
| model_path | 로컬(onnx 형식)으로 저장 모델에 대한 경로입니다. |
| params.model | 모델(문자열)에 대한 절대 가져오기 경로(예: &quot;sklearn.linear_model.LogisticRegression&quot;. |
| params.model_params | 모델 하이퍼매개 변수는 [sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 설명서를 참조하십시오. |
| node_instance.process(data_message_from_previous_node) | 이 메서드는 이전 노드에서 DataMsg를 `process()` 가져와서 변환을 적용합니다. 이는 사용 중인 현재 노드에 따라 다릅니다. |

### 분할

다음 노드를 사용하여 데이터 프레임을 교육 및 테스트로 분할하고 전달 `train_size` 또는 테스트를 수행합니다 `test_size`. 다중 인덱스가 있는 데이터 프레임을 반환합니다. 다음 예를 사용하여 데이터 파일에 액세스하고 테스트할 수 있습니다 `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 다음 단계

다음 단계는 실시간 머신 러닝 모델을 평가하는 데 사용할 노드를 만드는 것입니다. 자세한 내용은 실시간 기계 학습 모델 [의](./node-reference.md) 점수 매기에 관한 자습서를 참조하십시오.
