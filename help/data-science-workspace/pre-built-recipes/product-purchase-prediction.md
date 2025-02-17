---
keywords: Experience Platform;제품 구매 레시피;Data Science Workspace;인기 주제;레시피;사전 빌드 레시피
solution: Experience Platform
title: 제품 구매 예측 레서피
description: '제품 구매 예측 레시피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)의 가능성을 예측할 수 있습니다.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 5%

---

# 제품 구매 예측 레서피

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

제품 구매 예측 레시피를 사용하면 특정 유형의 고객 구매 이벤트(예: 제품 구매)의 가능성을 예측할 수 있습니다.

![](../images/pre-built-recipes/ppp_bigpicture.png)

다음 문서는 다음과 같은 질문에 답합니다.
* 이 요리법은 누구를 위해 만들어졌나요?
* 이 요리법은 어떤 역할을 하나요?

## 이 요리법은 누구를 위해 만들어졌나요?

귀하의 브랜드는 고객을 대상으로 효과적이고 타기팅된 프로모션을 통해 제품 라인의 분기별 매출을 늘리려고 합니다. 그러나 모든 고객이 다 같은 것은 아니며 당신은 당신의 돈의 가치를 원합니다. 누구를 타겟으로 합니까? 고객 중 어떤 고객이 프로모션에 방해가 되지 않는다는 사실을 발견하지 않고 가장 효과적으로 대응할 수 있습니까? 각 고객에 대한 프로모션을 어떻게 사용자 정의합니까? 어떤 채널을 사용해야 하며 언제 프로모션을 보내야 합니까?

## 이 요리법은 어떤 역할을 하나요?

제품 구매 예측 레시피는 고객 구매 행동을 예측하기 위해 머신 러닝을 활용한다. 이는 사용자 지정된 랜덤 포레스트 분류자와 2계층 XDM(경험 데이터 모델)을 적용하여 구매 이벤트의 확률을 예측하여 수행됩니다. 이 모델은 고객 프로필 정보와 과거 구매 내역을 포함하는 입력 데이터를 활용하며 데이터 과학자가 결정한 사전 결정된 구성 매개 변수로 기본값을 설정하여 예측 정확도를 향상시킵니다.

## 데이터 스키마

이 레시피는 [XDM 스키마](../../xdm/home.md)를 사용하여 데이터를 모델링합니다. 이 레시피에 사용되는 스키마는 아래에 표시되어 있습니다.

| 필드 이름 | 유형 |
| --- | --- |
| userId | 문자열 |
| 성별 비율 | 숫자 |
| Y세 | 숫자 |
| ageM | 숫자 |
| 이메일 선택 | 부울 |
| optinMobile | 부울 |
| optinAddress | 부울 |
| 생성됨 | 정수 |
| 합계 주문 수 | 숫자 |
| 전체 항목 수 | 숫자 |
| orderDate1 | 숫자 |
| shippingDate1 | 숫자 |
| totalPrice1 | 숫자 |
| tax1 | 숫자 |
| orderDate2 | 숫자 |
| shippingDate2 | 숫자 |
| totalPrice2 | 숫자 |


## 알고리즘

먼저 *ProductPrediction* 스키마의 교육 데이터 세트가 로드됩니다. 여기서 모델은 [랜덤 포리스트 분류기](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)를 사용하여 학습됩니다. 랜덤 포레스트 분류기는 개선된 예측 성능을 얻기 위해 다수의 알고리즘을 결합하는 알고리즘을 가리키는, 일종의 혼재 알고리즘이다. 알고리즘 이면의 아이디어는 랜덤 포레스트 분류기가 여러 개의 결정 트리를 작성하고 병합하여 보다 정확하고 안정적인 예측을 만든다는 것이다.

이 프로세스는 트레이닝 데이터의 하위 집합을 무작위로 선택하는 결정 트리의 세트를 생성하는 것으로 시작한다. 이후 각 의사 결정 트리에 대한 결과를 평균한다.
