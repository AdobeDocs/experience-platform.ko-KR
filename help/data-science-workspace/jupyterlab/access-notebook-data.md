---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 항목;%dataset;대화형 모드;배치 모드;Spark sdk;Python sdk;데이터 액세스;노트북 데이터 액세스
solution: Experience Platform
title: Jupyterlab Notebooks의 데이터 액세스
description: 이 안내서는 Data Science Workspace 내에 구축된 Jupyter Notebooks를 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '3320'
ht-degree: 3%

---

# [!DNL Jupyterlab]개 전자 필기장의 데이터 액세스

지원되는 각 커널은 노트북 내의 데이터 세트에서 플랫폼 데이터를 읽을 수 있는 내장 기능을 제공합니다. 현재 Adobe Experience Platform Data Science Workspace의 JupyterLab은 [!DNL Python], R, PySpark 및 Scala용 노트북을 지원합니다. 그러나 데이터 페이지 매김에 대한 지원은 [!DNL Python] 및 R 전자 필기장으로 제한됩니다. 이 안내서에서는 JupyterLab Notebooks를 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.

## 시작하기

이 안내서를 읽기 전에 [[!DNL JupyterLab] 사용 안내서](./overview.md)를 검토하여 [!DNL JupyterLab]에 대한 자세한 소개와 Data Science Workspace에서의 역할에 대해 알아보십시오.

## 노트북 데이터 제한 {#notebook-data-limits}

