---
keywords: Experience Platform;홈;데이터 과학 작업 공간;인기 항목;데이터 과학 작업 공간;데이터 과학
solution: Experience Platform
title: 데이터 과학 작업 공간 개요
topic-legacy: overview
description: 이 안내서에서는 Adobe Experience Platform의 데이터 과학 작업 공간과 관련된 주요 개념에 대한 개요를 제공합니다.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# Data Science Workspace 개요

Adobe Experience Platform [!DNL Data Science Workspace] 에서는 기계 학습 및 인공 지능을 사용하여 데이터로부터 통찰력을 제공합니다. Adobe Experience Platform에 통합, [!DNL Data Science Workspace] 은 Adobe 솔루션에서 콘텐츠 및 데이터 자산을 사용하여 예측을 하는 데 도움이 됩니다.

모든 기술 수준의 데이터 과학자들은 머신 러닝 레서피 개발, 교육 및 조정을 지원하는 정교하고 사용하기 쉬운 도구를 발견할 것입니다. 이는 복잡한 작업 없이 AI 기술의 모든 이점입니다.

사용 [!DNL Data Science Workspace], 데이터 과학자들은 기계 학습을 기반으로 지능형 서비스 API를 쉽게 생성할 수 있습니다. 이러한 서비스는 Adobe Target, Adobe Analytics Cloud 등 다른 Adobe 서비스와 연동하여 웹, 데스크탑 및 모바일 앱에서 개인화된 타깃팅된 디지털 경험을 자동화할 수 있습니다.

이 안내서에서는 와 관련된 주요 개념에 대한 개요를 제공합니다 [!DNL Data Science Workspace].

## 소개

오늘날의 기업에서는 고객 경험을 개인화하고 고객 및 비즈니스에 더 많은 가치를 제공하는 데 도움이 되는 예측 및 인사이트를 위한 빅 데이터를 마이닝 하는 데 우선 순위를 둡니다.
무엇보다 중요한 것은 데이터에서 인사이트로 들어오는 것은 비용이 많이 든다는 것입니다. 일반적으로 지능적인 서비스를 제공하는 기계 학습 모델 또는 레시피를 개발하려면 집중적이고 시간이 많이 소요되는 데이터 연구를 수행하는 숙련된 데이터 과학자들이 필요합니다. 그 과정은 길고, 그 기술은 복잡하며, 숙련된 데이터 과학자들은 찾기 어려울 수 있습니다.

사용 [!DNL Data Science Workspace], Adobe Experience Platform을 사용하면 기업 전체에 경험 중심의 AI를 구축하여 데이터-to-insights를 효율적으로 신속하게 처리할 수 있습니다.
- 머신 러닝 프레임워크 및 런타임
- Adobe Experience Platform에 저장된 데이터에 대한 통합 액세스
- 구축된 통합 데이터 스키마 [!DNL Experience Data Model] (XDM)
- 머신 러닝/AI 및 빅 데이터 세트 관리에 필수적인 컴퓨팅 능력
- AI 기반의 경험으로 도약하기 위한 사전 빌드된 기계 학습 레서피
- 다양한 기술 수준의 데이터 과학자를 위한 레서피 작성, 재사용 및 수정 간소화
- 개발자 없이 몇 번의 클릭으로 지능적인 서비스 게시 및 공유, 개인화된 고객 환경을 지속적으로 최적화하기 위한 모니터링 및 재교육

모든 기술 수준의 데이터 과학자들은 보다 신속하게 통찰력을 얻을 수 있고 보다 효과적인 디지털 경험을 더 빨리 얻을 수 있습니다.

## 시작하기

세부 사항으로 들어가기 전에 [!DNL Data Science Workspace], 주요 용어에 대한 간단한 요약은 다음과 같습니다.

