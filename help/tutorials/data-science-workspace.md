---
keywords: Experience Platform;home;popular topics;dsw;DSW
solution: Experience Platform
title: 데이터 과학 작업 공간 자습서
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace는 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 도출합니다. Adobe Experience Platform에 통합된 Data Science Workspace를 사용하면 Adobe 솔루션에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 있습니다.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 자습서

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 머신 러닝과 인공 지능을 사용하여 데이터를 통해 인사이트를 생성합니다. Adobe Experience Platform에 통합된 [!DNL Data Science Workspace]은(는) Adobe 솔루션에서 컨텐츠와 데이터 자산을 사용하여 예측하는 데 도움이 됩니다. 기술 수준에 관계없이 모든 데이터 과학자는 복잡한 AI 기술을 통해 얻을 수 있는 모든 이점을 비롯하여 머신 러닝 레서피의 신속한 개발, 트레이닝 및 조정을 지원하는 정교하고 사용하기 쉬운 툴을 갖추고 있습니다.

자세한 내용은 [데이터 과학 작업 공간 개요](../data-science-workspace/home.md)를 읽으십시오.

## [!DNL Sensei Machine Learning] API

[!DNL Sensei Machine Learning] API는 알고리즘 온보딩, 실험 및 서비스 배포에 이르기까지 데이터 과학자들이 기계 학습 서비스를 구성하고 관리하는 메커니즘을 제공합니다.

**다음 API 개발자 가이드를 사용할 수 있습니다.**
- [엔진](../data-science-workspace/api/engines.md)  -  [!DNL Docker] 레지스트리를 조회하고, 엔진을 생성하고, 피쳐 파이프라인 엔진을 생성하고, 엔진에 대한 정보를 검색하고, 엔진을 업데이트하고, 엔진을 삭제하는 방법을 알아봅니다.
- [MLInests(레서피)](../data-science-workspace/api/mlinstances.md) - MLInstance를 만들고, MLInstance에 대한 정보를 검색하고, MLInstance를 업데이트하고, MLInstance를 삭제하는 방법을 알아봅니다.
- [실험](../data-science-workspace/api/experiments.md)  - 실험 생성, 실험 또는 실험 실행 정보 검색, 실험 업데이트 및 실험 삭제 방법을 알아봅니다.
- [모델](../data-science-workspace/api/models.md)  - 자체 모델을 등록하고, 모델에 대한 정보를 검색하고, 모델을 업데이트하고, 모델을 삭제하고, 모델에 대한 새 트랜스코딩을 생성하고, 코드 변환된 모델의 세부 정보를 검색하는 방법을 알아봅니다.
- [MLSservices](../data-science-workspace/api/mlservices.md)  - MLService를 만들고, MLService에 대한 정보를 검색하고, MLService를 업데이트하고, MLService를 삭제하는 방법을 알아봅니다.
- [인사이트](../data-science-workspace/api/insights.md)  - 인사이트에 대한 정보를 검색하고, 새 모델 인사이트를 추가하고, 알고리즘에 대한 기본 지표 목록을 검색하는 방법을 알아봅니다.

Sensei Machine Learning API를 사용하여 CRUD 작업을 수행하는 데 필요한 값을 얻고 자세한 내용을 보려면 [시작 안내서](../data-science-workspace/api/getting-started.md)를 참조하십시오.

## [!DNL JupyterLab] 전자 필기장을 사용하는 방법

[!DNL JupyterLab] 는 Adobe Experience Platform에 긴밀하게 통합되어  [!DNL Project Jupyter] 있고 웹 기반의 유저 인터페이스입니다. 데이터 과학자들이 [!DNL Jupyter Notebooks], 코드 및 데이터를 사용하여 작업할 수 있는 대화형 개발 환경을 제공합니다. 이 문서에서는 [!DNL JupyterLab] 및 해당 기능에 대한 개요와 일반적인 작업을 수행하는 지침을 제공합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- [!DNL JupyterLab] 인터페이스에 액세스하고 파악합니다.
- [!DNL JupyterLab] 내에서 코드 셀과 사용 가능한 커널을 파악합니다.
- [!DNL Python]/R의 GPU 및 메모리 서버 구성에 대해 이해합니다.

자세한 내용은 [JupiterLab 사용자 안내서](../data-science-workspace/jupyterlab/overview.md)를 참조하십시오.

## JupiterLab 노트북의 데이터 액세스

