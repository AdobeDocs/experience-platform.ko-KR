---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;Python sdk;데이터 액세스 api;읽기 python;쓰기
solution: Experience Platform
title: 데이터 과학 작업 공간에서 Python을 사용하여 데이터 액세스
topic-legacy: tutorial
type: Tutorial
description: 다음 문서에는 데이터 과학 작업 공간에서 사용하기 위해 Python의 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 데이터 과학 작업 공간에서 Python을 사용하여 데이터 액세스

다음 문서에는 데이터 과학 작업 공간에서 사용하기 위해 Python을 사용하여 데이터에 액세스하는 방법에 대한 예가 포함되어 있습니다. JupiterLab 전자 필기장을 사용하여 데이터에 액세스하는 방법에 대한 자세한 내용은 [JupiterLab 전자 필기장 데이터 액세스](../jupyterlab/access-notebook-data.md) 설명서를 참조하십시오.

## 데이터 세트 읽기

환경 변수를 설정하고 설치를 완료한 후 이제 데이터 세트를 판다 데이터 프레임으로 읽을 수 있습니다.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 데이터 세트에서 열 선택

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 분할 정보 가져오기:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT 절

DISTINCT 절을 사용하면 모든 개별 값을 행/열 수준에서 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

`distinct()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE 절

Python의 특정 연산자를 사용하여 데이터 세트를 필터링할 수 있습니다.

>[!NOTE]
>
>필터링에 사용되는 함수는 대/소문자를 구분합니다.

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

ORDER BY 절을 사용하면 수신한 결과를 특정 순서(오름차순 또는 내림차순)의 지정된 열로 정렬할 수 있습니다. 이 작업은 `sort()` 함수를 사용하여 수행합니다.

`sort()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 세트에서 수신한 레코드 수를 제한할 수 있습니다.

`limit()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```python
df = dataset_reader.limit(100).read()
```

### OFFSET 절

OFFSET 절을 사용하면 처음부터 행을 건너뛰어 이후 이후 행으로부터 행 반환을 시작할 수 있습니다. LIMIT와 함께 사용하면 블록 내의 행을 반복할 수 있습니다.

`offset()` 함수를 사용하는 예는 아래에 볼 수 있습니다.

```python
df = dataset_reader.offset(100).read()
```

## 데이터 세트 쓰기

데이터 세트에 기록하려면 판다에게 데이터 프레임을 제공해야 합니다.

### 판다 데이터 프레임 쓰기

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## 사용자 공간 디렉토리(체크 포인트)

더 긴 실행 작업의 경우 중간 단계를 저장해야 할 수 있습니다. 이와 같은 경우에는 사용자 공간을 읽고 쓸 수 있습니다.

>[!NOTE]
>
>데이터에 대한 경로는 **저장되지 않습니다.** 해당 데이터에 해당하는 경로를 저장해야 합니다.

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

Adobe Experience Platform Data Science Workspace는 위 코드 샘플을 사용하여 데이터를 읽고 작성하는 레서피 샘플을 제공합니다. 데이터에 액세스하기 위해 Python을 사용하는 방법에 대한 자세한 내용은 [데이터 과학 작업 공간 Python GitHub 저장소](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)를 참조하십시오.