| 용어 | 정의 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] within [!DNL Experience Platform] 는 고객이 데이터를 활용하여 기계 학습 모델을 만들 수 있도록 지원합니다 [!DNL Experience Platform] 및 Adobe 솔루션을 사용하여 지능형 인사이트와 예측을 생성함으로써 유쾌한 최종 사용자 디지털 경험을 구축할 수 있습니다. |
| 인공 지능 | 인공 지능은 시각 인식, 음성 인식, 의사 결정, 언어 간의 번역과 같이 인간의 지능을 필요로 하는 작업을 수행할 수 있는 컴퓨터 시스템의 이론과 개발입니다. |
| 기계 학습 | 기계 학습은 컴퓨터가 명시적으로 프로그램되지 않고 배울 수 있도록 하는 학습 분야입니다. |
| [!DNL Sensei] ML 프레임워크 | [!DNL Sensei] ML Framework는 Adobe에서 데이터를 활용하는 통합 기계 학습 프레임워크입니다 [!DNL Experience Platform] 데이터 과학자들이 머신 러닝 기반의 인텔리전스 서비스 개발에 더 빠르고 확장 가능하며 재사용 가능한 방식으로 능력을 발휘할 수 있도록 합니다. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)은 Adobe이 다음과 같은 표준 스키마를 정의하기 위한 표준화 작업입니다 [!DNL Profile] 및 [!DNL ExperienceEvent], 고객 경험 관리를 위해 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 는 Project Jupiter를 위한 오픈 소스 웹 기반 인터페이스로서 [!DNL Experience Platform]. |
| 레서피 | 레서피는 모델 사양에 대한 Adobe의 용어이며, 특정 기계 학습, AI 알고리즘 또는 알고리즘 앙상블, 처리 논리 및 훈련 모델을 구축 및 실행하는 데 필요한 구성을 나타내어 특정 비즈니스 문제를 해결하는 데 도움이 되는 최상위 컨테이너입니다. |
| 모델 | 모델은 비즈니스 사용 사례를 해결하기 위해 이전 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피의 예입니다. |
| 교육 | 교육은 레이블이 지정된 데이터를 통해 학습 패턴과 인사이트를 얻는 프로세스입니다. |
| 숙련된 모델 | 숙련된 모델은 모델 훈련 프로세스의 실행 가능한 결과를 나타내며, 모델 인스턴스에 트레이닝 데이터 세트가 적용되었습니다. 숙련된 모델은 이 모델에서 만들어지는 모든 지능형 웹 서비스에 대한 참조를 유지합니다. 숙련된 모델은 점수를 매기고 지능형 웹 서비스를 만드는 데 적합합니다. 훈련된 모델의 수정 사항을 새 버전으로 추적할 수 있습니다. |
| 점수 책정 | 점수는 숙련된 모델을 사용하여 데이터에서 통찰력을 생성하는 프로세스입니다. |
| 서비스 | 배포된 서비스는 API를 통해 인공 지능, 기계 학습 모델 또는 고급 알고리즘의 기능을 노출하여 다른 서비스 또는 애플리케이션에서 지능형 앱을 생성하는 데 사용할 수 있도록 합니다. |

다음 차트는 레서피, 모델, 교육 실행 및 점수부여 실행 간의 계층적 관계를 설명합니다.

![](./images/home/recipe_hiearchy_ui.png)

## [!DNL Data Science Workspace] 이해 

사용 [!DNL Data Science Workspace]로 지정하는 경우 데이터 과학자들은 대규모 데이터 세트에서 통찰력을 찾아내는 번거로운 프로세스를 간소화할 수 있습니다. 공용 머신 러닝 프레임워크 및 런타임을 기반으로 구축, [!DNL Data Science Workspace] 고급 워크플로우 관리, 모델 관리 및 확장성을 제공합니다. 지능형 서비스는 기계 학습 레서피 재사용을 지원하여 Adobe 제품 및 솔루션을 사용하여 만든 다양한 애플리케이션을 지원합니다.

### 원스톱 데이터 액세스

데이터는 AI와 머신 러닝을 기반으로 합니다.

[!DNL Data Science Workspace] 는 Data Lake를 비롯한 Adobe Experience Platform과 완전히 통합되었습니다. [!DNL Real-Time Customer Profile], 및 [!DNL Unified Edge]. 빅데이터 및 심층 학습 라이브러리와 함께 Adobe Experience Platform에 저장된 모든 조직 데이터를 한 번에 탐색할 수 있습니다. [!DNL Spark] ML 및 [!DNL TensorFlow]. 필요한 항목을 찾지 못할 경우 XDM 표준화된 스키마를 사용하여 데이터 세트를 섭취합니다.

### 사전 빌드된 기계 학습 레서피

