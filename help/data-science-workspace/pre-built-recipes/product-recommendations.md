---
keywords: Experience Platform;제품 추천 레시피;Data Science Workspace;인기 주제;레시피;사전 빌드 레시피
solution: Experience Platform
title: 제품 추천 레시피
description: Product Recommendations 레시피를 통해 고객의 요구 사항과 관심사에 맞게 개인화된 제품 추천을 제공할 수 있습니다. 고객의 구매 내역은 정확한 예측 모델을 통해 고객이 관심을 가질 수 있는 제품에 대한 통찰력을 제공할 수 있습니다.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# 제품 추천 레시피

Product Recommendations 레시피를 통해 고객의 요구 사항과 관심사에 맞게 개인화된 제품 추천을 제공할 수 있습니다. 고객의 구매 내역은 정확한 예측 모델을 통해 고객이 관심을 가질 수 있는 제품에 대한 통찰력을 제공할 수 있습니다.

## 이 요리법은 누구를 위해 만들어졌나요?

현대에 유통업체는 고객에게 선택의 폭을 넓혀 고객 검색에 지장을 줄 수 있는 다양한 제품을 제공할 수 있습니다. 시간과 노력의 제약으로 인해 고객이 원하는 제품을 찾지 못해 인지부조화 정도가 심한 구매를 하거나 아예 구매하지 않을 수 있다.

## 이 요리법은 어떤 역할을 하나요?

Product Recommendations 레시피는 머신 러닝을 사용하여 과거 제품에 대한 고객의 상호 작용을 분석하고, 빠르고 간편하게 개인화된 제품 권장 사항 목록을 생성합니다. 이를 통해 제품 검색 프로세스를 최적화하고 고객을 위한 길고 비생산적이고 관련없는 검색을 제거할 수 있습니다. 결과적으로 Product Recommendations 레시피는 고객의 전반적인 구매 경험을 개선하여 참여도를 높이고 브랜드 충성도를 강화할 수 있습니다.

## 시작하려면 어떻게 해야 합니까?

Adobe Experience Platform Lab 자습서를 따라 시작할 수 있습니다(아래 랩 링크 참조). 이 튜토리얼에서는 다음을 따라 Jupyter Notebook에서 Product Recommendations 레시피를 만드는 방법을 보여줍니다. [조리법 전자 필기장](../jupyterlab/create-a-model.md) 워크플로 및 의 레시피 구현 [!DNL Experience Platform] [!DNL Data Science Workspace].

* [랩: 데이터 과학 작업 영역을 통해 미래 예측](https://expleague.azureedge.net/labs/L777/index.html)
* [랩 리소스](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 데이터 스키마

이 레시피는 사용자 지정 [XDM 스키마](../../xdm/schema/field-dictionary.md) 입력 및 출력 데이터를 모델링하려면 다음을 수행합니다.

### 입력 데이터 스키마

| 필드 이름 | 유형 |
| --- | --- |
| itemId | 문자열 |
| interactionType | 문자열 |
| timestamp | 문자열 |
| userId | 문자열 |

### 출력 데이터 스키마

| 필드 이름 | 유형 |
| --- | --- |
| 권장 사항 | 문자열 |
| userId | 정수 |

## 알고리즘

Product Recommendations 레시피는 협업 필터링을 활용하여 고객을 위한 개인화된 제품 권장 사항 목록을 생성합니다. 협업 필터링은 콘텐츠 기반 접근 방식과 달리 특정 제품에 대한 정보가 필요하지 않으며 제품 세트에 대한 고객의 과거 환경 설정을 활용합니다. 이 강력한 권장 사항 기법은 다음 두 가지 간단한 가정을 사용합니다.
* 관심사가 비슷한 고객이 있고, 구매 행동과 탐색 행동을 비교하며 묶을 수 있다.
* 고객은 구매 및 탐색 행동과 관련하여 유사한 고객을 기반으로 한 추천에 관심을 가질 가능성이 높습니다.

이 프로세스는 두 가지 주요 단계로 분류됩니다. 먼저 유사한 고객의 하위 집합을 정의합니다. 그런 다음 해당 세트 내에서 대상 고객에 대한 추천을 반환하기 위해 해당 고객 간에 유사한 기능을 식별합니다.
