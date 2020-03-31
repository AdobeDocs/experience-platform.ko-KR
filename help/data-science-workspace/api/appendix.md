---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 부록
topic: Developer guide
translation-type: tm+mt
source-git-commit: 0081cbd414e983d767b4a6f3aceed85d72a34816

---


# 부록

다음 섹션에서는 Sensei Machine Learning API의 다양한 기능에 대한 참조 정보를 제공합니다.

## 자산 검색을 위한 쿼리 매개 변수 {#query}

Sensei Machine Learning API는 자산 검색과 함께 쿼리 매개 변수를 지원합니다. 사용 가능한 쿼리 매개 변수 및 사용 방법은 다음 표에 설명되어 있습니다.

| 쿼리 매개 변수 | 설명 | 기본값 |
| --------------- | ----------- | ------- |
| `start` | 페이지 매김의 시작 인덱스를 나타냅니다. | `start=0` |
| `limit` | 반환할 최대 결과 수를 나타냅니다. | `limit=25` |
| `orderby` | 우선 순위 순서로 정렬하는 데 사용할 속성을 나타냅니다. 속성 이름 앞에 대시(**-**)를 포함하여 내림차순으로 정렬하면 결과가 오름차순으로 정렬됩니다. | `orderby=created` |
| `property` | 반환하기 위해 객체가 충족해야 하는 비교 표현식을 나타냅니다. | `property=deleted==false` |

>[!NOTE] 여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(**&amp;**)로 구분해야 합니다.

## Python CPU 및 GPU 구성 {#cpu-gpu-config}

Python Engine은 교육 또는 채점 목적으로 CPU 또는 GPU 중에서 선택할 수 있으며 MLInstance [를 작업](./mlinstances.md) 사양(`tasks.specification`)으로 정의합니다.

다음은 트레이닝용 CPU와 채점용 GPU를 사용하는 방법을 지정하는 예제 구성입니다.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE] 의 `cpus` 값과 `gpus` 값은 CPU 또는 GPU 수를 의미하지 않고 실제 시스템의 수를 나타냅니다. 이러한 값은 `"1"` 권한을 가지며, 그렇지 않으면 예외가 발생합니다.

## PySpark 및 Spark 리소스 구성 {#resource-config}

PySpark 및 Spark Engines는 교육 및 채점 목적으로 연산 리소스를 수정할 수 있는 기능을 갖추고 있습니다. 이러한 리소스는 다음 표에 설명되어 있습니다.

| 리소스 | 설명 | 유형 |
| -------- | ----------- | ---- |
| driverMemory | 드라이버 메모리(MB) | int |
| driverCore | 드라이버가 사용하는 코어 수 | int |
| executorMemory | Executor 메모리(MB) | int |
| executorCore | 실행자가 사용한 코어 수 | int |
| numExecuters | 집행자 수 | int |

리소스는 (A) [개별 교육 또는 채점](./mlinstances.md) 매개 변수 또는 (B) 추가 사양 개체(`specification`) 내에서 지정할 수 있습니다. 예를 들어 다음 리소스 구성은 교육 및 점수 모두에 대해 동일합니다.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
