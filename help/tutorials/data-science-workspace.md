---
keywords: Experience Platform;home;popular topics;dsw;DSW
solution: Experience Platform
title: 데이터 과학 작업 공간 자습서
topic: tutorial
type: Tutorial
description: Adobe Experience Platform 데이터 과학 작업 공간은 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 생성합니다. Adobe Experience Platform에 통합된 데이터 과학 작업 공간은 Adobe 솔루션에서 컨텐츠와 데이터 자산을 사용하여 예측할 수 있도록 도와줍니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 자습서

Adobe Experience Platform [!DNL Data Science Workspace] 는 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 도출합니다. Adobe Experience Platform에 통합되어 Adobe 솔루션에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 [!DNL Data Science Workspace] 있습니다. 모든 기술 수준에 속한 데이터 과학자는 복잡한 AI 기술을 통해 얻을 수 있는 모든 이점을 비롯하여 머신 러닝 레서치의 신속한 개발, 트레이닝 및 조정을 지원하는 세련되고 사용이 간편한 툴을 갖추고 있습니다.

자세한 내용은 [데이터 과학 작업 공간 개요를 읽어 보십시오](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

API는 [!DNL Sensei Machine Learning] 알고리즘 온보딩, 실험, 서비스 배포에 이르기까지 데이터 과학자들이 기계 학습 서비스를 구성하고 관리하는 메커니즘을 제공합니다.

**다음 API 개발자 가이드를 사용할 수 있습니다.**
- [엔진](../data-science-workspace/api/engines.md) - [!DNL Docker] 레지스트리를 조회, 엔진 생성, 피쳐 파이프라인 엔진 생성, 엔진 정보 검색, 엔진 업데이트 및 엔진 삭제 등의 방법을 알아봅니다.
- [MLInestas(레서피)](../data-science-workspace/api/mlinstances.md) - MLInestment를 만들고, MLInestment에 대한 정보를 검색하고, MLInestement를 업데이트하고, MLInestment를 삭제하는 방법을 알아봅니다.
- [실험](../data-science-workspace/api/experiments.md) - 실험(Experiment) 생성, 실험(Experiment) 또는 실험(Experiment) 실행 정보 검색(Retrieve an Experiment), 실험 업데이트(Experiment) 및 실험(Experiment)을 삭제하는 방법을 학습합니다.
- [모델](../data-science-workspace/api/models.md) - 자체 모델을 등록하거나, 모델에 대한 정보를 검색하고, 모델을 업데이트하거나, 모델을 삭제하고, 모델에 대한 새로운 트랜스코딩(transcoding) 을 생성하고, 트랜스코딩된 모델의 세부 정보를 검색하는 방법을 알아봅니다.
- [MLServices](../data-science-workspace/api/mlservices.md) - MLService를 만들고, MLService에 대한 정보를 검색하고, MLService를 업데이트하고, MLService를 삭제하는 방법을 알아봅니다.
- [인사이트](../data-science-workspace/api/insights.md) - 인사이트에 대한 정보를 검색하고, 새 모델 인사이트를 추가하고, 알고리즘에 대한 기본 지표 목록을 검색하는 방법을 알아봅니다.

Sensei Machine Learning API를 사용하여 CRUD 작업을 수행하는 데 필요한 값을 확인하고 자세한 내용을 보려면 [시작 안내서를 참조하십시오](../data-science-workspace/api/getting-started.md).

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] 는 Adobe Experience Platform과 긴밀하게 통합되어 [!DNL Project Jupyter] 있고 웹 기반의 유저 인터페이스입니다. 데이터 과학자들이 데이터, 코드 및 데이터를 사용하여 작업할 수 있는 인터랙티브한 개발 환경 [!DNL Jupyter notebooks]을 제공합니다. 이 문서에서는 일반적인 작업 [!DNL JupyterLab] 을 수행하기 위한 지침뿐만 아니라 기능과 기능에 대한 개요를 제공합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 인터페이스에 액세스하고 이해할 수 [!DNL JupyterLab] 있습니다.
- 코드 셀과 사용 가능한 커널을 파악할 수 [!DNL JupyterLab]있습니다.
- GPU 및 메모리 서버 구성을 [!DNL Python]/R에서 이해할 수 있습니다.

자세한 내용은 JupiterLab [사용자 안내서를 참조하십시오](../data-science-workspace/jupyterlab/overview.md).

