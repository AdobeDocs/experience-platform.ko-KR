---
keywords: Experience Platform; 개발자 안내서; 끝점; 데이터 과학 작업 영역; 인기 있는 주제;
solution: Experience Platform
title: Sensei Machine Learning API 안내서 부록
description: 다음 섹션에서는 Sensei Machine Learning API의 다양한 기능에 대한 참조 정보를 제공합니다.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning] API 안내서 부록

>[!NOTE]
>
>Data Science 작업 영역은(는) 더 이상 구매할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

다음 섹션에서는 [!DNL Sensei Machine Learning] API의 다양한 기능에 대한 참조 정보를 제공합니다.

## 자산 검색을 위한 쿼리 매개 변수 {#query}

[!DNL Sensei Machine Learning] API는 자산 검색과 함께 쿼리 매개 변수를 지원합니다. 사용 가능한 쿼리 매개 변수와 그 사용법은 다음 표에 설명되어 있습니다.

| 쿼리 매개 변수 | 설명 | 기본 값 |
| --------------- | ----------- | ------- |
| `start` | 페이지 매김의 시작 색인을 나타냅니다. | `start=0` |
| `limit` | 반환할 최대 결과 수를 나타냅니다. | `limit=25` |
| `orderby` | 우선 순위에 따라 정렬하는 데 사용할 속성을 나타냅니다. 내림차순으로 정렬하려면 속성 이름 앞에 대시(**-**)를 포함하고, 그렇지 않으면 결과가 오름차순으로 정렬됩니다. | `orderby=created` |
| `property` | 반환되려면 개체가 충족해야 하는 비교 표현식을 나타냅니다. | `property=deleted==false` |

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(**&amp;**)로 구분해야 합니다.

## Python CPU 및 GPU 구성 {#cpu-gpu-config}

Python 엔진은 교육 또는 채점 목적으로 CPU와 GPU 중 하나를 선택할 수 있으며 [MLInstance](./mlinstances.md)에서 작업 사양(`tasks.specification`)으로 정의됩니다.

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
>`cpus` 및 `gpus`의 값은 CPU 또는 GPU의 수가 아니라 실제 컴퓨터의 수를 나타냅니다. 이 값은 `"1"`일 수 있으며, 그렇지 않으면 예외를 throw합니다.

## PySpark 및 Spark 리소스 구성 {#resource-config}

Spark 엔진에는 교육 및 채점 목적으로 계산 리소스를 수정할 수 있는 기능이 있습니다. 이러한 리소스는 다음 표에 설명되어 있습니다.

| 리소스 | 설명 | 유형 |
| -------- | ----------- | ---- |
| driverMemory | 드라이버용 메모리(MB) | int |
| 드라이버 코어 | 드라이버에서 사용한 코어 수 | 정수 |
| executorMemory | 실행기용 메모리(MB) | 정수 |
| executorCores | Executor에서 사용한 코어 수 | int |
| numExecutors | 실행자 수 | int |

[MLInstance](./mlinstances.md)에 리소스를 (A) 개별 교육 또는 채점 매개 변수 또는 (B) 추가 사양 개체(`specification`) 내에서 지정할 수 있습니다. 예를 들어 다음 자원 구성은 교육과 채점 모두에 대해 동일합니다.

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
