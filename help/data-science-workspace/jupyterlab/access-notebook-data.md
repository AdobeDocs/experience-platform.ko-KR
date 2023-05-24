---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 항목;%dataset;대화형 모드;배치 모드;Spark sdk;Python sdk;데이터 액세스;노트북 데이터 액세스
solution: Experience Platform
title: Jupyterlab Notebooks의 데이터 액세스
description: 이 안내서는 Data Science Workspace 내에 구축된 Jupyter Notebooks를 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 8%

---

# 의 데이터 액세스 [!DNL Jupyterlab] notebooks

지원되는 각 커널은 노트북 내의 데이터 세트에서 플랫폼 데이터를 읽을 수 있는 내장 기능을 제공합니다. 현재 Adobe Experience Platform Data Science Workspace의 JupyterLab은 [!DNL Python], R, PySpark 및 Scala. 그러나 데이터 페이지 지정에 대한 지원은 다음으로 제한됩니다. [!DNL Python] 및 R notebooks. 이 안내서에서는 JupyterLab Notebooks를 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.

## 시작하기

이 안내서를 읽기 전에 다음을 검토하십시오. [[!DNL JupyterLab] 사용 안내서](./overview.md) 를 개괄적으로 소개하는 [!DNL JupyterLab] 및 Data Science Workspace에서의 역할.

## 노트북 데이터 제한 {#notebook-data-limits}

