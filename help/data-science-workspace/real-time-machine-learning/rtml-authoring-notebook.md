---
keywords: Experience Platform;개발자 가이드;데이터 과학 작업 공간;인기 항목;실시간 기계 학습;노드 참조;
solution: Experience Platform
title: 실시간 기계 학습 노트북 관리
topic-legacy: Training and scoring a ML model
description: 다음 가이드는 Adobe Experience Platform JupiterLab에서 실시간 기계 학습 애플리케이션을 구축하는 데 필요한 단계를 간략하게 설명합니다.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# 실시간 기계 학습 노트북(알파) 관리

>[!IMPORTANT]
>
>아직 모든 사용자는 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 버전이며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

다음 안내서에서는 실시간 기계 학습 응용 프로그램을 만드는 데 필요한 단계를 설명합니다. 이 안내서에서는 Adobe 제공 **[!UICONTROL Real-time ML]** Python 전자 필기장 템플릿을 사용하여 모델 교육, DSL 만들기, Edge에 DSL을 게시 및 요청 점수 지정에 대해 다룹니다. 실시간 머신 러닝 모델을 구현하는 작업이 진행되면 데이터세트의 요구 사항에 맞게 템플릿을 수정할 수 있습니다.

## 실시간 기계 학습 노트북 만들기

Adobe Experience Platform UI의 **데이터 과학** 내에서 **[!UICONTROL Notebooks]**&#x200B;을 선택합니다. 그런 다음 **[!UICONTROL JupyterLab]**&#x200B;을 선택하고 환경을 로드할 시간을 허용합니다.

![open JupiterLab](../images/rtml/open-jupyterlab.png)

[!DNL JupyterLab] 실행 프로그램이 나타납니다. *실시간 기계 학습*&#x200B;으로 스크롤하고 **[!UICONTROL Real-time ML]** 전자 필기장을 선택합니다. 예제 데이터세트의 노트북 셀이 들어 있는 템플릿이 열립니다.

![빈 파이트](../images/rtml/authoring-notebook.png)

## 노드 가져오기 및 검색

먼저 모델에 필요한 모든 패키지를 가져옵니다. 노드 작성에 사용할 패키지를 모두 가져와야 합니다.

>[!NOTE]
>
>가져오기 목록은 만들려는 모델에 따라 다를 수 있습니다. 시간이 지남에 따라 새 노드가 추가되면 이 목록이 변경됩니다. 사용 가능한 노드의 전체 목록은 [노드 참조 안내서](./node-reference.md)를 참조하십시오.

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

다음 코드 셀에서는 사용 가능한 노드 목록을 인쇄합니다.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![메모 목록](../images/rtml/node-list.png)

## 실시간 머신 러닝 모델 트레이닝

다음 옵션 중 하나를 사용하여 데이터를 읽고, 미리 처리하고, 분석하는 [!DNL Python] 코드를 작성하게 됩니다. 그런 다음 고유한 ML 모델을 교육하고 ONNX 포맷으로 일련화한 다음 실시간 머신 러닝 모델 스토어에 업로드해야 합니다.

