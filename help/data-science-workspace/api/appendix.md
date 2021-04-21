---
keywords: Experience Platform;개발자 가이드;종단점;데이터 과학 작업 공간;인기 있는 주제
solution: Experience Platform
title: Sensei 기계 학습 API 가이드 부록
topic-legacy: Developer guide
description: 다음 섹션에서는 Sensei Machine Learning API의 다양한 기능에 대한 참조 정보를 제공합니다.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API 안내서 부록

다음 섹션에서는 [!DNL Sensei Machine Learning] API의 다양한 기능에 대한 참조 정보를 제공합니다.

## 자산 검색을 위한 쿼리 매개 변수 {#query}

[!DNL Sensei Machine Learning] API는 자산 검색 시 쿼리 매개 변수를 지원합니다. 사용 가능한 쿼리 매개 변수 및 사용 방법은 다음 표에 설명되어 있습니다.

| 쿼리 매개 변수 | 설명 | 기본값 |
| --------------- | ----------- | ------- |
| `start` | 페이지 매기기에 대한 시작 인덱스를 나타냅니다. | `start=0` |
| `limit` | 반환할 최대 결과 수를 나타냅니다. | `limit=25` |
| `orderby` | 우선 순위 순서로 정렬하는 데 사용할 속성을 나타냅니다. 내림차순으로 정렬하려면 속성 이름 앞에 대시(**-**)를 포함하십시오. 그렇지 않으면 결과가 오름차순으로 정렬됩니다. | `orderby=created` |
| `property` | 반환하기 위해 객체가 충족해야 하는 비교 표현식을 나타냅니다. | `property=deleted==false` |

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(**&amp;**)로 구분해야 합니다.

## Python CPU 및 GPU 구성 {#cpu-gpu-config}

Python Engine은 교육 또는 채점 목적으로 CPU 또는 GPU 중에서 선택할 수 있으며 작업 사양(`tasks.specification`)으로 [MLInstance](./mlinstances.md)에 정의됩니다.

다음은 트레이닝용 CPU 및 채점용 GPU를 사용하는 예를 지정하는 구성입니다.

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
>`cpus` 및 `gpus` 값은 CPU 또는 GPU 수를 의미하지 않고 실제 컴퓨터 수를 나타냅니다. 이 값들은 권한 있게 `"1"`되며 그렇지 않으면 예외가 발생합니다.

## PySpark 및 Spark 리소스 구성 {#resource-config}

Spark Engine은 교육 및 채점 목적으로 컴퓨터 리소스를 수정할 수 있습니다. 이러한 리소스는 다음 표에 설명되어 있습니다.

| 리소스 | 설명 | 유형 |
| -------- | ----------- | ---- |
| driverMemory | 드라이버 메모리(MB) | int |
| driverCoes | 드라이버에서 사용하는 코어 수 | int |
| executorMemory | 유언집행자의 메모리(MB) | int |
| executorCoes | 실행자가 사용한 코어 수 | int |
| numExecuters | 수행자 수 | int |

리소스는 [MLInstance](./mlinstances.md)에 (A) 개별 교육 또는 채점 매개 변수로, 또는 (B) 추가 사양 개체(`specification`) 내에서 지정할 수 있습니다. 예를 들어 다음 리소스 구성은 교육 및 점수 모두에 대해 동일합니다.

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
