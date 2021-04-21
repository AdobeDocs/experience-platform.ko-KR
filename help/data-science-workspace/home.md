---
keywords: Experience Platform;홈;데이터 과학 작업 공간;인기 있는 주제;데이터 과학 작업 영역;데이터 과학;;home;data Science Workspace;popular topics
solution: Experience Platform
title: 데이터 과학 작업 공간 개요
topic-legacy: overview
description: 이 안내서에서는 Adobe Experience Platform의 데이터 과학 작업 공간과 관련된 주요 개념에 대한 개요를 제공합니다.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# 데이터 과학 작업 공간 개요

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 머신 러닝과 인공 지능을 사용하여 데이터로부터 인사이트를 도출합니다. Adobe Experience Platform에 통합된 [!DNL Data Science Workspace]은(는) Adobe 솔루션에서 컨텐츠와 데이터 자산을 사용하여 예측하는 데 도움이 됩니다.

기술 수준에 관계없이 모든 데이터 과학자는 복잡한 AI 기술 없이도 머신 러닝 레서피의 신속한 개발, 트레이닝 및 조정을 지원하는 세련되고 사용하기 쉬운 툴을 찾을 수 있습니다.

데이터 과학자는 [!DNL Data Science Workspace]을(를) 사용하여 머신 러닝 기반의 지능형 서비스 API를 쉽게 만들 수 있습니다. 이러한 서비스는 Adobe Target 및 Adobe Analytics Cloud을 비롯한 다른 Adobe 서비스와 연동되므로 웹, 데스크탑 및 모바일 앱에서 개인화된 대상화된 디지털 경험을 자동화할 수 있습니다.

이 안내서에서는 [!DNL Data Science Workspace]과(와) 관련된 주요 개념에 대한 개요를 제공합니다.

## 소개

오늘날 기업은 고객 경험을 개인화하고 고객과 기업에 더 많은 가치를 전달할 수 있는 예측과 인사이트를 얻기 위해 빅데이터를 수집하는 데 주력하고 있습니다.
데이터에서 인사이트로 이어지는 것은 비용이 많이 들 수 있습니다. 일반적으로 지능적인 서비스를 지원하는 기계 학습 모델 또는 레서피를 개발하려면 시간과 많은 시간이 소요되는 데이터 연구를 수행하는 숙련된 데이터 과학자들이 필요합니다. 그 과정은 길고, 기술은 복잡하고, 숙련된 데이터 과학자들은 찾기 어려울 수 있다.

[!DNL Data Science Workspace]을(를) 통해 Adobe Experience Platform을 사용하면 기업 전체에 경험 중심의 AI를 도입하여 데이터를 인사이트로 변환하는 과정을 능률화하고 가속화할 수 있습니다.
- 머신 러닝 프레임워크 및 런타임
- Adobe Experience Platform에 저장된 데이터에 대한 통합 액세스
- [!DNL Experience Data Model](XDM)을 기반으로 구축된 통합 데이터 스키마
- 머신 러닝/AI 및 빅데이터 세트 관리에 필요한 컴퓨팅 성능
- 인공 지능(AI) 기반의 경험으로 신속하게 발전할 수 있는 미리 만들어진 머신 러닝 방법
- 다양한 기술 수준의 데이터 과학자를 위한 레시피 작성, 재사용 및 수정 간소화
- 개발자 없이도 몇 번의 클릭만으로 지능적인 서비스 퍼블리싱 및 공유, 개인화된 고객 경험을 지속적으로 최적화할 수 있는 모니터링 및 재교육

모든 기술 수준에 속한 데이터 과학자는 보다 신속하게 인사이트를 확보하고 보다 효과적인 디지털 경험을 제공할 수 있습니다.

## 시작하기

[!DNL Data Science Workspace]의 세부 정보로 이동하기 전에 주요 용어의 간단한 요약을 제공합니다.