>[!IMPORTANT]
>
>PySpark 및 Scala Notebooks의 경우 &quot;원격 RPC 클라이언트 연결 해제&quot;라는 이유로 오류가 발생한 경우 이는 일반적으로 운전자나 실행자의 메모리가 부족함을 의미합니다. 다음으로 전환 시도: [&quot;batch&quot; 모드](#mode) 이 오류를 해결했습니다.

다음 정보는 읽을 수 있는 최대 데이터 양, 사용된 데이터 유형 및 데이터를 읽는 데 걸리는 예상 기간을 정의합니다.

대상 [!DNL Python] 그리고 R은 40GB RAM으로 구성된 노트북 서버를 벤치마크로 사용하였다. PySpark와 Scala의 경우 64GB RAM, 8코어, 2DBU로 구성된 데이터 클러스터(최대 4명의 작업자가 있음)를 아래 설명된 벤치마크에 사용했습니다.

사용되는 ExperienceEvent 스키마 데이터는 1천(1K) 행부터 최대 10억(1B) 행 범위까지 크기가 다양했습니다. PySpark의 경우 및 [!DNL Spark] 지표, 10일의 날짜 범위가 XDM 데이터에 사용되었습니다.

임시 스키마 데이터는 다음을 사용하여 사전 처리되었습니다. [!DNL Query Service] 선택(CTAS)으로 표 만들기. 이 데이터 또한 최대 10억 행(1B)에 이르는 1,000행(1K)부터 시작하여 크기가 다양했다.

### 배치 모드와 대화형 모드를 사용해야 하는 경우 {#mode}

PySpark 및 Scala notebooks로 데이터 세트를 읽을 때 대화형 모드 또는 일괄 처리 모드를 사용하여 데이터 세트를 읽을 수 있습니다. 대화형 은 빠른 결과를 위해 만들어지지만 배치 모드는 큰 데이터 세트를 위한 것입니다.

- PySpark 및 Scala Notebooks의 경우 500만 개 이상의 데이터 행을 읽을 때 일괄 처리 모드를 사용해야 합니다. 각 모드의 효율에 대한 자세한 내용은 [PySparc](#pyspark-data-limits) 또는 [스칼라](#scala-data-limits) 아래의 데이터 제한 테이블.

### [!DNL Python] 노트북 데이터 제한

**XDM ExperienceEvent 스키마:** XDM 데이터의 최대 200만 행( 디스크의 6.1GB 데이터 ~)을 22분 이내에 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 디스크의 크기(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK(초) | 20.3 | 86.8 | 63 | 659 | 1315 |

**임시 스키마:** 14분 이내에 XDM이 아닌(Ad-Hoc) 데이터의 최대 500만 행( 디스크의 5.6GB 데이터)을 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 디스크의 크기(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK(초) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R 노트북 데이터 제한

**XDM ExperienceEvent 스키마:** 13분 이내에 최대 100만 행의 XDM 데이터(디스크의 3GB 데이터)를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 디스크의 크기(MB) | 18.73 | 187.5 | 308 | 3000 |
| R 커널(초) | 14.03 | 69.6 | 86.8 | 775 |

**임시 스키마:** 약 10분 내에 최대 3백만 행의 임시 데이터(디스크의 293MB 데이터)를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 디스크의 크기(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK(초) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark ([!DNL Python] 커널) 노트북 데이터 제한: {#pyspark-data-limits}

**XDM ExperienceEvent 스키마:** 대화형 모드에서는 약 20분 내에 XDM 데이터의 최대 500만 행( 디스크의 13.42GB 데이터)을 읽을 수 있어야 합니다. 대화형 모드는 최대 500만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 배치 모드로 전환하는 것이 좋습니다. 배치 모드에서는 약 14시간 내에 최대 5억 행(디스크의 경우 1.31TB 이하 데이터)의 XDM 데이터를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK(대화형 모드) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK(배치 모드) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**임시 스키마:** 대화형 모드에서는 XDM이 아닌 데이터의 최대 500만 행(디스크의 5.36GB 데이터)을 3분 이내에 읽을 수 있어야 합니다. 일괄 처리 모드에서는 XDM이 아닌 데이터의 최대 10억 행(디스크의 경우 1.05TB 이하 데이터)을 약 18분 내에 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK 배치 모드(초) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] (Scala kernel) 노트북 데이터 제한 사항: {#scala-data-limits}

**XDM ExperienceEvent 스키마:** 대화형 모드에서는 약 18분 내에 XDM 데이터의 최대 500만 행( 디스크의 13.42GB 데이터)을 읽을 수 있어야 합니다. 대화형 모드는 최대 500만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 배치 모드로 전환하는 것이 좋습니다. 배치 모드에서는 약 14시간 내에 최대 5억 행(디스크의 경우 1.31TB 이하 데이터)의 XDM 데이터를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK 대화형 모드(초) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK 배치 모드(초) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**임시 스키마:** 대화형 모드에서는 XDM이 아닌 데이터의 최대 500만 행(디스크의 5.36GB 데이터)을 3분 이내에 읽을 수 있어야 합니다. 배치 모드에서는 약 16분 내에 XDM이 아닌 데이터의 최대 10억 행(디스크의 경우 1.05TB 이하 데이터)을 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK 배치 모드(초) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python 노트북 {#python-notebook}

[!DNL Python] notebooks에서는 데이터 세트에 액세스할 때 데이터에 페이지를 매길 수 있습니다. 페이지 매김이 있거나 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 스타터 Python 노트북에 대한 자세한 내용은 [[!DNL JupyterLab] 런처](./overview.md#launcher) 섹션에 자세히 설명되어 있습니다.

아래 Python 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#python-read-dataset)
- [데이터 세트에 쓰기](#write-python)
- [데이터 쿼리](#query-data-python)
- [ExperienceEvent 데이터 필터링](#python-filter)

### Python의 데이터 세트에서 읽기 {#python-read-dataset}

**페이지 매김 없음:**

다음 코드를 실행하면 전체 데이터 세트가 읽힙니다. 실행이 성공하면 데이터가 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다. `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**페이지 매김 사용:**

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽힙니다. 페이지 매김은 함수를 통해 데이터를 제한하고 오프셋함으로써 수행됩니다 `limit()` 및 `offset()` 각각. 데이터 제한은 읽을 데이터 포인트의 최대 수를 의미하며, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트의 수를 의미합니다. 읽기 작업이 성공적으로 실행되면 데이터가 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다. `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Python의 데이터 세트에 쓰기 {#write-python}

JupyterLab 노트북의 데이터 세트에 작성하려면 JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. 다음 **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉토리가 나타납니다. 선택 **[!UICONTROL 데이터 세트]** 을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Notebook에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/write-dataset.png)

- 사용 **[!UICONTROL Notebook에 데이터 쓰기]** 선택한 데이터 세트로 쓰기 셀을 생성합니다.
- 사용 **[!UICONTROL Notebook의 데이터 탐색]** 선택한 데이터 세트로 읽기 셀을 생성합니다.
- 사용 **[!UICONTROL Notebook의 데이터 쿼리]** 선택한 데이터 세트로 기본 쿼리 셀을 생성합니다.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다. 다음 두 가지를 모두 바꾸기 `{DATASET_ID}` 및 `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 다음을 사용하여 데이터 쿼리 [!DNL Query Service] 위치: [!DNL Python] {#query-data-python}

[!DNL JupyterLab] 날짜 [!DNL Platform] 에서 SQL을 사용할 수 있습니다. [!DNL Python] 다음을 통해 데이터에 액세스하는 전자 필기장 [Adobe Experience Platform 쿼리 서비스](https://www.adobe.com/go/query-service-home-en). 를 통해 데이터 액세스 [!DNL Query Service] 은 우수한 실행 시간으로 인해 큰 데이터 세트를 처리하는 데 유용할 수 있습니다. 다음을 사용하여 데이터 쿼리 [!DNL Query Service] 에는 10분의 처리 시간 제한이 있습니다.

사용하기 전에 [!DNL Query Service] 위치: [!DNL JupyterLab], 다음에 대해 잘 이해하고 있는지 확인합니다. [[!DNL Query Service] SQL 구문](https://www.adobe.com/go/query-service-sql-syntax-en).

다음을 사용하여 데이터 쿼리 [!DNL Query Service] 을(를) 사용하려면 타겟 데이터 세트의 이름을 입력해야 합니다. 다음을 사용하여 원하는 데이터 세트를 찾아 필요한 코드 셀을 생성할 수 있습니다. **[!UICONTROL 데이터 탐색기]**. 데이터 세트 목록을 마우스 오른쪽 버튼으로 클릭하고 **[!UICONTROL Notebook의 데이터 쿼리]** 수첩에서 두 개의 코드 셀을 생성합니다. 이 두 세포는 아래에 더 자세히 설명되어 있습니다.

![](../images/jupyterlab/data-access/python-query-dataset.png)

를 활용하기 위해 [!DNL Query Service] 위치: [!DNL JupyterLab], 먼저 작업 간에 연결을 만들어야 합니다 [!DNL Python] 노트북 및 [!DNL Query Service]. 이는 처음 생성된 셀을 실행함으로써 달성될 수 있다.

```python
qs_connect()
```

두 번째로 생성된 셀에서는 SQL 쿼리 앞에 첫 번째 행을 정의해야 합니다. 기본적으로 생성된 셀은 선택 변수( )를 정의합니다`df0`)를 사용하여 쿼리 결과를 Pandas 데이터 프레임으로서 저장합니다. <br>다음 `-c QS_CONNECTION` 인수는 필수이며 커널에 SQL 쿼리를 실행하도록 지시합니다. [!DNL Query Service]. 다음을 참조하십시오. [부록](#optional-sql-flags-for-query-service) 추가 인수 목록.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python 변수는 문자열 형식의 구문을 사용하고 중괄호( )로 변수를 묶어 SQL 쿼리 내에서 직접 참조할 수 있습니다.`{}`)를 클릭하여 제품에서 사용할 수 있습니다.

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 필터 [!DNL ExperienceEvent] 데이터 {#python-filter}

에 액세스하고 필터링하려면 [!DNL ExperienceEvent] 의 데이터 세트 [!DNL Python] notebook에서 데이터 세트( )의 ID를 제공해야 합니다.`{DATASET_ID}`논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 제공됩니다. 시간 범위가 정의된 경우 지정된 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 미만
- `le()`: 작거나 같음
- `And()`: 논리 AND 연산자
- `Or()`: 논리 OR 연산자

다음 셀은 [!DNL ExperienceEvent] 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터에 대한 데이터 세트입니다.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R 노트북 {#r-notebooks}

R Notebooks에서는 데이터 세트에 액세스할 때 데이터에 페이지를 지정할 수 있습니다. 페이지 매김이 있거나 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 스타터 R 노트북에 대한 자세한 내용은 [[!DNL JupyterLab] 런처](./overview.md#launcher) 섹션에 자세히 설명되어 있습니다.

아래 R 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#r-read-dataset)
- [데이터 세트에 쓰기](#write-r)
- [ExperienceEvent 데이터 필터링](#r-filter)

### R의 데이터 세트에서 읽기 {#r-read-dataset}

**페이지 매김 없음:**

다음 코드를 실행하면 전체 데이터 세트가 읽힙니다. 실행이 성공하면 데이터가 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다. `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**페이지 매김 사용:**

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽힙니다. 페이지 매김은 함수를 통해 데이터를 제한하고 오프셋함으로써 수행됩니다 `limit()` 및 `offset()` 각각. 데이터 제한은 읽을 데이터 포인트의 최대 수를 의미하며, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트의 수를 의미합니다. 읽기 작업이 성공적으로 실행되면 데이터가 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다. `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### R의 데이터 세트에 쓰기 {#write-r}

JupyterLab 노트북의 데이터 세트에 작성하려면 JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. 다음 **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉토리가 나타납니다. 선택 **[!UICONTROL 데이터 세트]** 을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Notebook에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 사용 **[!UICONTROL Notebook에 데이터 쓰기]** 선택한 데이터 세트로 쓰기 셀을 생성합니다.
- 사용 **[!UICONTROL Notebook의 데이터 탐색]** 선택한 데이터 세트로 읽기 셀을 생성합니다.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다.

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 필터 [!DNL ExperienceEvent] 데이터 {#r-filter}

에 액세스하고 필터링하려면 [!DNL ExperienceEvent] R notebook의 데이터 세트에서는 데이터 세트의 ID( )를 제공해야 합니다.`{DATASET_ID}`논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 제공됩니다. 시간 범위가 정의된 경우 지정된 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 미만
- `le()`: 작거나 같음
- `And()`: 논리 AND 연산자
- `Or()`: 논리 OR 연산자

다음 셀은 [!DNL ExperienceEvent] 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터에 대한 데이터 세트입니다.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3 노트북 {#pyspark-notebook}

아래 PySpark 설명서는 다음 개념을 간략하게 설명합니다.

- [SparkSession 초기화](#spark-initialize)
- [데이터 읽기 및 쓰기](#magic)
- [로컬 데이터 프레임 만들기](#pyspark-create-dataframe)
- [ExperienceEvent 데이터 필터링](#pyspark-filter-experienceevent)

### sparkSession 초기화 중 {#spark-initialize}

모두 [!DNL Spark] 2.4 notebooks에서는 다음 상용구 코드로 세션을 초기화해야 합니다.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### %dataset을 사용하여 PySpark 3 전자 필기장으로 읽고 쓰는 중 {#magic}

의 도입으로 [!DNL Spark] 2.4, `%dataset` 사용자 지정 마법은 PySpark 3에서 사용할 수 있습니다([!DNL Spark] 2.4) 노트북. IPython 커널에서 사용할 수 있는 매직 명령에 대한 자세한 내용은 [IPython 매직 설명서](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**사용**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**설명**

사용자 지정 [!DNL Data Science Workspace] 에서 데이터 세트를 읽거나 쓰기 위한 magic 명령 [!DNL PySpark] 전자 필기장([!DNL Python] 3 커널).

| 이름 | 설명 | 필수 여부 |
| --- | --- | --- |
| `{action}` | 데이터 세트에 대해 수행할 작업 유형입니다. 두 가지 작업을 &quot;읽기&quot; 또는 &quot;쓰기&quot;로 사용할 수 있습니다. | 예 |
| `--datasetId {id}` | 읽거나 쓸 데이터 세트의 ID를 제공하는 데 사용됩니다. | 예 |
| `--dataFrame {df}` | 팬더 데이터 프레임입니다. <ul><li> 작업이 &quot;read&quot;이면 {df}은(는) 데이터 세트 읽기 작업의 결과를 사용할 수 있는 변수입니다(예: 데이터 프레임). </li><li> 작업이 &quot;write&quot;이면 이 데이터 프레임 {df}이(가) 데이터 세트에 기록됩니다. </li></ul> | 예 |
| `--mode` | 데이터 읽기 방식을 변경하는 추가 매개 변수입니다. 허용된 매개 변수는 &quot;batch&quot; 및 &quot;interactive&quot;입니다. 기본적으로 모드는 &quot;batch&quot;로 설정됩니다.<br> 작은 데이터 세트에서 쿼리 성능을 높이려면 &quot;대화형&quot; 모드를 사용하는 것이 좋습니다. | 예 |

>[!TIP]
>
>내의 PySpark 테이블을 검토합니다. [노트북 데이터 제한](#notebook-data-limits) 섹션 을 사용하여 다음을 수행할 수 있는지 확인 `mode` 을 로 설정해야 합니다. `interactive` 또는 `batch`.

**예**

- **예제 읽기**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **쓰기 예**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 를 사용하여 데이터 캐싱 `df.cache()` 데이터를 쓰기 전에 노트북 성능을 크게 향상시킬 수 있습니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 다음을 참조하십시오. [문제 해결 안내서](../troubleshooting-guide.md) 추가 정보.

다음 방법을 사용하여 JupyterLab 구매에서 위의 예를 자동으로 생성할 수 있습니다.

JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. 다음 **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉토리가 나타납니다. 선택 **[!UICONTROL 데이터 세트]** 을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Notebook에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

- 사용 **[!UICONTROL Notebook의 데이터 탐색]** 읽기 셀을 생성합니다.
- 사용 **[!UICONTROL Notebook에 데이터 쓰기]** 쓰기 셀을 생성합니다.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 로컬 데이터 프레임 만들기 {#pyspark-create-dataframe}

PySpark 3을 사용하여 로컬 데이터 프레임을 만들려면 SQL 쿼리를 사용합니다. 예:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>Replacement, double fraction 또는 long seed와 같은 선택적 시드 샘플을 지정할 수도 있습니다.

### 필터 [!DNL ExperienceEvent] 데이터 {#pyspark-filter-experienceevent}

액세스 및 필터링 [!DNL ExperienceEvent] PySpark 노트북의 데이터 세트를 사용하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙. 필터링 시간 범위는 함수를 사용하여 정의됩니다 `spark.sql()`함수 매개 변수가 SQL 쿼리 문자열인 경우

다음 셀은 [!DNL ExperienceEvent] 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터에 대한 데이터 세트입니다.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## 노트북 크기 조절 {#scala-notebook}

아래 설명서에는 다음 개념에 대한 예제가 포함되어 있습니다.

- [SparkSession 초기화](#scala-initialize)
- [데이터 세트 읽기](#read-scala-dataset)
- [데이터 세트에 쓰기](#scala-write-dataset)
- [로컬 데이터 프레임 만들기](#scala-create-dataframe)
- [ExperienceEvent 데이터 필터링](#scala-experienceevent)

### SparkSession 초기화 중 {#scala-initialize}

모든 Scala Notebooks에서는 다음 상용구 코드로 세션을 초기화해야 합니다.

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 데이터 세트 읽기 {#read-scala-dataset}

Scala에서 다음을 가져올 수 있습니다. `clientContext` 플랫폼 값을 가져오고 반환하려면 와 같은 변수를 정의하지 않아도 됩니다. `var userToken`. 아래 Scala 예제에서 `clientContext` 는 데이터 세트를 읽는 데 필요한 모든 필수 값을 가져오고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 를 사용하여 데이터 캐싱 `df.cache()` 데이터를 쓰기 전에 노트북 성능을 크게 향상시킬 수 있습니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 다음을 참조하십시오. [문제 해결 안내서](../troubleshooting-guide.md) 추가 정보.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 요소 | 설명 |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 Pandas 데이터 프레임을 나타내는 변수입니다. |
| 사용자 토큰 | 을 사용하여 자동으로 가져오는 사용자 토큰 `clientContext.getUserToken()`. |
| 서비스 토큰 | 을 사용하여 자동으로 가져오는 서비스 토큰 `clientContext.getServiceToken()`. |
| ims-org | 을 사용하여 자동으로 가져오는 조직 ID `clientContext.getOrgId()`. |
| api 키 | 를 사용하여 자동으로 가져오는 API 키 `clientContext.getApiKey()`. |

>[!TIP]
>
>내의 Scala 테이블을 검토합니다. [노트북 데이터 제한](#notebook-data-limits) 섹션 을 사용하여 다음을 수행할 수 있는지 확인 `mode` 을 로 설정해야 합니다. `interactive` 또는 `batch`.

다음 방법을 사용하여 JupyterLab 구매에서 위의 예를 자동으로 생성할 수 있습니다.

JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. 다음 **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉토리가 나타납니다. 선택 **[!UICONTROL 데이터 세트]** 을(를) 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Notebook의 데이터 탐색]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.
및
- 사용 **[!UICONTROL Notebook의 데이터 탐색]** 읽기 셀을 생성합니다.
- 사용 **[!UICONTROL Notebook에 데이터 쓰기]** 쓰기 셀을 생성합니다.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 데이터 세트에 쓰기 {#scala-write-dataset}

Scala에서 다음을 가져올 수 있습니다. `clientContext` 플랫폼 값을 가져오고 반환하려면 와 같은 변수를 정의하지 않아도 됩니다. `var userToken`. 아래 Scala 예제에서 `clientContext` 는 데이터 집합에 쓰는 데 필요한 모든 필수 값을 정의하고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 를 사용하여 데이터 캐싱 `df.cache()` 데이터를 쓰기 전에 노트북 성능을 크게 향상시킬 수 있습니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 다음을 참조하십시오. [문제 해결 안내서](../troubleshooting-guide.md) 추가 정보.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | 설명 |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 Pandas 데이터 프레임을 나타내는 변수입니다. |
| 사용자 토큰 | 을 사용하여 자동으로 가져오는 사용자 토큰 `clientContext.getUserToken()`. |
| 서비스 토큰 | 을 사용하여 자동으로 가져오는 서비스 토큰 `clientContext.getServiceToken()`. |
| ims-org | 을 사용하여 자동으로 가져오는 조직 ID `clientContext.getOrgId()`. |
| api 키 | 를 사용하여 자동으로 가져오는 API 키 `clientContext.getApiKey()`. |

>[!TIP]
>
>내의 Scala 테이블을 검토합니다. [노트북 데이터 제한](#notebook-data-limits) 섹션 을 사용하여 다음을 수행할 수 있는지 확인 `mode` 을 로 설정해야 합니다. `interactive` 또는 `batch`.

### 로컬 데이터 프레임 만들기 {#scala-create-dataframe}

Scala를 사용하여 로컬 데이터 프레임을 만들려면 SQL 쿼리가 필요합니다. 예:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 필터 [!DNL ExperienceEvent] 데이터 {#scala-experienceevent}

액세스 및 필터링 [!DNL ExperienceEvent] Scala 노트북의 데이터 세트를 사용하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙. 필터링 시간 범위는 함수를 사용하여 정의됩니다 `spark.sql()`함수 매개 변수가 SQL 쿼리 문자열인 경우

다음 셀은 [!DNL ExperienceEvent] 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터에 대한 데이터 세트입니다.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## 다음 단계

이 문서에서는 JupyterLab 노트북을 사용한 데이터 세트에 액세스하기 위한 일반적인 지침을 다룹니다. 데이터 세트 쿼리에 대한 자세한 예를 보려면 다음을 방문하십시오. [JupyterLab 노트북의 쿼리 서비스](./query-service.md) 설명서를 참조하십시오. 데이터 세트를 탐색하고 시각화하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [notebooks를 사용하여 데이터 분석](./analyze-your-data.md).

## 선택적 SQL 플래그 [!DNL Query Service] {#optional-sql-flags-for-query-service}

이 테이블에서는에 사용할 수 있는 선택적 SQL 플래그를설명합니다. [!DNL Query Service].

| **플래그** | **설명** |
| --- | --- |
| `-h`, `--help` | 도움말 메시지를 표시하고 종료합니다. |
| `-n`, `--notify` | 쿼리 결과를 알리는 토글 옵션입니다. |
| `-a`, `--async` | 이 플래그를 사용하면 쿼리가 비동기적으로 실행되며 쿼리가 실행되는 동안 커널을 확보할 수 있습니다. 쿼리가 완료되지 않은 경우 정의되지 않을 수 있으므로 쿼리 결과를 변수에 할당할 때 주의하십시오. |
| `-d`, `--display` | 이 플래그를 사용하면 결과가 표시되지 않습니다. |
