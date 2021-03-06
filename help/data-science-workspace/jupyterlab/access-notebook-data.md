---
keywords: Experience Platform;JupiterLab;노트북;Data Science Workspace;인기 항목;%dataset;대화형 모드;일괄 처리 모드;Spark sdk;python sdk;액세스 데이터;노트북 데이터 액세스
solution: Experience Platform
title: Jupiterlab Notebook의 데이터 액세스
topic-legacy: Developer Guide
description: 이 안내서에서는 Data Science Workspace 내에 구축된 Jupiter Notebook을 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 9e41db60580146fa90542ed00ceedd4eecb88b47
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 8%

---

# [!DNL Jupyterlab] 전자 필기장의 데이터 액세스

지원되는 각 커널에서는 노트북 내의 데이터 세트에서 플랫폼 데이터를 읽을 수 있는 내장 기능을 제공합니다. 현재 Adobe Experience Platform 데이터 과학 작업 공간의 JupiterLab은 [!DNL Python], R, PySpark 및 Scala용 노트북을 지원합니다. 그러나 데이터 페이지 매김 지원은 [!DNL Python] 및 R 노트북으로 제한됩니다. 이 안내서에서는 JupiterLab 노트북을 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.

## 시작

이 안내서를 읽기 전에 [!DNL JupyterLab] 및 Data Science Workspace 내의 해당 역할에 대한 개요 정보는 [[!DNL JupyterLab] 사용 안내서](./overview.md)를 참조하십시오.

## 전자 필기장 데이터 제한 {#notebook-data-limits}

