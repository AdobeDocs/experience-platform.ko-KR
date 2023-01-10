---
keywords: Experience Platform;제품 구매 레서피;데이터 과학 작업 공간;인기 항목;레서피;사전 작성 레서피
solution: Experience Platform
title: 제품 구매 예측 레서피
description: '제품 구매 예측 레서피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)가 발생할 가능성을 예측할 수 있습니다.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 제품 구매 예측 레서피

제품 구매 예측 레서피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)가 발생할 가능성을 예측할 수 있습니다.

![](../images/pre-built-recipes/ppp_bigpicture.png)

다음 문서는 다음과 같은 질문에 답변합니다.
* 이 요리법은 누구를 위해 만들어진 건가요?
* 이 조리법은 어떤 역할을 합니까?

## 이 요리법은 누구를 위해 만들어진 건가요?

브랜드는 고객에게 효과적이고 타깃팅된 프로모션을 통해 제품 라인의 분기별 매출을 증대하려고 합니다. 하지만, 모든 고객이 다 똑같고, 돈을 원하는 것은 아니다. 누구를 목표로 하고 있습니까? 프로모션 중단 없이 응답할 가능성이 가장 높은 고객은 무엇입니까? 각 고객에게 프로모션을 사용자 지정하는 방법은 무엇입니까? 어떤 채널을 사용해야 하며 언제 프로모션을 내보내야 합니까?

## 이 조리법은 어떤 역할을 합니까?

제품 구매 예측 레서피는 기계 학습을 사용하여 고객 구매 행동을 예측합니다. 이 작업은 사용자 지정된 랜덤 포레스트 분류자와 2계층 XDM(Experience Data Model)을 적용하여 구매 이벤트의 확률을 예측하여 수행합니다. 이 모델은 고객 프로필 정보와 과거 구매 내역이 포함된 입력 데이터를 활용하며, 기본값은 Data Sciences에서 결정하는 사전 결정된 구성 매개 변수로 사용되어 예측 정확도를 높입니다.

## 데이터 스키마

이 조리법은 [XDM 스키마](../../xdm/home.md) 데이터를 모델링하는 데 사용됩니다. 이 레서피에 사용된 스키마가 아래에 표시됩니다.

| 필드 이름 | 유형 |
| --- | --- |
| userId | 문자열 |
| genderRatio | 숫자 |
| ageY | 숫자 |
| ageM | 숫자 |
| optinEmail | 부울 |
| optinMobile | 부울 |
| optinAddress | 부울 |
| 생성됨 | 정수 |
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

먼저, *제품 예측* 스키마가 로드되었습니다. 여기서 모델은 [random forest 분류기](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Random Forest 분류는 향상된 예측 성능을 얻기 위해 여러 알고리즘을 결합하는 알고리즘을 참조하는 조합 알고리즘 유형입니다. 알고리즘 이면의 아이디어는 무작위 포리스트 분류기가 여러 의사 결정 트리를 만들고 병합하여 보다 정확하고 안정적인 예측을 만든다는 것입니다.

이 프로세스는 교육 데이터의 하위 집합을 임의로 선택하는 의사 결정 트리 집합을 만드는 것으로 시작합니다. 그런 다음 각 의사 결정 트리의 결과를 평균합니다.
