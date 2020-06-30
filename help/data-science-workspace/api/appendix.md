---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 부록
topic: Developer guide
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---


# 부록

다음 섹션에서는 API의 다양한 기능에 대한 참조 정보를 [!DNL Sensei Machine Learning] 제공합니다.

## 자산 검색을 위한 쿼리 매개 변수 {#query}

API는 자산 검색과 관련된 쿼리 매개 변수를 지원합니다. [!DNL Sensei Machine Learning] 사용 가능한 쿼리 매개 변수 및 사용 방법은 다음 표에 설명되어 있습니다.

| 쿼리 매개 변수 | 설명 | 기본값 |
| --------------- | ----------- | ------- |
| `start` | 페이지 매김에 대한 시작 인덱스를 나타냅니다. | `start=0` |
| `limit` | 반환할 최대 결과 수를 나타냅니다. | `limit=25` |
| `orderby` | 우선 순위 순서로 정렬하는 데 사용할 속성을 나타냅니다. 속성 이름 앞에 대시(**-**)를 포함하여 내림차순으로 정렬하면 결과가 오름차순으로 정렬됩니다. | `orderby=created` |
| `property` | 반환하기 위해 개체가 충족해야 하는 비교 표현식을 나타냅니다. | `property=deleted==false` |

>[!NOTE] 여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(**&amp;**)로 구분해야 합니다.

## Python CPU 및 GPU 구성 {#cpu-gpu-config}

Python Engine은 교육 또는 채점 목적으로 CPU 또는 GPU 중 하나를 선택할 수 있으며 MLIniture에서 작업 사양( [](./mlinstances.md)`tasks.specification`)으로 정의됩니다.

다음은 트레이닝용 CPU와 채점용 GPU를 사용하는 것을 지정하는 예제 구성입니다.

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

>[!NOTE] 의 값 `cpus` 및 `gpus` 은 CPU 또는 GPU 수를 의미하지 않고 실제 시스템의 수를 의미하지 않습니다. 이러한 값은 권한을 가지며 `"1"` 그렇지 않으면 예외를 throw합니다.

## PySpark 및 Spark 리소스 구성 {#resource-config}

Spark Engine은 트레이닝 및 점수에 필요한 계산 리소스를 수정할 수 있습니다. 이러한 리소스는 다음 표에 설명되어 있습니다.

| 리소스 | 설명 | 유형 |
| -------- | ----------- | ---- |
| driverMemory | 드라이버 메모리(MB) | int |
| driverCore | 드라이버에서 사용하는 코어 수 | int |
| executorMemory | 실행 사용자를 위한 메모리(MB) | int |
| executorCoers | 시행자가 사용한 코어 수 | int |
| numExecuters | 집행자 수 | int |

리소스는 (A) 개별 [교육 또는 점수 매개 변수](./mlinstances.md) 또는 (B) 추가 사양 개체(`specification`)의 리소스로 MLInestment에 지정할 수 있습니다. 예를 들어 다음 리소스 구성은 교육 및 점수 모두에 대해 동일합니다.

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