- [JupiterLab 노트북에서 자신만의 모델 트레이닝](#training-your-own-model)
- [사전 교육된 ONNX 모델을 JupiterLab 노트북에 업로드](#pre-trained-model-upload)

### 고유한 모델 {#training-your-own-model} 교육

먼저 교육 데이터를 로드합니다.

>[!NOTE]
>
>**실시간 ML** 템플릿에서 [자동차 보험 CSV 데이터 세트](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance)는 [!DNL Github]에서 가져옵니다.

![교육 데이터 로드](../images/rtml/load_training.png)

Adobe Experience Platform 내에서 데이터 세트를 사용하려면 아래 셀의 주석을 해제합니다. 다음으로 `DATASET_ID`을(를) 적절한 값으로 바꿔야 합니다.

![rtml 데이터 집합](../images/rtml/rtml-dataset.png)

[!DNL JupyterLab] 전자 필기장의 데이터 세트에 액세스하려면 [!DNL JupyterLab]의 왼쪽 탐색에서 **데이터** 탭을 선택합니다. **[!UICONTROL Datasets]** 및 **[!UICONTROL Schemas]** 디렉토리가 표시됩니다. **[!UICONTROL Datasets]**&#x200B;을 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 집합의 드롭다운 메뉴에서 **[!UICONTROL Explore Data in Notebook]** 옵션을 선택합니다. 실행 가능한 코드 항목이 전자 필기장 하단에 표시됩니다. 이 셀에는 `dataset_id`이 있습니다.

![데이터 집합 액세스](../images/rtml/access-dataset.png)

완료되면 전자 필기장 하단에 생성한 셀을 마우스 오른쪽 단추로 클릭하고 삭제합니다.

### 교육 속성

제공된 템플릿을 사용하여 `config_properties` 내의 교육 속성을 수정합니다.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 모델 준비

**[!UICONTROL Real-time ML]** 템플릿을 사용하여 ML 모델을 분석, 사전 처리, 교육 및 평가해야 합니다. 이는 데이터 변형을 적용하고 교육 파이프라인을 구축하는 방식으로 이루어집니다.

**데이터 변형**

데이터 세트 작업을 수행하려면 **[!UICONTROL Real-time ML]** 템플릿 **데이터 변형** 셀을 수정해야 합니다. 일반적으로 열 이름 바꾸기, 데이터 롤업 및 데이터 준비/기능 엔지니어링이 포함됩니다.

>[!NOTE]
>
>다음 예제는 `[ ... ]`을(를) 사용하여 읽기 쉽게 사용할 수 있도록 압축되었습니다. 전체 코드 셀에 대한 *실시간 ML* 템플릿 데이터 변형 섹션을 보고 확장하십시오.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

제공된 셀을 실행하여 예제 결과를 확인합니다. `carinsurancedataset.csv` 데이터 세트에서 반환된 출력 표는 사용자가 정의한 수정 내용을 반환합니다.

![데이터 변형 예](../images/rtml/table-return.png)

**트레이닝 파이프라인**

그런 다음 교육 파이프라인을 만들어야 합니다. ONNX 파일을 변환 및 생성해야 하는 경우를 제외하면 다른 모든 교육 파이프라인 파일과 유사합니다.

이전 셀에 정의된 데이터 변형을 사용하여 템플릿을 수정합니다. 아래 강조 표시된 다음 코드는 피쳐 파이프라인에서 ONNX 파일을 생성하는 데 사용됩니다. 전체 파이프라인 코드 셀에 대한 *실시간 ML* 템플릿을 확인하십시오.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

교육 파이프라인을 완료하고 데이터 변형을 통해 데이터를 수정한 후에는 다음 셀을 사용하여 교육을 실행합니다.

```python
model = train(config_properties, df_final)
```

### ONNX 모델 생성 및 업로드

성공적인 트레이닝 실행을 완료하면 ONNX 모델을 생성하고 트레이닝된 모델을 실시간 머신 러닝 모델 스토어에 업로드해야 합니다. 다음 셀을 실행하면 ONNX 모델이 다른 모든 노트북과 함께 왼쪽 레일에 나타납니다.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>`model_path` 문자열 값(`model.onnx`)을 변경하여 모델의 이름을 변경합니다.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>다음 셀은 편집 또는 삭제할 수 없으며 실시간 기계 학습 응용 프로그램이 작동하기 위해 필요합니다.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![ONNX 모델](../images/rtml/onnx-model-rail.png)

### 사전 교육된 ONNX 모델 {#pre-trained-model-upload} 업로드

[!DNL JupyterLab] 전자 필기장에 있는 업로드 단추를 사용하여 사전 교육된 ONNX 모델을 [!DNL Data Science Workspace] 노트북 환경에 업로드합니다.

![업로드 아이콘](../images/rtml/upload.png)

그런 다음 *실시간 ML* 전자 필기장에서 `model_path` 문자열 값을 ONNX 모델 이름과 일치하도록 변경합니다. 완료하면 *모델 경로 설정* 셀을 실행한 다음 *모델을 RTML 모델 저장소* 셀에 업로드합니다. 모델 위치 및 모델 ID는 모두 성공하면 응답으로 반환됩니다.

![자체 모델 업로드](../images/rtml/upload-own-model.png)

## DSL(도메인별 언어) 만들기

이 섹션에서는 DSL을 만드는 방법에 대해 간략하게 설명합니다. ONNX 노드와 함께 데이터의 사전 처리가 포함된 노드를 작성하려고 합니다. 다음으로 노드 및 가장자리를 사용하여 DSL 그래프가 만들어집니다. Edge는 Tuple 기반 형식(node_1, node_2)을 사용하여 노드를 연결합니다. 그래프에는 주기가 없어야 합니다.

>[!IMPORTANT]
>
>ONNX 노드 사용은 필수입니다. ONNX 노드가 없으면 응용 프로그램이 실패합니다.

### 노드 작성

>[!NOTE]
>
> 사용 중인 데이터 유형에 따라 여러 노드가 있을 수 있습니다. 다음 예제에서는 *실시간 ML* 템플릿의 단일 노드만 간략하게 설명합니다. 전체 코드 셀에 대한 *실시간 ML* 템플릿 *노드 작성* 섹션을 참조하십시오.

아래의 Pendas 노드는 `"import": "map"`을 사용하여 매개 변수에 문자열 이름을 가져온 다음 매개 변수를 지도 함수로 입력하는 방법을 사용합니다. 아래 예제는 `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`을 사용하여 이 작업을 수행합니다. 맵을 제자리에 배치하면 `inplace`을 `True` 또는 `False`로 설정할 수 있습니다. 변형을 즉석 적용할지 여부를 기준으로 `inplace`을 `True` 또는 `False`로 설정합니다. 기본적으로 `"inplace": False`은(는) 새 열을 만듭니다. 새 열 이름을 제공하기 위한 지원이 후속 릴리스에서 추가되도록 설정되어 있습니다. 마지막 행 `cols`은 단일 열 이름 또는 열 목록이 될 수 있습니다. 변형을 적용할 열을 지정합니다. 이 예에서 `leasing`이(가) 지정되었습니다. 사용 가능한 노드 및 사용 방법에 대한 자세한 내용은 [노드 참조 안내서](./node-reference.md)를 참조하십시오.

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### DSL 그래프 만들기

노드를 만든 상태에서 다음 단계는 노드를 서로 연결하여 그래프를 만드는 것입니다.

배열을 작성하여 그래프의 일부인 모든 노드를 나열하는 것부터 시작합니다.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

그런 다음 모서리와 노드를 연결합니다. 각 튜플은 [!DNL Edge] 연결입니다.

>[!TIP]
>
> 노드가 서로 선형으로 종속되므로(각 노드가 이전 노드의 출력에 따라 다름) 간단한 Python 목록 이해를 사용하여 링크를 만들 수 있습니다. 노드가 여러 입력에 의존하는 경우 직접 연결을 추가하십시오.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

노드가 연결되면 그래프를 만듭니다. 아래 셀은 필수 항목이므로 편집하거나 삭제할 수 없습니다.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

완료하면 각 노드와 해당 노드에 매핑된 매개 변수가 포함된 `edge` 객체가 반환됩니다.

![가장자리 반환](../images/rtml/edge-return.png)

## Edge(Hub)에 게시

>[!NOTE]
>
>실시간 머신 러닝은 Adobe Experience Platform 허브에 임시로 배포되고 관리됩니다. 자세한 내용은 [실시간 기계 학습 아키텍처](./home.md#architecture)의 개요 섹션을 참조하십시오.

이제 DSL 그래프를 만들었으므로 그래프를 [!DNL Edge]에 배포할 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Edge]에 자주 게시하지 마십시오. 이 경우 [!DNL Edge] 노드를 오버로드할 수 있습니다. 동일한 모델을 여러 번 게시하는 것은 권장되지 않습니다.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### DSL 업데이트 및 Edge에 다시 게시(선택 사항)

DSL을 업데이트할 필요가 없는 경우 [점수 지정](#scoring)으로 건너뛸 수 있습니다.

>[!NOTE]
>
>다음 셀은 Edge에 게시된 기존 DSL을 업데이트하려는 경우에만 필요합니다.

모델은 계속 개발될 것입니다. 새 서비스를 완전히 만드는 대신 새 모델로 기존 서비스를 업데이트할 수 있습니다. 업데이트할 노드를 정의하고, 새 ID를 지정한 다음, 새 DSL을 [!DNL Edge]에 다시 업로드할 수 있습니다.

아래 예에서 노드 0은 새 ID로 업데이트됩니다.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![업데이트된 노드](../images/rtml/updated-node.png)

노드 ID를 업데이트하면 업데이트된 DSL을 Edge에 다시 게시할 수 있습니다.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

업데이트된 DSL이 반환됩니다.

![업데이트된 DSL](../images/rtml/updated-dsl.png)

## 점수 지정 {#scoring}

[!DNL Edge]에 게시한 후에는 클라이언트의 POST 요청에 의해 점수를 매깁니다. 일반적으로 ML 점수가 필요한 클라이언트 애플리케이션에서 이 작업을 수행할 수 있습니다. 포스트맨에서도 가능합니다. **[!UICONTROL Real-time ML]** 템플릿은 EdgeUtils를 사용하여 이 프로세스를 보여줍니다.

>[!NOTE]
>
>점수가 시작되기 전에 처리 시간이 약간 필요합니다.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

교육에 사용된 동일한 스키마를 사용하면 샘플 점수 데이터가 생성됩니다. 이 데이터는 점수 지정 데이터 프레임을 만든 다음 점수 지정 사전으로 변환하는 데 사용됩니다. 전체 코드 셀에 대한 *실시간 ML* 템플릿을 확인하십시오.

![점수 데이터](../images/rtml/generate-score-data.png)

### 가장자리 끝점에 대한 점수

*실시간 ML* 템플릿 내에서 다음 셀을 사용하여 [!DNL Edge] 서비스에 대해 점수를 매깁니다.

![가장자리 기준 점수](../images/rtml/scoring-edge.png)

점수 지정이 완료되면 [!DNL Edge]에서 [!DNL Edge] URL, 페이로드 및 점수가 지정된 출력이 반환됩니다.

## [!DNL Edge]에서 배포된 앱을 나열합니다.

[!DNL Edge]에 현재 배포된 앱 목록을 생성하려면 다음 코드 셀을 실행하십시오. 이 셀은 편집하거나 삭제할 수 없습니다.

```python
services = edge_utils.list_deployed_services()
print(services)
```

반환된 응답은 배포된 서비스의 배열입니다.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## [!DNL Edge]에서 배포된 앱 또는 서비스 ID 삭제(선택 사항)

>[!CAUTION]
>
>이 셀은 배포된 Edge 응용 프로그램을 삭제하는 데 사용됩니다. 배포된 [!DNL Edge] 응용 프로그램을 삭제할 필요가 없으면 다음 셀을 사용하지 마십시오.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 다음 단계

위의 튜토리얼을 따라 ONNX 모델을 Real-time Machine Learning Model Store에 성공적으로 교육하고 업로드했습니다. 또한 실시간 머신 러닝 모델을 평가하고 배포했습니다. 모델 작성에 사용할 수 있는 노드에 대해 자세히 알려면 [노드 참조 안내서](./node-reference.md)를 참조하십시오.