| 용어 | 정의 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] 이  [!DNL Experience Platform] 솔루션을 통해 고객은 지능형 통찰력과 예측을  [!DNL Experience Platform] 생성하여 매력적인 최종 사용자 디지털 경험을 만들 수 있습니다. |
| 인공 지능 | 인공 지능은 시각 인식, 음성 인식, 의사 결정, 언어 간 번역 등과 같이 인간의 지능을 필요로 하는 작업을 수행할 수 있는 컴퓨터 시스템의 이론과 개발입니다. |
| 기계 학습 | 기계 학습은 컴퓨터가 명시적으로 프로그래밍되지 않고 배울 수 있도록 하는 연구 분야이다. |
| [!DNL Sensei] ML 프레임워크 | [!DNL Sensei] ML Framework는 데이터 [!DNL Experience Platform] 를 활용하여 데이터 과학자들이 머신 러닝 기반의 인텔리전스 서비스를 신속하고 확장 가능하고 재사용 가능한 방식으로 개발할 수 있도록 하는 Adobe의 통합 머신 러닝 프레임워크입니다. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)은 Adobe이 고객 경험 관리에 대한 표준 스키마 [!DNL Profile] 와  [!DNL ExperienceEvent]같은 표준 스키마를 정의하기 위한 표준화 작업입니다. |
| [!DNL JupyterLab] | [!DNL JupyterLab] 는 Project Jupiter를 위한 오픈 소스 웹 기반 인터페이스로, 와 긴밀하게 통합되어  [!DNL Experience Platform]있습니다. |
| 레서피 | 레서피는 모델 사양에 대한 Adobe의 용어이며 특정 기계 학습, AI 알고리즘 또는 알고리즘, 처리 논리 및 구성을 나타내는 최상위 컨테이너로, 훈련된 모델을 구축 및 실행하여 특정 비즈니스 문제를 해결하는 데 필요한 구체적인 비즈니스 문제를 해결합니다. |
| 모델 | 모델은 비즈니스 사용 사례를 해결하기 위해 내역 데이터 및 구성을 사용하여 교육되는 기계 학습 레서피 인스턴스입니다. |
| 교육 | 트레이닝은 레이블이 지정된 데이터에서 패턴과 인사이트를 배우는 프로세스입니다. |
| 트레이닝된 모델 | 훈련된 모델은 모델 교육 프로세스의 실행 가능한 출력을 나타내며, 이 경우 일련의 교육 데이터가 모델 인스턴스에 적용되었습니다. 훈련된 모델은 이를 통해 만들어지는 모든 지능형 웹 서비스에 대한 참조를 유지합니다. 트레이닝된 모델은 점수를 매기고 지능적인 웹 서비스를 만드는 데 적합합니다. 훈련된 모델의 수정 사항은 새 버전으로 추적할 수 있습니다. |
| 채점 | 채점이란 훈련된 모델을 사용하여 데이터로부터 통찰력을 생성하는 프로세스입니다. |
| 서비스 | 배포된 서비스는 API를 통해 인공 지능, 머신 러닝 모델 또는 고급 알고리즘 기능을 노출하므로 다른 서비스 또는 애플리케이션에서 인텔리전트 앱을 작성할 수 있습니다. |

다음 차트는 레서피, 모델, 트레이닝 실행 및 점수부여 실행 간의 계층 관계에 대해 설명합니다.

![](./images/home/recipe_hiearchy_ui.png)

## [!DNL Data Science Workspace] 이해 

데이터 과학자는 [!DNL Data Science Workspace]을 사용하여 대량의 데이터 세트에서 인사이트를 찾는 번거로운 프로세스를 간소화할 수 있습니다. 공통 머신 러닝 프레임워크 및 런타임을 기반으로 구축된 [!DNL Data Science Workspace]은 고급 워크플로우 관리, 모델 관리 및 확장성을 제공합니다. 지능형 서비스는 기계 학습 레서피를 다시 사용하여 Adobe 제품 및 솔루션을 사용하여 만든 다양한 애플리케이션을 강화합니다.

### 원스톱 데이터 액세스

데이터는 AI와 머신 러닝의 초석입니다.

[!DNL Data Science Workspace] Data Lake 등 Adobe Experience Platform과 완벽하게 통합되어  [!DNL Real-time Customer Profile]있습니다 [!DNL Unified Edge]. 일반적인 빅데이터 및 [!DNL Spark] ML 및 [!DNL TensorFlow]과 같은 딥 러닝 라이브러리와 함께 Adobe Experience Platform에 저장된 모든 조직 데이터를 한 번에 탐색할 수 있습니다. 필요한 내용을 찾지 못하면 XDM 표준화된 스키마를 사용하여 데이터 세트를 인제스트합니다.

### 미리 만들어진 기계 학습 방법

