---
keywords: Experience Platform;개발자 안내서;엔드포인트;Data Science Workspace;인기 항목;
solution: Experience Platform
title: Sensei 머신 러닝 API 안내서 부록
description: 다음 섹션에서는 Sensei 머신 러닝 API의 다양한 기능에 대한 참조 정보를 제공합니다.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API 안내서 부록

다음 섹션에서는 의 다양한 기능에 대한 참조 정보를 제공합니다 [!DNL Sensei Machine Learning] API.

## 자산 검색을 위한 쿼리 매개 변수 {#query}

다음 [!DNL Sensei Machine Learning] API는 에셋 검색과 함께 쿼리 매개 변수를 지원합니다. 사용 가능한 쿼리 매개 변수와 그 사용법은 다음 표에 설명되어 있습니다.

| 쿼리 매개 변수 | 설명 | 기본값 |
| --------------- | ----------- | ------- |
| `start` | 페이지 매김의 시작 색인을 나타냅니다. | `start=0` |
| `limit` | 반환할 최대 결과 수를 나타냅니다. | `limit=25` |
| `orderby` | 우선순위 순서로 정렬하는 데 사용할 속성을 나타냅니다. 대시(**-**) 속성 이름 앞에 를 추가하여 내림차순으로 정렬하고, 그렇지 않으면 결과를 오름차순으로 정렬합니다. | `orderby=created` |
| `property` | 반환되려면 개체가 충족해야 하는 비교 표현식을 나타냅니다. | `property=deleted==false` |

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(**및**).

## Python CPU 및 GPU 구성 {#cpu-gpu-config}

Python 엔진은 교육 또는 채점 목적으로 CPU와 GPU 중 하나를 선택할 수 있으며, [MLInstance](./mlinstances.md) 작업 사양(`tasks.specification`).

다음은 교육용 CPU와 채점용 GPU를 지정하는 예제 구성입니다.

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

>[!NOTE]
>
>값: `cpus` 및 `gpus` 는 CPU 또는 GPU의 수를 의미하지 않고 실제 시스템의 수를 나타냅니다. 이 값은 허용 가능합니다. `"1"` 및 가 아닌 경우 예외를 throw합니다.

## PySpark 및 Spark 리소스 구성 {#resource-config}

Spark 엔진은 교육 및 채점 목적으로 계산 리소스를 수정하는 능력이 있습니다. 이러한 리소스는 다음 표에 설명되어 있습니다.

| 리소스 | 설명 | 유형 |
| -------- | ----------- | ---- |
| driverMemory | 드라이버용 메모리(MB) | int |
| 드라이버 코어 | 드라이버에서 사용한 코어 수 | int |
| 실행자메모리 | 실행기 메모리(MB) | int |
| executorCores | Executor에서 사용한 코어 수 | int |
| numExecutors | 실행자 수 | int |

리소스를에 지정할 수 있습니다. [MLInstance](./mlinstances.md) (A) 개별 교육 또는 채점 매개 변수 또는 (B) 추가 사양 객체(`specification`). 예를 들어 다음 자원 구성은 교육과 채점 모두에 대해 동일합니다.

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
