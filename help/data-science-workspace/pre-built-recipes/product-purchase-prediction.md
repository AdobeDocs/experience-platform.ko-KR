---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 제품 구매 방법
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 제품 구매 방법

## 개요

제품 구매 예측 레서피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)의 가능성을 예측할 수 있습니다.

![](../images/pre-built-recipes/ppp_bigpicture.png)

다음 문서는 다음과 같은 질문에 응답합니다.
* 이 레시피는 누구를 위해 만든 것입니까?
* 이 레시피는 어떤 역할을 합니까?

## 이 레시피는 누구를 위해 만든 것입니까?

브랜드는 고객에게 효과적이고 대상화된 프로모션을 통해 제품 라인의 분기별 매출을 증대시키고자 합니다. 그러나 모든 고객이 동일하지는 않으며 원하는 가치가 있습니다. 누구를 타깃팅하니? 프로모션을 중단시키지 않고 응답할 가능성이 가장 높은 고객은 누구입니까? 각 고객에 맞게 프로모션을 어떻게 맞춤화할 수 있습니까? 어떤 채널을 이용해야 하며 언제 프로모션을 진행해야 합니까?

## 이 레시피는 어떤 역할을 합니까?

제품 구매 예측 레서피는 머신 러닝을 활용하여 고객 구매 행동을 예측합니다. 이는 사용자 지정된 임의 포리스트 분류자와 두 개의 계층의 경험 데이터 모델(XDM)을 적용하여 구매 이벤트의 가능성을 예측함으로써 이루어집니다. 이 모델은 고객 프로파일 정보와 과거 구매 내역이 포함된 입력 데이터를 활용하며 데이터 과학자가 예측의 정확도를 높이기 위해 사전에 결정한 구성 매개 변수에 대한 기본값을 활용합니다.

## 데이터 스키마

이 레시피는 [XDM 스키마를](../../xdm/home.md) 사용하여 데이터를 모델링합니다. 이 레서피에 사용된 스키마는 다음과 같습니다.

| 필드 이름 | 유형 |
--- | ---
| userId | 문자열 |
| genderRatio | 숫자 |
| ageY | 숫자 |
| ageM | 숫자 |
| optinEmail | 부울 |
| optinMobile | 부울 |
| optinAddress | 부울 |
| created | 정수 |
| totalOrders | 숫자 |
| totalItems | 숫자 |
| orderDate1 | 숫자 |
| shippingDate1 | 숫자 |
| totalPrice1 | 숫자 |
| tax1 | 숫자 |
| orderDate2 | 숫자 |
| shippingDate2 | 숫자 |
| totalPrice2 | 숫자 |


## 알고리즘

먼저 ProductPrediction *스키마의 교육* 데이터 세트가 로드됩니다. 여기서 모델은 [무작위 포리스트 분류자를 사용하여 교육됩니다](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). 임의 포리스트 분류자는 향상된 예측 성능을 얻기 위해 여러 알고리즘을 결합하는 통합 알고리즘 유형입니다. 알고리즘 뒤의 아이디어는 임의 포리스트 분류기가 여러 결정 트리를 만들고 이를 병합하여 보다 정확하고 안정적인 예측을 만든다는 것입니다.

이 프로세스는 교육 데이터의 하위 집합을 임의로 선택하는 의사 결정 트리 집합을 만들기 시작합니다. 그 후 각 의사 결정 트리의 결과는 평균으로 계산됩니다.