[!DNL Data Science Workspace] 리테일 판매 예측 및 이상치 탐지 등 일반적인 비즈니스 요구에 맞게 미리 만들어진 기계 학습 레서피를 포함하므로 데이터 과학자와 개발자는 처음부터 시작할 필요가 없습니다. 현재 3개의 레서피가 제공되고 있습니다. [제품 구매 예측](./pre-built-recipes/product-purchase-prediction.md), [제품 추천](./pre-built-recipes/product-recommendations.md) 및 [소매 판매](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

원하는 경우 미리 만들어진 레서피를 필요에 맞게 조정하거나 레서피를 가져오거나 처음부터 새로 시작하여 사용자 정의 레서피를 만들 수 있습니다. 그러나 레서피를 트레이닝하고 세부적으로 조정한 다음에는 개발자가 몇 번의 클릭만으로 지능적인 맞춤형 디지털 경험을 제작할 수 있습니다. 이를 통해 타깃팅되고 개인화된 디지털 경험을 구축할 수 있습니다.

### 데이터 과학자에 초점을 맞춘 워크플로우

데이터 과학에 대한 전문 지식이 없더라도 [!DNL Data Science Workspace]은(는) 데이터에서 통찰력을 찾아 디지털 경험에 적용하는 과정을 간소화하고 가속화시켜 줍니다.

### 데이터 탐색

적합한 데이터를 찾아 준비하는 것은 효과적인 레시피를 구축하는 데 있어 가장 많은 노동력이 필요한 부분입니다. [!DNL Data Science Workspace] 또한 Adobe Experience Platform을 사용하면 데이터에서 인사이트를 빠르게 확보할 수 있습니다.

Adobe Experience Platform에서 크로스 채널 데이터는 XDM 표준화된 스키마에 중앙 집중화되고 저장되므로 데이터를 보다 손쉽게 찾고 이해하고 정리할 수 있습니다. 일반적인 스키마를 기반으로 한 단일 데이터 저장소를 통해 데이터 탐색과 준비 시간을 크게 절약할 수 있습니다.

탐색할 때 통합된 호스트 [!DNL Jupyter Notebook]과 함께 R, [!DNL Python] 또는 Scala를 사용하여 [!DNL Platform]의 데이터 카탈로그를 찾습니다. 이러한 언어 중 하나를 사용하여 [!DNL Spark] ML 및 TensorFlow를 활용할 수도 있습니다. 처음부터 새로 만들거나 특정 비즈니스 문제에 대해 제공된 노트북 템플릿 중 하나를 사용할 수 있습니다.

데이터 탐색 워크플로우의 일부로, 새 데이터를 인제스트하거나 기존 기능을 사용하여 데이터 준비를 지원할 수도 있습니다.

### 작성

[!DNL Data Science Workspace]에서 레서피 작성 방법을 결정합니다.

- 비즈니스 요구 사항을 충족시키는 미리 만들어진 레서피를 찾아보고 그대로 사용하거나 특정 요구 사항을 충족하도록 구성하여 시간을 절약할 수 있습니다.
- Jupiter Notebook의 제작 런타임을 사용하여 레서피를 개발하고 등록하여 처음부터 레서피를 만들 수 있습니다.
- Adobe Experience Platform 외부에서 작성한 레서피를 [!DNL Data Science Workspace]에 업로드하거나 [!DNL Git]와 [!DNL Data Science Workspace] 사이에 사용할 수 있는 인증 및 통합을 사용하여 [!DNL Git] 등의 저장소에서 레서피 코드를 가져옵니다.

### 실험

Data Science Workspace는 실험 프로세스에 엄청난 유연성을 제공합니다. 조리법부터 시작해 보세요. 그런 다음 동일한 코어 알고리즘을 하이퍼튜닝 매개 변수와 같은 고유한 특성과 함께 사용하여 별도의 인스턴스를 만듭니다. 필요한 만큼 인스턴스를 만들고, 각 인스턴스를 원하는 만큼 트레이닝하고 평가할 수 있습니다. 트레이닝을 수행하면서 [!DNL Data Science Workspace]은 평가 지표와 함께 레서피, 레서피 인스턴스 및 트레이닝된 인스턴스를 추적하므로 그럴 필요가 없습니다.

### 운영

레시피가 만족스러우면 몇 번의 클릭만으로 인텔리전트 서비스를 만들 수 있습니다. 코딩 작업 없이도 개발자 또는 엔지니어를 등록하지 않고도 직접 코드를 작성할 수 있습니다. 마지막으로 지능형 서비스를 Adobe IO에 게시하면 디지털 경험 팀이 사용할 수 있습니다.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 지속적인 개선

[!DNL Data Science Workspace] 지능적인 서비스가 호출되는 위치와 그 성능을 추적합니다. 데이터가 입력될 때 지능적인 서비스 정확도를 평가하여 루프를 닫고 필요에 따라 레서피를 재교육하여 성능을 향상시킬 수 있습니다. 그 결과 고객 개인화의 정확성을 지속적으로 개선할 수 있습니다.

### 새로운 기능 및 데이터 세트 이용

데이터 과학자는 Adobe 서비스를 통해 새로운 기술과 데이터 세트를 출시와 동시에 이용할 수 있습니다. 잦은 업데이트를 통해 데이터 세트 및 기술을 플랫폼에 통합함으로써 번거롭게 작업을 수행할 필요가 없습니다.

### 철저한 보안

데이터 보안은 Adobe의 최우선 순위입니다. Adobe은 업계에서 인정하는 표준, 규정 및 인증 준수를 위해 개발된 보안 프로세스와 제어 기능을 통해 데이터를 보호합니다.

보안은 Adobe Secure Product Lifecycle의 일부로 소프트웨어 및 서비스에 내장되어 있습니다.
Adobe 데이터 및 소프트웨어 보안, 규정 준수 등에 대한 자세한 내용은 보안 페이지(https://www.adobe.com/security.html)을 참조하십시오.

## [!DNL Data Science Workspace] 실행 중

예측 및 통찰력은 웹 사이트를 방문하거나 콜센터에 연락하거나 다른 디지털 경험에 참여하는 각 고객에게 개인화된 경험을 전달하는 데 필요한 정보를 제공합니다. 다음은 [!DNL Data Science Workspace]에서 일상적인 작업을 수행하는 방법입니다.

### 문제 정의

모두 비즈니스 문제로 시작합니다. 예를 들어 온라인 콜센터는 부정적인 고객 센티멘트를 긍정적으로 표현하는 데 컨텍스트를 필요로 합니다.

고객에 대한 많은 데이터가 있습니다. 사이트를 찾아보고, 장바구니에 품목을 싣고 심지어 주문까지 했습니다. 이메일, 사용 쿠폰 또는 이전에 콜센터에 연락했을 수 있습니다. 그런 다음, 레서피는 고객과 고객 활동에 대해 사용 가능한 데이터를 사용하여 구매 경향을 결정하고 고객이 감사하고 사용할 가능성이 있는 오퍼를 추천해야 합니다.

![](./images/home/example_problem.png)

콜센터 연락 시 고객은 여전히 장바구니에 두 쌍의 신발을 가지고 있지만 셔츠를 제거했습니다. 이러한 정보를 바탕으로, 지능형 서비스는 콜센터 에이전트가 통화 중에 20% 할인해 주는 쿠폰을 제공하는 것을 추천할 수 있습니다. 고객이 쿠폰을 사용하는 경우 해당 정보가 데이터 세트에 추가되고 다음에 고객이 전화를 할 때 예측이 더 좋아집니다.

### 데이터 탐색 및 준비

정의된 비즈니스 문제를 기반으로, 레서피는 사이트 방문, 검색, 페이지 보기, 클릭한 링크, 장바구니 작업, 받은 이메일, 받은 이메일, 콜 센터 상호 작용 등을 포함하여 모든 고객의 웹 거래를 조사해야 한다는 것을 알고 있습니다.

데이터 과학자는 일반적으로 데이터를 탐색하고 변형하는 레서피를 만드는 데 필요한 시간의 최대 75%를 소비합니다. 여러 저장소에서 가져온 데이터로서 서로 다른 스키마로 저장된 경우가 많습니다. 레서피를 생성하는 데 사용하기 전에 데이터를 결합하고 매핑해야 합니다.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

처음부터 새로 시작하거나 기존 레서피를 구성하는 경우 조직의 중앙 집중화되고 표준화된 데이터 카탈로그에서 데이터 검색을 시작하여 검색을 상당히 간소화할 수 있습니다. 조직에서 다른 데이터 과학자가 이미 유사한 데이터 세트를 식별했으며 처음부터 새로 시작하지 않고 해당 데이터 세트를 미세 조정하도록 선택할 수도 있습니다.
Adobe Experience Platform의 모든 데이터는 표준화된 XDM 스키마를 준수하므로 복잡한 모델을 만들어 데이터를 연결하거나 데이터 엔지니어의 도움을 받을 필요가 없습니다.

필요한 데이터를 바로 찾지 않아도 Adobe Experience Platform 외부에 있는 경우 데이터 세트를 추가로 수집하는 작업은 비교적 간단한 작업이므로 이를 표준화된 XDM 스키마로 변환할 수 있습니다.\
[!DNL Jupyter Notebook]을(를) 사용하여 데이터 사전 처리를 단순화할 수 있습니다. 이 프로세스는 이전에 구매 성향에 사용한 노트북 템플릿이나 노트북부터 시작됩니다.

![](./images/home/notebook_templates.png)

### 레시피 작성

이미 여러분의 모든 요구에 맞는 조리법을 발견했다면, 실험을 시작할 수 있다. 또는 [!DNL Jupyter Notebook]에서 [!DNL Data Science Workspace] 제작 런타임을 활용하여 레서피를 비트나 처음부터 새로 만들 수 있습니다. 제작 런타임을 사용하면 [!DNL Data Science Workspace] 교육 및 채점 워크플로우를 모두 사용할 수 있고 나중에 레서피를 변환할 수 있으므로 조직의 다른 사용자가 저장하고 다시 사용할 수 있습니다.

또한 레서피를 [!DNL Data Science Workspace]으로 가져와서 지능형 서비스를 만들 때 실험 워크플로우를 활용할 수도 있습니다.

### 레시피로 실험

핵심 기계 학습 알고리즘을 통합하는 레서피를 사용하면 하나의 레서피를 사용하여 다양한 레서피 인스턴스를 만들 수 있습니다. 이러한 레서피 인스턴스를 모델이라고 합니다. 일반적으로 시행착오 과정인 운영 효율성과 효율성을 최적화하기 위해 모델이 필요한 교육 및 평가입니다.

![](./images/home/recipe_hiearchy_ui.png)

모델을 교육하면 교육 실행 및 평가가 생성됩니다. [!DNL Data Science Workspace] 는 각 고유 모델과 해당 교육 실행에 대한 평가 지표를 추적합니다. 실험을 통해 생성된 평가 지표를 사용하면 가장 성과가 좋은 교육 실행을 결정할 수 있습니다.

![](./images/home/evaluation_metrics.png)

[!DNL Data Science Workspace]에서 모델을 트레이닝하고 평가하는 방법은 [API](./models-recipes/train-evaluate-model-api.md) 또는 [UI](./models-recipes/train-evaluate-model-ui.md) 자습서를 참조하십시오.

### 모델 운영

비즈니스 요구 사항을 충족하기 위해 가장 잘 훈련된 레서피를 선택한 경우 개발자 지원 없이도 [!DNL Data Science Workspace]에 지능적인 서비스를 만들 수 있습니다. 코드를 작성하지 않고도 몇 번의 클릭만으로 가능합니다. 게시된 지능형 서비스는 모델을 다시 만들지 않고도 조직의 다른 구성원이 액세스할 수 있습니다.

게시된 지능형 서비스는 새로운 데이터를 사용할 수 있게 되면 수시로 자동으로 트레이닝하도록 구성할 수 있습니다. 따라서 시간이 지남에 따라 서비스가 효율성과 효과를 유지할 수 있습니다.

## 다음 단계

[!DNL Data Science Workspace] 데이터 수집에서부터 알고리즘에 이르기까지 모든 기술 수준의 데이터 과학자를 위한 지능형 서비스에 이르기까지 데이터 과학 워크플로우를 능률화하고 단순화합니다. 정교한 도구 [!DNL Data Science Workspace]를 사용하면 데이터에서 인사이트에 이르는 시간을 대폭 단축할 수 있습니다.

더욱 중요한 점은 [!DNL Data Science Workspace]은(는) 기업 데이터 과학자들이 Adobe의 선도적인 마케팅 플랫폼의 데이터 과학 및 알고리즘 최적화 기능을 활용할 수 있다는 점입니다. 기업은 처음으로 독점 알고리즘을 플랫폼으로 가져올 수 있으며, Adobe의 강력한 머신 러닝 및 AI 기능을 활용하여 개인화된 고객 경험을 대규모로 전달할 수 있습니다.

브랜드 전문 지식과 Adobe의 머신 러닝 및 AI 기량의 결합으로 기업은 고객이 요구하는 바가 있기 전에 원하는 것을 제공함으로써 비즈니스 가치와 브랜드 충성도를 높일 수 있습니다.

전체 일상적인 작업 과정과 같은 추가 정보를 보려면 [데이터 과학 작업 공간 작업 공간 연습](./walkthrough.md) 설명서를 읽으십시오.

## 추가 리소스

다음 비디오는 [!DNL Data Science Workspace]에 대한 이해를 지원하기 위해 설계되었습니다.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)
