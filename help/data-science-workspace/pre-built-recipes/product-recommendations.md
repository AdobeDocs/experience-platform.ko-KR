---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 제품 추천 레시피
topic: overview
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 3%

---


# 제품 추천 레시피

제품 Recommendations 레서피를 사용하면 고객의 요구 사항과 관심사에 맞는 맞춤형 제품 추천을 제공할 수 있습니다. 정확한 예측 모델을 통해 고객의 구매 내역을 통해 고객이 관심을 가질 수 있는 제품에 대한 통찰력을 얻을 수 있습니다.

## 이 레시피는 누구를 위해 만든 것입니까?

오늘날 소매업체는 다양한 제품을 제공하여 고객에게 다양한 선택권을 제공하여 고객의 검색을 방해할 수 있습니다. 시간과 노력 제약으로 인해 고객은 원하는 제품을 찾을 수 없어 인지 장애 수준이 높거나 구매를 전혀 하지 않는 제품을 구입할 수 있습니다.

## 이 레시피는 어떤 역할을 합니까?

제품 Recommendations 레서피 업체는 기계 학습을 통해 과거 제품과 고객의 상호 작용을 분석하고 개인화된 제품 추천 목록을 신속하고 쉽게 생성합니다. 제품 검색 프로세스를 최적화하여 고객을 장기적으로 비생산적이고 불필요한 검색을 제거합니다. 그 결과 제품 Recommendations 레서피는 고객의 전체 구매 경험을 향상시킬 수 있으므로 고객 참여도가 높아지고 브랜드 충성도가 높아집니다.

## 시작하려면 어떻게 해야 합니까?

Adobe Experience Platform Lab 자습서를 따라 시작할 수 있습니다(아래 Lab 링크 참조). 이 자습서에서는 레서피 워크플로우에 대한 [노트북에 따라 레서피](../jupyterlab/create-a-recipe.md) 워크플로우를 수행하고 레서피 레시피를 구현하여 Jupiter 노트북에서 제품 Recommendations 레서피 [!DNL Experience Platform] 를 만드는 방법을 설명합니다 [!DNL Data Science Workspace].

* [랩: 데이터 과학 작업 공간에서 미래 예측](https://expleague.azureedge.net/labs/L777/index.html)
* [랩 리소스](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 데이터 스키마

이 레시피는 사용자 지정 [XDM 스키마를](../../xdm/schema/field-dictionary.md) 사용하여 입력 및 출력 데이터를 모델링합니다.

### 입력 데이터 스키마

| 필드 이름 | 유형 |
--- | ---
| itemId | 문자열 |
| interactionType | 문자열 |
| timestamp | 문자열 |
| userId | 문자열 |

### 출력 데이터 스키마

| 필드 이름 | 유형 |
--- | ---
| recommendations | 문자열 |
| userId | 정수 |

## 알고리즘

제품 Recommendations 레서피는 공동 필터링 기능을 활용하여 고객을 위한 제품 권장 사항의 개인화된 목록을 생성합니다. 컨텐츠 기반 접근 방식과 달리 협업 필터링은 특정 제품에 대한 정보를 필요로 하지 않고 제품 세트에 대한 고객의 이전 기본 설정을 활용합니다. 이 강력한 권장 사항 기술은 다음과 같은 두 가지 간단한 가정을 사용합니다.
* 비슷한 관심사를 가진 고객이 있으며 구매 및 탐색 행동을 비교하여 그룹화할 수 있습니다.
* 고객은 구매 및 탐색 행동과 관련하여 유사한 고객을 기반으로 한 권장 사항에 더 많은 관심을 가질 수 있습니다.

이 과정은 두 가지 주요 단계로 나누어져 있다. 먼저 유사한 고객의 하위 집합을 정의합니다. 그런 다음 해당 세트에서 타겟 고객에 대한 권장 사항을 반환하기 위해 이러한 고객 간의 유사한 기능을 식별합니다.