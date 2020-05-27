---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 실시간 머신 러닝 시작하기
topic: Getting started
translation-type: tm+mt
source-git-commit: 626bb7a0856a663e235ecd2b19954f4617fe9b6f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# 실시간 기계 학습(알파) 시작하기

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 활용하려면 Adobe Experience Platform 및 Data Science Workspace로 규정된 조직에 액세스해야 합니다. 또한 트레이닝 및 점수 매기용으로 전체 데이터 세트를 사용해야 합니다.

실시간 머신 러닝 가이드는 Python 3, Jupiter 노트북 [](../jupyterlab/overview.md), 데이터 과학 및 머신 러닝에 대한 실무 이해를 필요로 합니다.

**주요 약관:**

- **DSL:** 도메인별 언어.
- **Edge:** 실시간 머신 러닝 점수 서비스는 Edge 클러스터에서 활성화와 애플리케이션에 가까운 곳에서 실행할 수 있습니다.
- **허브:** 현재 알파 버전은 Experience Edge Network가 개발 중인 동안 Adobe Experience Platform 허브에서 실시간 기계 학습 점수 서비스를 실행하고 있습니다.
- **노드:** 노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 ML 파이프라인을 나타내는 그래프를 형성하는 링크를 사용하여 서로 연결할 수 있습니다. 노드에서 수행하는 작업은 데이터 또는 스키마 변환 또는 기계 학습 유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 노드는 변형되거나 유추된 값을 다음 노드로 출력합니다.

## Adobe Experience Platform의 데이터 세트

실시간 머신 러닝을 사용하려면 데이터 세트에 액세스할 수 있어야 합니다. 외부 데이터 세트를 사용하여 JupiterLab 환경에 업로드하거나, 아직 업데이트하지 않은 경우 플랫폼 내에서 새로운 데이터 세트를 만들 수 있습니다.

>[!NOTE]
>이미 사용할 데이터 세트를 가지고 있는 경우 [다음 단계로 건너뛸 수 있습니다](#next-steps).

### 외부 데이터 집합 사용

JupiterLab 환경에 데이터 업로드와 같은 외부 데이터 세트를 사용하는 방법에 대한 자세한 내용은 노트북을 사용하여 데이터 [분석에 대한 자습서를 참조하십시오](../jupyterlab/analyze-your-data.md#external-data).

### 새 데이터 집합 만들기

실시간 시스템 학습에서 사용할 데이터 세트를 새로 만들려면 데이터 세트에 대한 데이터 스키마가 필요합니다. 그런 다음 만든 스키마를 사용하여 데이터를 인제스트해야 합니다. 다음 자습서를 사용하여 플랫폼에 대한 데이터 세트를 만들고 채울 수 있습니다.

- [API에서 데이터 세트 만들기 및 채우기](../../catalog/datasets/create.md)
- [UI에서 데이터 세트 만들기 및 채우기](../../ingestion/tutorials/ingest-batch-data.md)

## 다음 단계 {#next-steps}

실시간 머신 러닝을 위한 데이터를 준비했다면 [실시간 머신 러닝 노트북 사용 안내서를](./rtml-authoring-notebook.md) 참조하여 ONNX 모델을 만들고 Real-time Machine Learning model store에 업로드하는 방법을 알아보십시오.