## JupiterLab 노트북의 데이터 액세스

현재 데이터 과학 작업 공간의 JupiterLab은 R, PySpark 및 Scala용 노트북 [!DNL Python]을 지원합니다. 지원되는 각 커널은 노트북 내의 데이터 세트에서 플랫폼 데이터를 읽을 수 있도록 해주는 내장 기능을 제공합니다. 그러나 페이지 매김 데이터에 대한 지원은 [!DNL Python] 및 R 노트북으로 제한됩니다. 이 안내서에서는 JupiterLab 노트북을 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- Python, R, PySpark 또는 Scala 노트북을 사용하여 플랫폼 데이터를 읽고 쓰고 쿼리할 수 있습니다.
- 각 노트북 유형의 읽기 제한 사항을 이해합니다.

자세한 내용은 JupiterLab [노트북 데이터 액세스 개발자 가이드를 참조하십시오.](../data-science-workspace/jupyterlab/access-notebook-data.md)

## 레서피 작성을 위한 소스 파일 [!DNL Docker] 패키지

이미지 [!DNL Docker] 를 사용하면 애플리케이션을 필요한 모든 부분으로 패키지화할 수 있습니다. 여기에는 라이브러리와 기타 종속성이 모두 하나의 패키지에 포함됩니다. 작성된 [!DNL Docker] 이미지는 레서피 생성 워크플로우 동안 제공된 자격 증명을 사용하여 [!DNL Azure Container Registry] 로 푸시됩니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 레서피 작성을 위해 필요한 사전 요구 사항을 다운로드합니다.
- 모델 [!DNL Docker] 작성을 이해합니다.
- R, PySpark [!DNL Docker] 또는 Scala( [!DNL Python][!DNL Spark])용 이미지를 만듭니다.
- 소스 [!DNL Docker] 파일 URL을 얻습니다.

