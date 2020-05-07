---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: 실시간 기계 학습 모델 점수 지정
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 실시간 기계 학습 모델 점수 지정

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

이 자습서에서는 실시간 기계 학습 노드를 사용하여 수신 데이터를 미리 처리하고 ONNX 모델에 대해 점수를 매기는 방법을 설명합니다.

>[!IMPORTANT]
> - 노드에 사용된 함수를 직렬화할 수 없습니다. 예를 들어 판다 노드에 사용되는 람다 함수입니다.
> - Edge Deployment를 수동으로 수행한 후 60초 절전 모드가 수행됩니다. EdgeUtils의 score_edge 메서드로 전송할 수 있습니다.


>[!NOTE]
>실시간 기계 학습에서 사용할 모델을 평가하려면 실시간 기계 학습용 모델 [트레이닝에 대한 이전 자습서를 수료해야 합니다](./training-ml-model.md)

## 새 전자 필기장 만들기

Adobe Experience Platform UI의 **[!UICONTROL 데이터 과학]** 내에서 *노트북을 선택합니다*. 그런 다음 **[!UICONTROL JupiterLab을]** 선택하고 환경을 로드하는 데 시간을 허용합니다.

![open JupiterLab](../images/rtml/open-jupyterlab.png)

JupiterLab launcher 내에서 **빈 Python 3 노트북을** 선택하여 시작합니다.

![빈 비단뱀](../images/rtml/python-blank.png)

## 노드 가져오기 및 검색

먼저 모델에 필요한 모든 패키지를 가져옵니다. 노드 작성에 사용할 모든 패키지를 가져왔는지 확인하십시오.

>[!NOTE]
>가져오기의 목록은 사용자가 만든 모델에 따라 다를 수 있습니다.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

사용 가능한 노드 목록을 보려면 다음 예제를 복사하여 전자 필기장에 붙여 넣습니다.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

수신된 응답은 노드 목록입니다.

![메모 목록](../images/rtml/node-list.png)

## 에지 점수를 위한 노드 작성

다음으로, 가장자리 점수에 대한 노드를 정의하고 작성해야 합니다. 예제 `model_id` 의 ID를 [이전 자습서에서 교육 완료 후 받은 모델 ID로 바꿉니다](./training-ml-model.md). 이 예에서는 팬더 노드를 사용하여 pd.DataDrame 메서드 또는 일반 팬더 최상위 함수를 가져옵니다. 맵 함수를 가져와서 두 개의 노드를 만드는 데 사용합니다. 사용 가능한 노드 및 사용 방법에 대한 자세한 내용은 [노드 참조 안내서를 참조하십시오](./node-reference.md).

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## 그래프 DSL 작성

노드가 만들어지면 다음 단계는 노드를 서로 연결하여 그래프를 만드는 것입니다.

먼저 그래프의 일부인 모든 노드를 나눕니다.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

그런 다음 모서리와 노드를 연결합니다. 각 튜플은 모서리 연결입니다.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

노드가 연결되면 그래프를 만듭니다.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## 가장자리에 게시

그래프를 만들었으므로 이제 그래프를 가장자리에 배포할 수 있습니다.

>[!IMPORTANT]
>가장자리에 자주 게시하지 마십시오. 에지 노드를 오버로드할 수 있습니다. 동일한 모델을 여러 번 게시하는 것은 권장되지 않습니다.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Edge 클라이언트

Edge에 게시한 후에는 클라이언트의 POST 요청에 의해 점수가 매겨집니다. 일반적으로 ML 점수가 필요한 클라이언트 애플리케이션에서 이 작업을 수행할 수 있습니다. 포스트맨에서도 가능합니다. 여기서 EdgeUtils를 사용하여 프로세스를 시연합니다.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

점수 지정이 완료되면 가장자리 URL, 페이로드 및 가장자리에서 나온 점수가 반환됩니다.

![채점 완료](../images/rtml/scoring-complete.png)

## 가장자리에서 배포된 앱 삭제(선택 사항)

>!![CAUTION]
이 셀은 배포된 Edge 응용 프로그램을 삭제하는 데 사용됩니다. 배포된 Edge Application을 삭제할 필요가 없으면 다음 셀을 사용하지 마십시오.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 다음 단계

위의 튜토리얼을 따라 실시간 기계 학습 모델을 성공적으로 테스트 및 배포했습니다. 모델 작성에 사용할 수 있는 노드에 대해 자세히 알려면 [노드 참조 안내서를 참조하십시오](./node-reference.md).



