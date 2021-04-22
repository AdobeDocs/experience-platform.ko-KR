---
keywords: Experience Platform;제품 구입 레서피;데이터 과학 작업 공간;인기 있는 주제;레서피;사전 작성 레서피;;product purchase recipe;Data Science Workspace;popular topics;recipes;pre build recipe
solution: Experience Platform
title: 제품 구매 예측 레서피
topic-legacy: overview
description: '제품 구매 예측 레서피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)를 예측할 수 있습니다.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 제품 구매 예측 레서피

제품 구매 예측 레서피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)를 예측할 수 있습니다.

![](../images/pre-built-recipes/ppp_bigpicture.png)

다음 문서는 다음과 같은 질문에 응답합니다.
* 이 레시피는 누구를 위해 만들어졌는가?
* 이 조리법은 어떤 역할을 합니까?

## 이 레시피는 누구를 위해 만들어졌는가?

브랜드는 고객에게 효과적이고 타깃팅된 프로모션을 통해 제품 라인의 분기별 매출을 높이고자 합니다. 그러나 모든 고객들은 다 똑같지 않고 여러분은 돈의 가치를 원한다. 누구를 타깃팅하니? 프로모션 관련 정보를 파악하지 않고 응답하는 고객 중 가장 많은 고객은 누구입니까? 각 고객에 대한 프로모션을 어떻게 맞춤화할 수 있습니까? 어떤 채널을 이용해야 하며 언제 프로모션을 보내야 합니까?

## 이 조리법은 어떤 역할을 합니까?

제품 구매 예측 레서피는 머신 러닝을 활용하여 고객의 구매 행동을 예측합니다. 이는 사용자 지정된 임의 포리스트 분류자와 2개의 계층의 경험 데이터 모델(XDM)을 적용하여 구매 이벤트의 가능성을 예측함으로써 발생합니다. 이 모델은 예측 정확도를 높이기 위해 Adobe Data Sciences에서 결정한 사전 결정된 구성 매개 변수에 고객 프로파일 정보와 이전 구매 내역과 기본값을 결합한 입력 데이터를 활용합니다.

## 데이터 스키마

이 레시피는 [XDM 스키마](../../xdm/home.md)를 사용하여 데이터를 모델링합니다. 이 레서피에 사용된 스키마는 다음과 같습니다.

| 필드 이름 | 유형 |
| --- | --- |
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
| 세금1 | 숫자 |
| orderDate2 | 숫자 |
| shippingDate2 | 숫자 |
| totalPrice2 | 숫자 |


## 알고리즘

먼저 *ProductPrediction* 스키마의 교육 데이터 세트가 로드됩니다. 여기서 모델은 [임의 포리스트 분류자](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)를 사용하여 교육됩니다. 임의 포리스트 분류자는 개선된 예측 성능을 얻기 위해 여러 알고리즘을 결합하는 조합 알고리즘 유형입니다. 알고리즘 뒤의 아이디어는 임의 포리스트 분류자가 여러 의사 결정 트리를 만들고 이를 병합하여 보다 정확하고 안정적인 예측을 만든다는 것입니다.

이 프로세스는 교육 데이터의 하위 세트를 임의로 선택하는 일련의 결정 트리를 만들기 시작합니다. 그 후 각 의사 결정 트리의 결과는 평균으로 계산됩니다.