현재 데이터 과학 작업 영역의 JupiterLab은 [!DNL Python], R, PySpark 및 Scala용 노트북을 지원합니다. 지원되는 각 커널은 노트북 내의 데이터 세트에서 플랫폼 데이터를 읽을 수 있도록 하는 내장 기능을 제공합니다. 그러나 데이터 페이지 매김 지원은 [!DNL Python] 및 R 노트북으로 제한됩니다. 이 안내서에서는 JupiterLab 전자 필기장을 사용하여 데이터에 액세스하는 방법에 중점을 둡니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- Python, R, PySpark 또는 Scala 노트북을 사용하여 플랫폼 데이터를 읽고 작성 및 쿼리할 수 있습니다.
- 각 노트북 유형의 읽기 제한 사항을 이해합니다.

자세한 내용은 [JupiterLab 노트북 데이터 액세스 개발자 가이드](../data-science-workspace/jupyterlab/access-notebook-data.md)를 참조하십시오.

## [!DNL Docker] 레서피 작성을 위한 소스 파일 패키지

[!DNL Docker] 이미지를 사용하면 필요한 모든 부분으로 애플리케이션을 패키지화할 수 있습니다. 여기에는 하나의 패키지에서 라이브러리 및 기타 종속성이 모두 포함됩니다. 레서피 만들기 작업 과정 중에 제공된 자격 증명을 사용하여 작성된 [!DNL Docker] 이미지가 [!DNL Azure Container Registry]로 푸시됩니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 레서피 제작에 필요한 사전 요구 사항을 다운로드합니다.
- [!DNL Docker] 기반 모델 작성을 이해합니다.
- [!DNL Python], R, PySpark 또는 Scala([!DNL Spark])에 대한 [!DNL Docker] 이미지를 만듭니다.
- [!DNL Docker] 소스 파일 URL을 얻습니다.

자세한 내용은 [소스 파일을 레서피 자습서](../data-science-workspace/models-recipes/package-source-files-recipe.md)에 패키지하십시오.

## 레서피 가져오기

>[!NOTE]
>
>이 자습서를 사용하려면 [!DNL Docker] 소스 파일 URL이 있어야 합니다. [!DNL Docker] 소스 파일 URL이 없는 경우 [소스 파일을 레서피 자습서](../data-science-workspace/models-recipes/package-source-files-recipe.md)로 패키징합니다.

가져오기 레서피 자습서에서는 패키징된 레서피를 구성하고 가져오는 방법에 대한 통찰력을 제공합니다. 이 자습서가 끝나면 Adobe Experience Platform [!DNL Data Science Workspace]에서 모델을 만들고, 교육하고, 평가할 수 있습니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 레서피에 대한 구성 세트를 만듭니다.
- [!DNL Python], R, PySpark 또는 Scala([!DNL Spark])에 대한 [!DNL Docker] 기반 레서피를 가져옵니다.

자세한 내용을 보려면 패키지된 레서피 [UI 자습서](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) 또는 [API 자습서](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)를 가져오십시오.

## 모델 트레이닝 및 평가

Adobe Experience Platform [!DNL Data Science Workspace]에서 기계 학습 모델은 모델 의도에 적합한 기존 레서피를 결합하여 만들어집니다. 그런 다음 연관된 하이퍼매개 변수를 미세 조정하여 모델의 운영 효율성과 효과를 최적화하기 위해 교육 및 평가를 수행합니다. 레서피는 재사용 가능하므로, 하나의 레서피를 사용하여 여러 모델을 생성하고 특정 목적에 맞게 변경할 수 있습니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 새 모델 만들기를 참조하십시오.
- 모델에 대한 교육 실행을 만듭니다.
- 모델 교육 실행을 평가합니다.

시작하려면 교육 및 모델 [API 자습서](../data-science-workspace/models-recipes/train-evaluate-model-api.md) 또는 [UI 자습서](../data-science-workspace/models-recipes/train-evaluate-model-ui.md) 평가에 따르십시오.

## Model Insights 프레임워크를 사용하여 모델 최적화

Model Insights Framework는 실험을 기반으로 최적의 기계 학습 모델을 위한 신속하고 정확한 선택을 할 수 있도록 데이터 과학자에게 Adobe Experience Platform [!DNL Data Science Workspace]의 도구를 제공합니다. 이 프레임워크는 시스템 학습 워크플로우의 속도와 효율성을 향상시키고 데이터 과학자의 사용 용이성을 향상시킵니다. 이 작업은 모델 조정을 지원하기 위해 각 기계 학습 알고리즘 유형에 대한 기본 템플릿을 제공하여 수행됩니다. 최종 결과를 통해 데이터 과학자와 시민 데이터 과학자는 최종 고객을 위해 보다 효과적인 모델 최적화 결정을 내릴 수 있습니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 레서피 코드를 구성합니다.
- 사용자 지정 지표를 정의합니다.
- 미리 만들어진 평가 지표 및 시각화 차트를 사용할 수 있습니다.

