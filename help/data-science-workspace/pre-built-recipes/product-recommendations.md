---
keywords: Experience Platform;제품 추천 레서피;데이터 과학 작업 공간;인기 항목;레서피;사전 작성 레서피
solution: Experience Platform
title: 제품 추천 레서피
description: 제품 Recommendations 레서피를 사용하면 고객의 요구 사항과 관심사에 맞는 개인화된 제품 추천을 제공할 수 있습니다. 정확한 예측 모델을 통해 고객의 구매 내역을 통해 고객이 관심이 있는 제품에 대한 통찰력을 얻을 수 있습니다.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# 제품 추천 레서피

제품 Recommendations 레서피를 사용하면 고객의 요구 사항과 관심사에 맞는 개인화된 제품 추천을 제공할 수 있습니다. 정확한 예측 모델을 통해 고객의 구매 내역을 통해 고객이 관심이 있는 제품에 대한 통찰력을 얻을 수 있습니다.

## 이 요리법은 누구를 위해 만들어진 건가요?

오늘날 소매업체는 다양한 제품을 제공할 수 있어 고객에게 다양한 선택을 제공하고 고객의 검색을 방해할 수 있습니다. 시간과 노력 제약으로 인해 고객은 원하는 제품을 찾을 수 없으므로 높은 수준의 인지 장애 또는 구매가 전혀 없는 제품을 구매할 수 있습니다.

## 이 조리법은 어떤 역할을 합니까?

제품 Recommendations 레서피 는 기계 학습을 사용하여 고객의 과거 제품과 상호 작용을 분석하고 개인화된 제품 추천 목록을 빠르고 쉽게 생성합니다. 따라서 제품 검색 프로세스를 최적화하고 장기간 비생산적이고 무관한 검색을 수행할 수 있습니다. 그 결과, 제품 Recommendations 레서피는 고객의 전체 구매 경험을 개선하여 참여도가 높아지고 브랜드 충성도가 향상될 수 있습니다.

## 시작하려면 어떻게 해야 합니까?

Adobe Experience Platform Lab 자습서를 따라 시작할 수 있습니다(아래 Lab 링크 참조). 이 튜토리얼에서는 다음을 수행하여 Jupiter 노트북에서 Product Recommendations 레서피를 만드는 방법을 보여 줍니다. [레서피](../jupyterlab/create-a-model.md) 워크플로우 및 레서피 구현 [!DNL Experience Platform] [!DNL Data Science Workspace].

* [랩: 데이터 과학 작업 공간으로 미래 예측](https://expleague.azureedge.net/labs/L777/index.html)
* [랩 리소스](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 데이터 스키마

이 레서피는 사용자 정의 [XDM 스키마](../../xdm/schema/field-dictionary.md) 입력 및 출력 데이터를 모델링하려면

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

제품 Recommendations 레서피는 협업 필터링을 사용하여 고객을 위한 개인화된 제품 권장 사항 목록을 생성합니다. 컨텐츠 기반 접근 방식과 달리 협업 필터링은 특정 제품에 대한 정보가 필요하지 않고 제품 세트에 대한 고객의 과거 환경 설정을 활용합니다. 이 강력한 권장 사항 기법은 다음과 같은 두 가지 간단한 가정을 사용합니다.
* 비슷한 관심사를 갖는 고객이 있으며 구매 및 탐색 행동을 비교하여 그룹화할 수 있습니다.
* 고객은 구매 및 탐색 행동에 관하여 유사한 고객을 기반으로 한 추천에 더 관심이 있을 것입니다.

이 프로세스는 두 가지 주요 단계로 분류됩니다. 먼저 유사한 고객 하위 집합을 정의합니다. 그런 다음 해당 세트 내에서 대상 고객에 대한 권장 사항을 반환하기 위해 해당 고객 간의 유사한 기능을 식별합니다.
