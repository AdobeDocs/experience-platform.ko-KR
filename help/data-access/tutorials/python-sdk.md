---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api
solution: Experience Platform
title: Secure Python Data Access SDK
topic: tutorial
type: Tutorial
description: Secure Python Data Access SDK는 Adobe Experience Platform에서 데이터 세트를 읽고 쓸 수 있는 소프트웨어 개발 키트입니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---


# 보안 [!DNL Python] [!DNL Data Access] SDK

보안 [!DNL Python][!DNL Data Access] SDK는 Adobe Experience Platform에서 데이터 세트를 읽고 쓸 수 있는 소프트웨어 개발 키트입니다.

## 시작하기

보안 [SDK를 호출하기 위해 값에 액세스하려면](../../tutorials/authentication.md) 인증 [!DNL Python] 자습서를 [!DNL Data Access] 완료해야 합니다.

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. SDK를 [!DNL Python] 사용하려면 작업이 수행할 샌드박스의 이름과 ID가 필요합니다.

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## 환경 설정

기본적으로 서비스 끝점은 통합 환경 끝점으로 설정됩니다. 그 결과 프로덕션을 가리키려면 다음 환경 변수를 다음 값으로 설정합니다.

| 변수 | 끝점 |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

또한 자격 증명을 환경 변수로 추가할 수 있습니다.

| 변수 | 값 |
| -------- | ----- |
| `ORG_ID` | 귀하의 `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | 가치 `{API_KEY}` 를 |
| `USER_TOKEN` | 가치 `{ACCESS_TOKEN}` 를 |
| `SERVICE_TOKEN` | 서비스 간 `{SERVICE_TOKEN}`의 백 채널 요청을 승인해야 할 수 있습니다. |
| `SANDBOX_ID` | 샌드박스의 `{SANDBOX_ID}` 값. |
| `SANDBOX_NAME` | 샌드박스의 `{SANDBOX_NAME}` 값. |

## 설치

모든 소포들은 건물 `./dist` 후에 출력된다.

### 바퀴

```python
python3 setup.py bdist_wheel --universal
```

프로젝트 디렉토리에서 [!DNL Python] 3 환경에 휠을 로드합니다.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### 계란 파일

```python
python3 setup.py bdist_egg
```

## 데이터 세트 읽기

환경 변수를 설정하고 설치를 완료한 후 데이터 세트를 판더 데이터 프레임으로 읽을 수 있습니다.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### 데이터 세트에서 열 선택

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 분할 정보 다운로드:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT 절

DISTINCT 절을 사용하면 모든 고유한 값을 행/열 수준에서 가져와 응답에서 모든 중복 값을 제거할 수 있습니다.

함수 사용 예는 아래에 `distinct()` 나와 있습니다.

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE 절

SDK는 데이터 세트를 필터링하는 데 도움이 되는 특정 연산자를 지원합니다. [!DNL Python]

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

다음은 이러한 필터링 기능을 사용하는 예입니다.

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY 절

ORDER BY 절을 사용하면 수신한 결과를 특정 순서(오름차순 또는 내림차순)의 지정된 열로 정렬할 수 있습니다. SDK에서 [!DNL Python] 이 작업은 `sort()` 함수를 사용하여 수행됩니다.

함수 사용 예는 아래에 `sort()` 나와 있습니다.

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT 절

LIMIT 절을 사용하면 데이터 세트에서 수신한 레코드 수를 제한할 수 있습니다.

함수 사용 예는 아래에 `limit()` 나와 있습니다.

```python
df = dataset_reader.limit(100).read()
```

### OFFSET 절

OFFSET 절을 사용하면 처음 부분부터 행을 건너뛰어 이후 행으로부터 돌아오는 것을 시작할 수 있습니다. LIMIT와 함께 사용하면 블록의 행을 반복하는 데 사용할 수 있습니다.

함수 사용 예는 아래에 `offset()` 나와 있습니다.

```python
df = dataset_reader.offset(100).read()
```

## 데이터 세트 작성

SDK는 데이터 집합 작성을 지원합니다. [!DNL Python] 사용자는 데이터 세트에 작성해야 하는 판다에게 데이터 프레임을 제공해야 합니다.

### 판다의 데이터 프레임 작성

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## 사용자 공간 디렉토리(체크 포인트)

더 긴 실행 작업의 경우 사용자는 중간 단계를 저장해야 할 수 있습니다. 이와 같은 경우, [!DNL Python] SDK는 사용자에게 사용자 공간을 읽고 쓸 수 있는 기능을 제공합니다.

>[!NOTE]
>
>데이터에 대한 경로는 SDK에서 **저장되지** 않습니다. 사용자는 해당 데이터에 해당하는 경로를 저장해야 합니다.

### 사용자 공간에 쓰기

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 사용자 공간에서 읽기

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