시작하려면 [모델](../data-science-workspace/models-recipes/optimize-model.md) 최적화의 자습서를 따르십시오.

## 모델 점수 지정

Adobe Experience Platform [!DNL Data Science Workspace]에서 채점하는 방법은 입력 데이터를 기존 트레이닝된 모델에 제공함으로써 달성됩니다. 그러면 점수 지정 결과가 저장되고 지정된 출력 데이터 세트에 새로운 일괄 처리로 표시됩니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 새로운 점수부여 실행을 만듭니다.
- 채점 결과를 확인합니다.

시작하려면 모델 [API 자습서](../data-science-workspace/models-recipes/score-model-api.md) 또는 [UI 자습서](../data-science-workspace/models-recipes/score-model-ui.md) 점수를 따르십시오.

## 모델을 서비스로 게시

Adobe Experience Platform [!DNL Data Science Workspace]을 사용하면 모델을 서비스로 게시하여 IMS 조직 내의 사용자가 자체 모델을 만들지 않고도 데이터를 점수를 매길 수 있습니다. 이 작업은 [!DNL Platform] 사용자 인터페이스 또는 [!DNL Sensei Machine Learning] API를 사용하여 수행할 수 있습니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 모델을 서비스로 게시합니다.
- [!DNL Platform] [!UICONTROL Service Gallery]을 통해 서비스를 사용하여 데이터를 점화합니다.

시작하려면 모델을 서비스 [API 자습서](../data-science-workspace/models-recipes/publish-model-service-api.md) 또는 [UI 자습서](../data-science-workspace/models-recipes/publish-model-service-ui.md)로 게시하십시오.

## 모델에 대한 교육 및 점수 예약

Adobe Experience Platform [!DNL Data Science Workspace]에서는 기계 학습 서비스에서 예약된 점수 지정 및 교육 실행을 설정할 수 있습니다. 트레이닝 및 점수 지정 프로세스를 자동화하면 데이터 내의 패턴을 유지하여 시간 경과에 따른 서비스 효율성을 유지 관리하고 개선하는 데 도움이 됩니다.

**이 자습서는 다음과 같은 이점을 제공합니다.**
- 예약된 점수 구성
- 예약된 교육 구성

시작하려면 [모델 UI 자습서](../data-science-workspace/models-recipes/schedule-models-ui.md) 예약을 따르십시오.

## 피쳐 파이프라인 만들기

>[!NOTE]
>
>현재 기능 파이프라인은 API를 통해서만 사용할 수 있습니다.

Adobe Experience Platform을 사용하면 사용자 지정 기능 파이프라인을 만들고 만들어 [!DNL Sensei Machine Learning Framework Runtime]을 통해 기능 엔지니어링을 규모에 맞게 수행할 수 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 기능 파이프라인 클래스를 구현합니다.
- API를 사용하여 피쳐 파이프라인 엔진을 만듭니다.

자세한 내용은 [기능 파이프라인 만들기](../data-science-workspace/authoring/feature-pipeline.md)에 대한 자습서를 참조하십시오.

## [!DNL Real-Time Machine Learning] 응용 프로그램 만들기(알파)

허브와 [!DNL Edge]에 대한 매끄러운 계산으로 인해 관련이 있고 응답성이 높은 고도로 개인화된 경험을 제공하기 위해 전통적으로 수반되는 지연이 크게 줄어듭니다. 따라서 [!DNL Real-time Machine Learning]은 동기 의사 결정을 위한 지연 시간이 매우 짧은 환경 설정을 제공합니다. 예를 들면 맞춤형 웹 페이지 컨텐츠 렌더링, 제안 표시, 이탈률을 줄이면서 웹 스토어에서의 전환을 늘리는 할인 등이 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- [!DNL Real-time Machine Learning] 아키텍처를 이해합니다.
- [!DNL Real-time Machine Learning] 작업 과정을 이해합니다.
- [!DNL Real-time Machine Learning]의 현재 기능을 파악합니다.
- 자신의 [!DNL Real-time Machine Learning model]을(를) 만들기 위한 다음 단계를 제공합니다.

자세한 내용은 [실시간 기계 학습 개요](../data-science-workspace/real-time-machine-learning/home.md)를 참조하십시오.