자세한 내용은 [패키지 소스 파일을 레서피 튜토리얼에 따르십시오](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## 레서피 가져오기

>[!NOTE]
>
>이 자습서에서는 [!DNL Docker] 소스 파일 URL을 필요로 합니다. 소스 파일 URL이 없는 경우 [패키지 소스 파일을 레서피 자습서로](../data-science-workspace/models-recipes/package-source-files-recipe.md) 방문합니다 [!DNL Docker] .

가져오기 레서피 자습서에서는 패키지된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 튜토리얼이 끝나면 Adobe Experience Platform에서 모델을 생성, 교육 및 평가할 수 있습니다 [!DNL Data Science Workspace].

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 레서피에 대한 구성 집합을 만듭니다.
- R, PySpark [!DNL Docker] 또는 Scala( [!DNL Python][!DNL Spark])에 대한 기반 레시피를 가져올 수 있습니다.

자세한 내용은 패키지된 레서피 [UI 가져오기 자습서](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) 또는 [API 자습서를](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)따르십시오.

## 모델 트레이닝 및 평가

Adobe Experience Platform [!DNL Data Science Workspace]에서 기계 학습 모델은 모델의 의도에 적합한 기존 레서피를 결합함으로써 생성됩니다. 그런 다음 연관된 하이퍼매개 변수를 세밀하게 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 교육을 받고 평가합니다. 레서피는 재사용할 수 있습니다. 즉, 하나의 레서피를 사용하여 여러 모델을 생성하고 특정 목적에 맞게 변경할 수 있습니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 새 모델을 생성합니다.
- 모델에 대한 교육 실행을 만듭니다.
- 모델 교육 실행 평가

시작하려면 트레이닝과 모델 [API 자습서](../data-science-workspace/models-recipes/train-evaluate-model-api.md) 평가 또는 [UI 자습서를 따르십시오](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## 모델 인사이트 프레임워크를 사용하여 모델 최적화

Model Insights Framework는 데이터 과학자에게 실험을 기반으로 최적의 기계 학습 모델을 위한 신속하고 정확한 선택 [!DNL Data Science Workspace] 을 해주는 Adobe Experience Platform의 도구를 제공합니다. 이 프레임워크는 머신 러닝 워크플로우의 속도와 효율성을 향상시키고 데이터 과학자의 사용 용이성을 향상시킵니다. 이 작업은 모델 조정을 지원하기 위해 각 기계 학습 알고리즘 유형에 대한 기본 템플릿을 제공하여 수행됩니다. 최종 결과를 통해 데이터 과학자와 시민 데이터 과학자는 최종 고객을 위한 보다 효과적인 모델 최적화 결정을 내릴 수 있습니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 레서피 코드를 구성합니다.
- 사용자 지정 지표를 정의합니다.
- 사전 빌드된 평가 지표 및 시각화 차트를 사용하십시오.

시작하려면 모델 [최적화에 대한 자습서를 따르십시오](../data-science-workspace/models-recipes/optimize-model.md).

## 모델 점수 지정

Adobe Experience Platform에서 채점하는 것은 입력 데이터를 기존 트레이닝된 모델에 제공함으로써 달성될 [!DNL Data Science Workspace] 수 있습니다. 그러면 점수 결과가 저장되고 지정된 출력 데이터 세트에 새로운 일괄 처리로 표시됩니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 새로운 점수 실행을 만듭니다.
- 점수 지정 결과를 확인하십시오.

시작하려면 모델 [API 자습서](../data-science-workspace/models-recipes/score-model-api.md) 또는 [UI 자습서의 점수를](../data-science-workspace/models-recipes/score-model-ui.md)따르십시오.

## 모델을 서비스로 게시

Adobe Experience Platform [!DNL Data Science Workspace] 를 사용하면 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 자체 모델을 만들지 않고도 데이터를 평가할 수 있습니다. 사용자 인터페이스 또는 [!DNL Platform] [!DNL Sensei Machine Learning] API를 사용하여 수행할 수 있습니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 모델을 서비스로 게시합니다.
- 서비스 갤러리를 통해 서비스를 사용하여 데이터 [!DNL Platform] 를 [!UICONTROL 점화합니다].

시작하려면 모델을 서비스 [API 자습서](../data-science-workspace/models-recipes/publish-model-service-api.md) 또는 [UI 자습서로 게시하십시오](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## 모델의 교육 및 점수 예약

Adobe Experience Platform [!DNL Data Science Workspace] 는 기계 학습 서비스에서 예약된 점수 지정 및 교육 실행을 설정할 수 있도록 해줍니다. 트레이닝 및 점수 지정 프로세스를 자동화하면 데이터 내의 패턴을 유지하여 시간의 경과에 따라 서비스의 효율성을 유지 관리하고 개선하는 데 도움이 됩니다.

**이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.**
- 예약된 점수 구성
- 예약된 교육 구성

시작하려면 모델 UI [예약 자습서에 따르십시오](../data-science-workspace/models-recipes/schedule-models-ui.md).

## 피쳐 파이프라인 만들기

>[!NOTE]
>
>현재 기능 파이프라인은 API를 통해서만 사용할 수 있습니다.

Adobe Experience Platform을 사용하면 사용자 정의 기능 파이프라인을 구축하여 사용자 요구에 맞게 확장할 수 있습니다 [!DNL Sensei Machine Learning Framework Runtime].

**이 가이드는 다음과 같은 도움을 줍니다.**
- 기능 파이프라인 클래스 구현
- API를 사용하여 피쳐 파이프라인 엔진을 만듭니다.

자세한 내용은 튜토리얼을 참조하여 피쳐 파이프라인 [을 만듭니다](../data-science-workspace/authoring/feature-pipeline.md).

## 응용 프로그램 [!DNL Real-Time Machine Learning] 만들기(알파)

허브와 허브에서 매끄러운 계산을 함께 사용하면 일반적으로 적절하고 응답성이 높은 고도로 개인화된 경험을 구현하는데 관련된 지연을 크게 줄일 수 있습니다. [!DNL Edge] 따라서, 동기 의사 결정 시 매우 짧은 지연 시간을 갖는 참조 사항을 [!DNL Real-time Machine Learning] 제공합니다. 예를 들어 맞춤형 웹 페이지 컨텐츠 렌더링, 제안 표시, 이탈률 감소 및 웹 스토어의 구매 전환율 증가를 위한 할인 등이 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 아키텍처를 [!DNL Real-time Machine Learning] 파악합니다.
- 워크플로우를 [!DNL Real-time Machine Learning] 파악합니다.
- 의 현재 기능을 파악합니다 [!DNL Real-time Machine Learning].
- 직접 만드는 다음 단계를 제공합니다 [!DNL Real-time Machine Learning model].

자세한 내용은 [실시간 머신 러닝 개요를 참조하십시오](../data-science-workspace/real-time-machine-learning/home.md).