>[!IMPORTANT]
>
>PySpark 및 Scala 노트북의 경우 &quot;Remote RPC 클라이언트가 연결되지 않음&quot;이라는 이유로 오류가 표시됩니다. 일반적으로 드라이버나 실행자의 메모리가 부족함을 의미합니다. 이 오류를 해결하려면 [&quot;batch&quot; mode](#mode)로 전환하십시오.

다음 정보는 읽을 수 있는 최대 데이터 양, 사용된 데이터 유형 및 데이터를 읽는 예상 기간을 정의합니다.

[!DNL Python] 및 R의 경우 40GB RAM으로 구성된 노트북 서버가 벤치마크에 사용되었습니다. PySpark와 Scala의 경우, 64GB RAM으로 구성된 데이터베이스 클러스터, 8코어, 2DBU가 사용되었으며, 이 벤치마크에는 최대 4명의 직원이 사용되었습니다.

사용되는 ExperienceEvent 스키마 데이터는 최대 10억(1B) 행 1천 개부터 크기가 변경되었습니다. PySpark 및 [!DNL Spark] 지표의 경우, XDM 데이터에 10일의 날짜 범위가 사용되었습니다.

임시 스키마 데이터는 [!DNL Query Service] Create Table as Select (CTAS)를 사용하여 미리 처리되었습니다. 또한 이 데이터는 최대 10억(1B) 행에 이르는 1,000개(1K) 행부터 크기가 변경되었습니다.

### 일괄 처리 모드와 대화형 모드를 사용해야 하는 경우 {#mode}

PySpark 및 Scala 노트북으로 데이터 세트를 읽을 때 대화형 모드나 일괄 처리 모드를 사용하여 데이터 집합을 읽을 수 있습니다. 일괄 처리 모드는 큰 데이터 세트에 사용되지만 빠른 결과를 위해 인터랙티브하게 수행됩니다.

- PySpark 및 Scala 노트북의 경우 500만 개 이상의 데이터 행을 읽고 있는 경우 일괄 처리 모드를 사용해야 합니다. 각 모드의 효율성에 대한 자세한 내용은 아래의 [PySpark](#pyspark-data-limits) 또는 [Scala](#scala-data-limits) 데이터 제한 표를 참조하십시오.

### [!DNL Python] 전자 필기장 데이터 제한

**XDM ExperienceEvent 스키마:**  22분 이내에 XDM 데이터의 최대 200만 행(~6.1GB 데이터의 디스크 데이터)을 읽을 수 있습니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 디스크 크기(MB) | 18.73 | 187.5 | 308년 | 3000년 | 6050년 |
| SDK (초) | 20.3 | 86.8 | 63 | 659년 | 1315 |

**임시 스키마:** 임시(ad-hoc) XDM(ad-hoc) 이외의 데이터의 최대 500만 개의 행(~5.6GB 데이터의 디스크)을 14분 이내에 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 디스크 크기(MB) | 1.21 | 11.72 | 115 | 1120년 | 2250년 | 3380년 | 5630년 |
| SDK (초) | 7.27 | 9.04 | 27.3 | 180 | 346년 | 487년 | 819년 |

### 전자 필기장 데이터 제한

**XDM ExperienceEvent 스키마:**  13분 이내에 최대 100만 개의 XDM 데이터 행(디스크의 3GB 데이터)을 읽을 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 디스크 크기(MB) | 18.73 | 187.5 | 308년 | 3000년 |
| R 커널(초) | 14.03 | 69.6 | 86.8 | 775년 |

**임시 스키마:**  최대 300만 개의 임시 데이터 행(293MB 데이터의 디스크)을 10분 이내에 읽을 수 있어야 합니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 디스크 크기(MB) | 0.082 | 0.612 | 9.0 | 91 | 188년 | 293 |
| R SDK(초) | 7.7 | 4.58 | 35.9 | 233년 | 470.5 | 603년 |

### PySpark([!DNL Python] 커널) 노트북 데이터 제한:{#pyspark-data-limits}

**XDM ExperienceEvent 스키마:**  대화형 모드에서 약 20분 내에 XDM 데이터의 최대 500만 행(~13.42GB 데이터의 디스크)을 읽을 수 있습니다. 대화형 모드는 최대 5백만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 일괄 처리 모드로 전환하는 것이 좋습니다. 일괄 처리 모드에서는 약 14시간 내에 XDM 데이터의 최대 5억 행(~1.31TB 데이터의 디스크)을 읽을 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK(대화형 모드) | 33년대 | 32.4s | 55.1s | 253.5s | 489.2년대 | 729.6s | 1206.8s | - | - | - | - |
| SDK(배치 모드) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2년대 | 1104.1s | 1786년대 | 53,87.2년대 | 10624.6s | 50547 |

**ad-hoc 스키마:**  대화형 모드에서 XDM이 아닌 데이터의 최대 500만 행(~5.36GB 데이터의 디스크)을 3분 이내에 읽을 수 있습니다. 일괄 처리 모드에서는 약 18분 내에 XDM 이외의 데이터의 최대 10억 행(~1.05TB 데이터) 을 읽을 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK 일괄 처리 모드(초) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3년대 | 411년대 | 675년대 | 702년대 | 719.2년대 | 1022.1s | 112.3s |

### [!DNL Spark] (스칼라 커널) 노트북 데이터 제한:  {#scala-data-limits}

**XDM ExperienceEvent 스키마:**  대화형 모드에서 약 18분 내에 XDM 데이터의 최대 5백만 행(~13.42GB 데이터의 디스크)을 읽을 수 있습니다. 대화형 모드는 최대 5백만 개의 행만 지원합니다. 더 큰 데이터 세트를 읽으려면 일괄 처리 모드로 전환하는 것이 좋습니다. 일괄 처리 모드에서는 약 14시간 내에 XDM 데이터의 최대 5억 행(~1.31TB 데이터의 디스크)을 읽을 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크의 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK 대화형 모드(초) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100년대 | - | - | - | - |
| SDK 일괄 처리 모드(초) | 374.4s | 398.5s | 527년대 | 487.9s | 588.9s | 829년대 | 939.1s | 1441년대 | 54,73.2s | 10118.8 | 49207.6 |

**ad-hoc 스키마:**  대화형 모드에서 XDM이 아닌 데이터의 최대 500만 행(~5.36GB 데이터의 디스크)을 3분 이내에 읽을 수 있습니다. 일괄 처리 모드에서는 약 16분 내에 XDM 이외의 데이터의 최대 10억 행(~1.05TB 데이터) 을 읽을 수 있습니다.

| 행 수 | 1K | 10켈빈 | 100켈빈 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 디스크의 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 35.7s | 31초 | 19.5s | 25.3s | 23년대 | 33.2s | 25.5s | - | - | - | - | - |
| SDK 일괄 처리 모드(초) | 448.8s | 459.7s | 519년대 | 475.8s | 599.9년대 | 347.6s | 407.8s | 397년대 | 518.8s | 487.9s | 760.2년대 | 975.4s |

## Python 노트북 {#python-notebook}

[!DNL Python] 전자 필기장을 사용하면 데이터 세트에 액세스할 때 데이터를 페이지 매기기를 사용할 수 있습니다. 페이지 매김이 있는 데이터와 페이지 매김이 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 시작 Python 전자 필기장에 대한 자세한 내용은 JupiterLab 사용 안내서의 [[!DNL JupyterLab] 시작 관리자](./overview.md#launcher) 섹션을 참조하십시오.

아래 Python 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#python-read-dataset)
- [데이터 집합에 쓰기](#write-python)
- [쿼리 데이터](#query-data-python)
- [ExperienceEvent 데이터 필터링](#python-filter)

### Python {#python-read-dataset}의 데이터 세트에서 읽기

**페이지 매김 없이:**

다음 코드를 실행하면 전체 데이터 세트가 읽습니다. 실행이 성공적으로 수행되면 데이터는 변수 `df`에서 참조하는 Pendder 데이터 프레임으로 저장됩니다.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**페이지 매김 사용:**

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽습니다. 페이지 매김이 각각 `limit()` 및 `offset()` 함수를 통해 데이터를 제한 및 오프셋하여 달성됩니다. 데이터 제한은 읽을 최대 데이터 포인트 수를 나타내지만, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트 수를 나타냅니다. 읽기 작업이 성공적으로 실행되면 데이터가 변수 `df`에서 참조하는 Pendder 데이터 프레임으로 저장됩니다.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Python {#write-python}의 데이터 집합에 쓰기

JupiterLab 전자 필기장의 데이터 집합에 쓰려면 JupiterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 노트북에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장의 아래쪽에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/write-dataset.png)

- **[!UICONTROL Write Data in Notebook]**&#x200B;을 사용하여 선택한 데이터 집합과 함께 쓰기 셀을 생성합니다.
- **[!UICONTROL 노트북에서 데이터 탐색]**&#x200B;을 사용하여 선택한 데이터 집합과 함께 읽기 셀을 생성합니다.
- 선택한 데이터 집합과 함께 기본 쿼리 셀을 생성하려면 **[!UICONTROL 전자 필기장의 데이터 쿼리]**&#x200B;를 사용하십시오.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다. `{DATASET_ID}` 및 `{PANDA_DATAFRAME}` 모두 바꿉니다.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### [!DNL Python] {#query-data-python}에서 [!DNL Query Service]을 사용하여 데이터를 쿼리합니다.

[!DNL JupyterLab] on  [!DNL Platform] 을 사용하면 전자 필기장의 SQL을 사용하여  [!DNL Python] Adobe Experience Platform Query Service [를 통해 ](https://www.adobe.com/go/query-service-home-en)데이터에 액세스할 수 있습니다. [!DNL Query Service]을 통해 데이터에 액세스하는 것은 실행 시간이 뛰어나 큰 데이터 세트를 처리하는 데 유용할 수 있습니다. [!DNL Query Service]을 사용하여 데이터를 쿼리하는 데 처리 시간 제한이 10분입니다.

[!DNL JupyterLab]에서 [!DNL Query Service]을 사용하기 전에 [[!DNL Query Service] SQL 구문](https://www.adobe.com/go/query-service-sql-syntax-en)에 대한 작업 이해를 갖도록 하십시오.

[!DNL Query Service]을 사용하여 데이터를 쿼리하려면 대상 데이터 세트의 이름을 제공해야 합니다. **[!UICONTROL 데이터 탐색기]**&#x200B;를 사용하여 원하는 데이터 세트를 찾아 필요한 코드 셀을 생성할 수 있습니다. 데이터 집합 목록을 마우스 오른쪽 단추로 클릭하고 전자 필기장에서 **[!UICONTROL 데이터 쿼리]**&#x200B;를 클릭하여 전자 필기장에서 두 개의 코드 셀을 생성합니다. 이 두 셀은 아래에 더 자세히 설명되어 있습니다.

![](../images/jupyterlab/data-access/python-query-dataset.png)

[!DNL JupyterLab]에서 [!DNL Query Service]을 활용하려면 먼저 작업 중인 [!DNL Python] 노트북과 [!DNL Query Service] 간에 연결을 만들어야 합니다. 이 작업은 첫 번째 생성된 셀을 실행하여 수행할 수 있습니다.

```python
qs_connect()
```

두 번째 생성된 셀에서 첫 번째 줄을 SQL 쿼리 앞에 정의해야 합니다. 기본적으로 생성된 셀은 쿼리 결과를 팬더 데이터 프레임으로 저장하는 선택적 변수(`df0`)를 정의합니다. <br>인수 `-c QS_CONNECTION` 는 필수 항목이며 커널에 SQL 쿼리를 실행하라고 지시합니다  [!DNL Query Service]. 추가 인수 목록은 [부록](#optional-sql-flags-for-query-service)을 참조하십시오.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

다음 예와 같이 문자열 형식의 구문을 사용하고 변수를 중괄호(`{}`)로 래핑하여 SQL 쿼리 내에서 직접 Python 변수를 참조할 수 있습니다.

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

[!DNL Python] 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 데이터 집합(`{DATASET_ID}`)의 ID를 제공해야 합니다. 시간 범위가 정의되면 지정된 모든 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 보다 작음
- `le()`: 작거나 같음
- `And()`:논리 AND 연산자
- `Or()`:논리 OR 연산자

다음 셀은 [!DNL ExperienceEvent] 데이터 세트를 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터로 필터링합니다.

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

R 전자 필기장을 사용하면 데이터 세트에 액세스할 때 데이터를 페이지 매기기를 사용할 수 있습니다. 페이지 매김이 있는 데이터와 페이지 매김이 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다. 사용 가능한 시작 R 노트북에 대한 자세한 내용은 JupiterLab 사용 안내서의 [[!DNL JupyterLab] 시작 관리자](./overview.md#launcher) 섹션을 참조하십시오.

아래 R 설명서에서는 다음 개념을 간략하게 설명합니다.

- [데이터 세트에서 읽기](#r-read-dataset)
- [데이터 집합에 쓰기](#write-r)
- [ExperienceEvent 데이터 필터링](#r-filter)

### R {#r-read-dataset}의 데이터 세트에서 읽기

**페이지 매김 없이:**

다음 코드를 실행하면 전체 데이터 세트가 읽습니다. 실행이 성공적으로 수행되면 데이터는 변수 `df0`에서 참조하는 Pendder 데이터 프레임으로 저장됩니다.

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

다음 코드를 실행하면 지정된 데이터 세트에서 데이터가 읽습니다. 페이지 매김이 각각 `limit()` 및 `offset()` 함수를 통해 데이터를 제한 및 오프셋하여 달성됩니다. 데이터 제한은 읽을 최대 데이터 포인트 수를 나타내지만, 오프셋은 데이터를 읽기 전에 건너뛸 데이터 포인트 수를 나타냅니다. 읽기 작업이 성공적으로 실행되면 데이터가 변수 `df0`에서 참조하는 Pendder 데이터 프레임으로 저장됩니다.

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

### R {#write-r}의 데이터 세트에 쓰기

JupiterLab 전자 필기장의 데이터 집합에 쓰려면 JupiterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래 강조 표시)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 노트북에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장의 아래쪽에 실행 가능한 코드 항목이 나타납니다.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- **[!UICONTROL Write Data in Notebook]**&#x200B;을 사용하여 선택한 데이터 집합과 함께 쓰기 셀을 생성합니다.
- **[!UICONTROL 노트북에서 데이터 탐색]**&#x200B;을 사용하여 선택한 데이터 집합과 함께 읽기 셀을 생성합니다.

또는 다음 코드 셀을 복사하여 붙여넣을 수 있습니다.

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### [!DNL ExperienceEvent] 데이터 필터링 {#r-filter}

R 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 데이터 집합(`{DATASET_ID}`)의 ID를 제공해야 합니다. 시간 범위가 정의되면 지정된 모든 페이지 매김이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

- `eq()`: 같음
- `gt()`: 보다 큼
- `ge()`: 크거나 같음
- `lt()`: 보다 작음
- `le()`: 작거나 같음
- `And()`:논리 AND 연산자
- `Or()`:논리 OR 연산자

다음 셀은 [!DNL ExperienceEvent] 데이터 세트를 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터로 필터링합니다.

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

아래 PySpark 설명서에서는 다음 개념을 간략하게 설명합니다.

- [SparkSession 초기화](#spark-initialize)
- [데이터 읽기 및 쓰기](#magic)
- [로컬 데이터 프레임 만들기](#pyspark-create-dataframe)
- [ExperienceEvent 데이터 필터링](#pyspark-filter-experienceevent)

### sparkSession {#spark-initialize} 초기화

모든 [!DNL Spark] 2.4 전자 필기장은 다음 표준 코드로 세션을 초기화해야 합니다.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### %dataset을 사용하여 PySpark 3 전자 필기장으로 읽고 쓸 수 있습니다. {#magic}

[!DNL Spark] 2.4의 도입으로 `%dataset` 사용자 정의 매직이 PySpark 3([!DNL Spark] 2.4) 노트북에 사용될 수 있습니다. IPython 커널에서 사용할 수 있는 매직 명령에 대한 자세한 내용은 [IPython 매직 설명서](https://ipython.readthedocs.io/en/stable/interactive/magics.html)를 참조하십시오.


**사용**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**설명**

[!DNL PySpark] 전자 필기장([!DNL Python] 3 커널)에서 데이터 집합을 읽거나 쓰는 사용자 지정 [!DNL Data Science Workspace] 매직 명령입니다.

| 이름 | 설명 | 필수 여부 |
| --- | --- | --- |
| `{action}` | 데이터 집합에 수행할 작업 유형입니다. 두 가지 작업을 &quot;읽기&quot; 또는 &quot;쓰기&quot;로 사용할 수 있습니다. | 예 |
| `--datasetId {id}` | 읽거나 쓸 데이터 세트의 ID를 제공하는 데 사용됩니다. | 예 |
| `--dataFrame {df}` | 팬더 데이터 프레임 <ul><li> 작업이 &quot;읽기&quot;이면 {df}은(는) 데이터 집합 읽기 작업 결과를 사용할 수 있는 변수입니다(데이터 프레임 등). </li><li> 작업이 &quot;write&quot;이면 이 데이터 프레임 {df}이(가) 데이터 집합에 기록됩니다. </li></ul> | 예 |
| `--mode` | 데이터 읽기 방식을 변경하는 추가 매개 변수입니다. 허용되는 매개 변수는 &quot;batch&quot; 및 &quot;interactive&quot;입니다. 기본적으로 모드는 &quot;batch&quot;로 설정됩니다.<br> 더 작은 데이터 세트에서 쿼리 성능을 향상시키기 위해 &quot;대화형&quot; 모드를 사용하는 것이 좋습니다. | 예 |

>[!TIP]
>
>[노트북 데이터 제한](#notebook-data-limits) 섹션 내에서 PySpark 테이블을 검토하여 `mode`를 `interactive` 또는 `batch`로 설정해야 하는지 확인합니다.

**예**

- **다음 참조**:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **쓰기 예**:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류를 수신하는 경우 도움이 될 수 있습니다.
> 
> - 스테이지 오류로 인해 작업이 중단되었습니다..각 파티션에서 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트가 연결이 끊기고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

> 
> 
자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

다음 방법을 사용하여 JupiterLab buy에서 위의 예를 자동으로 생성할 수 있습니다.

JupiterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 노트북에 데이터 쓰기]** 옵션을 선택합니다. 전자 필기장의 아래쪽에 실행 가능한 코드 항목이 나타납니다.

- **[!UICONTROL 전자 필기장에서 데이터 탐색]**&#x200B;을 사용하여 읽기 셀을 생성합니다.
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
>대체(Replacement), 이중 분수(double fraction) 또는 긴 시드(long seed)와 같은 선택적 시드 샘플을 지정할 수도 있습니다.

### [!DNL ExperienceEvent] 데이터 필터링 {#pyspark-filter-experienceevent}

PySpark 전자 필기장에서 [!DNL ExperienceEvent] 데이터 집합에 액세스하고 필터링하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙을 제공해야 합니다. 필터링 시간 범위는 함수 `spark.sql()`을 사용하여 정의됩니다. 여기서 함수 매개 변수는 SQL 쿼리 문자열입니다.

다음 셀은 [!DNL ExperienceEvent] 데이터 세트를 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터로 필터링합니다.

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

## 스칼라 노트북 {#scala-notebook}

아래 설명서에는 다음 개념에 대한 예가 나와 있습니다.

- [SparkSession 초기화](#scala-initialize)
- [데이터 집합 읽기](#read-scala-dataset)
- [데이터 집합에 쓰기](#scala-write-dataset)
- [로컬 데이터 프레임 만들기](#scala-create-dataframe)
- [ExperienceEvent 데이터 필터링](#scala-experienceevent)

### SparkSession {#scala-initialize} 초기화

모든 Scala 전자 필기장에서 다음 표준 코드로 세션을 초기화해야 합니다.

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 데이터 집합 읽기 {#read-scala-dataset}

Scala에서는 `clientContext` 을 가져와서 플랫폼 값을 가져오고 반환할 수 있으므로 `var userToken` 등의 변수를 정의할 필요가 없습니다. 아래 스칼라 예에서 `clientContext` 는 데이터 집합을 읽는 데 필요한 모든 값을 가져오고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류를 수신하는 경우 도움이 될 수 있습니다.
> 
> - 스테이지 오류로 인해 작업이 중단되었습니다..각 파티션에서 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트가 연결이 끊기고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

> 
> 
자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

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
| df1 | 데이터를 읽고 쓰는 데 사용되는 Pendder 데이터 프레임을 나타내는 변수입니다. |
| user-token | `clientContext.getUserToken()`을 사용하여 자동으로 가져오는 사용자 토큰입니다. |
| 서비스 토큰 | `clientContext.getServiceToken()`을 사용하여 자동으로 가져오는 서비스 토큰입니다. |
| ims 조직 | `clientContext.getOrgId()`을 사용하여 자동으로 가져오는 IMS 조직 ID입니다. |
| api 키 | `clientContext.getApiKey()`을 사용하여 자동으로 가져오는 API 키입니다. |

>[!TIP]
>
>[노트북 데이터 제한](#notebook-data-limits) 섹션 내에서 스칼라 테이블을 검토하여 `mode`를 `interactive` 또는 `batch`로 설정해야 하는지 확인합니다.

다음 방법을 사용하여 JupiterLab buy에서 위의 예를 자동으로 생성할 수 있습니다.

JupiterLab의 왼쪽 탐색에서 데이터 아이콘 탭(아래에 강조 표시됨)을 선택합니다. **[!UICONTROL 데이터 세트]** 및 **[!UICONTROL 스키마]** 디렉터리가 나타납니다. **[!UICONTROL 데이터 세트]**&#x200B;를 선택하고 마우스 오른쪽 단추를 클릭한 다음 사용할 데이터 세트의 드롭다운 메뉴에서 **[!UICONTROL 노트북에서 데이터 탐색]** 옵션을 선택합니다. 전자 필기장의 아래쪽에 실행 가능한 코드 항목이 나타납니다.
및
- **[!UICONTROL 전자 필기장에서 데이터 탐색]**&#x200B;을 사용하여 읽기 셀을 생성합니다.
- **[!UICONTROL 전자 필기장에 데이터 쓰기]**&#x200B;를 사용하여 쓰기 셀을 생성합니다.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 데이터 집합 {#scala-write-dataset}에 쓰기

Scala에서는 `clientContext` 을 가져와서 플랫폼 값을 가져오고 반환할 수 있으므로 `var userToken` 등의 변수를 정의할 필요가 없습니다. 아래 스칼라 예에서 `clientContext` 는 데이터 집합에 쓰는 데 필요한 모든 값을 정의하고 반환하는 데 사용됩니다.

>[!IMPORTANT]
>
> 데이터를 쓰기 전에 `df.cache()`을 사용하여 데이터를 캐시하면 전자 필기장 성능이 크게 향상됩니다. 다음 오류를 수신하는 경우 도움이 될 수 있습니다.
> 
> - 스테이지 오류로 인해 작업이 중단되었습니다..각 파티션에서 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
> - 원격 RPC 클라이언트가 연결이 끊기고 다른 메모리 오류가 발생했습니다.
> - 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

> 
> 
자세한 내용은 [문제 해결 안내서](../troubleshooting-guide.md)를 참조하십시오.

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

| 요소를 생성하지 않습니다 | 설명 |
| ------- | ----------- |
| df1 | 데이터를 읽고 쓰는 데 사용되는 Pendder 데이터 프레임을 나타내는 변수입니다. |
| user-token | `clientContext.getUserToken()`을 사용하여 자동으로 가져오는 사용자 토큰입니다. |
| 서비스 토큰 | `clientContext.getServiceToken()`을 사용하여 자동으로 가져오는 서비스 토큰입니다. |
| ims 조직 | `clientContext.getOrgId()`을 사용하여 자동으로 가져오는 IMS 조직 ID입니다. |
| api 키 | `clientContext.getApiKey()`을 사용하여 자동으로 가져오는 API 키입니다. |

>[!TIP]
>
>[노트북 데이터 제한](#notebook-data-limits) 섹션 내에서 스칼라 테이블을 검토하여 `mode`를 `interactive` 또는 `batch`로 설정해야 하는지 확인합니다.

### 로컬 데이터 프레임 만들기 {#scala-create-dataframe}

Scala를 사용하여 로컬 데이터 프레임을 만들려면 SQL 쿼리가 필요합니다. 예:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### [!DNL ExperienceEvent] 데이터 필터링 {#scala-experienceevent}

Scala 전자 필기장의 [!DNL ExperienceEvent] 데이터 세트에 액세스 및 필터링하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙을 제공해야 합니다. 필터링 시간 범위는 함수 `spark.sql()`을 사용하여 정의됩니다. 여기서 함수 매개 변수는 SQL 쿼리 문자열입니다.

다음 셀은 [!DNL ExperienceEvent] 데이터 세트를 2019년 1월 1일부터 2019년 12월 31일 말까지 독점 존재하는 데이터로 필터링합니다.

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

이 문서에서는 JupiterLab 노트북을 사용하여 데이터 세트에 액세스하는 일반적인 지침을 다룹니다. 데이터 세트 쿼리에 대한 자세한 예는 JupiterLab notebook](./query-service.md) 설명서의 [쿼리 서비스 를 참조하십시오. 데이터 세트를 탐색하고 시각화하는 방법에 대한 자세한 내용은 [notebook](./analyze-your-data.md)을 사용하여 데이터를 분석하는 문서를 참조하십시오.

## [!DNL Query Service] {#optional-sql-flags-for-query-service}에 대한 선택적 SQL 플래그

이 표에서는 [!DNL Query Service]에 사용할 수 있는 선택적 SQL 플래그에 대해 설명합니다.

| **플래그** | **설명** |
| --- | --- |
| `-h`, `--help` | 도움말 메시지를 표시하고 종료합니다. |
| `-n`,  `--notify` | 쿼리 결과를 알리는 토글 옵션. |
| `-a`,  `--async` | 이 플래그를 사용하면 쿼리가 비동기식으로 실행되며 쿼리가 실행되는 동안 커널을 해제할 수 있습니다. 쿼리가 완료되지 않은 경우 정의되지 않을 수 있으므로 쿼리 결과를 변수에 할당할 때는 주의하십시오. |
| `-d`,  `--display` | 이 플래그를 사용하면 결과가 표시되지 않습니다. |
