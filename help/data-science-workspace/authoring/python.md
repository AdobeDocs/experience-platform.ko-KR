---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;python sdk;데이터 액세스 api;python 읽기;python 쓰기
solution: Experience Platform
title: Data Science Workspace에서 Python을 사용하여 데이터 액세스
type: Tutorial
description: 다음 문서에는 데이터 과학 Workspace에서 사용하기 위해 Python의 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Data Science Workspace에서 Python을 사용하여 데이터 액세스

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

다음 문서에는 데이터 과학 작업 영역 에서 사용하기 위해 Python을 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다. JupiterLab 노트북을 사용한 데이터 액세스에 대한 자세한 내용은 JupiterLab 노트북 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 방문 참조하십시오[.

## 데이터 세트 읽기

환경 변수를 설정하고 설치를 완료한 후 이제 데이터 세트 데이터를 팬더 데이터 프레임으로 읽을 수 있습니다.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 데이터 세트 SELECT 열

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 파티셔닝 정보 가져오기:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT 절

DISTINCT 절을 사용하면 행/열 수준에서 모든 고유 값을 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

`distinct()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE 절

Python에서 특정 연산자를 사용하여 데이터 세트 필터링을 도울 수 있습니다.

>[!NOTE]
>
>필터링에 사용되는 함수는 대소문자 구분

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

이러한 필터링 기능을 사용하는 예는 다음과 같습니다.

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신된 결과를 지정된 열을 기준으로 특정 순서(오름차순 또는 내림차순)로 정렬할 수 있습니다. 이 작업은 함수를 사용하여 `sort()` 수행됩니다.

`sort()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 집합에서 받는 레코드 수를 제한할 수 있습니다.

`limit()` 함수를 사용하는 예는 아래에서 확인할 수 있습니다.

```python
df = dataset_reader.limit(100).read()
```

### OFFSET 절

OFFSET 절을 사용하면 처음부터 행을 건너뛰고 이후 지점에서 행 반환을 시작할 수 있습니다. LIMIT와 함께 블록의 행을 반복하는 데 사용할 수 있습니다.

함수 사용 `offset()` 의 예는 다음과 같습니다.

```python
df = dataset_reader.offset(100).read()
```

## 데이터 세트 쓰기

데이터 세트에 쓰려면 데이터 세트에 pandas 데이터 프레임을 제공해야 합니다.

### 팬더 데이터 프레임 작성

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## 사용자 공간 디렉토리(체크포인트)

실행 시간이 긴 작업의 경우 중간 단계를 저장해야 할 수 있습니다. 이와 같은 경우 사용자 공간을 읽고 쓸 수 있습니다.

>[!NOTE]
>
>데이터 경로가 **저장되지 않음**. 해당 데이터에 해당하는 경로를 저장해야 합니다.

### 사용자 공간에 쓰기

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 사용자 공간에서 읽기

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## 다음 단계

Adobe Experience Platform Data Science 작업 영역는 위의 코드 샘플을 사용하여 데이터를 읽고 쓰는 레서피 샘플을 제공합니다. Python을 사용하여 데이터에 액세스하는 방법에 대해 자세히 알아보려면 데이터 과학 작업 영역 Python GitHub 리포지토리](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)를 [검토하세요.
