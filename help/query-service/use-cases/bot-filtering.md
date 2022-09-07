---
title: 기계 학습을 사용하여 쿼리 서비스에서 보트 필터링
description: 이 문서에서는 Query Service 및 기계 학습을 사용하여 보트 활동을 확인하고 실제 온라인 웹 사이트 방문자 트래픽에서 작업을 필터링하는 방법에 대한 개요를 제공합니다.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: 8a7c04ebe8fe372dbf686fddc92867e938a93614
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# 에서 보트 필터링 [!DNL Query Service] 기계 학습

보트 활동은 분석 지표에 영향을 주고 데이터 무결성에 영향을 줄 수 있습니다. Adobe Experience Platform [!DNL Query Service] 보트 필터링 프로세스를 통해 데이터 품질을 유지하는 데 사용할 수 있습니다.

보트 필터링을 사용하면 사람이 아닌 웹 사이트와의 상호 작용으로 인한 데이터 오염을 광범위하게 제거하여 데이터 품질을 유지할 수 있습니다. 이 프로세스는 SQL 쿼리와 시스템 학습의 조합을 통해 수행됩니다.

보트 활동은 다양한 방법으로 식별할 수 있습니다. 이 문서에서 취해진 접근 방식은 지정된 기간 동안 사용자가 수행한 작업 수인 활동 스파이크에 중점을 둡니다. 처음에 SQL 쿼리는 일정 시간 동안 보트 활동으로 자격을 적용하기 위해 수행한 작업 수에 대한 임계값을 임의로 설정합니다. 그런 다음 기계 학습 모델을 사용하여 이 임계값을 동적으로 재정의하여 이 비율의 정확도를 높입니다.

이 문서에서는 SQL 보트 필터링 쿼리 및 사용자 환경에서 프로세스를 설정하는 데 필요한 기계 학습 모델에 대한 개요 및 자세한 예를 제공합니다.

## 시작하기

이 프로세스의 일부로 기계 학습 모델을 교육해야 하므로 이 문서에서는 하나 이상의 기계 학습 환경에 대한 작업 지식을 가정합니다.

이 예에서는 을 사용합니다 [!DNL Jupyter Notebook] 를 개발 환경으로 설정합니다. 여러 가지 옵션을 사용할 수 있지만, [!DNL Jupyter Notebook] 계산 요구 사항이 낮은 오픈 소스 웹 애플리케이션이므로 를 사용하는 것이 좋습니다. 그럴 수 있습니다 [공식 사이트에서 다운로드](https://jupyter.org/).

## 사용 [!DNL Query Service] 보트 활동에 대한 임계값을 정의하려면

보트 탐지를 위해 데이터를 추출하는 데 사용되는 두 가지 속성은 다음과 같습니다.

* Experience Cloud 방문자 ID(MCID라고도 함): 모든 Adobe 솔루션에서 방문자를 식별하는 범용 영구 ID를 제공합니다.
* 타임스탬프: 웹 사이트에서 활동이 발생한 UTC 형식의 시간 및 날짜를 제공합니다.

>[!NOTE]
>
>의 사용 `mcid` 아래 예와 같이 Experience Cloud 방문자 ID에 대한 네임스페이스 참조에서 여전히 찾을 수 있습니다.

다음 SQL 문은 보트 활동을 식별하는 초기 예를 제공합니다. 이 문에서는 방문자가 1분 내에 50번의 클릭을 수행하면 사용자가 봇이라고 가정합니다.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

표현식은 ECID(`mcid`) 임계값을 충족하지만 다른 간격의 트래픽 스파이크를 처리하지 않는 모든 방문자의 수입니다.

## 머신 러닝을 통해 보트 탐지 개선

초기 SQL 문을 재정의하여 기계 학습을 위한 기능 추출 쿼리로 만들 수 있습니다. 향상된 쿼리는 정확성이 높은 학습 모델을 위한 다양한 간격으로 더 많은 기능을 생성할 수 있습니다.

예제 문은 클릭 수가 300인 5분 및 30분을 포함하여 클릭 수가 각각 1800인 1분부터 확장됩니다.

example 문은 각 ECID에 대한 최대 클릭 수(`mcid`)을 클릭하여 제품에서 사용할 수 있습니다. 이 초기 문은 1분(60초), 5분(300초), 1시간(즉, 1800초) 기간을 포함하도록 확장되었습니다.

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

이 식의 결과는 아래 제공된 테이블과 유사할 수 있습니다.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2개 | 2개 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## 기계 학습을 사용하여 새로운 스파이크 임계값 식별

그런 다음 결과 쿼리 데이터 세트를 CSV 형식으로 내보내고 다음 로 가져옵니다 [!DNL Jupyter Notebook]. 이러한 환경에서 최신 기계 학습 라이브러리를 사용하여 기계 학습 모델을 교육할 수 있습니다. 자세한 내용은 문제 해결 안내서 를 참조하십시오 [데이터를 내보내는 방법 [!DNL Query Service] CSV 형식으로](../troubleshooting-guide.md#export-csv)

처음에 설정한 임시 스파이크 임계값은 데이터 중심의 임계값이 아니므로 정확도가 떨어집니다. 기계 학습 모델을 사용하여 매개변수를 임계값으로 교육할 수 있습니다. 그 결과, `GROUP BY` 불필요한 기능을 제거하여 키워드를 만듭니다.

이 예제에서는 기본적으로 [!DNL Jupyter Notebook]. 팬더 파이톤 라이브러리도 이곳에서 사용하기 위해 수입됩니다. 다음 명령이 [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

다음으로, 데이터 집합에 대한 의사 결정 트리 분류자를 교육하고 모델에서 나오는 논리를 관찰해야 합니다.

아래 예에서 &quot;Matplotlib&quot; 라이브러리는 의사 결정 트리 분류자를 시각화하는 데 사용됩니다.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

다음에서 반환된 값 [!DNL Jupyter Notebook] 이 예제는 다음과 같습니다.

```text
Model Accuracy: 0.99935
```

![통계적 출력 [!DNL Jupyter Notebook] 기계 학습 모델.](../images/use-cases/jupiter-notebook-output.png)

위의 예에 표시된 모델의 결과는 99% 정확합니다.

의사 결정 트리 분류기는 의 데이터를 사용하여 교육할 수 있습니다. [!DNL Query Service] 예약된 쿼리를 사용하는 일반 케이던스에서는 보트 활동을 높은 정확도로 필터링하여 데이터 무결성을 보장할 수 있습니다. 기계 학습 모델에서 파생된 매개변수를 사용하여 원래 질의를 모델에서 생성한 매우 정확한 매개변수로 업데이트할 수 있습니다.

5분 안에 상호 작용이 130개 이상인 방문자는 보트라는 정확도가 높은 예제 모델을 확인했습니다. 이제 이 정보를 사용하여 보트 필터링 SQL 쿼리를 구체화할 수 있습니다.

## 다음 단계

이 문서를 읽으면 사용 방법을 더 잘 이해할 수 있습니다 [!DNL Query Service] 보트 활동을 결정하고 필터링하는 기계 학습을 살펴보십시오.

다음과 같은 이점을 보여주는 기타 문서 [!DNL Query Service] 조직의 전략적 비즈니스 인사이트는 [중단된 찾아보기 사용 사례](./abandoned-browse.md) 예.
