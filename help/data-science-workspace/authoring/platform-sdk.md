---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: 플랫폼 SDK 안내서
topic: SDK authoring
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 플랫폼 SDK 안내서

이 자습서에서는 Python과 R `data_access_sdk_python` 에서 새로운 Python으로 전환하는 방법에 `platform_sdk` 대한 정보를 제공합니다.이 자습서에서는 다음 작업에 대한 정보를 제공합니다.

- [인증 빌드](#build-authentication)
- [데이터 기본 읽기](#basic-reading-of-data)
- [데이터 기본 작성](#basic-writing-of-data)

## 인증 빌드 {#build-authentication}

Adobe Experience Platform을 호출하려면 인증이 필요하며 API 키, IMS 조직 ID, 사용자 토큰 및 서비스 토큰으로 구성됩니다.

### Python

Jupiter Notebook을 사용하는 경우 아래 코드를 사용하여 `client_context`다음을 빌드하십시오.

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Jupiter Notebook을 사용하지 않거나 IMS Org를 변경해야 하는 경우 아래 코드 샘플을 사용하십시오.

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Jupiter Notebook을 사용하는 경우 아래 코드를 사용하여 `client_context`다음을 빌드하십시오.

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Jupiter Notebook을 사용하지 않거나 IMS Org를 변경해야 하는 경우 아래 코드 샘플을 사용하십시오.

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 데이터 기본 읽기 {#basic-reading-of-data}

새로운 플랫폼 SDK를 사용하면 최대 읽기 크기는 32GB이며 최대 읽기 시간은 10분입니다.

읽기 시간이 너무 오래 걸리는 경우 다음 필터링 옵션 중 하나를 사용할 수 있습니다.

- [오프셋 및 제한별 데이터 필터링](#filter-by-offset-and-limit)
- [날짜별 데이터 필터링](#filter-by-date)
- [열별 데이터 필터링](#filter-by-selected-columns)
- [정렬된 결과 가져오기](#get-sorted-results)

>[!NOTE] IMS 조직은 에 설정되어 `client_context`있습니다.

### Python

Python에서 데이터를 읽으려면 아래 코드 샘플을 사용하십시오.

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

R에서 데이터를 읽으려면 아래 코드 샘플을 사용하십시오.

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 오프셋 및 제한별 필터링 {#filter-by-offset-and-limit}

더 이상 일괄 처리 ID로 필터링이 지원되지 않으므로 데이터 읽기 범위를 지정하려면 `offset` 및 `limit`을 사용해야 합니다.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## 날짜별 필터링 {#filter-by-date}

이제 날짜의 세부기간을 요일로 설정하는 것이 아니라 타임스탬프에 의해 필터링이 정의됩니다.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

새 플랫폼 SDK는 다음 작업을 지원합니다.

| 작업 | 함수 |
| --------- | -------- |
| 다음과 같음 (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| And (`&`) | `And()` |
| 또는 (`|`) | `Or()` |

## 선택한 열로 필터링 {#filter-by-selected-columns}

데이터 읽기를 더 세밀하게 조정하기 위해 열 이름별로 필터링할 수도 있습니다.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 정렬된 결과 가져오기 {#get-sorted-results}

수신한 결과는 대상 데이터 집합의 지정된 열과 순서(asc/desc)별로 정렬할 수 있습니다.

다음 예에서 데이터 프레임은 먼저 &quot;column-a&quot;로 오름차순으로 정렬됩니다. 그런 다음 &quot;column-a&quot;에 대해 동일한 값이 있는 행은 &quot;column-b&quot;로 내림차순으로 정렬됩니다.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 데이터 기본 작성 {#basic-writing-of-data}

>[!NOTE] IMS 조직은 에 설정되어 `client_context`있습니다.

Python 및 R에서 데이터를 작성하려면 아래 예제 중 하나를 사용하십시오.

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## 다음 단계

데이터 로더를 구성하면 `platform_sdk` 데이터가 준비를 거쳐 `train` 및 `val` 데이터 세트로 분할됩니다. 데이터 준비 및 기능 엔지니어링에 대한 자세한 내용은 JupiterLab 노트북을 사용하여 레서피를 만드는 방법에 대한 자습서의 [데이터 준비 및 기능 엔지니어링](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) 섹션을 참조하십시오.