>[!IMPORTANT]
>
>PySpark 및 Scala Notebooks의 경우 &quot;원격 RPC 클라이언트 연결 해제&quot;라는 이유로 오류가 발생한 경우 이는 일반적으로 운전자나 실행자의 메모리가 부족함을 의미합니다. 이 오류를 해결하려면 [&quot;일괄 처리&quot; 모드](#mode)(으)로 전환해 보십시오.

다음 정보는 읽을 수 있는 최대 데이터 양, 사용된 데이터 유형 및 데이터를 읽는 데 걸리는 예상 기간을 정의합니다.

[!DNL Python] 및 R의 경우 40GB RAM으로 구성된 노트북 서버가 벤치마크에 사용되었습니다. PySpark와 Scala의 경우 64GB RAM, 8코어, 2DBU로 구성된 데이터 클러스터(최대 4명의 작업자가 있음)를 아래 설명된 벤치마크에 사용했습니다.

사용되는 ExperienceEvent 스키마 데이터는 1천(1K) 행부터 최대 10억(1B) 행 범위까지 크기가 다양했습니다. PySpark 및 [!DNL Spark] 지표의 경우 10일의 날짜 범위가 XDM 데이터에 사용되었습니다.

임시 스키마 데이터는 [!DNL Query Service] CTAS(Create Table as Select)를 사용하여 사전 처리되었습니다. 이 데이터 또한 최대 10억 행(1B)에 이르는 1,000행(1K)부터 시작하여 크기가 다양했다.

### 배치 모드와 대화형 모드를 사용해야 하는 경우 {#mode}

PySpark 및 Scala notebooks로 데이터 세트를 읽을 때 대화형 모드 또는 일괄 처리 모드를 사용하여 데이터 세트를 읽을 수 있습니다. 대화형 은 빠른 결과를 위해 만들어지지만 배치 모드는 큰 데이터 세트를 위한 것입니다.

- PySpark 및 Scala Notebooks의 경우 500만 개 이상의 데이터 행을 읽을 때 일괄 처리 모드를 사용해야 합니다. 각 모드의 효율성에 대한 자세한 내용은 아래의 [PySpark](#pyspark-data-limits) 또는 [Scala](#scala-data-limits) 데이터 제한 표를 참조하십시오.

### [!DNL Python] 전자 필기장 데이터 제한

**XDM ExperienceEvent 스키마:** 22분 이내에 최대 200만 행(디스크의 6.1GB 데이터)의 XDM 데이터를 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 디스크의 크기(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK(초) | 20.3 | 86.8 | 63 | 659 | 1315 |

**임시 스키마:** 14분 이내에 XDM(임시)이 아닌 데이터의 최대 500만 행(디스크의 5.6GB 데이터)을 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M | 5분 |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 디스크의 크기(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK(초) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R 노트북 데이터 제한

**XDM ExperienceEvent 스키마:** 13분 이내에 최대 100만 행의 XDM 데이터(디스크의 3GB 데이터)를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 |
| ----------------------- | ------ | ------ | ----- | ----- |
| 디스크의 크기(MB) | 18.73 | 187.5 | 308 | 3000 |
| R 커널(초) | 14.03 | 69.6 | 86.8 | 775 |

**임시 스키마:** 약 10분 내에 최대 3백만 행의 임시 데이터(디스크에 있는 293MB 데이터)를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 디스크의 크기(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK(초) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark([!DNL Python] 커널) 전자 필기장 데이터 제한: {#pyspark-data-limits}

**XDM ExperienceEvent 스키마:** 대화형 모드에서는 최대 500만 행(디스크의 13.42GB 데이터)의 XDM 데이터를 약 20분 내에 읽을 수 있어야 합니다. 대화형 모드는 최대 500만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 배치 모드로 전환하는 것이 좋습니다. 배치 모드에서는 약 14시간 내에 최대 5억 행(디스크의 경우 1.31TB 이하 데이터)의 XDM 데이터를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M | 5분 | 10분 | 50분 | 10억 | 5억 |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK(대화형 모드) | 33초 | 32.4초 | 55.1초 | 253.5초 | 489.2초 | 729.6초 | 1206.8초 | - | - | - | - |
| SDK(배치 모드) | 815.8초 | 492.8초 | 379.1초 | 637.4초 | 624.5초 | 869.2초 | 11,041초 | 년대 | 53,872초 | 10624.6초 | 50547초 |

**임시 스키마:** 대화형 모드에서는 XDM이 아닌 데이터의 최대 5백만 행(디스크의 5.36GB 데이터)을 3분 이내에 읽을 수 있어야 합니다. 일괄 처리 모드에서는 XDM이 아닌 데이터의 최대 10억 행(디스크의 경우 1.05TB 이하 데이터)을 약 18분 내에 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M | 5분 | 10분 | 50분 | 10억 | 5억 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48메가바이트 | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 28.2초 | 18.6초 | 20.8초 | 20.9초 | 23.8초 | 21.7초 | 24.7초 | - | - | - | - | - |
| SDK 배치 모드(초) | 428.8초 | 578.8초 | 641.4초 | 538.5초 | 630.9초 | 467.3초 | 년대 | 년대 | 년대 | 719.2초 | 10,221초 | 11,223초 |

### [!DNL Spark](Scala kernel) 전자 필기장 데이터 제한: {#scala-data-limits}

**XDM ExperienceEvent 스키마:** 대화형 모드에서는 약 18분 내에 최대 500만 행(디스크의 13.42GB 데이터)의 XDM 데이터를 읽을 수 있어야 합니다. 대화형 모드는 최대 500만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 배치 모드로 전환하는 것이 좋습니다. 배치 모드에서는 약 14시간 내에 최대 5억 행(디스크의 경우 1.31TB 이하 데이터)의 XDM 데이터를 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M | 5분 | 10분 | 50분 | 10억 | 5억 |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK 대화형 모드(초) | 37.9초 | 22.7초 | 45.6초 | 231.7초 | 444.7초 | 660.6초 | 년대 | - | - | - | - |
| SDK 배치 모드(초) | 374.4초 | 398.5초 | 년대 | 487.9초 | 588.9초 | 년대 | 939.1초 | 년대 | 54,732초 | 10118.8 | 49207.6 |

**임시 스키마:** 대화형 모드에서는 XDM이 아닌 데이터의 최대 5백만 행(디스크의 5.36GB 데이터)을 3분 이내에 읽을 수 있어야 합니다. 배치 모드에서는 약 16분 내에 XDM이 아닌 데이터의 최대 10억 행(디스크의 경우 1.05TB 이하 데이터)을 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 100만 | 200만 | 3M | 5분 | 10분 | 50분 | 10억 | 5억 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48메가바이트 | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 35.7초 | 31초 | 19.5초 | 25.3초 | 23s | 33.2초 | 25.5초 | - | - | - | - | - |
| SDK 배치 모드(초) | 448.8초 | 459.7초 | 년대 | 475.8초 | 599.9초 | 347.6초 | 407.8초 | 년대 | 518.8초 | 487.9초 | 760.2초 | 975.4초 |

## Python 노트북 {#python-notebook}

[!DNL Python]개의 전자 필기장을 사용하면 데이터 세트에 액세스할 때 데이터에 페이지를 매길 수 있습니다. 페이지 매김이 있거나 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 스타터 Python 노트북에 대한 자세한 내용은 JupyterLab 사용 안내서의 [[!DNL JupyterLab] 런처](./overview.md#launcher) 섹션을 참조하십시오.

아래 Python 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#python-read-dataset)
- [데이터 세트에 쓰기](#write-python)
- [데이터 쿼리](#query-data-python)
- [ExperienceEvent 데이터 필터링](#python-filter)

### Python의 데이터 세트에서 읽기 {#python-read-dataset}

**페이지 매김 없음:**

다음 코드를 실행하면 전체 데이터 세트가 읽힙니다. 실행이 성공하면 데이터는 `df` 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**페이지 매김 사용:**

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽힙니다. 페이지 매김은 각각 함수 `limit()` 및 `offset()`을(를) 통해 데이터를 제한하고 오프셋함으로써 수행됩니다. 데이터 제한은 읽을 데이터 포인트의 최대 수를 의미하며, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트의 수를 의미합니다. 읽기 작업이 성공적으로 실행되면 데이터가 `df` 변수에 의해 참조된 Pandas 데이터 프레임으로 저장됩니다.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Python의 데이터 세트에 쓰기 {#write-python}

JupyterLab 노트북의 데이터 세트에 작성하려면 JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 전자 필기장에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/write-dataset.png)

- **[!UICONTROL 전자 필기장에 데이터 쓰기]**&#x200B;를 사용하여 선택한 데이터 집합으로 쓰기 셀을 생성합니다.
- **[!UICONTROL Notebook에서 데이터 탐색]**&#x200B;을 사용하여 선택한 데이터 집합으로 읽기 셀을 생성합니다.
- **[!UICONTROL 전자 필기장의 데이터 쿼리]**&#x200B;를 사용하여 선택한 데이터 집합으로 기본 쿼리 셀을 생성합니다.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다. `{DATASET_ID}`과(와) `{PANDA_DATAFRAME}`을(를) 모두 바꿉니다.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### [!DNL Python]의 [!DNL Query Service]을(를) 사용하여 데이터 쿼리 {#query-data-python}

[!DNL Platform]의 [!DNL JupyterLab]에서 [!DNL Python] 전자 필기장의 SQL을 사용하여 [Adobe Experience Platform 쿼리 서비스](https://www.adobe.com/go/query-service-home-en)를 통해 데이터에 액세스할 수 있습니다. [!DNL Query Service]을(를) 통해 데이터에 액세스하면 실행 시간이 길어 대용량 데이터 세트를 처리하는 데 유용할 수 있습니다. [!DNL Query Service]을(를) 사용하여 데이터를 쿼리하는 데 10분의 처리 시간 제한이 있습니다.

[!DNL JupyterLab]에서 [!DNL Query Service]을(를) 사용하기 전에 [[!DNL Query Service] SQL 구문](https://www.adobe.com/go/query-service-sql-syntax-en)을(를) 이해하고 있는지 확인하십시오.

[!DNL Query Service]을(를) 사용하여 데이터를 쿼리하려면 대상 데이터 집합의 이름을 제공해야 합니다. **[!UICONTROL 데이터 탐색기]**&#x200B;를 사용하여 원하는 데이터 집합을 찾아 필요한 코드 셀을 생성할 수 있습니다. 데이터 집합 목록을 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 전자 필기장의 데이터 쿼리]**&#x200B;를 클릭하여 전자 필기장에 두 개의 코드 셀을 생성합니다. 이 두 세포는 아래에 더 자세히 설명되어 있습니다.

![](../images/jupyterlab/data-access/python-query-dataset.png)

[!DNL JupyterLab]에서 [!DNL Query Service]을(를) 활용하려면 먼저 작업 중인 [!DNL Python] 전자 필기장과 [!DNL Query Service] 간에 연결을 만들어야 합니다. 이는 처음 생성된 셀을 실행함으로써 달성될 수 있다.

```python
qs_connect()
```

두 번째로 생성된 셀에서는 SQL 쿼리 앞에 첫 번째 행을 정의해야 합니다. 기본적으로 생성된 셀은 쿼리 결과를 Pandas 데이터 프레임으로서 저장하는 선택적 변수(`df0`)를 정의합니다. <br>`-c QS_CONNECTION` 인수는 필수이며 커널에 [!DNL Query Service]에 대해 SQL 쿼리를 실행하도록 지시합니다. 추가 인수 목록은 [부록](#optional-sql-flags-for-query-service)을 참조하십시오.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

다음 예제와 같이 문자열 형식의 구문을 사용하고 중괄호(`{}`)로 변수를 줄바꿈하여 SQL 쿼리 내에서 Python 변수를 직접 참조할 수 있습니다.

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### [!DNL ExperienceEvent] 데이터 필터링 {#python-filter}

[!DNL Python] 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 데이터 집합 ID(`{DATASET_ID}`)를 제공해야 합니다. 시간 범위가 정의된 경우 지정된 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 보다 작음
- `le()`: 작거나 같음
- `And()`: 논리 AND 연산자
- `Or()`: 논리 OR 연산자

다음 셀은 2019년 1월 1일부터 2019년 12월 31일 말까지 독점적으로 존재하는 데이터에 [!DNL ExperienceEvent] 데이터 집합을 필터링합니다.

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

R Notebooks에서는 데이터 세트에 액세스할 때 데이터에 페이지를 지정할 수 있습니다. 페이지 매김이 있거나 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 스타터 R 노트북에 대한 자세한 내용은 JupyterLab 사용 안내서의 [[!DNL JupyterLab] 런처](./overview.md#launcher) 섹션을 참조하십시오.

아래 R 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#r-read-dataset)
- [데이터 세트에 쓰기](#write-r)
- [ExperienceEvent 데이터 필터링](#r-filter)

### R의 데이터 세트에서 읽기 {#r-read-dataset}

**페이지 매김 없음:**

다음 코드를 실행하면 전체 데이터 세트가 읽힙니다. 실행이 성공하면 데이터는 `df0` 변수에 의해 참조되는 Pandas 데이터 프레임으로 저장됩니다.

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

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽힙니다. 페이지 매김은 각각 함수 `limit()` 및 `offset()`을(를) 통해 데이터를 제한하고 오프셋함으로써 수행됩니다. 데이터 제한은 읽을 데이터 포인트의 최대 수를 의미하며, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트의 수를 의미합니다. 읽기 작업이 성공적으로 실행되면 데이터가 `df0` 변수에 의해 참조된 Pandas 데이터 프레임으로 저장됩니다.

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

JupyterLab 노트북의 데이터 세트에 작성하려면 JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 전자 필기장에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- **[!UICONTROL 전자 필기장에 데이터 쓰기]**&#x200B;를 사용하여 선택한 데이터 집합으로 쓰기 셀을 생성합니다.
- **[!UICONTROL Notebook에서 데이터 탐색]**&#x200B;을 사용하여 선택한 데이터 집합으로 읽기 셀을 생성합니다.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다.

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### [!DNL ExperienceEvent] 데이터 필터링 {#r-filter}

R 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 데이터 집합 ID(`{DATASET_ID}`)를 제공해야 합니다. 시간 범위가 정의된 경우 지정된 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 보다 작음
- `le()`: 작거나 같음
- `And()`: 논리 AND 연산자
- `Or()`: 논리 OR 연산자

다음 셀은 2019년 1월 1일부터 2019년 12월 31일 말까지 독점적으로 존재하는 데이터에 [!DNL ExperienceEvent] 데이터 집합을 필터링합니다.

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

모든 [!DNL Spark] 2.4 전자 필기장에는 다음 표준 코드로 세션을 초기화해야 합니다.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### %dataset을 사용하여 PySpark 3 전자 필기장으로 읽고 쓰는 중 {#magic}

[!DNL Spark] 2.4의 도입으로 PySpark 3([!DNL Spark] 2.4) 전자 필기장에서 사용할 수 있도록 `%dataset` 사용자 지정 매직이 제공됩니다. IPython 커널에서 사용할 수 있는 매직 명령에 대한 자세한 내용은 [IPython 매직 설명서](https://ipython.readthedocs.io/en/stable/interactive/magics.html)를 참조하세요.


**사용**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**설명**

[!DNL PySpark] 전자 필기장([!DNL Python] 3 커널)에서 데이터 집합을 읽거나 쓰는 사용자 지정 [!DNL Data Science Workspace] 매직 명령입니다.

| 이름 | 설명 | 필수 여부 |
| --- | --- | --- |
| `{action}` | 데이터 세트에 대해 수행할 작업 유형입니다. 두 가지 작업을 &quot;읽기&quot; 또는 &quot;쓰기&quot;로 사용할 수 있습니다. | 예 |
| `--datasetId {id}` | 읽거나 쓸 데이터 세트의 ID를 제공하는 데 사용됩니다. | 예 |
| `--dataFrame {df}` | 팬더 데이터 프레임입니다. <ul><li> 작업이 &quot;읽기&quot;이면 {df}은(는) 데이터 집합 읽기 작업의 결과를 사용할 수 있는 변수입니다(예: 데이터 프레임). </li><li> 작업이 &quot;쓰기&quot;이면 이 데이터 프레임 {df}이(가) 데이터 집합에 기록됩니다. </li></ul> | 예 |
| `--mode` | 데이터 읽기 방식을 변경하는 추가 매개 변수입니다. 허용된 매개 변수는 &quot;batch&quot; 및 &quot;interactive&quot;입니다. 기본적으로 모드는 &quot;batch&quot;로 설정됩니다.<br> 작은 데이터 세트에서 쿼리 성능을 높이려면 &quot;대화형&quot; 모드를 사용하는 것이 좋습니다. | 예 |

>[!TIP]
>
>[전자 필기장 데이터 제한](#notebook-data-limits) 섹션의 PySpark 테이블을 검토하여 `mode`을(를) `interactive` 또는 `batch`(으)로 설정해야 하는지 확인하십시오.

**예**

- **예제 읽기**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **예제 작성**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을(를) 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

다음 방법을 사용하여 JupyterLab 구매에서 위의 예를 자동으로 생성할 수 있습니다.

JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 전자 필기장에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.

- **[!UICONTROL Notebook에서 데이터 탐색]**&#x200B;을 사용하여 읽기 셀을 생성합니다.
- **[!UICONTROL 전자 필기장에 데이터 쓰기]**&#x200B;를 사용하여 쓰기 셀을 생성합니다.

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

### [!DNL ExperienceEvent] 데이터 필터링 {#pyspark-filter-experienceevent}

PySpark 전자 필기장의 [!DNL ExperienceEvent] 데이터 세트에 액세스하고 필터링하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙을 제공해야 합니다. `spark.sql()` 함수를 사용하여 필터링 시간 범위를 정의합니다. 여기서 함수 매개 변수는 SQL 쿼리 문자열입니다.

다음 셀은 2019년 1월 1일부터 2019년 12월 31일 말까지 독점적으로 존재하는 데이터로 [!DNL ExperienceEvent] 데이터 집합을 필터링합니다.

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

Scala에서 `clientContext`을(를) 가져와서 플랫폼 값을 가져오고 반환할 수 있으므로 `var userToken`과(와) 같은 변수를 정의할 필요가 없습니다. 아래 Scala 예제에서 `clientContext`은(는) 데이터 집합을 읽는 데 필요한 모든 필수 값을 가져오고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을(를) 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

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
| 사용자 토큰 | `clientContext.getUserToken()`을(를) 사용하여 자동으로 가져오는 사용자 토큰입니다. |
| 서비스 토큰 | `clientContext.getServiceToken()`을(를) 사용하여 자동으로 가져오는 서비스 토큰입니다. |
| ims-org | `clientContext.getOrgId()`을(를) 사용하여 자동으로 가져오는 조직 ID입니다. |
| api 키 | `clientContext.getApiKey()`을(를) 사용하여 자동으로 가져오는 API 키입니다. |

>[!TIP]
>
>[전자 필기장 데이터 제한](#notebook-data-limits) 섹션의 Scala 테이블을 검토하여 `mode`을(를) `interactive` 또는 `batch`(으)로 설정해야 하는지 확인하십시오.

다음 방법을 사용하여 JupyterLab 구매에서 위의 예를 자동으로 생성할 수 있습니다.

JupyterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL Notebook에서 데이터 탐색]** 옵션을 선택합니다. 전자 필기장 하단에 실행 가능한 코드 항목이 나타납니다.
및
- **[!UICONTROL Notebook에서 데이터 탐색]**&#x200B;을 사용하여 읽기 셀을 생성합니다.
- **[!UICONTROL 전자 필기장에 데이터 쓰기]**&#x200B;를 사용하여 쓰기 셀을 생성합니다.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 데이터 세트에 쓰기 {#scala-write-dataset}

Scala에서 `clientContext`을(를) 가져와서 플랫폼 값을 가져오고 반환할 수 있으므로 `var userToken`과(와) 같은 변수를 정의할 필요가 없습니다. 아래 Scala 예제에서 `clientContext`은(는) 데이터 집합에 쓰는 데 필요한 모든 필수 값을 정의하고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을(를) 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류가 발생하는 경우 도움이 될 수 있습니다.
> 
> - 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.
> 
> 자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

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

| 요소 | 설명 |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 Pandas 데이터 프레임을 나타내는 변수입니다. |
| 사용자 토큰 | `clientContext.getUserToken()`을(를) 사용하여 자동으로 가져오는 사용자 토큰입니다. |
| 서비스 토큰 | `clientContext.getServiceToken()`을(를) 사용하여 자동으로 가져오는 서비스 토큰입니다. |
| ims-org | `clientContext.getOrgId()`을(를) 사용하여 자동으로 가져오는 조직 ID입니다. |
| api 키 | `clientContext.getApiKey()`을(를) 사용하여 자동으로 가져오는 API 키입니다. |

>[!TIP]
>
>[전자 필기장 데이터 제한](#notebook-data-limits) 섹션의 Scala 테이블을 검토하여 `mode`을(를) `interactive` 또는 `batch`(으)로 설정해야 하는지 확인하십시오.

### 로컬 데이터 프레임 만들기 {#scala-create-dataframe}

Scala를 사용하여 로컬 데이터 프레임을 만들려면 SQL 쿼리가 필요합니다. 예:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### [!DNL ExperienceEvent] 데이터 필터링 {#scala-experienceevent}

Scala 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 데이터 집합 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙을 제공해야 합니다. `spark.sql()` 함수를 사용하여 필터링 시간 범위를 정의합니다. 여기서 함수 매개 변수는 SQL 쿼리 문자열입니다.

다음 셀은 2019년 1월 1일부터 2019년 12월 31일 말까지 독점적으로 존재하는 데이터로 [!DNL ExperienceEvent] 데이터 집합을 필터링합니다.

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

이 문서에서는 JupyterLab 노트북을 사용한 데이터 세트에 액세스하기 위한 일반적인 지침을 다룹니다. 데이터 세트 쿼리에 대한 자세한 예제는 [JupyterLab 전자 필기장의 쿼리 서비스](./query-service.md) 설명서를 참조하십시오. 데이터 세트를 탐색하고 시각화하는 방법에 대한 자세한 내용은 [전자 필기장을 사용하여 데이터 분석](./analyze-your-data.md)의 문서를 참조하십시오.

## [!DNL Query Service]에 대한 선택적 SQL 플래그 {#optional-sql-flags-for-query-service}

이 표에서는 [!DNL Query Service]에 사용할 수 있는 선택적 SQL 플래그를 간략하게 설명합니다.

| **플래그** | **설명** |
| --- | --- |
| `-h`, `--help` | 도움말 메시지를 표시하고 종료합니다. |
| `-n`, `--notify` | 쿼리 결과를 알리는 토글 옵션입니다. |
| `-a`, `--async` | 이 플래그를 사용하면 쿼리가 비동기적으로 실행되며 쿼리가 실행되는 동안 커널을 확보할 수 있습니다. 쿼리가 완료되지 않은 경우 정의되지 않을 수 있으므로 쿼리 결과를 변수에 할당할 때 주의하십시오. |
| `-d`, `--display` | 이 플래그를 사용하면 결과가 표시되지 않습니다. |
