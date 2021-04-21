---
keywords: Experience Platform;개발자 가이드;데이터 과학 작업 공간;인기 항목;실시간 기계 학습;노드 참조;
solution: Experience Platform
title: 실시간 기계 학습 노드 참조
topic-legacy: Nodes reference
description: 노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 ML 파이프라인을 나타내는 그래프를 형성하는 링크를 사용하여 함께 연결할 수 있습니다. 노드에서 수행하는 작업은 데이터 또는 스키마 변형 또는 기계 학습 유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변형되거나 유추된 값을 다음 노드로 출력합니다.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 실시간 기계 학습 노드 참조(알파)

>[!IMPORTANT]
>
>아직 모든 사용자는 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 버전이며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 ML 파이프라인을 나타내는 그래프를 형성하는 링크를 사용하여 함께 연결할 수 있습니다. 노드에서 수행하는 작업은 데이터 또는 스키마 변형 또는 기계 학습 유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변형되거나 유추된 값을 다음 노드로 출력합니다.

다음 가이드는 실시간 기계 학습을 위해 지원되는 노드 라이브러리에 대해 간략하게 설명합니다.

## ML 파이프라인에서 사용할 노드 검색

다음 코드를 [!DNL Python] 전자 필기장에 복사하여 사용할 수 있는 모든 노드를 확인합니다.

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

표준 노드는 Pendanda 및 ScikitLearn과 같은 오픈 소스 데이터 과학 라이브러리를 기반으로 구축됩니다.

### ModelUpload

ModelUpload 노드는 model_path를 가져와 로컬 모델 경로에서 실시간 기계 학습 Blob 저장소로 모델을 업로드하는 내부 Adobe 노드입니다.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode는 사전 교육된 ONNX 모델을 가져오기 위해 모델 ID를 사용하고 이를 통해 들어오는 데이터에 대해 점수를 매기는 내부 Adobe 노드입니다.

>[!TIP]
>
>데이터를 ONNX 모델로 전송하여 점수를 매길 것과 동일한 순서로 열을 지정합니다.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 판다 {#pandas}

다음 팬더 노드를 사용하면 `pd.DataFrame` 메서드 또는 일반적인 팬더 최상위 함수를 가져올 수 있습니다. 팬더 방식에 대한 자세한 내용은 [팬더 메서드 설명서](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)를 참조하십시오. 최상위 함수에 대한 자세한 내용은 일반 함수](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)에 대한 [Fanda API 참조 안내서를 참조하십시오.

아래 노드는 `"import": "map"`을 사용하여 메서드 이름을 매개 변수에 문자열로 가져온 다음 매개 변수를 지도 함수로 삽입합니다. 아래 예제는 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`을 사용하여 이 작업을 수행합니다. 맵을 제자리에 배치하면 `inplace`을 `True` 또는 `False`로 설정할 수 있습니다. 변형을 즉석 적용할지 여부를 기준으로 `inplace`을 `True` 또는 `False`로 설정합니다. 기본적으로 `"inplace": False`은(는) 새 열을 만듭니다. 새 열 이름을 제공하기 위한 지원이 후속 릴리스에서 추가되도록 설정되어 있습니다. 마지막 행 `cols`은 단일 열 이름 또는 열 목록이 될 수 있습니다. 변형을 적용할 열을 지정합니다. 이 예에서 `device`이(가) 지정되었습니다.

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

ScikitLearn 노드를 사용하면 ScrikitLearn ML 모델 또는 스케일러를 가져올 수 있습니다. 다음 예제에서 사용되는 값에 대한 자세한 내용은 아래 표를 참조하십시오.

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
| features | 모델에 기능을 입력합니다(문자열 목록). <br> 예: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Target 열 이름(문자열). |
| mode | 트레이닝/테스트(문자열). |
| model_path | 저장 모델의 경로를 onnx 형식으로 로컬로 설정합니다. |
| params.model | 모델(문자열)에 대한 절대 가져오기 경로(예:`sklearn.linear_model.LogisticRegression`. |
| params.model_params | 모델 하이퍼매개 변수는 자세한 내용은 [Sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 설명서를 참조하십시오. |
| node_instance.process(data_message_from_previous_node) | `process()` 메서드는 이전 노드에서 DataMsg를 가져와서 변환을 적용합니다. 사용 중인 현재 노드에 따라 다릅니다. |

### 분할

다음 노드를 사용하여 `train_size` 또는 `test_size`을(를) 전달하여 데이터 프레임을 트레이닝하고 테스트합니다. 다중 인덱스가 있는 데이터 프레임을 반환합니다. 다음 예인 `msg5.data.xs(“train”)`을 사용하여 데이터 프레임을 교육 및 테스트할 수 있습니다.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 다음 단계

다음 단계는 실시간 기계 학습 모델 점수를 매길 때 사용할 노드를 만드는 것입니다. 자세한 내용은 [실시간 기계 학습 노트북 사용자 안내서](./rtml-authoring-notebook.md)를 참조하십시오.