[!DNL Data Science Workspace] 소매 판매 예측 및 예외 항목 탐지 등의 일반적인 비즈니스 요구에 대해 사전 빌드된 기계 학습 레서피를 포함하므로 데이터 과학자와 개발자는 처음부터 시작하지 않아도 됩니다. 현재 세 가지의 조리법이 제공되어 있고 [제품 구매 예측](./pre-built-recipes/product-purchase-prediction.md), [제품 추천](./pre-built-recipes/product-recommendations.md), 및 [소매 판매](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

선호하는 경우, 사전 빌드된 레서피를 필요에 맞게 조정하거나, 레서피를 가져오거나, 처음부터 시작하여 사용자 정의 레서피를 만들 수 있습니다. 그러나 레서피를 교육 및 하이퍼튜닝하고 나면 맞춤 지능형 서비스를 만들 때 개발자는 필요하지 않습니다. 몇 번의 클릭만으로 타겟팅되고 개인화된 디지털 경험을 만들 수 있습니다.

### 데이터 과학자에 중점을 둔 워크플로우

데이터 과학 분야의 전문 지식이 무엇이든 [!DNL Data Science Workspace] 은 데이터에서 통찰력을 찾아 디지털 경험에 적용하는 프로세스를 간소화하고 가속화하는 데 도움이 됩니다.

### 데이터 탐색

올바른 데이터를 찾고 준비하는 것은 효과적인 레시피를 만드는 데 있어 가장 많은 노동력이 필요한 부분입니다. [!DNL Data Science Workspace] 또한 Adobe Experience Platform을 사용하면 데이터를 통해 보다 신속하게 통찰력을 얻을 수 있습니다.

Adobe Experience Platform에서 크로스 채널 데이터는 중앙 집중화되고 XDM 표준화된 스키마에 저장되므로 데이터를 쉽게 찾고, 이해하고, 정리할 수 있습니다. 공통 스키마를 기반으로 한 단일 데이터 저장소를 사용하면 데이터 탐색 및 준비 시간을 수 없이 줄일 수 있습니다.

탐색하면서 R을 사용하십시오. [!DNL Python]또는 통합 호스팅 [!DNL Jupyter Notebook] 데이터 카탈로그를 찾아보려면 [!DNL Platform]. 이러한 언어 중 하나를 사용하면 [!DNL Spark] ML 및 TensorFlow입니다. 처음부터 새로 시작하거나 특정 비즈니스 문제에 대해 제공된 노트북 템플릿 중 하나를 사용하십시오.

데이터 탐색 워크플로우의 일부로, 새 데이터를 수집하거나 기존 기능을 사용하여 데이터 준비를 지원할 수도 있습니다.

### 작성

사용 [!DNL Data Science Workspace]를 채울 방법을 결정합니다.

- 현재 상태로 사용하거나 특정 요구 사항을 충족하도록 구성할 수 있는 사전 빌드된 레서피를 찾아보고 시간을 절약할 수 있습니다.
- Jupiter Notebook에서 작성 런타임을 사용하여 레서피를 처음부터 만들고 등록합니다.
- Adobe Experience Platform 외부에서 작성된 레서피를 [!DNL Data Science Workspace] 또는 다음과 같은 저장소에서 레서피 코드를 가져옵니다 [!DNL Git], 다음 사이에 사용 가능한 인증 및 통합을 사용하여 [!DNL Git] 및 [!DNL Data Science Workspace].

### 실험

Data Science Workspace는 실험 프로세스에 엄청난 유연성을 제공합니다. 조리법으로 시작하십시오. 그런 다음 동일한 코어 알고리즘을 사용하여 하이퍼튜닝 매개 변수와 같은 고유한 특성을 사용하여 별도의 인스턴스를 만듭니다. 필요한 만큼 인스턴스를 만들고, 각 인스턴스에 필요한 만큼 교육을 수행하고, 각 인스턴스를 원하는 만큼 채점할 수 있습니다. 훈련하면서 [!DNL Data Science Workspace] 평가 지표와 함께 레서피, 레서피 인스턴스 및 숙련된 인스턴스를 추적하므로 필요하지 않습니다.

### 운영

조리법에 만족하면 몇 번의 클릭만으로 지능형 서비스를 만들 수 있습니다. 코딩 필요 없음 - 개발자나 엔지니어를 등록하지 않고도 직접 코드를 작성할 수 있습니다. 마지막으로 지능형 서비스를 Adobe IO에 게시하면 디지털 경험 팀이 사용할 수 있습니다.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 지속적인 개선

[!DNL Data Science Workspace] intelligent services가 호출되는 위치와 서비스 수행 방식을 추적합니다. 데이터가 로드될 때 지능형 서비스 정확도를 평가하여 루프를 닫고 필요에 따라 레서피를 재교육하여 성능을 향상시킬 수 있습니다. 그 결과는 고객 개인화의 정확성을 지속적으로 개선합니다.

### 새로운 기능 및 데이터 세트에 대한 액세스

데이터 과학자들은 Adobe 서비스를 통해 새로운 기술과 데이터 세트를 사용할 수 있는 즉시 활용할 수 있습니다. Adobe에서는 잦은 업데이트를 통해 데이터 세트와 기술을 플랫폼에 통합하기 위해 작업하므로 별도의 작업이 필요하지 않습니다.

### 안전 및 마음의 평화

Adobe 시 데이터 보안이 최우선 과제입니다. Adobe은 업계에서 인정하는 표준, 규정 및 인증을 준수하는 데 도움이 되도록 개발된 보안 프로세스와 제어를 통해 데이터를 보호합니다.

보안 기능은 Adobe Secure Product Lifecycle의 일부로 소프트웨어 및 서비스에 내장되어 있습니다.
Adobe 데이터 및 소프트웨어 보안, 규정 준수 등에 대해 알아보려면 https://www.adobe.com/security.html 보안 페이지를 참조하십시오.

## [!DNL Data Science Workspace] 작업

예측 및 인사이트는 웹 사이트를 방문하거나 콜 센터에 문의하거나 다른 디지털 경험에 참여하는 각 고객에게 고도로 개인화된 경험을 전달하는 데 필요한 정보를 제공합니다. 다음은 일상적인 작업을 수행하는 방법입니다 [!DNL Data Science Workspace].

### 문제 정의

모든 것은 비즈니스 문제로 시작됩니다. 예를 들어, 온라인 콜센터는 부정적인 고객 감정을 긍정적으로 바꾸는 데 도움이 되도록 컨텍스트를 필요로 합니다.

고객에 대한 많은 데이터가 있습니다. 사이트를 탐색하고 장바구니에 항목을 넣고 심지어 주문을 했습니다. 그들은 이메일을 받거나, 쿠폰을 사용하거나, 이전에 콜 센터에 연락했을 수도 있습니다. 그런 다음, 레서피는 고객 및 해당 활동에 대해 사용할 수 있는 데이터를 사용하여 구매 경향을 결정하고 고객이 평가하고 사용할 가능성이 있는 오퍼를 추천해야 합니다.

![](./images/home/example_problem.png)

콜 센터 연락 시 고객은 여전히 장바구니에 두 쌍의 신발을 가지고 있지만 셔츠를 제거했습니다. 이러한 정보를 통해, 지능형 서비스는 콜 센터 에이전트가 통화 중에 신발을 20% 할인해줄 수 있는 쿠폰을 제공하는 것을 추천할 수 있습니다. 고객이 쿠폰을 사용하는 경우 해당 정보가 데이터 세트에 추가되고 다음에 고객이 전화할 때 예측이 더 잘 수행됩니다.

### 데이터 탐색 및 준비

정의된 비즈니스 문제를 기반으로 사이트 방문, 검색, 페이지 보기, 클릭한 링크, 장바구니 작업, 받은 오퍼, 이메일 수신, 콜 센터 상호 작용 등을 포함하여 모든 고객의 웹 트랜잭션을 레서피가 확인해야 한다는 것을 알고 있습니다.

데이터 과학자는 일반적으로 데이터를 탐색하고 변환하는 조리법을 만드는 데 필요한 시간의 최대 75%를 소비합니다. 데이터는 종종 여러 리포지토리에서 가져오고 다른 스키마에 저장됩니다. 레서피를 만드는 데 사용하려면 먼저 데이터를 결합하고 매핑해야 합니다.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

처음부터 새로 만들거나 기존 레서피를 구성하는 경우, 조직의 중앙 집중식 표준화된 데이터 카탈로그에서 데이터 검색을 시작하여 수집을 상당히 간소화합니다. 조직의 다른 데이터 과학자가 이미 유사한 데이터 세트를 식별했으며 처음부터 새로 시작하지 않고 해당 데이터 세트를 세부 조정하도록 선택할 수도 있습니다.
Adobe Experience Platform의 모든 데이터는 표준화된 XDM 스키마를 준수하므로 데이터를 결합하거나 데이터 엔지니어의 지원을 받기 위한 복잡한 모델을 만들 필요가 없습니다.

필요한 데이터를 즉시 찾지 못하지만 Adobe Experience Platform 외부에 있는 경우 추가 데이터 세트를 수집하는 것이 비교적 간단한 작업이며 이를 표준화된 XDM 스키마로도 변환할 수 있습니다.\
다음을 사용할 수 있습니다 [!DNL Jupyter Notebook] 데이터 사전 처리를 단순화하기 위해 - 이전에 구매 성향에 사용한 노트북 템플릿이나 노트북으로 시작할 수 있습니다.

![](./images/home/notebook_templates-new.png)

### 레시피 작성

만약 여러분이 이미 여러분의 모든 요구에 맞는 조리법을 발견했다면, 실험으로 옮길 수 있습니다. 또는 레서피를 약간 수정하거나 새로 만들 수 있습니다. 레서피를 이용하여 [!DNL Data Science Workspace] 런타임 작성 [!DNL Jupyter Notebook]. 작성 런타임을 사용하면 두 작업 모두에서 [!DNL Data Science Workspace] 교육 및 점수 책정 워크플로우를 실행하고 나중에 배합식을 변환하여 조직의 다른 사용자가 저장하고 재사용할 수 있습니다.

레서피를에 가져올 수도 있습니다. [!DNL Data Science Workspace] 또한 지능형 서비스를 만들 때 실험 워크플로우를 활용할 수 있습니다.

### 조리법을 실험해 보세요

핵심 기계 학습 알고리즘을 통합하는 레서피와 함께 많은 레서피 인스턴스를 단일 레서피로 만들 수 있습니다. 이러한 레서피 인스턴스는 모델이라고 합니다. 모델을 사용하려면 운영 효율성과 효율성을 최적화하기 위해 교육 및 평가가 필요하며, 일반적으로 시행착오와 오류로 구성된 프로세스입니다.

![](./images/home/recipe_hiearchy_ui.png)

모델을 교육하면 교육 실행 및 평가가 생성됩니다. [!DNL Data Science Workspace] 는 각 고유 모델 및 해당 교육 실행에 대한 평가 지표를 추적합니다. 실험을 통해 생성된 평가 지표를 통해 성과가 가장 좋은 교육 실행을 결정할 수 있습니다.

![](./images/home/evaluation_metrics.png)

다음 중 하나를 방문 [API](./models-recipes/train-evaluate-model-api.md) 또는 [UI](./models-recipes/train-evaluate-model-ui.md) 에서 모델을 교육하고 평가하는 방법에 대한 자습서 [!DNL Data Science Workspace].

### 모델 운영

비즈니스 요구 사항을 충족하기 위해 가장 잘 훈련된 레서피를 선택한 경우, [!DNL Data Science Workspace] 개발자 지원 없이 몇 번의 클릭만으로 코딩이 필요 없습니다. 게시된 지능형 서비스는 모델을 다시 작성하지 않고도 조직의 다른 구성원이 액세스할 수 있습니다.

게시된 지능형 서비스는 새로운 데이터를 사용할 수 있게 되면 수시로 자동으로 자체 트레이닝을 수행하도록 구성할 수 있습니다. 따라서 시간이 지남에 따라 서비스의 효율성과 효능이 유지됩니다.

## 다음 단계

[!DNL Data Science Workspace] 는 데이터 수집에서 알고리즘, 모든 기술 수준의 데이터 과학자를 위한 지능형 서비스에 이르기까지 데이터 과학 워크플로우를 간소화하고 단순화하는 데 도움이 됩니다. 정교한 도구 사용 [!DNL Data Science Workspace] 을 사용하면 데이터에서 인사이트로 이동하는 시간을 크게 단축할 수 있습니다.

더 중요한 건 [!DNL Data Science Workspace] 에서는 엔터프라이즈 데이터 과학자의 손에 Adobe의 선도적인 마케팅 플랫폼의 데이터 과학 및 알고리즘 최적화 기능을 제공합니다. 기업은 처음으로 독점 알고리즘을 플랫폼으로 가져오고, Adobe의 강력한 머신 러닝 및 AI 기능을 활용하여 개인화된 고객 경험을 대규모로 제공할 수 있습니다.

브랜드 전문 지식과 Adobe의 머신 러닝 및 AI 기량의 결합으로, 기업은 고객이 원하는 것을 고객에게 제공함으로써 더 많은 비즈니스 가치 및 브랜드 충성도를 높일 수 있습니다.

전체 일상적인 워크플로우와 같은 추가 정보를 보려면 [데이터 과학 작업 공간 둘러보기](./walkthrough.md) 설명서.

## 추가 리소스

다음 비디오는 사용자의 이해를 지원하도록 설계되었습니다 [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)