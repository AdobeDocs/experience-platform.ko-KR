---
keywords: Experience Platform;개발자 안내서;SDK;데이터 액세스 SDK;Data Science Workspace;인기 있는 주제
solution: Experience Platform
title: Adobe Experience Platform Platform SDK를 사용한 모델 작성
description: 이 자습서에서는 data_access_sdk_python을 Python 및 R에서 모두 새로운 Python platform_sdk로 변환하는 방법에 대한 정보를 제공합니다.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Adobe Experience Platform을 사용한 모델 작성 [!DNL Platform] SDK

이 자습서에서는 전환에 대한 정보를 제공합니다 `data_access_sdk_python` 새로운 Python으로 `platform_sdk` Python과 R 둘 다에서. 이 자습서에서는 다음 작업에 대해 설명합니다.

- [빌드 인증](#build-authentication)
- [기본 데이터 읽기](#basic-reading-of-data)
- [기본 데이터 쓰기](#basic-writing-of-data)

## 빌드 인증 {#build-authentication}

을 호출하려면 인증이 필요합니다. [!DNL Adobe Experience Platform]는 API 키, IMS 조직 ID, 사용자 토큰 및 서비스 토큰으로 구성됩니다.

### Python

Jupyter Notebook을 사용하는 경우 아래 코드를 사용하여 `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Jupyter Notebook을 사용하지 않거나 IMS 조직을 변경해야 하는 경우 아래 코드 샘플을 사용하십시오.

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Jupyter Notebook을 사용하는 경우 아래 코드를 사용하여 `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Jupyter Notebook을 사용하지 않거나 IMS 조직을 변경해야 하는 경우 아래 코드 샘플을 사용하십시오.

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 기본 데이터 읽기 {#basic-reading-of-data}

새로운 기능 [!DNL Platform] SDK의 경우 최대 읽기 크기는 32GB이며 최대 읽기 시간은 10분입니다.

읽기 시간이 너무 오래 걸리는 경우 다음 필터링 옵션 중 하나를 사용할 수 있습니다.

- [오프셋 및 제한으로 데이터 필터링](#filter-by-offset-and-limit)
- [날짜별 데이터 필터링](#filter-by-date)
- [열별 데이터 필터링](#filter-by-selected-columns)
- [정렬된 결과 가져오는 중](#get-sorted-results)

>[!NOTE]
>
>IMS 조직이 `client_context`.

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

## 오프셋 및 제한으로 필터링 {#filter-by-offset-and-limit}

일괄 처리 ID로 필터링하는 기능은 더 이상 지원되지 않으므로 데이터를 읽는 범위를 지정하려면 다음을 사용해야 합니다 `offset` 및 `limit`.

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

## 날짜별로 필터링 {#filter-by-date}

이제 날짜 필터링의 세부기간은 일별로 설정되지 않고 타임스탬프로 정의됩니다.

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

새로운 [!DNL Platform] SDK는 다음 작업을 지원합니다.

| 작업 | 함수 |
| --------- | -------- |
| 다음과 같음 (`=`) | `eq()` |
| 보다 큼 (`>`) | `gt()` |
| 크거나 같음 (`>=`) | `ge()` |
| 미만 (`<`) | `lt()` |
| 작거나 같음 (`<=`) | `le()` |
| 및 (`&`) | `And()` |
| 또는 (`|`) | `Or()` |

## 선택한 열로 필터링 {#filter-by-selected-columns}

데이터 읽기를 세분화하기 위해 열 이름별로 필터링할 수도 있습니다.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 정렬된 결과 가져오기 {#get-sorted-results}

수신된 결과는 대상 데이터 세트의 지정된 열 및 해당 순서(asc/desc)별로 정렬할 수 있습니다.

다음 예제에서는 데이터 프레임이 먼저 오름차순으로 &quot;column-a&quot;별로 정렬됩니다. &quot;column-a&quot;에 대해 동일한 값을 갖는 행은 &quot;column-b&quot;별로 내림차순으로 정렬됩니다.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 기본 데이터 쓰기 {#basic-writing-of-data}

>[!NOTE]
>
>IMS 조직이 `client_context`.

Python 및 R로 데이터를 쓰려면 아래의 예제 중 하나를 사용하십시오.

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

을(를) 구성했으면 `platform_sdk` 데이터 로더에서, 데이터는 준비를 거치고 다음 로 분할됩니다. `train` 및 `val` 데이터 세트. 데이터 준비 및 기능 엔지니어링에 대한 자세한 내용은 다음 섹션에서 확인하십시오. [데이터 준비 및 기능 엔지니어링](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) 을 사용하여 레시피를 만드는 자습서에서 [!DNL JupyterLab] 전자 필기장.
